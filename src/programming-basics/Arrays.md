# Массивы


# Одномерные массивы
Если переменные предназначены для хранения одиночного значения, то массив представляет набор однотипных значений. Объявление массива похоже на объявление переменной, причем есть два способа объявления массива:

```java
тип_данных[] название_массива;
// либо
тип_данных []название_массива;
// либо
тип_данных название_массива[];
```

Например, определим массив чисел:

```java
int[] nums3; // best practice
int []nums2;
int nums[];
```

После объявления массива мы можем инициализовать его:

```java
int nums[]; // объявили
nums = new int[4]; // инициализировали (массив из 4 чисел)
```

Создание массива производится с помощью следующей конструкции: `new тип_данных[количество_элементов]`, где `new` - ключевое слово, выделяющее память для указанного в скобках количества элементов. Например, `nums = new int[4];` - в этом выражении создается массив из четырех элементов `int` и каждый элемент по умолчанию равен `0`.

Также можно сразу при объявлении массива инициализировать его:

```java
int nums[] = new int[4]; // массив из 4 чисел
int[] nums2 = new int[5]; // массив из 5 чисел
```

При подобной инициализации все элементы массива имеют значение по умолчанию. Для числовых типов (в том числе для типа `char`) это число `0`, для типа `boolean` это значение `false`, а для остальных объектов это значение `null`. Например, для типа `int` значением по умолчанию является число `0`, поэтому выше определенный массив `nums` будет состоять из четырех нулей.

Однако также можно задать конкретные значения для элементов массива при его создании:

```java
// эти два способа равноценны
int[] nums = new int[] {1, 2, 3, 5};
int[] nums2 = {1, 2, 3, 5};
```

Стоит отметить, что в этом случае в квадратных скобках не указывается размер массива, так как он вычисляется по количеству элементов в фигурных скобках.

После создания массива мы можем обратиться к любому его элементу и изменить его:

```java
int[] nums = new int[4];
nums[0] = 1;
nums[1] = 2;
nums[2] = 4;
nums[3] = 100;
System.out.println(nums[2]); // 4
```

Отсчет элементов массива начинается с `0`, поэтому в данном случае, чтобы обратиться к четвертому элементу в массиве, нам надо использовать выражение `nums[3]`.

И так как у нас массив определен только для 4 элементов, то мы не можем обратиться, например, к шестому элементу: `nums[5] = 5;`. Если мы так попытаемся сделать, то мы получим ошибку.


# Многомерные массивы
Ранее мы рассматривали одномерные массивы, которые можно представить как цепочку или строку однотипных значений. Но кроме одномерных массивов также бывают и многомерными. Наиболее известный многомерный массив - таблица, представляющая двухмерный массив:

```java
int[] nums1 = new int[] {0, 1, 2, 3, 4, 5};
int[][] nums2 = {{0, 1, 2}, {3, 4, 5}};
```
Визуально оба массива можно представить следующим образом:

### Одномерный массив `nums1`
|   |   |   |   |   |   |
|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 |
|   |   |   |   |   |   |

### Двухмерный массив `nums2`
|   |   |   |
|---|---|---|
| 0 | 1 | 2 |
| 3 | 4 | 5 |
|   |   |   |

Поскольку массив `nums2` двухмерный, он представляет собой простую таблицу. Его также можно было создать следующим образом: `int[][] nums2 = new int[3][3];`. Количество квадратных скобок указывает на размерность массива. А числа в скобках - на количество строк и столбцов. И также, используя индексы, мы можем использовать элементы массива в программе:

```java
// установим элемент первого столбца второй строки
nums2[1][0] = 44;
System.out.println(nums2[1][0]);
```

Объявление трехмерного массива могло бы выглядеть так:

```java
int[][][] nums3 = new int[2][3][4];
```


## Массив массивов
Многомерные массивы могут быть также представлены как "зубчатые массивы". В вышеприведенном примере двухмерный массив имел 3 строчки и три столбца, поэтому у нас получалась ровная таблица. Но мы можем каждому элементу в двухмерном массиве присвоить отдельный массив с различным количеством элементов:

```java
int[][] nums = new int[3][];
nums[0] = new int[2];
nums[1] = new int[3];
nums[2] = new int[5];
...
```
|   |   |   |   |   |
|---|---|---|---|---|
| 0 | 1 |   |   |   |
| 2 | 3 | 4 |   |   |
| 5 | 6 | 7 | 8 | 9 |
|   |   |   |   |   |


## Работа с массивами

Важнейшее свойство, которым обладают массивы, является свойство `length`, возвращающее длину массива, то есть количество его элементов:

```java
int length = nums.length;
```

Нередко бывает неизвестная последний индекс, и чтобы получить последний элемент массива, мы можем использовать это свойство:

```java
int last = nums[nums.length - 1];
```


## Класс `Arrays`
Класс `java.util.Arrays` предназначен для работы с массивами. Он содержит удобные методы для работы с целыми массивами:

- `String toString(T[])` − позволяет получить все элементы в виде одной строки
- `T[] copyOf(T[], int)` − предназначен для копирования массива
- `T[] copyOfRange(T[], int, int)` − копирует часть массива
- `void sort(T[])` — сортирует массив методом `quick sort`
- `void sort(T[], int, int)` — сортирует массив методом `quick sort`
- `int binarySearch(T[], T)` − ищет элемент методом бинарного поиска
- `int binarySearch(T[], int, int, T)` − ищет элемент методом бинарного поиска
- `void fill(T[], T)` − заполняет массив переданным значением (удобно использовать, если нам необходимо значение по умолчанию для массива)
- `void fill(T[], int, int, T)` − заполняет массив переданным значением (удобно использовать, если нам необходимо значение по умолчанию для массива)
- `boolean equals(T[], T[])` − проверяет на идентичность массивы
- `boolean equals(T[], int, int, T[], int, int)` − проверяет на идентичность массивы
- `int compare(T[], T[])` − сравнивает массивы
- `int compare(T[], int, int, T[], int, int)` − сравнивает массивы
- `boolean deepEquals(Object[], Object[])` − проверяет на идентичность массивы массивов
- `List<T> asList(T...)` − возвращает массив как коллекцию