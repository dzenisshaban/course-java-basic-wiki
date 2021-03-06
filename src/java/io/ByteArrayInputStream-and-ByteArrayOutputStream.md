Для работы с массивами байтов - их чтения и записи используются классы `ByteArrayInputStream` и `ByteArrayOutputStream`.

## Чтение массива байтов и класс `ByteArrayInputStream`
Класс ByteArrayInputStream представляет входной поток, использующий в качестве источника данных массив байтов. Он имеет следующие конструкторы:
- `ByteArrayInputStream(byte[] buf)`
- `ByteArrayInputStream(byte[] buf, int offset, int length)`

В качестве параметров конструкторы используют массив байтов `buf`, из которого производится считывание, смещение относительно начала массива `offset` и количество считываемых символов `length`.

Считаем массив байтов и выведем его на экран:

```java
import java.io.ByteArrayInputStream;

public class Program {
    public static void main(String[] args) {
        byte[] array1 = new byte[] {1, 3, 5, 7};
        ByteArrayInputStream byteStream1 = new ByteArrayInputStream(array1);
        int b;
        while ((b = byteStream1.read()) != -1) {
            System.out.println(b);
        }
        String text = "Hello world!";
        byte[] array2 = text.getBytes();
        ByteArrayInputStream byteStream2 = new ByteArrayInputStream(array2, 0, 5); // считываем 5 символов
        int c;
        while ((c = byteStream2.read()) != -1) {
            System.out.println((char) c);
        }
    }
}
```

В отличие от других классов потоков для закрытия объекта `ByteArrayInputStream` не требуется вызывать метод `close()`.


## Запись массива байт и класс `ByteArrayOutputStream`
Класс `ByteArrayOutputStream` представляет поток вывода, использующий массив байтов в качестве места вывода.

Чтобы создать объект данного класса, мы можем использовать один из его конструкторов:
- `ByteArrayOutputStream()`
- `ByteArrayOutputStream(int size)`

Первая версия создает массив для хранения байтов длиной в *32 байта*, а вторая версия создает массив длиной `size`.

Рассмотрим применение класса:

```java
import java.io.ByteArrayOutputStream;

public class Program {
    public static void main(String[] args) {
        ByteArrayOutputStream baos = new ByteArrayOutputStream();
        String text = "Hello Wolrd!";
        byte[] buffer = text.getBytes();
        try {
            baos.write(buffer);
        } catch (Exception ex) {
            System.out.println(ex.getMessage());
        }
        System.out.println(baos.toString()); // превращаем массив байтов в строку
        byte[] array = baos.toByteArray(); // получаем массив байтов и выводим по символьно
        for (byte b : array) {
            System.out.print((char) b);
        }
        System.out.println();
    }
}
```

Как и в других потоках вывода в классе `ByteArrayOutputStream` определен метод `write()`, который записывает в поток некоторые данные. В данном случае мы записываем в поток массив байтов. Этот массив байтов записывается в объекте `ByteArrayOutputStream` в защищенное поле `buf`, которое представляет также массив байтов `(protected byte[] buf)`.

Так как метод `write()` может сгенерировать исключение, то вызов этого метода помещается в блок `try...catch`.

Используя методы `toString()` и `toByteArray()`, можно получить массив байтов `buf` в виде текста или непосредственно в виде массива байт.

С помощью метода `writeTo()` мы можем вывести массив байт в другой поток. Данный метод в качестве параметра принимает объект `OutputStream`, в который производится запись массива байт:

```java
ByteArrayOutputStream baos = new ByteArrayOutputStream();
String text = "Hello Wolrd!";
byte[] buffer = text.getBytes();
try {
    baos.write(buffer);
} catch (Exception ex) {
    System.out.println(ex.getMessage());
}
try (FileOutputStream fos = new FileOutputStream("hello.txt")) {
    baos.writeTo(fos);
} catch (IOException e) {
    System.out.println(e.getMessage());
}
```

После выполнения этой программы в папке с программой появится файл `hello.txt`, который будет содержать строку `Hello Wolrd!`.

И в заключении также надо сказать, что как и для объектов `ByteArrayInputStream`, для `ByteArrayOutputStream` не надо явным образом закрывать поток с помощью метода `close()`.