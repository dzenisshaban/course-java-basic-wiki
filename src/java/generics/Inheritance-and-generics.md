## Наследование и обобщения
Обобщенные классы могут участвовать в иерархии наследования: могут наследоваться от других, либо выполнять роль базовых классов. Рассмотрим различные ситуации.

### Базовый обобщенный класс
При наследовании от обобщенного класса класс-наследник должен передавать данные о типе в конструкции базового класса:

```java
class Account<T> {
    private T id;

    public T getId() {
        return this.id;
    }

    public Account(T id) {
        this.id = id;
    }
}

class DepositAccount<T> extends Account<T> {
    public DepositAccount(T id) {
        super(id);
    }
}
```

В конструкторе `DepositAccount()` идет обращение к конструктору базового класса, в который передаются данные о типе.

Варианты использования классов:

```java
DepositAccount dAccount1 = new DepositAccount(20);
System.out.println(dAccount1.getId());
         
DepositAccount dAccount2 = new DepositAccount("12345");
System.out.println(dAccount2.getId());
```

При этом класс-наследник может добавлять и использовать какие-то свои параметры типов:

```java
class Account<T> {
    private T id;

    public T getId() {
        return this.id;
    }

    public Account(T id) {
        this.id = id;
    }
}

class DepositAccount<T, S> extends Account<T> {
    private S name;

    public S getName() {
        return this.name;
    }

    public DepositAccount(T id, S name) {
        super(id);
        this.name = name;
    }
}
```

Варианты использования:

```java
DepositAccount<Integer, String> dAccount1 = new DepositAccount(20, "Tom");
System.out.println(dAccount1.getId() + " : " + dAccount1.getName());
         
DepositAccount<String, Integer> dAccount2 = new DepositAccount("12345", 23456);
System.out.println(dAccount2.getId() + " : " + dAccount2.getName());
```

И еще одна ситуация - класс-наследник вообще может не быть обобщенным:

```java
class Account<T> {
    private T id;

    public T getId() {
        return this.id;
    }

    public Account(T id) {
        this.id = id;
    }
}

class DepositAccount extends Account<Integer> {
    public DepositAccount() {
        super(5);
    }
}
```

Здесь при наследовании явным образом указывается тип, который будет использоваться конструкциями базового класса, то есть тип `Integer`. Затем в конструктор базового класса передается значение именно этого типа - в данном случае число `5`.

Вариант использования:

```java
DepositAccount dAccount1 = new DepositAccount();
System.out.println(dAccount1.getId());
```


## Обобщенный класс-наследник
Также может быть ситуация, когда базовый класс является обычным необобщенным классом. Например:

```java
class Account {
    private String name;

    public String getName() {
        return this.name;
    }

    public Account(String name) {
        this.name = name;
    }
}

class DepositAccount<T> extends Account {
    private T id;

    public T getId() {
        return this.id;
    }

    public DepositAccount(String name, T id) {
        super(name);
        this.id = id;
    }
}
```

В этом случае использование конструкций базового класса в наследнике происходит как обычно.

## Преобразование обобщенных типов
Объект одного обобщенного типа можно привести к другому типу, если они используют один и тот же тип. Рассмотрим преобразование типов на примере следующих двух обобщенных классов:

```java
class Account<T> {
    private T id;

    T getId() {
        return this.id;
    }

    Account(T id) {
        this.id = id;
    }
}

class DepositAccount<T> extends Account<T> {
    DepositAccount(T id) {
        super(id);
    }
}
```

Мы можем привести объект `DepositAccount<Integer>` к `Account<Integer>` или `DepositAccount<String>` к `Account<String>`:

```java
DepositAccount<Integer> depAccount = new DepositAccount(10);
Account<Integer> account = (Account<Integer>) depAccount;
System.out.println(account.getId());
```

Но сделать то же самое с разнотипными объектами мы не можем. Например, следующий код не будет работать:

```java
DepositAccount<Integer> depAccount = new DepositAccount(10);
Account<String> account = (Account<String>) depAccount;
```