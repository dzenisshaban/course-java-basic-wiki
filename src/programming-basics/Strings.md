# Строки


## Введение в строки
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


### Конкатенация строк
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


## `StringBuffer` и `StringBuilder`
Объекты `String` являются неизменяемыми, поэтому все операции, которые изменяют строки, фактически приводят к созданию новой строки, что сказывается на производительности приложения. Для решения этой проблемы, чтобы работа со строками проходила с меньшими издержками в Java были добавлены классы `StringBuffer` и `StringBuilder`. По сути они напоминает расширяемую строку, которую можно изменять без ущерба для производительности.

Эти классы похожи, практически двойники, они имеют одинаковые конструкторы, одни и те же методы, которые одинаково используются. Единственное их различие состоит в том, что класс `StringBuffer` синхронизированный и потокобезопасный. То есть класс `StringBuffer` удобнее использовать в многопоточных приложениях, где объект данного класса может меняться в различных потоках. Если же речь о многопоточных приложениях не идет, то лучше использовать класс `StringBuilder`, который не потокобезопасный, но при этом работает быстрее, чем `StringBuffer` в однопоточных приложениях.

`StringBuffer` определяет четыре конструктора:

```java
StringBuffer()
StringBuffer(int capacity)
StringBuffer(String str)
StringBuffer(CharSequence chars)
```

Аналогичные конструкторы определяет `StringBuilder`:

```java
StringBuilder()
StringBuilder(int capacity)
StringBuilder(String str)
StringBuilder(CharSequence chars)
```

Рассмотрим работу этих классов на примере функциональности `StringBuffer`.

При всех операциях со строками `StringBuffer` / `StringBuilder` перераспределяет выделенную память. И чтобы избежать слишком частого перераспределения памяти, `StringBuffer`/`StringBuilder` заранее резервирует некоторую область памяти, которая может использоваться. Конструктор без параметров резервирует в памяти место для 16 символов. Если мы хотим, чтобы количество символов было иным, то мы можем применить второй конструктор, который в качестве параметра принимает количество символов.

Третий и четвертый конструкторы обоих классов принимают строку и набор символов, при этом резервируя память для дополнительных 16 символов.

С помощью метода `capacity()` мы можем получить количество символов, для которых зарезервирована память. А с помощью метода `ensureCapacity()` изменить минимальную емкость буфера символов:

```java
String str = "Java";
StringBuffer strBuffer = new StringBuffer(str);
System.out.println("Емкость: " + strBuffer.capacity()); // 20
strBuffer.ensureCapacity(32);
System.out.println("Емкость: " + strBuffer.capacity()); // 42
System.out.println("Длина: " + strBuffer.length()); // 4
```

Так как в самом начале `StringBuffer` инициализируется строкой `"Java"`, то его емкость составляет 4 + 16 = 20 символов. Затем мы увеличиваем емкость буфера с помощью вызова `strBuffer.ensureCapacity(32)` повышаем минимальную емкость буфера до 32 символов. Однако финальная емкость может отличаться в большую сторону. Так, в данном случае я получаю емкость не 32 и не 32 + 4 = 36, а 42 символа. Дело в том, что в целях повышения эффективности Java может дополнительно выделять память.

Но в любом случае вне зависимости от емкости длина строки, которую можно получить с помощью метода `length()`, в `StringBuffer` остается прежней - 4 символа (так как в `"Java"` 4 символа).

Чтобы получить строку, которая хранится в `StringBuffer`, мы можем использовать стандартный метод `toString()`:

```java
String str = "Java";
StringBuffer strBuffer = new StringBuffer(str);
System.out.println(strBuffer.toString()); // Java
```

По всем своим операциям `StringBuffer` и `StringBuilder` напоминают класс `String`.

### `charAt()` и `setCharAt()`
Метод `charAt()` получает, а метод `setCharAt()` устанавливает символ по определенному индексу:

```java
StringBuffer strBuffer = new StringBuffer("Java");
char c = strBuffer.charAt(0); // J
System.out.println(c);
strBuffer.setCharAt(0, 'c');
System.out.println(strBuffer.toString()); // cava
```


### `getChars()`
Метод `getChars()` получает набор символов между определенными индексами:

```java
StringBuffer strBuffer = new StringBuffer("world");
int startIndex = 1;
int endIndex = 4;
char[] buffer = new char[endIndex-startIndex];
strBuffer.getChars(startIndex, endIndex, buffer, 0);
System.out.println(buffer); // orl
```


### `append()`
Метод `append()` добавляет подстроку в конец `StringBuffer`:

```java
StringBuffer strBuffer = new StringBuffer("hello");
strBuffer.append(" world");
System.out.println(strBuffer.toString()); // hello world
```


### `insert()`
Метод `insert()` добавляет строку или символ по определенному индексу в `StringBuffer`:

```java
StringBuffer strBuffer = new StringBuffer("word");
         
strBuffer.insert(3, 'l');
System.out.println(strBuffer.toString()); // world
 
strBuffer.insert(0, "s");
System.out.println(strBuffer.toString()); // sworld
```


### `delete()` и `deleteCharAt()`
Метод `delete()` удаляет все символы с определенного индекса о определенной позиции, а метод `deleteCharAt()` удаляет один символ по определенному индексу:

```java
StringBuffer strBuffer = new StringBuffer("assembler");
strBuffer.delete(0,2);
System.out.println(strBuffer.toString()); // sembler
         
strBuffer.deleteCharAt(6);
System.out.println(strBuffer.toString()); // semble
```


### `substring()`
Метод `substring()` обрезает строку с определенного индекса до конца, либо до определенного индекса:

```java
StringBuffer strBuffer = new StringBuffer("hello java!");
String str1 = strBuffer.substring(6); // обрезка строки с 6 символа до конца
System.out.println(str1); //java!
         
String str2 = strBuffer.substring(3, 9); // обрезка строки с 3 по 9 символ 
System.out.println(str2); //lo jav
```


### `setLength()`
Для изменения длины `StringBuffer` (не емкости буфера символов) применяется метод `setLength()`. Если `StringBuffer` увеличивается, то его строка просто дополняется в конце пустыми символами, если уменьшается - то строка по сути обрезается:

```java
StringBuffer strBuffer = new StringBuffer("hello");
strBuffer.setLength(10);
System.out.println(strBuffer.toString()); // "hello     "
         
strBuffer.setLength(4);
System.out.println(strBuffer.toString()); // "hell"
```


### `replace()`
Для замены подстроки между определенными позициями в `StringBuffer` на другую подстроку применяется метод `replace()`:

```java
StringBuffer strBuffer = new StringBuffer("hello world!");
strBuffer.replace(6, 11, "java");
System.out.println(strBuffer.toString()); // hello java!
```

Первый параметр метода `replace()` указывает, с какой позиции надо начать замену, второй параметр - до какой позиции, а третий параметр указывает на подстроку замены.


### `reverse()`
Метод `reverse()` меняет порядок в `StringBuffer` на обратный:

```java
StringBuffer strBuffer = new StringBuffer("assembler");
strBuffer.reverse();
System.out.println(strBuffer.toString()); // relbmessa
```


## Регулярные выражения
Регулярные выражения представляют мощный инструмент для обработки строк. Регулярные выражения позволяют задать шаблон, которому должна соответствовать строка или подстрока.

Большая часть функциональности по работе с регулярными выражениями в **Java** сосредоточена в пакете `java.util.regex`.

Само регулярное выражение представляет шаблон для поиска совпадений в строке. Для задания подобного шаблона и поиска подстрок в строке, которые удовлетворяют данному шаблону, в **Java** определены классы `Pattern` и `Matcher`.


### `Pattern`
#### `matches()`
Для простого поиска соответствий в классе `Pattern` определен статический метод `matches(String pattern, CharSequence input)`. Данный метод возвращает `true`, если последовательность символов `input` полностью соответствует шаблону строки `pattern`:

```java
import java.util.regex.Pattern;
 
public class StringsApp {
    public static void main(String[] args) {
        String input = "Hello";
        boolean found = Pattern.matches("Hello", input);
        if(found) {
            System.out.println("Найдено");
        } else {
            System.out.println("Не найдено");
        }
    }   
}
```


#### `split()`
С помощью метода `split()` класса `Pattern` можно разделить строку на массив подстрок по определенному разделителю. Например, мы хотим выделить из строки отдельные слова:

```java
import java.util.regex.Pattern;
 
public class StringsApp {
    public static void main(String[] args) {
        String input = "Hello Java! Hello JavaScript! JavaSE.";
        Pattern pattern = Pattern.compile("[ ,.!?]");
        String[] words = pattern.split(input);
        for (String word : words) {
            System.out.println(word);
        }
    }   
}
```

И консоль выведет набор слов:

```
Hello
Java

Hello
JavaScript

JavaSE
```

При этом все символы-разделители удаляются. Однако, данный способ разбивки не идеален: у нас остаются некоторые пробелы, которые расцениваются как лексемы, а не как разделители. Для более точной и изощренной разбивки нам следует применять элементы регулярных выражений. Так, заменим шаблон на следующий:

```java
Pattern pattern = Pattern.compile("\\s*(\\s|,|!|\\.)\\s*");
```

Теперь у нас останутся только слова:

```
Hello
Java
Hello
JavaScript
JavaSE
8
```


### `Matcher`
Но, как правило, для поиска соответствий применяется другой способ - использование класса `Matcher`.

Используем класс `Matcher`. Для этого вначале надо создать объект `Pattern` с помощью статического метода `compile()`, который позволяет установить шаблон:

```java
Pattern pattern = Pattern.compile("Hello");
```

В качестве шаблона выступает строка `"Hello"`. Метод `compile()` возвращает объект `Pattern`, который мы затем можем использовать в программе.

В классе `Pattern` также определен метод `matcher()`, который в качестве параметра принимает строку, где надо проводить поиск, и возвращает объект `Matcher`:

```java
String input = "Hello world! Hello Java!";
Pattern pattern = Pattern.compile("hello");
Matcher matcher = pattern.matcher(input);
```


#### `matches()`
Затем у объекта `Matcher` вызывается метод `matches()` для поиска соответствий шаблону в тексте:

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;
 
public class StringsApp {
    public static void main(String[] args) {
        String input = "Hello";
        Pattern pattern = Pattern.compile("Hello");
        Matcher matcher = pattern.matcher(input);
        boolean found = matcher.matches();
        if (found) {
            System.out.println("Найдено");
        } else {
            System.out.println("Не найдено");
        }
    }   
}
```


#### `find()` и `group()`
Рассмотрим более функциональный пример с нахождением не полного соответствия, а отдельных совпадений в строке:

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;
 
public class StringsApp {
    public static void main(String[] args) {
        String input = "Hello Java! Hello JavaScript! JavaSE.";
        Pattern pattern = Pattern.compile("Java(\\w*)");
        Matcher matcher = pattern.matcher(input);
        while (matcher.find()) {
            System.out.println(matcher.group());
        }
    }   
}
```

Допустим, мы хотим найти в строке все вхождения слова `Java`. В исходной строке это три слова: `"Java"`, `"JavaScript"` и `"JavaSE"`. Для этого применим шаблон `"Java(\\w*)"`. Данный шаблон использует синтаксис регулярных выражений. Слово `"Java"` в начале говорит о том, что все совпадения в строке должны начинаться на `Java`. Выражение `(\\w*)` означает, что после `"Java"` в совпадении может находиться любое количество алфавитно-цифровых символов. Выражение `\w` означает алфавитно-цифровой символ, а звездочка после выражения указывает на неопределенное их количество - их может быть один, два, три или вообще не быть. И чтобы java не рассматривала `\w` как эскейп-последовательность, как `\n`, то выражение экранируется еще одним слешем.

Далее применяется метод `find()` класса `Matcher`, который позволяет переходить к следующему совпадению в строке. То есть первый вызов этого метода найдет первое совпадение в строке, второй вызов найдет второе совпадение и т.д. То есть с помощью цикла `while(matcher.find())` мы можем пройтись по всем совпадениям. Каждое совпадение мы можем получить с помощью метода `matcher.group()`. В итоге программа выдаст следующий результат:

```
Java
JavaScript
JavaSE
```


#### `replaceAll()`
Можно сделать замену всех совпадений с помощью метода `replaceAll()`:

```java
String input = "Hello Java! Hello JavaScript! JavaSE.";
Pattern pattern = Pattern.compile("Java(\\w*)");
Matcher matcher = pattern.matcher(input);
String newStr = matcher.replaceAll("HTML");
System.out.println(newStr); // Hello HTML! Hello HTML! HTML.
```


### `String`
Некоторые методы класса `String` принимают регулярные выражения и используют их для выполнения операций над строками.


#### `split()`
Для разделения строки на подстроки применяется метод `split()`. В качестве параметра он может принимать регулярное выражение, которое представляет критерий разделения строки.

Например, разделим предложение на слова:

```java
String text = "FIFA will never regret it";
String[] words = text.split("\\s*(\\s|,|!|\\.)\\s*");
for (String word : words) {
    System.out.println(word);
}
```

Для разделения применяется регулярное выражение `"\\s*(\\s|,|!|\\.)\\s*"`. Подвыражние `"\\s"` по сути представляет пробел. Звездочка указывает, что символ может присутствовать от 0 до бесконечного количества раз. То есть добавляем звездочку и мы получаем неопределенное количество идущих подряд пробелов - `"\\s*"` (то есть неважно, сколько пробелов между словами). Причем пробелы может вообще не быть. В скобках указывает группа выражений, которая может идти после неопределенного количества пробелов. Группа позволяет нам определить набо значений через вертикальную черту, и подстрока должна соответствовать одному из этих значений. То есть в группе `"\\s|,|!|\\."` подстрока может соответствовать пробелу, запятой, восклицательному знаку или точке. Причем поскольку точка представляет специальную последовательность, то, чтобы указать, что мы имеем в виду имеено знак точки, а не специальную последовательность, перед точкой ставим слеши.


#### `matches()`
Еще один метод класса `String` - `matches()` принимает регулярное выражение и возвращает `true`, если строка соответствует этому выражению. Иначе возвращает `false`.

Например, проверим, соответствует ли строка номеру телефона:

```java
String input = "+12343454556";
boolean result = input.matches("(\\+*)\\d{11}");
if (result == true) {
    System.out.println("It is a phone number");
} else {
    System.out.println("It is not a phone number!");    
}
```

В данном случае в регулярном выражение сначала определяется группа `"(\\+*)"`. То есть вначале может идти знак плюса, но также он может отсутствовать. Далее смотрим, соответствуют ли последующие 11 символов цифрам. Выражение `"\\d"` представляет цифровой символ, а число в фигурных скобках - `{11}` - сколько раз данный тип символов должен повторяться. То есть мы ищем строку, где вначале может идти знак плюс (или он может отсутствовать), а потом идет 11 цифровых символов.


#### `replaceAll()`
Также надо отметить, что в классе `String` также имеется метод `replaceAll()` с заменой всех выражений, удовлетворяющих регулярному выражению:

```java
String input = "Hello Java! Hello JavaScript! JavaSE.";
String myStr =input.replaceAll("Java(\\w*)", "HTML");
System.out.println(myStr); // Hello HTML! Hello HTML! HTML.
```