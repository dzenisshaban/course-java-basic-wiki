## Запись текста через буфер и `BufferedWriter`
Класс `BufferedWriter` записывает текст в поток, предварительно буферизируя записываемые символы, тем самым снижая количество обращений к физическому носителю для записи данных.

Класс `BufferedWriter` имеет следующие конструкторы:
- `BufferedWriter(Writer out)`
- `BufferedWriter(Writer out, int sz)`

В качестве параметра он принимает поток вывода, в который надо осуществить запись. Второй параметр указывает на размер буфера.

Например, осуществим запись в файл:

```java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;

public class Program {
    public static void main(String[] args) {
        try (BufferedWriter bw = new BufferedWriter(new FileWriter("notes4.txt"))) {
            String text = "Hello  World!\nHey! Teachers! Leave them kids alone.";
            bw.write(text);
        } catch (IOException ex) {
            System.out.println(ex.getMessage());
        }
    }
}
```


## Чтение текста и `BufferedReader`
Класс `BufferedReader` считывает текст из символьного потока ввода, буферизируя прочитанные символы. Использование буфера призвано увеличить производительность чтения данных из потока.

Класс `BufferedReader` имеет следующие конструкторы:
- `BufferedReader(Reader in)`
- `BufferedReader(Reader in, int sz)`

Второй конструктор, кроме потока ввода, из которого производится чтение, также определяет размер буфера, в который будут считываться символы.

Так как `BufferedReader` наследуется от класса `Reader`, то он может использовать все те методы для чтения из потока, которые определены в `Reader`. И также `BufferedReader` определяет свой собственный метод `readLine()`, который позволяет считывать из потока построчно.

Рассмотрим применение `BufferedReader`:

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class Program {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new FileReader("notes4.txt"))) {
            // чтение посимвольно
            int c;
            while ((c = br.read()) != -1) {
                System.out.print((char) c);
            }
        } catch (IOException ex) {
            System.out.println(ex.getMessage());
        }
    }
}
```

Также можно считать текст построчно:

```java
try (BufferedReader br = new BufferedReader(new FileReader("notes4.txt"))) {
    //чтение построчно
    String s;
    while ((s = br.readLine()) != null) {
        System.out.println(s);
    }
} catch (IOException ex) {
    System.out.println(ex.getMessage());
}
```


## Считывание с консоли в файл
Соединим оба класса `BufferedReader` и `BufferedWriter` для считывания с консоли в файл. Для этого определим следующий код программы:

```java
import java.io.*;

public class Program {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
             BufferedWriter bw = new BufferedWriter(new FileWriter("notes5.txt"))) {
            // чтение построчно
            String text;
            while (!(text = br.readLine()).equals("ESC")) {
                bw.write(text + "\n");
                bw.flush();
            }
        } catch (IOException ex) {
            System.out.println(ex.getMessage());
        }
    }
}
```

Здесь объект `BufferedReader` устанавливается для чтения с консоли с помощью объекта `new InputStreamReader(System.in)`. В цикле `while` считывается введенный текст. И пока пользователь не введет строку `ESC`, объект `BufferedWriter` будет записывать текст файл.

