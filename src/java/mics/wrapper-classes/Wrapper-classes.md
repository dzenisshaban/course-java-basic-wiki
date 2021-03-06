# Классы-оболочки
Очень часто необходимо создать класс, основное назначение которого содержать в себе какое-то примитивное значение. Например, как мы увидим в следующих занятиях, обобщенные классы и в частности коллекции работают только с объектами. Поэтому, чтобы каждый разработчик не изобретал велосипед, в Java уже добавлены такие классы, которые называются **оболочки типов** (**классы обертки**, **wrappers**).

К оболочкам типов относятся классы `Double`, `Float`, `Long`, `Integer`, `Short`, `Byte`, `Character`, `Boolean`, `Void`. Для каждого примитивного значения и ключевого слова `void` есть свой класс-двойник. Имя класса, как вы видите, совпадает с именем примитивного значения. Исключения составляют класс `Integer` (примитивный тип `int`) и класс `Character` (примитивный тип `char`). Кроме содержания в себе значения, классы оболочки предоставляют обширный ряд методов.

Объекты классов оболочек **неизменяемые** (**immutable**). Это значит, что объект не может быть изменен. 

Все классы-обертки числовых типов имеют переопределенный метод `equals(Object)`, сравнивающий примитивные значения объектов.


## Конструкторы оболочек
В следующей таблицы для каждого класса оболочки указан соответствующий примитивный тип и варианты конструкторов.

|Примитивный тип|Оболочка|Аргументы конструктора|
|---| ---|---|
|boolean|Boolean|boolean or String|
|byte|Byte|byte or String|
|char|Character|char|
|double|Double|double or String|
|float|Float|float, double, or String|
|int|Integer|int or String|
|long|Long|long or String|
|short|Short|short or String|

Как вы видите каждый класс имеет два конструктора, которые принимаю значения типа:
- соответствующего примитива
- `String`

Исключения: класс `Character`, у которого только один конструктор с аргументом `char` и класс `Float`, объявляющий три конструктора - для значения `float`, `String` и еще `double`.

Рассмотрим варианты вызова конструкторов на примере. Чтобы создать объект класса `Integer`, передаем в конструктор либо значение типа `int` либо `String`.

```java
Integer i1 = new Integer(42);
Integer i2 = new Integer("42");

Float f1 = new Float(3.14f);
Float f2 = new Float("3.14f");

Character c1 = new Character('c');
```

Если передаваемая в конструктор строка не содержит числового значения, то выбросится исключение `NumberFormatException`.

При вызове конструктора с аргументом `String` класса `Boolean`, не обязательно передавать строки `true` или `false`. Если аргумент содержит любую другую строку, просто будет создан объект, содержащий значение `false`. Исключение выброшено не будет:

```java
public class WrapperDemo1 {
    public static void main(String[] args) {
        Boolean boolean1 = new Boolean(true);
        Boolean boolean2 = new Boolean("Some String");

        System.out.println(boolean2);
    }
}
```


## Методы классов оболочек
Как уже было сказано, классы оболочки содержат обширный ряд методов. Рассмотрим их.


### Методы `valueOf()`
Метод `valueOf()` предоставляет второй способ создания объектов оболочек. Метод перегруженный, для каждого класса существует два варианта - один принимает на вход значение соответствующего типа, а второй - значение типа `String`. Так же как и с конструкторами, передаваемая строка должна содержать числовое значение. Исключение составляет опять же класс `Character` - в нем объявлен только один метод, принимающий на вход значение `char`. 

И в целочисленные классы `Byte`, `Short`, `Integer`, `Long` добавлен еще один метод, в который можно передать строку, содержащую число в любой системе исчисления. Вторым параметром вы указываете саму систему исчисления.

В следующем примере показано использование всех трех вариантов для создания объектов класса `Integer`:

```java
public class WrapperValueOf {
    public static void main(String[] args) {
        Integer integer1 = Integer.valueOf("6");
        Integer integer2 = Integer.valueOf(6);
        // преобразовывает 101011 к 43
        Integer integer3 = Integer.valueOf("101011", 2);

        System.out.println(integer1);
        System.out.println(integer2);
        System.out.println(integer3);
    }
}
```


### Методы `parseXxx()`
В каждом классе оболочке содержатся методы, позволяющие преобразовывать строку в соответствующее примитивное значение. В классе `Double` - это метод `parseDouble()`, в классе `Long` - `parseLong()` и так далее. Разница с методом `valueOf()` состоит в том, что метод `valueOf()` возвращает объект, а `parseXxx()` - примитивное значение.

Также в целочисленные классы `Byte`, `Short`, `Integer`, `Long` добавлен метод, в который можно передать строку, содержащую число в любой системе исчисления. Вторым параметром вы указываете саму систему исчисления. Следующий пример показывает использование метода `parseLong()`:

```java
public class WrapperDemo3 {
    public static void main(String[] args) {
        Long long1 = Long.valueOf("45");
        long long2 = Long.parseLong("67");
        long long3 = Long.parseLong("101010", 2);

        System.out.println("long1 = " + long1);
        System.out.println("long2 = " + long2);
        System.out.println("long3 = " + long3);
    }
}
```


### Методы `toString()`
Все типы-оболочки переопределяют `toString()`. Этот метод возвращает читабельную для человека форму значения, содержащегося в оболочке. Это позволяет выводить значение, передавая объект оболочки типа методу `println()`:

```java
Double double1 = Double.valueOf("4.6");
System.out.println(double1);​
```

Также все числовые оболочки типов предоставляют статический метод `toString()`, на вход которого передается примитивное значение. Метод возвращает значение `String`:

```java
String string1 = Double.toString(3.14);
```

`Integer` и `Long` предоставляют третий вариант `toString()` метода, позволяющий представить число в любой системе исчисления. Он статический, первый аргумент – примитивный тип, второй - основание системы счисления:

```java
String string2 = Long.toString(254, 16); // string2 = "fe"​
```


### Методы `toHexString()`, `toOctalString()`, `toBinaryString()`
`Integer` и `Long` позволяют преобразовывать числа из десятичной системы исчисления к шестнадцатеричной, восьмеричной и двоичной. Например:

```java
public class WrapperToXString {
    public static void main(String[] args) {
        String string1 = Integer.toHexString(254);
        System.out.println("254 в 16-ой системе = " + string1);

        String string2 = Long.toOctalString(254);
        System.out.println("254 в  8-ой системе = " + string2);

        String string3 = Long.toBinaryString(254);
        System.out.println("254 в  2-ой системе = " + string3);
    }
}
```

В классы `Double` и `Float` добавлен только метод `toHexString()`.


## Класс `Number`
Все оболочки числовых типов наследуют абстрактный класс `Number`. `Number` объявляет методы, которые возвращают значение объекта в каждом из различных числовых форматов.

![Класс Number](res/img/java/mics/wrapper-classes/wrapper-classes.png)

Пример приведения типов

```java
public class WrapperDemo2 {
    public static void main(String[] args) {
        Integer iOb = new Integer(1000);
        System.out.println(iOb.byteValue());
        System.out.println(iOb.shortValue());
        System.out.println(iOb.intValue());
        System.out.println(iOb.longValue());
        System.out.println(iOb.floatValue());
        System.out.println(iOb.doubleValue());
    }
}
```


## Статические константы классов оболочек
Каждый класс оболочка содержит статические константы, содержащие максимальное и минимальное значения для данного типа.

Например в классе `Integer` есть константы `Integer.MIN_VALUE` – минимальное `int` значение и `Integer.MAX_VALUE` – максимальное `int` значение.

Классы-обертки числовых типов `Float` и `Double`, помимо описанного для целочисленных примитивных типов, дополнительно содержат определения следующих констант:
- `NEGATIVE_INFINITY` – отрицательная бесконечность
- `POSITIVE_INFINITY` – положительная бесконечность
- `NaN` – не числовое значение (расшифровывается как **Not a Number**)

Следующий пример демонстрирует использование трех последних переменных. При делении на ноль возникает ошибка - на ноль делить нельзя. Чтобы этого не происходило, и ввели переменные `NEGATIVE_INFINITY` и `POSITIVE_INFINITY`. Результат умножения бесконечности на ноль - это значение `NaN`:

```java
public class InfinityDemo {
    public static void main(String[] args) {
        int a = 7;
        double b = 0.0;
        double c = -0.0;
        double g = Double.NEGATIVE_INFINITY;
        System.out.println("7 / 0.0 = " + a / b);
        System.out.println("7 / -0.0 = " + a / c);
        System.out.println("0.0 == -0.0 = " + (b == c));
        System.out.println("-Infinity * 0 = " + g * 0);
    }
}
```

Результат выполнения кода:

```out
7 / 0.0 = Infinity
7 / -0.0 = -Infinity
0.0 == -0.0 =  true
-Infinity * 0 = NaN
```