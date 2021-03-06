# Блокировки. `ReentrantLock`
Для управления доступом к общему ресурсу в качестве альтернативы оператору synchronized мы можем использовать блокировки. Функциональность блокировок заключена в пакете `java.util.concurrent.locks`.

Вначале поток пытается получить доступ к общему ресурсу. Если он свободен, то на него накладывает блокировку. После завершения работы блокировка с общего ресурса снимается. Если же ресурс не свободен и на него уже наложена блокировка, то поток ожидает, пока эта блокировка не будет снята.

Классы блокировок реализуют интерфейс `Lock`, который определяет следующие методы:
- `void lock()` ожидает, пока не будет получена блокировка
- `void lockInterruptibly() throws InterruptedException` ожидает, пока не будет получена блокировка, если поток не прерван
- `boolean tryLock()` пытается получить блокировку, если блокировка получена, то возвращает `true`. Если блокировка не получена, то возвращает `false`. В отличие от метода `lock()` не ожидает получения блокировки, если она недоступна
- `void unlock()` снимает блокировку
- `Condition newCondition()` возвращает объект `Condition`, который связан с текущей блокировкой

Организация блокировки в общем случае довольно проста: для получения блокировки вызывается метод `lock()`, а после окончания работы с общими ресурсами вызывается метод `unlock()`, который снимает блокировку.

Объект `Condition` позволяет управлять блокировкой.

Как правило, для работы с блокировками используется класс `ReentrantLock` из пакета `java.util.concurrent.locks`. Данный класс реализует интерфейс `Lock`.

Для примера возьмем код из темы про оператор synchronized и перепишем данный код с использованием заглушки `ReentrantLock`:

```java
import java.util.concurrent.locks.ReentrantLock;
 
public class Program {
    public static void main(String[] args) {
        CommonResource commonResource= new CommonResource();
        ReentrantLock locker = new ReentrantLock(); // создаем заглушку
        for (int i = 1; i < 6; i++) {
            Thread t = new Thread(new CountThread(commonResource, locker));
            t.setName("Thread "+ i);
            t.start();
        }
    }
}
  
class CommonResource {
    int x = 0;
}
  
class CountThread implements Runnable {
    CommonResource res;
    ReentrantLock locker;

    CountThread(CommonResource res, ReentrantLock lock) {
        this.res = res;
        this.locker = lock;
    }

    public void run() {
        locker.lock(); // устанавливаем блокировку
        try {
            res.x = 1;
            for (int i = 1; i < 5; i++) {
                System.out.printf("%s %d \n", Thread.currentThread().getName(), res.x);
                res.x++;
                Thread.sleep(100);
            }
        } catch (InterruptedException e) {
            System.out.println(e.getMessage());
        } finally {
            locker.unlock(); // снимаем блокировку
        }
    }
}
```

Здесь также используется общий ресурс `CommonResource`, для управления которым создается пять потоков. На входе в критическую секцию устанавливается заглушка:

```java
locker.lock();
```

После этого только один поток имеет доступ к критической секции, а остальные потоки ожидают снятия блокировки. В блоке `finally` после всей окончания основной работы потока эта блокировка снимается. Причем делается это обязательно в блоке `finally`, так как в случае возникновения ошибки все остальные потоки окажутся заблокированными.

В итоге мы получим вывод, аналогичный тому, который был в случае с оператором `synchronized`:

```out
Thread 4 1 
Thread 4 2 
Thread 4 3 
Thread 4 4 
Thread 3 1 
Thread 3 2 
Thread 3 3 
Thread 3 4 
Thread 2 1 
Thread 2 2 
Thread 2 3 
Thread 2 4 
Thread 1 1 
Thread 1 2 
Thread 1 3 
Thread 1 4 
Thread 5 1 
Thread 5 2 
Thread 5 3 
Thread 5 4
```