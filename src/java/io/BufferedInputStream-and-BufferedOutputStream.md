Для оптимизации операций ввода-вывода используются буферизуемые потоки. Эти потоки добавляют к стандартным специальный буфер в памяти, с помощью которого повышается производительность при чтении и записи потоков.


## Класс `BufferedInputStream`
Класс `BufferedInputStream` накапливает вводимые данные в специальном буфере без постоянного обращения к устройству ввода. Класс `BufferedInputStream` определяет два конструктора:
- `BufferedInputStream(InputStream inputStream)`
- `BufferedInputStream(InputStream inputStream, int bufSize)`

Первый параметр - это поток ввода, с которого данные будут считываться в буфер. Второй параметр - размер буфера.

Например, буферизируем считывание данных из потока `ByteArrayInputStream`:

```java
import java.io.BufferedInputStream;
import java.io.ByteArrayInputStream;

public class Program {
    public static void main(String[] args) {
        String text = "Hello world!";
        byte[] buffer = text.getBytes();
        ByteArrayInputStream in = new ByteArrayInputStream(buffer);
        try (BufferedInputStream bis = new BufferedInputStream(in)) {
            int c;
            while ((c = bis.read()) != -1) {
                System.out.print((char) c);
            }
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
        System.out.println();
    }
}
```

Класс `BufferedInputStream` в конструкторе принимает объект `InputStream`. В данном случае таким объектом является экземпляр класса `ByteArrayInputStream`.

Как и все потоки ввода `BufferedInputStream` обладает методом `read()`, который считывает данные. И здесь мы считываем с помощью метода `read()` каждый байт из массива `buffer`.

Фактические все то же самое можно было сделать и с помощью одного `ByteArrayInputStream`, не прибегая к буферизированному потоку. Класс `BufferedInputStream` просто оптимизирует производительность при работе с потоком `ByteArrayInputStream`. Естественно вместо `ByteArrayInputStream` может использоваться любой другой класс, который унаследован от `InputStream`.


## Класс `BufferedOutputStream`
Класс `BufferedOutputStream` аналогично создает буфер для потоков вывода. Этот буфер накапливает выводимые байты без постоянного обращения к устройству. И когда буфер заполнен, производится запись данных.

`BufferedOutputStream` определяет два конструктора:
- `BufferedOutputStream(OutputStream outputStream)`
- `BufferedOutputStream(OutputStream outputStream, int bufSize)`

`outputStream` - это поток вывода, который унаследован от `OutputStream`, а `bufSize` - размер буфера.

Рассмотрим на примере записи в файл:

```java
import java.io.BufferedOutputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class Program {
    public static void main(String[] args) {
        String text = "Hello world!"; // строка для записи
        try (FileOutputStream out = new FileOutputStream("notes.txt");
             BufferedOutputStream bos = new BufferedOutputStream(out)) {
            byte[] buffer = text.getBytes(); // перевод строки в байты
            bos.write(buffer, 0, buffer.length);
        } catch (IOException ex) {
            System.out.println(ex.getMessage());
        }
    }
}
```

Класс `BufferedOutputStream` в конструкторе принимает в качестве параметра объект `OutputStream` - в данном случае это файловый поток вывода `FileOutputStream`. И также производится запись в файл. Опять же `BufferedOutputStream` не добавляет много новой функциональности, он просто оптимизирует действие потока вывода.