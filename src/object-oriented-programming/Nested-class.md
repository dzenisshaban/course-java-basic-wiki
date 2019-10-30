## Вложенные классы
Классы могут быть **вложенными** (**nested**), то есть могут быть определены внури других классов.

![Nested Class](res/img/nested-class.png)

Частным случаем вложенных классов являются **внутренние классы** (**inner class**). Например, имеется класс `Person`, внутри которого определен класс `Account`:
```java
public class Program {
    public static void main(String[] args) {
        Person tom = new Person("Tom", "qwerty");
        tom.displayPerson();
        tom.account.displayAccount();
    }
}

class Person {
    private String name;
    Account account;

    Person(String name, String password) {
        this.name = name;
        account = new Account(password);
    }

    public void displayPerson() {
        System.out.printf("Person \t Name: %s \t Password: %s \n", name, account.password);
    }

    public class Account {
        private String password;

        Account(String pass) {
            this.password = pass;
        }

        void displayAccount() {
            System.out.printf("Account Login: %s \t Password: %s \n", Person.this.name, password);
        }
    }
}
```

Внутренний класс ведет себя как обычный класс за тем исключением, что его объекты могут быть созданы только внутри внешнего класса.

Внутренний класс имеет доступ ко всем полям внешнего класса, в том числе закрытым с помощью модификатора `private`. Аналогично внешний класс имеет доступ ко всем членам внутреннего класса, в том числе к полям и методам с модификатором `private`.

Ссылку на объект внешнего класса из внутреннего класса можно получить с помощью выражения `Внешний_класс.this`, например, `Person.this`.

Объекты внутренних классов могут быть созданы только в том классе, в котором внутренние классы опеределены. В других внешних классах объекты внутреннего класса создать нельзя.

Еще одной особенностей внутренних классов является то, что их можно объявить внутри любого контекста, в том числе внутри метода и даже в цикле:

```java
public class Program {
    public static void main(String[] args) {
        Person tom = new Person("Tom");
        tom.setAccount("qwerty");
    }
}

class Person {
    private String name;

    Person(String name) {
        this.name = name;
    }

    public void setAccount(String password) {
        class Account {
            void display() {
                System.out.printf("Account Login: %s \t Password: %s \n", name, password);
            }
        }
        Account account = new Account();
        account.display();
    }
}
```


## Статические вложенные классы
Кроме внутренних классов также могут статические вложенные классы. Статические вложенные классы позволяют скрыть некоторую комплексную информацию внутри внешнего класса:

```java
class Math {
    public static class Factorial {
        private int result;
        private int key;

        public Factorial(int number, int x) {
            this.result = number;
            this.key = x;
        }

        public int getResult() {
            return this.result;
        }

        public int getKey() {
            return this.key;
        }
    }

    public static Factorial getFactorial(int x) {
        int result = 1;
        for (int i = 1; i <= x; i++) {
            result *= i;
        }
        return new Factorial(result, x);
    }
}
```

Здесь определен вложенный класс для хранения данных о вычислении факториала. Основные действия выполняет метод `getFactorial()`, который возвращает объект вложенного класса. И теперь используем классы в методе `main()`:

```java
public static void main(String[] args) {
    Math.Factorial fact = Math.getFactorial(6);
    System.out.printf("Факториал числа %d равен %d \n", fact.getKey(), fact.getResult());
}
```