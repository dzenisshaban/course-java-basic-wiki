# Форматирование строк
## Класс `Formatter`
Базовой частью поддержки создания форматированного вывода в языке Java служит класс `Formatter`, включенный в пакет `java.util`. Он обеспечивает **преобразования формата** (**format conversions**) позволяющие выводить числа, строки и время и даты практически в любом понравившемся вам формате.

В классе `Formatter` объявлен метод `format()`, который преобразует переданные в него параметры в строку заданного формата и сохраняет в объекте типа `Formatter`.

Рассмотрим использование класса `Formatter`:

```java
import java.util.Formatter;

public class SimpleFormatString {
    public static void main(String[] args) {
        Formatter f = new Formatter();
        f.format("This %s is about %n%S %c", "book", "java", '8');
        System.out.print(f);
    }
}
```
где `%s` называется **спецификатором формата**.

Следующий пример использует класс `Formatter` для отображения дробного числа:

```java
import java.util.Formatter;

public class FormatDemo1 {
    public static void main(String[] args) {
        double x = 1000.0 / 3.0;
        System.out.println("Строка без форматирования: " + x);

        Formatter formatter = new Formatter();
        formatter.format("Строка c форматированием: %.2f%n", x);
        formatter.format("Строка c форматированием: %8.2f%n", x);
        formatter.format("Строка c форматированием: %16.2f%n", x);
        System.out.println(formatter);
    }
}
```

## Метод `format()` классов `String`, `PrintStream` и `PrintWriter`
Аналогичный метод `format()` объявлен у классов `PrintStream` и `PrintWriter`. `System.out` это статическая переменная типа `PrintStream`.

В Java 5 для классов `PrintStream` и `PrintWriter` добавлен метод `printf()`. Методы `printf()` и `format()` автоматически используют класс `Formatter`:

```java
public class FormatDemo4 {
    public static void main(String[] args) {
        System.out.printf("Строка c форматированием: %.2f%n", 1000.0 / 3.0);
        System.out.format("%s, в следующем году вам будет %d", "Джон", 23);
    }
}
```

С помощью метода `String.format()` тоже возможно форматирование:

```java
public class StringFormatDemo {
    public static void main(String[] args) {
        String str = String.format("Строка c форматированием: %16.2f", 1000.0 / 3.0);
        System.out.println(str);
    }
}
```


## Спецификаторы формата
- `%a` Шестнадцатеричное значение с плавающей точкой
- `%b` Логическое (булево) значение аргумента
- `%c` Символьное представление аргумента
- `%d` Десятичное целое значение аргумента
- `%h` Хэш-код аргумента
- `%e` Экспоненциальное представление аргумента
- `%f` Десятичное значение с плавающей точкой
- `%g` Выбирает более короткое представление из двух: `%е` или `%f`
- `%o` Восьмеричное целое значение аргумента
- `%n` Вставка символа новой строки
- `%s` Строковое представление аргумента
- `%t` Время и дата
- `%x` Шестнадцатеричное целое значение аргумента
- `%%` Вставка знака `%`


## Флаги формата
- `-` выравнивание влево
- `#` изменяет формат преобразования
- `0` выводит значение, дополненное нулями вместо пробелов. Применим только к числам
- ` ` положительные числа предваряются пробелом
- `+` положительные числа предваряются знаком +. Применим только к числам
- `,` числовые значения включают разделители групп. Применим только к числам
- `(` отрицательные числовые значения заключаются в скобки. Применим только к числам

Рассмотрим пример использования флагов:

```java
public class FormatterDemo2 {
    public static void main(String[] args) {
        System.out.printf("%,.2f%n", 10000.0 / 3.0);
        System.out.printf("%, (.2f%n", -10000.0 / 3.0);
        System.out.printf("%09.2f%n", 10000.0 / 3.0);
    }
}
```

В строке, определяющей формат, может задаваться индекс форматируемого параметра. Индекс должен следовать непосредственно за символом `%` и завершаться знаком `$`:

```java
public class FormatterDemo3 {
    public static void main(String[] args) {
        System.out.printf("Hello %1$s!%n%1$s, how are you?%n"
                        + "Welcome to the site %2$s",
                "John", "www.site.com");
    }
}
```

Общий синтаксис можно описать так:

```java
%[аргумент_индекс][флаги][ширина][.точность]символ_преобразования
```