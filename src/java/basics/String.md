# Строки
Строка представляет собой последовательность символов. Для работы со строками в Java определен класс `String`, который предоставляет ряд методов для манипуляции строками. Физически объект `String` представляет собой ссылку на область в памяти, в которой размещены символы.

Для создания новой строки мы можем использовать один из конструкторов класса `String`, либо напрямую присвоить строку в двойных кавычках:

```java
public static void main(String[] args) {
    String str1 = "Java";
    String str2 = new String(); // пустая строка
    String str3 = new String(new char[] {'h', 'e', 'l', 'l', 'o'});
    String str4 = new String(new char[] {'w', 'e', 'l', 'c', 'o', 'm', 'e'}, 3, 4); // 3 -начальный индекс, 4 -количество символов
         
    System.out.println(str1); // Java
    System.out.println(str2); //
    System.out.println(str3); // hello
    System.out.println(str4); // come
}
```

При работе со строками важно понимать, что объект `String` является неизменяемым (**immutable**). То есть при любых операциях над строкой, которые изменяют эту строку, фактически будет создаваться новая строка.


## Конкатенация строк
Для соединения строк можно использовать операцию сложения `+`:
```java
String str1 = "Java";
String str2 = "Hello";
String str3 = str2 + " " + str1;
         
System.out.println(str3); // Hello Java
```
При этом если в операции сложения строк используется нестроковый объект, например, число, то этот объект преобразуется к строке:

```java
String str3 = "Год " + 2015;
```

Фактически же при сложении строк с нестроковыми объектами будет вызываться метод `valueOf()` класса `String`. Данный метод имеет множество перегрузок и преобразует практически все типы данных к строке. Для преобразования объектов различных классов метод `valueOf()` вызывает метод `toString()` этих классов.


## Основные методы класса String


### `lenght()`
Поскольку строка рассматривается как набор символов, то мы можем применить метод `length()` для нахождения длины строки или длины набора символов:

```java
String str1 = "Java";
System.out.println(str1.length()); // 4
```


### `toCharArray()`
С помощью метода `toCharArray()` можно обратно преобразовать строку в массив символов:

```java
String str1 = new String(new char[] {'h', 'e', 'l', 'l', 'o'});
char[] helloArray = str1.toCharArray();
```

Строка может быть пустой. Для этого ей можно присвоить пустые кавычки или удалить из стоки все символы:

```java
String s = ""; // строка не указывает на объект
if (s.length() == 0) {
    System.out.println("String is empty");
}
```
В этом случае длина строки, возвращаемая методом `length()`, равна `0`.


### `isEmpty()`
Класс `String` имеет специальный метод, который позволяет проверить строку на пустоту - `isEmpty()`. Если строка пуста, он возвращает `true`:

```java
String s = ""; // строка не указывает на объект
if (s.length() == 0) {
    System.out.println("String is empty");
}
```

Переменная `String` может не указывать на какой-либо объект и иметь значение `null`:

```java
String s = null; // строка не указывает на объект
if (s == null) {
    System.out.println("String is null");
}
```

Значение `null` не эквивалентно пустой строке. Например, в следующем случае мы столкнемся с ошибкой выполнения:

```java
String s = null; // строка не указывает на объект
if (s.length() == 0) { // NullPointerException
    System.out.println("String is empty");
}
```

Так как переменная не указывает ни на какой объект `String`, то соответственно мы не можем обращаться к методам объекта `String`. Чтобы избежать подобных ошибок, можно предварительно проверять строку на `null`:

```java
String s = null; // строка не указывает на объект
if (s != null && s.length() == 0) {
    System.out.println("String is empty");
}
```


### `concat()`
Для объединения строк измользуют метод `concat()`:

```java
String str1 = "Java";
String str2 = "Hello";
str2 = str2.concat(str1); // HelloJava
```

Метод `concat()` принимает строку, с которой надо объединить вызывающую строку, и возвращает соединенную строку.


### `join()`
Для объединения строт используют метод `join()`, который позволяет объединить строки с учетом разделителя. Например, выше две строки сливались в одно слово `"HelloJava"`, но в идеале мы бы хотели, чтобы две подстроки были разделены пробелом. И для этого используем метод `join()`:

```java
String str1 = "Java";
String str2 = "Hello";
String str3 = String.join(" ", str2, str1); // Hello Java
```

Метод `join()` является статическим. Первым параметром идет разделитель, которым будут разделяться подстроки в общей строке, а все последующие параметры передают через запятую произвольный набор объединяемых подстрок - в данном случае две строки, хотя их может быть и больше.


### `charAt()`
Для извлечения символов по индексу в классе `String` определен метод `charAt()`. Он принимает индекс, по которому надо получить символов, и возвращает извлеченный символ:

```java
String str = "Java";
char c = str.charAt(2);
System.out.println(c); // v
```

Как и в массивах индексация начинается с нуля.


### `getChars()`

Для извлечения группы символов или подстроку, то можно использовать метод `getChars(int srcBegin, int srcEnd, char[] dst, int dstBegin)`. Он принимает следующие параметры:
- `srcBegin` индекс в строке, с которого начинается извлечение символов
- `srcEnd` индекс в строке, до которого идет извлечение символов
- `dst` массив символов, в который будут извлекаться символы
- `dstBegin` индекс в массиве `dst`, с которого надо добавлять извлеченные из строки символы

```java
String str = "Hello world!";
int start = 6;
int end = 11;
char[] dst=new char[end - start];
str.getChars(start, end, dst, 0);
System.out.println(dst); // world
```


### `equals()` и `equalsIgnoreCase()`
Для сравнения строк используются методы `equals()` (с учетом регистра) и `equalsIgnoreCase()` (без учета регистра). Оба метода в качестве параметра принимают строку, с которой надо сравнить:

```java
String str1 = "Hello";
String str2 = "hello";
         
System.out.println(str1.equals(str2)); // false
System.out.println(str1.equalsIgnoreCase(str2)); // true
```

В отличие от сравнения числовых и других данных примитивных типов для строк не применяется знак равенства `==.` Вместо него надо использовать метод `equals()`.


### `regionMatches()`
Еще один специальный метод `regionMatches()` сравнивает отдельные подстроки в рамках двух строк. Он имеет следующие формы:

```java
boolean regionMatches(int toffset, String other, int oofset, int len)
boolean regionMatches(boolean ignoreCase, int toffset, String other, int oofset, int len)
```

Метод принимает следующие параметры:
- `ignoreCase` надо ли игнорировать регистр символов при сравнении. Если значение `true`, регистр игнорируется
- `toffset` начальный индекс в вызывающей строке, с которого начнется сравнение
- `other` строка, с которой сравнивается вызывающая
- `oofset` начальный индекс в сравниваемой строке, с которого начнется сравнение
- `len` количество сравниваемых символов в обеих строках

Используем метод:

```java
String str1 = "Hello world";
String str2 = "I work";
boolean result = str1.regionMatches(6, str2, 2, 3);
System.out.println(result); // true
```

В данном случае метод сравнивает 3 символа с 6-го индекса первой строки (`"wor"`) и 3 символа со 2-го индекса второй строки (`"wor"`). Так как эти подстроки одинаковы, то возвращается `true`.


### `compareTo()` и `compareToIgnoreCase()`
Методы `compareTo()` и `compareToIgnoreCase()` позволяют сравнить две строки, но при этом они также позволяют узнать больше ли одна строка, чем другая или нет. Если возвращаемое значение больше `0`, то первая строка больше второй, если меньше нуля, то, наоборот, вторая больше первой. Если строки равны, то возвращается `0`.

Для определения больше или меньше одна строка, чем другая, используется лексикографический порядок. То есть, например, строка `"A"` меньше, чем строка `"B"`, так как символ `'A'` в алфавите стоит перед символом `'B'`. Если первые символы строк равны, то в расчет берутся следующие символы. Например:

```java
String str1 = "hello";
String str2 = "world";
String str3 = "hell";
         
System.out.println(str1.compareTo(str2)); // -15 -> str1 меньше чем strt2
System.out.println(str1.compareTo(str3)); // 1 -> str1 больше чем str3
```


### `indexOf()` и `lastIndexOf()`
Метод `indexOf()` находит индекс первого вхождения подстроки в строку, а метод `lastIndexOf()` - индекс последнего вхождения. Если подстрока не будет найдена, то оба метода возвращают `-1`:

```java
String str = "Hello world";
int index1 = str.indexOf('l'); // 2
int index2 = str.indexOf("wo"); // 6
int index3 = str.lastIndexOf('l'); // 9
```


### `startsWith()` и `endsWith()`
Метод `startsWith()` позволяют определить начинается ли строка с определенной подстроки, а метод `endsWith()` позволяет определить заканчивается строка на определенную подстроку:

```java
String str = "myfile.exe";
boolean start = str.startsWith("my"); // true
boolean end = str.endsWith("exe"); // true
```

### `replace()`
Метод `replace()` позволяет заменить в строке одну последовательность символов на другую:

```java
String str = "Hello world";
String replStr1 = str.replace('l', 'd'); // Heddo world
String replStr2 = str.replace("Hello", "Bye"); // Bye world
```


### `trim()`
Метод `trim()` позволяет удалить начальные и конечные пробелы:

```java
String str = "  hello world  ";
str = str.trim(); // "hello world"
```


### `substring()`
Метод `substring()` возвращает подстроку, начиная с определенного индекса до конца или до определенного индекса:

```java
String str = "Hello world";
String substr1 = str.substring(6); // "world"
String substr2 = str.substring(3,5); // "lo"
```


### `toLowerCase()` и `toUpperCase()`
Метод `toLowerCase()` переводит все символы строки в нижний регистр, а метод `toUpperCase()` - в верхний

```java
String str = "Hello World"; 
System.out.println(str.toLowerCase()); // hello world
System.out.println(str.toUpperCase()); // HELLO WORLD
```


### `split()`
Метод `split()` позволяет разбить строку на подстроки по определенному разделителю. Разделитель - какой-нибудь символ или набор символов передается в качестве параметра в метод. Например, разобьем текст на отдельные слова:

```java
String text = "FIFA will never regret it";
String[] words = text.split(" ");
for (String word : words) {
    System.out.println(word);
}
```

В данном случае строка будет разделяться по пробелу. Консольный вывод:

```
FIFA
will
never
regret
it
```