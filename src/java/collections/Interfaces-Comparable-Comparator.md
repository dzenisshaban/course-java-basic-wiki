## Interface `Comparable`
Рассмотрим коллекции `TreeSet`, типизированную объектами `String`. При добавлении новых элементов объект `TreeSet` автоматически проводит сортировку, помещая новый объект на правильное для него место. Что если бы использовались не строки, а классы, например, следующий класс `Person`:

```java
class Person {
    private String name;

    Person(String name) {
        this.name = name;
    }

    String getName() {
        return name;
    }
}
```

Объект `TreeSet` нельзя типизировать данным классом, поскольку в случае добавления объектов `TreeSet` не будет знать, как их сравнивать, и следующий код не будет работать:

```java
TreeSet<Person> people = new TreeSet<Person>();
people.add(new Person("Tom"));
```

При выполнении этого кода возникнет ошибка, которая скажет, что объект `Person` не может быть преобразован к типу `java.lang.Comparable`.

Для того, чтобы объекты `Person` можно было сравнить и сортировать, они должны применять интерфейс `Comparable<E>`. При применении интерфейса он типизируется текущим классом. Применим его к классу `Person`:

```java
class Person implements Comparable<Person> {
    private String name;

    Person(String name) {
        this.name = name;
    }

    String getName() {
        return name;
    }

    public int compareTo(Person p) {
        return name.compareTo(p.getName());
    }
}
```

Интерфейс `Comparable` содержит один единственный метод `int compareTo(E item)`, который сравнивает текущий объект с объектом, переданным в качестве параметра. Если этот метод возвращает отрицательное число, то текущий объект будет располагаться перед тем, который передается через параметр. Если метод вернет положительное число, то, наоборот, после второго объекта. Если метод возвратит `0`, значит, оба объекта равны.

В данном случае мы не возвращаем явным образом никакое число, а полагаемся на встроенный механизм сравнения, который есть у класса `String`. Но мы также можем определить и свою логику, например, сравнивать по длине имени:

```java
public int compareTo(Person p) {
    return name.length() - p.getName().length();
}
```

Теперь можно типизировать `TreeSet` типом `Person` и добавлять в дерево соответствующие объекты:

```java
TreeSet<Person> people = new TreeSet<Person>();
people.add(new Person("Tom"));
```


## Interface `Comparator`
Однако перед нами может возникнуть проблема, что если разработчик не реализовал в своем классе, который мы хотим использовать, интерфейс `Comparable`, либо реализовал, но нас не устраивает его функциональность, и мы хотим ее переопределить? На этот случай есть еще более гибкий способ, предполагающий применение интерфейса `Comparator<E>`.

Интерфейс `Comparator` содержит ряд методов, ключевым из которых является метод `compare()`:

```java
public interface Comparator<E> {
    int compare(T a, T b);
    // остальные методы
}
```

Метод `compare()` также возвращает числовое значение - если оно отрицательное, то объект `a` предшествует объекту `b`, иначе - наоборот. А если метод возвращает `0`, то объекты равны. Для применения интерфейса нам вначале надо создать класс компаратора, который реализует этот интерфейс:

```java
class PersonComparator implements Comparator<Person> {
    public int compare(Person a, Person b) {
        return a.getName().compareTo(b.getName());
    }
}
```

Здесь опять же проводим сравнение по строкам. Теперь используем класс компаратора для создания объекта `TreeSet`:

```java
PersonComparator pcomp = new PersonComparator();
TreeSet<Person> people = new TreeSet<Person>(pcomp);
people.add(new Person("Tom"));
people.add(new Person("Nick"));
people.add(new Person("Alice"));
people.add(new Person("Bill"));
for (Person p : people) {
    System.out.println(p.getName());
}
```

Для создания `TreeSet` здесь используется одна из версий конструктора, которая в качестве параметра принимает компаратор. Теперь вне зависимости от того, реализован ли в классе `Person` интерфейс `Comparable`, логика сравнения и сортировки будет использоваться та, которая определена в классе компаратора.


## Сортировка по нескольким критериям
Начиная с JDK 8 в механизм работы компараторов были внесены некоторые дополнения. В частности, теперь мы можем применять сразу несколько компараторов по принципу приоритета. Например, изменим класс `Person` следующим образом:

```java
class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    String getName() {
        return this.name;
    }

    int getAge() {
        return this.age;
    }
}
```

Здесь добавлено поле для хранения возраста пользователя. И, допустим, нам надо отсортировать пользователей по имени и по возрасту. Для этого определим два компаратора:
```java
class PersonNameComparator implements Comparator<Person> {
    public int compare(Person a, Person b) {
        return a.getName().compareTo(b.getName());
    }
}
```

```java
class PersonAgeComparator implements Comparator<Person> {
    public int compare(Person a, Person b) {
        int result = 0;
        if (a.getAge() > b.getAge()) {
            result = 1;
        } else if (a.getAge() < b.getAge()) {
            result = -1;
        }
        return result;
    }
}
```

Интерфейс компаратора определяет специальный метод по умолчанию `thenComparing()`, который позволяет использовать цепочки компараторов для сортировки набора:

```java
Comparator<Person> pcomp = new PersonNameComparator().thenComparing(new PersonAgeComparator());
TreeSet<Person> people = new TreeSet(pcomp);
people.add(new Person("Tom", 23));
people.add(new Person("Nick", 34));
people.add(new Person("Tom", 10));
people.add(new Person("Bill", 14));

for (Person p : people) {
    System.out.println(p.getName() + " " + p.getAge());
}
```

В данном случае сначала применяется сортировка по имени, а потом по возрасту.