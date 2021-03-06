# Класс `Exchanger`

Класс `Exchanger` предназначен для обмена данными между потоками. Он является типизированным и типизируется типом данных, которыми потоки должны обмениваться.

Обмен данными производится с помощью единственного метода этого класса `exchange()`:

```java
V exchange(V x) throws InterruptedException
V exchange(V x, long timeout, TimeUnit unit) throws InterruptedException, TimeoutException
```

Параметр `x` представляет буфер данных для обмена. Вторая форма метода также определяет параметр `timeout` - время ожидания и `unit` - тип временных единиц, применяемых для параметра `timeout`.

Данный класс очень просто использовать:

```java
import java.util.concurrent.Exchanger;
  
public class Program {
    public static void main(String[] args) {
        Exchanger<String> ex = new Exchanger<String>();
        new Thread(new PutThread(ex)).start();
        new Thread(new GetThread(ex)).start();
    }
}
  
class PutThread implements Runnable {
    Exchanger<String> exchanger;
    String message;
  
    PutThread(Exchanger<String> ex) {
        this.exchanger = ex;
        message = "Hello Java!";
    }

    public void run() {
        try {
            message = exchanger.exchange(message);
            System.out.println("PutThread has received: " + message);
        } catch(InterruptedException ex) {
            System.out.println(ex.getMessage());
        }
    }
}

class GetThread implements Runnable {
    Exchanger<String> exchanger;
    String message;
  
    GetThread(Exchanger<String> ex) {
        this.exchanger = ex;
        message = "Hello World!";
    }

    public void run() {
        try {
            message = exchanger.exchange(message);
            System.out.println("GetThread has received: " + message);
        } catch(InterruptedException ex) {
            System.out.println(ex.getMessage());
        }
    }
}
```

В классе `PutThread` отправляет в буфер сообщение `Hello Java!`:

```java
message = exchanger.exchange(message);
```

Причем в ответ метод `exchange()` возвращает данные, которые отправил в буфер другой поток. То есть происходит обмен данными. Хотя нам необязательно получать данные, мы можем просто их отправить:

```java
exchanger.exchange(message);
```

Логика класса `GetThread` аналогична - также отправляется сообщение.

В итоге консоль выведет следующий результат:

```out
PutThread has received: Hello World!
GetThread has received: Hello Java!
```