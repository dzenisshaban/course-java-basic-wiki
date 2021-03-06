## Aвтоупаковка и распаковка (since version 5)
Автоупаковка и распаковка это процесс преобразования примитивных типов в объектные и наоборот. Весь процесс выполняется автоматически средой выполнения Java (JRE). 

```java
public class AutoBoxDemo1 {
    public static void main(String[] args) {
        Integer iOb = 100; // упаковать значение int
        int i = iOb; // распаковать
        System.out.println(i + " " + iOb);
    }
}
```

Автоупаковка происходит при прямом присвоении примитива классу-обертке (с помощью оператора `=`), либо при передаче примитива в параметры метода.

Распаковка происходит при прямом присвоении классу-обертке примитива.

Компилятор использует метод `valueOf()` для упаковки, а методы `intValue()`, `doubleValue()` и так далее, для распаковки.

Автоупаковке в *классы-обертки* могут быть подвергнуты как переменные примитивных типов, так и литералы:

```java
Integer iOb1 = 100;
int i = 200;
Integer iOb2 = i;
```
Автоупаковка переменных примитивных типов требует точного соответствия типа исходного примитива — типу *класса-обертки*.

Например, попытка автоупаковать переменную типа `byte` в `Short`, без предварительного явного приведения `byte` в `short` вызовет ошибку компиляции:

```java
byte b = 4;
// Short s1 = b;
Short s2 = (short) b;
```

Автоупаковку можно использовать при вызове метода:

```java
public class AutoBoxAndMethods {
    static int someMethod(Integer value) {
        return value;
    }

    public static void main(String[] args) {
        Integer iOb = someMethod(100);
        System.out.println(iOb);
    }
}
```

Внутри выражения числовой объект автоматически распаковывается. Выходной результат выражения при необходимости упаковывается заново:

```java
public class AutoBoxAndOperations {
    public static void main(String[] args) {
        Integer iOb1, iOb2;
        int i;

        iOb1 = 100;

        iOb2 = iOb1 + iOb1 / 3;
        System.out.println("iOb2 после выражения: " + iOb2);

        i = iOb1 + iOb1 / 3;
        System.out.println("i после выражения: " + i);
    }
}
```

C появлением автоупаковки/распаковки стало возможным применять объекты `Boolean` для управления в операторе `if` и других циклических конструкциях Java:

```java
public class AutoBoxAndCharacters {
    public static void main(String[] args) {
        Boolean b = true;

        if (b) {
            System.out.println("В if тоже можно использовать распаковку.");
        }

        Character ch = 'x';
        char ch2 = ch;

        System.out.println("ch2 = " + ch2);
    }
}
```

До Java 5 работа с классами обертками была более трудоемкой:

```java
public class AutoBoxDemo2 {
    public static void main(String[] args) {
        Integer y = new Integer(567);
        int x = y.intValue();
        x++;
        y = new Integer(x);
        System.out.println("y = " + y);
    }
}
```

Перепишет тот же пример для работы с классами начиная с Java 5:

```java
public class AutoBoxDemo3 {
    public static void main(String[] args) {
        Integer y = new Integer(567);
        y++;
        System.out.println("y = " + y);
    }
}
```


## Объекты классов оболочек неизменяемые
Объекты классов оболочек **неизменяемые** (**immutable**):

```java
public class AutoBoxImmutability {
    public static void main(String[] args) {
        Integer y = 567;
        Integer x = y;
        // проверяем, что x и y указывают на один объект
        System.out.println(y == x);

        y++;
        System.out.println(x + " " + y);
        // проверяем, что x и y указывают на один объект
        System.out.println(y == x);
    }
}
```
Рассмотрим следующий пример:

```java
Integer y = 567;
```

Переменная `y` указывает на объект в памяти:

![Объекты классов оболочек неизменяемы](res/img/java/mics/wrapper-classes/wrapper-immutable1.png)

Если мы попытаемся изменить `y`, у нас создастся еще один объект в памяти, на который теперь и будет указывать `y`:

```java
Integer y = 567;
y++;
```

![Объекты классов оболочек неизменяемы](res/img/java/mics/wrapper-classes/wrapper-immutable2.png)


## Кэширование объектов классов оболочек
Метод `valueOf()` не всегда создает новый объект. Он кэширует следующие значения:
- `Boolean`, 
- `Byte`,
- `Character` от `\u0000` до `\u007f` (`7f` это `127`),
- `Short` и `Integer` от `-128` до `127`.

Если передаваемое значение выходит за эти пределы, то новый объект создается, а если нет, то нет.

Если мы пишем `new Integer()`, то гарантированно создается новый объект.

Рассмотрим это на следующем примере:

```java
public class AutoBoxDemoCaching {
    public static void main(String[] args) {
        Integer i1 = 23;
        Integer i2 = 23;
        System.out.println(i1 == i2);
        System.out.println(i1.equals(i2));

        Integer i3 = 2300;
        Integer i4 = 2300;
        System.out.println(i3 == i4);
        System.out.println(i3.equals(i4));
    }
}
```