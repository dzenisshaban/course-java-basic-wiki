# Фильтрация, перебор элементов и отображение

## `forEach()`
Для перебора элементов потока применяется метод `forEach()`, который представляет терминальную операцию. В качестве параметра он принимает объект `Consumer<? super String>`, который представляет действие, выполняемое для каждого элемента набора. Например:

```java
Stream<String> citiesStream = Stream.of("Париж", "Лондон", "Мадрид","Берлин", "Брюссель");
citiesStream.forEach(s -> System.out.println(s));
```

Фактически это будет аналогично перебору всех элементов в цикле `for` и выполнению с ними действия, а именно вывод на консоль. В итоге консоль выведет:

```output
Париж
Лондон
Мадрид
Берлин
Брюссель
```

Кстати мы можем сократить в данном случае применение метода `forEach` следующим образом:

```java
Stream<String> citiesStream = Stream.of("Париж", "Лондон", "Мадрид","Берлин", "Брюссель");
citiesStream.forEach(System.out::println);
```

Фактически здесь переадается ссылка на статический метод, который выводит строку на консоль.


## `filter()`
Для фильтрации элементов в потоке применяется метод `filter()`, который представляет промежуточную операцию. Он принимает в качестве параметра некоторое условие в виде объекта `Predicate<T>` и возвращает новый поток из элементов, которые удовлетворяют этому условию:

```java
Stream<String> citiesStream = Stream.of("Париж", "Лондон", "Мадрид","Берлин", "Брюссель");
citiesStream.filter(s -> s.length() == 6).forEach(s -> System.out.println(s));
```

Здесь условие `s.length() == 6` возвращает `true` для тех элементов, длина которых равна `6` символам. То есть в итоге программа выведет:

```output
Лондон
Мадрид
Берлин
```

Рассмотрим еще один пример фильтрации с более сложными данными. Допустим, у нас есть следующий класс `Phone`:

```java
class Phone {
    private String name;
    private int price;

    public Phone(String name, int price) {
        this.name = name;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getPrice() {
        return price;
    }

    public void setPrice(int price) {
        this.price = price;
    }
}
```

Отфильтруем набор телефонов по цене:

```java
Stream<Phone> phoneStream = Stream.of(
    new Phone("iPhone 6 S", 54000),
    new Phone("Lumia 950", 45000),
    new Phone("Samsung Galaxy S 6", 40000)
);

phoneStream.filter(p -> p.getPrice() < 50000)
        .forEach(p -> System.out.println(p.getName()));
```

## `map()`
Отображение или маппинг позволяет задать функцию преобразования одного объекта в другой, то есть получить из элемента одного типа элемент другого типа. Для отображения используется метод `map()`, который имеет следующее определение:

```java
<R> Stream<R> map(Function<? super T, ? extends R> mapper)
```

Передаваемая в метод `map()` функция задает преобразование от объектов типа `T` к типу `R`. И в результате возвращается новый поток с преобразованными объектами.

Возьмем вышеопределенный класс телефонов и выполним преобразование от типа `Phone` к типу `String`:

```java
Stream<Phone> phoneStream = Stream.of(
    new Phone("iPhone 6 S", 54000),
    new Phone("Lumia 950", 45000),
    new Phone("Samsung Galaxy S 6", 40000)
);
phoneStream.map(p -> p.getName()) // помещаем в поток только названия телефонов
        .forEach(s -> System.out.println(s));
```

Операция `map(p -> p.getName())` помещает в новый поток только названия телефонов. В итоге на консоли будут только названия:

```output
iPhone 6 S
Lumia 950
Samsung Galaxy S 6
```

Еще проведем преобразования:

```java
phoneStream
        .map(p -> "название: " + p.getName() + " цена: " + p.getPrice())
        .forEach(s -> System.out.println(s));
```

Здесь также результирующий поток содержит только строки, только теперь названия соединяются с ценами.

Для преобразования объектов в типы `Integer`, `Long`, `Double` определены специальные методы `mapToInt()`, `mapToLong()` и `mapToDouble()` соответственно.


### `flatMap()`
Плоское отображение выполняется тогда, когда из одного элемента нужно получить несколько. Данную операцию выполняет метод `flatMap`:

```java
<R> Stream<R> flatMap(Function<? super T, ? extends Stream<? extends R>> mapper)
```

Например, в примере выше мы выводим название телефона и его цену. Но что, если мы хотим установить для каждого телефона цену со скидкой и цену без скидки. То есть из одного объекта `Phone` нам надо получить два объекта с информацией, например, в виде строки. Для этого применим `flatMap`:

```java
Stream<Phone> phoneStream = Stream.of(
    new Phone("iPhone 6 S", 54000),
    new Phone("Lumia 950", 45000),
    new Phone("Samsung Galaxy S 6", 40000)
);

phoneStream
        .flatMap(p -> Stream.of(
                String.format("название: %s  цена без скидки: %d", p.getName(), p.getPrice()),
                String.format("название: %s  цена со скидкой: %d", p.getName(), p.getPrice() - (int) (p.getPrice() * 0.1))
        ))
        .forEach(s -> System.out.println(s));
```

Результат работы программы:

```output
название: iPhone 6 S цена без скидки: 54000
название: iPhone 6 S цена со скидкой: 48600
название: Lumia 950 цена без скидки: 45000
название: Lumia 950 цена со скидкой: 40500
название: Samsung Galaxy S 6 цена без скидки: 40000
название: Samsung Galaxy S 6 цена со скидкой: 36000
```