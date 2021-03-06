# Класс DateTimeFormatter
Класс `DateTimeFormatter` используется в Java 8 при форматировании и разборе даты.

Для создания объекта этого класса используется статический метод `ofPattern()`, на вход которого передается строка и объект класс `Locale`:

```java
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("MMMM, dd, yyyy HH:mm:ss", Locale.US);
```

Строка описывает формат написания даты и времени. Если локаль не указана, используется текущая локаль.

В следующей табличке указаны возможные символы, для описания формата даты:

|Символ|Что означает|Пример|
|---|---|---|
|`y`|год в эре|2014; 14|
|`M/L`|месяц (название или номер)|9; 09; Sep; September; S|
|`d`|день месяца|17|
|`E`|день недели|Вт; вторник|
|`h`|время в 12-часовом формате|6|
|`H`|часы в 24-часовом формате|6|
|`m`|минуты|32|
|`s`|секунды|11|
|`S`|миллисекунды|109|

Для разбора даты и времени из строковых значений существует два статических метода `parse()`:

- `parse(CharSequence text)` - конвертация строки, которая содержит дату и время, в объект `LocalDateTime`. При этом используется формат строки вида `2007-12-03T10:15:30`.
- `parse(CharSequence text, DateTimeFormatter formatter)` - конвертация строки, которая содержит дату и время, в объект `LocalDateTime` с использованием указанного формата.

Рассмотрим пример разбора даты:

```java
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class FormatLocalDateTimeDemo1 {
    public static void main(String[] args) {
        DateTimeFormatter formatter1 = DateTimeFormatter.ofPattern("MMMM d, yyyy HH:mm:ss");
        LocalDateTime localDateTime = LocalDateTime.parse("июня 5, 2018 12:10:56", formatter1);
        System.out.println(localDateTime);

        DateTimeFormatter formatter2 = DateTimeFormatter.ofPattern("MMMM d, yyyy");
        LocalDate localDate = LocalDate.parse("июня 5, 2018", formatter2);
        System.out.println(localDate);
    }
}
```

Следующий пример описывает форматирование даты:

```java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.Locale;

public class FormatLocalDateTimeDemo2 {
    public static void main(String[] args) {
        LocalDateTime dateTime = LocalDateTime.now();
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("MMMM, dd, yyyy HH:mm:ss", Locale.US);
        System.out.println(dateTime.format(formatter));
    }
}
```