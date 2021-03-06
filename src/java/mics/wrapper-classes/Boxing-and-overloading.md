# Перегрузка с дополнительными факторами (since version 5)
Перегрузка методов усложняется при одновременном использовании следующих факторов:
- расширение
- автоупаковка/распаковка
- аргументы переменной длины


## Расширение примитивных типов
При расширение примитивных типов используется наименьший возможный вариант из всех методов.

```java
public class EasyOver {
    static void go(int x) {
        System.out.print("int ");
    }

    static void go(long x) {
        System.out.print("long ");
    }

    static void go(double x) {
        System.out.print("double ");
    }

    public static void main(String[] args) {
        byte b = 5;
        short s = 5;
        long l = 5;
        float f = 5.0f;
        go(b);
        go(s);
        go(l);
        go(f);
    }
}
```


## Расширение и boxing
Между расширением примитивных типов и boxing всегда выигрывает расширение. Исторически это более старый вид преобразования.

```java
public class AddBoxing {
    public static void go(Integer x) {
        System.out.println("Integer");
    }

    public static void go(long x) {
        System.out.println("long");
    }

    public static void main(String[] args) {
        int i = 5;
        go(i); // какой go() вызовется?
    }
}
```


## Упаковка и расширение
Можно упаковать, а потом расширить. Значение типа `int` может стать `Object`, через преобразование `Integer`.

```java
public class BoxAndWiden {
    public static void go(Object o) {
        Byte b2 = (Byte) o;
        System.out.println(b2);
    }

    public static void main(String[] args) {
        byte b = 5;
        go(b); // можно ли преобразовать byte в Object?
    }
}
```


## Расширение и упаковка
Нельзя расширить и упаковать. Значение типа `byte` не может стать `Long`. Нельзя расширить от одного класса обертки к другой. (**IS-A** не работает.)

```java
public class WidenAndBox {
    static void go(Long x) {
        System.out.println("Long");
    }

    public static void main(String[] args) {
        byte b = 5;
        // go(b); // нужно расширить до long и упаковать, что невозможно
    }
}
```


## Расширение и аргументы переменной длины
Между расширением примитивных типов и *var-args* всегда проигрывает *var-args*:

public class AddVarargs {
    public static void go(int x, int y) {
        System.out.println("int,int");
    }

    public static void go(byte... x) {
        System.out.println("byte... ");
    }

    public static void main(String[] args) {
        byte b = 5;
        go(b, b); // какой go() вызовется?
    }
}


## Упаковка и аргументы переменной длины
Упаковка и *var-args* совместимы с перегрузкой методов. *Var-args* всегда проигрывает:

```java
public class BoxOrVararg {
    public static void go(Byte x, Byte y) {
        System.out.println("Byte, Byte");
    }

    public static void go(byte... x) {
        System.out.println("byte... ");
    }

    public static void main(String[] args) {
        byte b = 5;
        go(b, b); // какой go() вызовется?
    }
}
```


## Правила перегрузки методов при использовании расширения, упаковки и аргументов переменной длины
Подытожим все правила:
- При расширение примитивных типов используется наименьший возможный вариант из всех методов.
- Между расширением примитивных типов и упаковкой всегда выигрывает расширение. Исторически это более старый вид преобразования.
- Можно упаковать, а потом расширить. (Значение типа `int` может стать `Object`, через преобразование `Integer`.)
- Нельзя расширить и упаковать. Значение типа `byte` не может стать `Long`. Нельзя расширить от одного класса обертки к другой. (*IS-A* не работает.)
- Можно комбинировать *var-args* с расширением или упаковкой. *var-args* всегда проигрывает.