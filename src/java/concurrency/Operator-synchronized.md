## Оператор `synchronized`
При работе потоки нередко обращаются к каким-то общим ресурсам, которые определены вне потока, например, обращение к какому-то файлу. Если одновременно несколько потоков обратятся к общему ресурсу, то результаты выполнения программы могут быть неожиданными и даже непредсказуемыми. Например, определим следующий код:

```java
public class Program {
    public static void main(String[] args) {
        CommonResource commonResource = new CommonResource();
        for (int i = 1; i < 6; i++) {
            Thread t = new Thread(new CountThread(commonResource));
            t.setName("Thread " + i);
            t.start();
        }
    }
}

class CommonResource {
    int x = 0;
}

class CountThread implements Runnable {
    CommonResource res;

    CountThread(CommonResource res) {
        this.res = res;
    }

    public void run() {
        res.x = 1;
        for (int i = 1; i < 5; i++) {
            System.out.printf("%s %d \n", Thread.currentThread().getName(), res.x);
            res.x++;
            try {
                Thread.sleep(100);
            } catch (InterruptedException e) {
                System.out.println(e.toString());
            }
        }
    }
}
```

Здесь определен класс `CommonResource`, который представляет общий ресурс и в котором определено одно целочисленное поле `x`.

Этот ресурс используется классом потока `CountThread`. Этот класс просто увеличивает в цикле значение `x` на единицу. Причем при входе в поток значение `x = 1`:

```java
res.x = 1;
```

То есть в итоге мы ожидаем, что после выполнения цикла `res.x` будет равно `4`.

В главном классе программы запускается пять потоков. То есть мы ожидаем, что каждый поток будет увеличивать `res.x` с `1` до `4` и так пять раз. Но если мы посмотрим на результат работы программы, то он будет иным:

```out
Thread 1 1 
Thread 2 1 
Thread 3 1 
Thread 5 1 
Thread 4 1 
Thread 5 6 
Thread 2 6 
Thread 1 6 
Thread 3 6 
Thread 4 6 
Thread 4 11 
Thread 2 11 
Thread 5 11 
Thread 3 11 
Thread 1 11 
Thread 4 16 
Thread 1 16 
Thread 3 16 
Thread 5 16 
Thread 2 16
```

То есть пока один поток не окончил работу с полем `res.x`, с ним начинает работать другой поток.

Чтобы избежать подобной ситуации, надо **синхронизировать потоки**. Одним из способов синхронизации является использование ключевого слова `synchronized`. Этот оператор предваряет блок кода или метод, который подлежит синхронизации. Для его применения изменим класс `CountThread`:

```java
class CountThread implements Runnable {
    CommonResource res;

    CountThread(CommonResource res) {
        this.res = res;
    }

    public void run() {
        synchronized (res) {
            res.x = 1;
            for (int i = 1; i < 5; i++) {
                System.out.printf("%s %d \n", Thread.currentThread().getName(), res.x);
                res.x++;
                try {
                    Thread.sleep(100);
                } catch (InterruptedException e) {
                    System.out.println(e.toString());
                }
            }
        }
    }
}
```

При создании синхронизированного блока кода после оператора `synchronized` идет объект-заглушка: `synchronized(res)`. Причем в качестве объекта может использоваться только объект какого-нибудь класса, но не примитивного типа.

Каждый объект в Java имеет ассоциированный с ним **монитор**. Монитор представляет своего рода инструмент для управления доступа к объекту. Когда выполнение кода доходит до оператора `synchronized`, монитор объекта `res` блокируется, и на время его блокировки монопольный доступ к блоку кода имеет только один поток, который и произвел блокировку. После окончания работы блока кода, монитор объекта `res` освобождается и становится доступным для других потоков.

После освобождения монитора его захватывает другой поток, а все остальные потоки продолжают ожидать его освобождения.

В итоге консольный вывод изменится:

```out
Thread 1 1 
Thread 1 2
Thread 1 3
Thread 1 4
Thread 3 1 
Thread 3 2
Thread 3 3
Thread 3 4
Thread 5 1 
Thread 5 2
Thread 5 3
Thread 5 4
Thread 4 1 
Thread 4 2
Thread 4 3
Thread 4 4
Thread 2 1 
Thread 2 2
Thread 2 3
Thread 2 4
```

При применении оператора `synchronized` к методу пока этот метод не завершит выполнение, монопольный доступ имеет только один поток - первый, который начал его выполнение. Для применения `synchronized` к методу, изменим классы программы:

```java
public class Program {
    public static void main(String[] args) {
        CommonResource commonResource= new CommonResource();
        for (int i = 1; i < 6; i++) {
            Thread t = new Thread(new CountThread(commonResource));
            t.setName("Thread " + i);
            t.start();
        }
    }
}
 
class CommonResource {
    int x;

    synchronized void increment() {
        x = 1;
        for (int i = 1; i < 5; i++) {
            System.out.printf("%s %d \n", Thread.currentThread().getName(), x);
            x++;
            try {
                Thread.sleep(100);
            } catch(InterruptedException e) {
                System.out.println(e.toString());
            }
        }
    }
}
 
class CountThread implements Runnable {
    CommonResource res;

    CountThread(CommonResource res) {
        this.res = res;
    }
     
    public void run() {
        res.increment();
    }
}
```

Результат работы в данном случае будет аналогичен примеру выше с блоком `synchronized`. Здесь опять в дело вступает монитор объекта `CommonResource` - общего объекта для всех потоков. Поэтому синхронизированным объявляется не метод `run()` в классе `CountThread`, а метод `increment()` класса `CommonResource`. Когда первый поток начинает выполнение метода `increment()`, он захватывает монитор объекта `CommonResource`. А все потоки также продолжают ожидать его освобождения.