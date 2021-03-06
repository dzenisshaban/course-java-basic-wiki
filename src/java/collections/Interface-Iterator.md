# Interface `Iterator`
Одним из ключевых методов интерфейса `Collection`, который он унаследовал от интерфейса `Iterable` является метод `Iterator<E> iterator()`. Он возвращает **итератор** - то есть объект, реализующий интерфейс `Iterator`.
    
Интерфейс `Iterator` имеет следующее определение:

```java
public interface Iterator <E> {
    E next();

    boolean hasNext();

    void remove();
}
```

Реализация интерфейса предполагает, что с помощью вызова метода `next()` можно получить следующий элемент. С помощью метода `hasNext()` можно узнать, есть ли следующий элемент, и не достигнут ли конец коллекции. И если элементы еще имеются, то `hasNext()` вернет значение `true`. Метод `hasNext()` следует вызывать перед методом `next()`, так как при достижении конца коллекции метод `next()` выбрасывает исключение `NoSuchElementException`. И метод `remove()` удаляет текущий элемент, который был получен последним вызовом `next()`.

Используем итератор для перебора коллекции `ArrayList`:

```java
import java.util.ArrayList;
import java.util.Iterator;

public class Program {
    public static void main(String[] args) {
        ArrayList<String> states = new ArrayList<String>();
        states.add("Germany");
        states.add("France");
        states.add("Italy");
        states.add("Spain");

        Iterator<String> iter = states.iterator();
        while (iter.hasNext()) {
            System.out.println(iter.next());
        }
    }
}
```