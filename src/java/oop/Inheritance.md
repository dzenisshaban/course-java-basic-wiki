# Наследование
Одним из ключевых аспектов объектно-ориентированного программирования является **наследование** (**inheritance**). С помощью наследования можно расширить функционал уже имеющихся классов за счет добавления нового функционала или изменения старого. Например, имеется следующий класс `Person`, описывающий отдельного человека:

```java
class Person {
    private String name;
    public String getName() {
        return name;
    }
     
    public Person(String name) {  
        this.name = name;
    }
   
    public void display() {
        System.out.println("Name: " + name);
    }
}
```

И, возможно, впоследствии мы захотим добавить еще один класс, который описывает сотрудника предприятия - класс `Employee`. Так как этот класс реализует тот же функционал, что и класс `Person`, так как сотрудник - это также и человек, то было бы рационально сделать класс `Employee` **производным** (**subclass**, **наследником**, **подклассом**) от класса `Person`, который, в свою очередь, называется **базовым классом** (**superclass**, **родителем**, **суперклассом**):

```java
class Employee extends Person {
}
```

Чтобы объявить один класс наследником от другого, надо использовать после имени класса-наследника ключевое слово `extends`, после которого идет имя базового класса. Для класса `Employee` базовым является `Person`, и поэтому класс `Employee` наследует все те же поля и методы, которые есть в классе `Person`.

Использование классов:

```java
public class Program {
    public static void main(String[] args) {
        Person tom = new Person("Tom");
        tom.display();
        Employee sam = new Employee("Sam");
        sam.display();
    }
}

class Person {
    private String name;

    public String getName() {
        return name;
    }

    public Person(String name) {
        this.name = name;
    }

    public void display() {
        System.out.println("Name: " + name);
    }
}

class Employee extends Person {
}
```

Производный класс имеет доступ ко всем методам и полям базового класса (даже если базовый класс находится в другом пакете) кроме тех, которые определены с модификатором `private`. При этом производный класс также может добавлять свои поля и методы:

```java
public class Program {
    public static void main(String[] args) {
        Employee sam = new Employee("Sam", "Red Hat");
        sam.display(); // Sam
        sam.work(); // Sam works in Red Hat
    }
}

class Person {
    private String name;

    public String getName() {
        return name;
    }

    public Person(String name) {
        this.name = name;
    }

    public void display() {
        System.out.println("Name: " + name);
    }
}

class Employee extends Person {
    private String company;

    public Employee(String name, String company) {
        super(name);
        this.company = company;
    }

    public void work() {
        System.out.printf("%s works in %s \n", getName(), company);
    }
}
```

В данном случае класс `Employee` добавляет поле `company`, которое хранит место работы сотрудника, а также метод `work()`.

Если в базовом классе определены конструкторы, то в конструкторе производного классы необходимо вызвать один из конструкторов базового класса с помощью ключевого слова `super`. Например, класс `Person` имеет конструктор, который принимает один параметр. Поэтому в классе `Employee` в конструкторе нужно вызвать констуктор класса `Person`. После слова `super` в скобках идет перечисление передаваемых аргументов. Таким образом, установка имени сотрудника делегируется конструктору базового класса.

При этом вызов конструктора базового класса должен идти в самом начале в конструкторе производного класса.


## Переопределение методов
Производный класс может определять свои методы, а может переопределять методы, которые унаследованы от базового класса. Например, переопределим в классе `Employee` метод `display()`:

```java
public class Program {
    public static void main(String[] args) {
        Employee sam = new Employee("Sam", "Red Hat");
        sam.display();  // Sam
        // Works in Red Hat
    }
}

class Person {
    private String name;

    public String getName() {
        return name;
    }

    public Person(String name) {
        this.name = name;
    }

    public void display() {
        System.out.println("Name: " + name);
    }
}

class Employee extends Person {
    private String company;

    public Employee(String name, String company) {
        super(name);
        this.company = company;
    }

    @Override
    public void display() {
        System.out.printf("Name: %s \n", getName());
        System.out.printf("Works in %s \n", company);
    }
}
```

Перед переопределяемым методом указывается аннотация `@Override`. Данная аннотация в принципе необязательна.

При переопределении метода он должен иметь уровень доступа не меньше, чем уровень доступа в базовом класса. Например, если в базовом классе метод имеет модификатор `public`, то и в производном классе метод должен иметь модификатор `public`.

Однако в данном случае мы видим, что часть метода `display` в `Employee` повторяет действия из метода `display()` базового класса. Поэтому мы можем сократить класс `Employee`:

```java
class Employee extends Person {
    private String company;
      
    public Employee(String name, String company) {
        super(name);
        this.company = company;
    }

    @Override
    public void display() {
        super.display();
        System.out.printf("Works in %s \n", company);
    }
}
```
С помощью ключевого слова `super` мы также можем обратиться к реализации методов базового класса.


## Запрет наследования
Хотя наследование очень интересный и эффективный механизм, но в некоторых ситуациях его применение может быть нежелательным. И в этом случае можно запретить наследование с помощью ключевого слова `final`. Например:

```java
public final class Person {
}
```

Если бы класс `Person` был бы определен таким образом, то следующий код был бы ошибочным и не сработал, так как мы тем самым запретили наследование:

```java
class Employee extends Person {
}
```

Кроме запрета наследования можно также запретить переопределение отдельных методов. Например, в примере выше переопределен метод `displayInfo()`, запретим его переопределение:

```java
public class Person {
    public final void display() {
        System.out.println("Имя: " + name);
    }
}
```
В этом случае класс `Employee` не сможет переопределить метод `display()`.


## Динамическая диспетчеризация методов
Наследование и возможность переопределения методов открывают нам большие возможности. Прежде всего мы можем передать переменной суперкласса ссылку на объект подкласса:

```java
Person sam = new Employee("Sam", "Oracle");
```

Так как `Employee` наследуется от `Person`, то объект `Employee` является в то же время и объектом `Person`. Грубо говоря, любой работник предприятия одновременно является человеком.

Однако несмотря на то, что переменная представляет объект `Person`, виртуальная машина видит, что в реальности она указывает на объект `Employee`. Поэтому при вызове методов у этого объектов будет вызывать та версия методов, которая определена в классе `Employee`, а не в `Person`. Например:

```java
public class Program {
    public static void main(String[] args) {
        Person tom = new Person("Tom");
        tom.display();
        Person sam = new Employee("Sam", "Oracle");
        sam.display();
    }
}

class Person {
    private String name;

    public String getName() {
        return name;
    }

    public Person(String name) {
        this.name = name;
    }

    public void display() {
        System.out.printf("Person %s \n", name);
    }
}

class Employee extends Person {
    private String company;

    public Employee(String name, String company) {
        super(name);
        this.company = company;
    }

    @Override
    public void display() {
        System.out.printf("Employee %s works in %s \n", super.getName(), company);
    }
}
```

При вызове переопределенного метода виртуального машина динамически находит и вызывает именно ту версию метода, которая определена в подклассе. Данный процесс еще называется **динамическая диспетчеризация методов** (**dynamic method lookup**, **динамический поиск метода**).