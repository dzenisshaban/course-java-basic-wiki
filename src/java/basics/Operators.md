# Операторы


## Арифметические операторы
Большинство операций в Java аналогичны тем, которые применяются в других **C**-подобных языках. Для выполнения операции используются **оператор** (**operator**), т.е. символ, который используется для этой операции (например: `+`, `-` и т.д.).

Есть следующие операторы:
- **унарные** - выполняются над одним операндом
- **бинарные** - выполняются над двумя операндами
- **тернарные** - выполняются над тремя операндами

**Операндом** является *переменная* или *литерал* (например, литерал типа `int`), участвующее в операции. Рассмотрим все виды операторов.

В арифметических операциях участвуют числа. Для этих операций в Java есть бинарные и унарные арифметические операторы

### Бинарные
К бинарным операторам относят следующие:


#### +
оператор сложения двух чисел:

```java
int a = 10;
int b = 7;
int c = a + b; // 17
int d = 4 + b; // 11
```


#### -
оператор вычитания двух чисел:

```java
int a = 10;
int b = 7;
int c = a - b; // 3
int d = 4 - a; // -6
```


#### *
оператор умножения двух чисел

```java
int a = 10;
int b = 7;
int c = a * b; // 70
int d = b * 5; // 35
```


#### /
оператор деления двух чисел:

```java
int a = 20;
int b = 5;
int c = a / b; // 4
double d = 22.5 / 4.5; // 5.0
```

При делении стоит учитывать, так как если в операции участвуют два целых числа, то результат деления будет округляться до целого числа, даже если результат присваивается переменной `float` или `double`:

```java
double k = 10 / 4; // 2
System.out.println(k);
```

Чтобы результат представлял число с плавающей точкой, один из операндов также должен представлять число с плавающей точкой:

```java
double k = 10.0 / 4; // 2.5
System.out.println(k);
```


#### %
получение остатка от деления двух чисел:

```java
int a = 33;
int b = 5;
int c = a % b; // 3
int d = 22 % 4; // 22 - 4 * 5 = 2
```


### Унарные
В Java есть два унарных арифметических оператора, которые применяются к одному числу:
- `++` **инкремент**
- `--` **декремент**

Каждый из операторов имеет две разновидности:
- префиксный
- постфиксный


#### ++ (префиксный инкремент)
Увеличение переменной на единицу, например, `z = ++y` (вначале значение переменной `y` увеличивается на `1`, а затем ее значение присваивается переменной `z`)

```java
int a = 8;
int b = ++a;
System.out.println(a); // 9
System.out.println(b); // 9
```


#### ++ (постфиксный инкремент)
Увеличение переменной на единицу, например, `z = y++` (вначале значение переменной y присваивается переменной `z`, а потом значение переменной `y` увеличивается на `1`)

```java
int a = 8;
int b = a++;
System.out.println(a); // 9
System.out.println(b); // 8
```


#### -- (префиксный декремент)
Уменьшение переменной на единицу, например, `z = --y` (вначале значение переменной `y` уменьшается на `1`, а потом ее значение присваивается переменной `z`)

```java
int a = 8;
int b = --a;
System.out.println(a); // 7
System.out.println(b); // 7
```

#### -- (постфиксный декремент)
Уменьшение переменной на единицу, например, `z = y--` (сначала значение переменной `y` присваивается переменной `z`, а затем значение переменной `y` уменьшается на `1`)

```java
int a = 8;
int b = a--;
System.out.println(a); // 7
System.out.println(b); // 8
```


## Операторы сравнения
Условные выражения представляют собой некоторое условие и возвращают значение типа `boolean`, то есть значение `true` (если условие истинно), или значение `false` (если условие ложно). К условным выражениям относятся выражения, которыя содержат операторы сравнения и логические операторы.

C операторами сравнения в выражении используются два операнда, и возвращается значение типа `boolean` - `true`, если выражение верно, и `false`, если выражение неверно.


### ==
сравнивает два операнда на равенство и возвращает `true` (если операнды равны) и `false` (если операнды не равны)

```java
int a = 10;
int b = 4;
boolean c = a == b; // false
boolean d = a == 10; // true
```


### !=
сравнивает два операнда и возвращает `true`, если операнды НЕ равны, и `false`, если операнды равны

```java
int a = 10;
int b = 4;
boolean c = a != b; // true
boolean d = a != 10; // false
```


### < (меньше чем)
Возвращает `true`, если первый операнд меньше второго, иначе возвращает `false`

```java
int a = 10;
int b = 4;
boolean c = a < b; // false
```


### > (больше чем)
Возвращает `true`, если первый операнд больше второго, иначе возвращает `false`

```java
int a = 10;
int b = 4;
boolean c = a > b; // true
```


### >= (больше или равно)
Возвращает `true`, если первый операнд больше второго или равен второму, иначе возвращает `false`

```java
boolean c = 10 >= 10; // true
boolean b = 10 >= 4; // true
boolean d = 10 >= 20; // false
```


### <= (меньше или равно)
Возвращает `true`, если первый операнд меньше второго или равен второму, иначе возвращает `false`

```java
boolean c = 10 <= 10; // true
boolean b = 10 <= 4; // false
boolean d = 10 <= 20; // true
```


## Логические операторы
Также в Java есть логические операторы, которые используются в условиях и возвращают `true` или `false` и обычно объединяют несколько операторов сравнения. К логическим операторам относят следующие:


### `|`

```java
boolean c = a | b;
```

`c` равно `true`, если либо `a`, либо `b` (либо и `a`, и `b`) равны `true`, иначе c будет равно `false`


### `&`

```java
boolean c = a & b;
```

`c` равно `true`, если и `a`, и `b` равны `true`, иначе `c` будет равно `false`


### `!`

```java
boolean c = !b;
```

`c` равно `true`, если `b` равно `false`, иначе `c` будет равно `false`


### `^`

```java
boolean c = a ^ b;
```

`c` равно `true`, если либо `a`, либо `b` (но не одновременно) равны `true`, иначе `c` будет равно `false`


### `||`

```java
boolean c = a || b;
```

`c` равно `true`, если либо `a`, либо `b` (либо и `a`, и `b`) равны `true`, иначе c будет равно `false`


### `&&`

```java
boolean c = a && b;
```

`c` равно `true`, если и `a`, и `b` равны `true`, иначе c будет равно `false`


### Разница между `|` и `||`, `&` и `&&`
Здесь две пары операторов `|` и `||` (а также `&` и `&&`) возвращают похожие результаты, однако же они не равнозначны.

Выражение `c = a | b;` будет вычислять сначала оба значения - `a` и `b` и на их основе выводить результат.

В выражении же `c = a || b;` вначале будет вычисляться значение `a`, и если оно равно `true`, то вычисление значения `b` уже смысла не имеет, так как у нас в любом случае уже `c` будет равно `true`. Значение `b` будет вычисляться только в том случае, если `a` равно `false`

То же самое касается пары операций `&`/`&&`. В выражении `c = a & b;` будут вычисляться оба значения - `a` и `b`.

В выражении же `c = a && b;` сначала будет вычисляться значение `a`, и если оно равно `false`, то вычисление значения `b` уже не имеет смысла, так как значение `c` в любом случае равно `false`. Значение `b` будет вычисляться только в том случае, если a равно `true`

Таким образом, операторы `||` и `&&` более удобны в вычислениях, позволяя сократить время на вычисление значения выражения и тем самым повышая производительность. А операторы `|` и `&` больше подходят для выполнения поразрядных операций над числами.


### Примеры:

```java
boolean a1 = (5 > 6) || (4 < 6); // 5 > 6 - false, 4 < 6 - true, поэтому возвращается true
boolean a2 = (5 > 6) || (4 > 6); // 5 > 6 - false, 4 > 6 - false, поэтому возвращается false
boolean a3 = (5 > 6) && (4 < 6); // 5 > 6 - false, 4 < 6 - true, поэтому возвращается false
boolean a4 = (50 > 6) && (4 / 2 < 3); // 50 > 6 - true, 4/2 < 3 - true, поэтому возвращается true
boolean a5 = (5 > 6) ^ (4 < 6); // 5 > 6 - false, 4 < 6 - true, поэтому возвращается true
boolean a6 = (50 > 6) ^ (4 / 2 < 3); // 50 > 6 - true, 4/2 < 3 - true, поэтому возвращается false
```


## Операторы присваивания
Операторы присваивания в основном представляют комбинацию простого присваивания с другими операторами:


### `=`

`c = b;` (переменной `c` приравнивает значение переменной `b`)


### `+=`

`c += b;` (переменной `c` присваивается результат сложения `c` и `b`)


### `-=`

`c -= b;` (переменной `c` присваивается результат вычитания `b` из `c`)


### `*=`

`c *= b;` (переменной `c` присваивается результат произведения `c `и `b`)


### `/=`

`c /= b;` (переменной `c` присваивается результат деления `c` на `b`)


### `%=`


`c %= b;` (переменной `c` присваивается остаток от деления `c` на `b`)

### `&=`


`c &= b;` (переменной `c` присваивается значение `c & b`)

### `|=`


`c |= b;` (переменной `c` присваивается значение `c | b`)

### `^=`

`c ^= b;` (переменной `c` присваивается значение `c ^ b`)


### `<<=`

`c <<= b;` (переменной `c` присваивается значение `c << b`)


### `>>=`

`c >>= b;` (переменной `c` присваивается значение `c >> b`)


### `>>>=`

`c >>>= b;` (переменной `c` присваивается значение `c >>> b`)


### Примеры операций:

```java
int a = 5;
a += 10; // 15
a -= 3; // 12
a *= 2; // 24
a /= 6; // 4
a <<= 4; // 64
a >>= 2; // 16
System.out.println(a);  // 16
```


## Побитовые операторы
Побитовые операторы применяются к отдельным разрядам или битами чисел. Данные опараторы применяются с операндами, которые являются только целыми числами.


### Логические  побитовые операторы
Логические побитовые операторы для чисeл представляют собой поразрядные операторы. В данном случае числа рассматриваются в двоичном представлении, например, `2` в двоичной системе равно `10` и имеет два разряда, число `7` - `111` и имеет три разряда.


#### `&` (логическое умножение)

Умножение производится поразрядно, и если у обоих операндов значения разрядов равно `1`, то после применения оператора возвращается `1`, иначе возвращается число `0`. Например:

```java
int a1 = 2; //010
int b1 = 5; //101
System.out.println(a1 & b1); // результат 0

int a2 = 4; //100
int b2 = 5; //101
System.out.println(a2 & b2); // результат 4
```

В первом случае у нас два числа `2` и `5`. `2` в двоичном виде представляет число `010`, а `5` - `101`. Поразрядное умножение чисел `(0*1, 1*0, 0*1)` дает результат `000`.

Во втором случае у нас вместо `2` число `4`, у которого в первом разряде `1`, так же как и у числа `5`, поэтому здесь результатом применения оператора `(1*1, 0*0, 0 *1) = 100` будет число `4` в десятичном формате.


#### `|` (логическое сложение)

Данный оператор также применяется к двоичным разрядам, но теперь возвращается единица, если хотя бы у одного числа в данном разряде имеется единица (оператор **логическое ИЛИ**). Например:

```java
int a1 = 2; //010
int b1 = 5; //101
System.out.println(a1 | b1); // результат 7 - 111

int a2 = 4; //100
int b2 = 5; //101
System.out.println(a2 | b2); // результат 5 - 101
```


#### `^` (логическое исключающее ИЛИ)

Иногда этот оператор называют `XOR`, нередко его применяют для простого шифрования:

```java
int number = 45; // 1001 Значение, которое надо зашифровать - в двоичной форме 101101
int key = 102; // Ключ шифрования - в двоичной системе 1100110
int encrypt = number ^ key; // Результатом будет число 1001011 или 75
System.out.println("Зашифрованное число: " +encrypt);

int decrypt = encrypt ^ key; // Результатом будет исходное число 45
System.out.println("Расшифрованное число: " + decrypt);
```

Здесь также производятся поразрядное применение оператора. Если значения текущего разряда у обоих чисел разные, то возвращается `1`, иначе возвращается `0`. Например, результатом выражения `9 ^ 5` будет число `12`. А чтобы расшифровать число, мы применяем обратный оператор к результату.


#### `~` (логическое отрицание)

Поразрядный оператор, инвертирующий все разряды числа: если значение разряда равно `1`, то оно становится равным `0`, и наоборот.

```java
int a = 56; 
System.out.println(~a);
```


### Побитовые операторы сдвига
Операторы сдвига также производятся над разрядами чисел. Сдвиг может происходить вправо и влево.


#### `<<`

```java
a << b
```

сдвигает число `a` влево на `b` разрядов. Например, выражение `4 << 1` сдвигает число `4` (которое в двоичном представлении `100`) на один разряд влево, в результате получается число `1000` или число `8` в десятичном представлении.


#### `>>`

```java
a >> b
```

смещает число `a` вправо на `b` разрядов. Например, `16 >> 1` сдвигает число 16 (которое в двоичной системе `10000`) на один разряд вправо, то есть в итоге получается `1000` или число `8` в десятичном представлении.


#### `>>>`

```java
a >>> b
```

в отличие от предыдущих типов сдвигов данный оператор представляет беззнаковый сдвиг - сдвигает число `a` вправо на `b` разрядов. Например, выражение `-8 >>> 2` будет равно `1073741822`.

Таким образом, если исходное число, которое надо сдвинуть в ту или другую строну, делится на два, то фактически получается умножение или деление на два. Поэтому подобный оператор можно использовать вместо непосредственного умножения или деления на два, так как оператор сдвига на аппаратном уровне менее дорогостоящая оператор в отличие от операторов деления или умножения.


## Приоритет операций
При работе с операторами важно понимать их приоритет, который можно описать следующей схемой (по убыванию приоритета):

```java
i++ i--

++i --i +i -i ~ !

* / %

+ -

<< >> >>>

< > <= >= instanceof

== !=

&

^

|

&&

||

? : (тернарный оператор)

= += -= *= /= %= &= ^= |= <<= >>= >>>= (операторы присваивания)
```

> Cкобки повышают приоритет операторы, используемой в выражении.