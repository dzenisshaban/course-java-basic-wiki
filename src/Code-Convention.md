# Code Convention
Рассмотрим предназначение и использование **Code Convention** на примере Java.


## Зачем нужно `Соглашения по оформлению кода`
**Соглашения по оформлению кода** важны для программистов по ряду причин:
- 80% от стоимости программного обеспечения приходится на его обслуживание
- программное обеспечение не всегда поддерживается инженером, который его разработал
- исходный код программ становится более удобочитаемым, позволяя инженерам более быстро и тщательно понимать код

На данный момент существует большое количество *custom code convention*, но обычно в их основе лежит одна из приведенных ниже:
- [Code Conventions for the Java™ Programming Language](https://www.oracle.com/technetwork/java/codeconvtoc-136057.html)
- [Google Java Style](http://google.github.io/styleguide/javaguide.html)

Для повседневного использования рекомендуется использовать **Google Java Style**, потому что она развивается совместно с Java, в отличии от **Code Conventions for the Java™ Programming Language**, которая последний раз изменялась 20 апреля 1999.

Едиственное что стоит изменить, это:
- разрешенная ширина строки кода: `100` -> `120`
- отступы: 4 whitespaces -> 1 tab


## Основные выдержки
### `WHITESPACE`
Пустая строка используется между:
- членами класса
- методами
- логическими секциями в методе

Пробел используется:
- между `keyword` и скобкой
- после запятой
- вокруг бинарных операторов
- выражения в цикле `for`

### `LINE FEED`
Перенос строки используется:
- после точки с запятой (исключение оператор `for`)
- после запятой
- перед операцией


## Examples
### Форматирование троичного оператора
**Wrong**:
```java
alpha=aLongBooleanExpression?beta:gamma;
```
**Right**:
```java
alpha = (aLongBooleanExpression) ? beta
                                 : gamma;
```
```java
alpha = (aLongBooleanExpression) ? beta : gamma;
```
```java
alpha = (aLongBooleanExpression)
	? beta
	: gamma;
```

### Объявление переменных
**Wrong**:
```java
int foo, fooarray[];
```
```java
int level;           //indentation level
int size;            //size of table
Object currentEntry; //table entry
```

**Right**:
```java
int foo;
int[] fooarray;
```
```java
int level; // indentation level
int size; // size of table
Object currentEntry; // table entry
```

### `if`, `if ... else`, `if ... else if`

**Wrong**:
```java
if(condition)
{
statements;
}
```
```java
if(condition){
statements;
} 
else 
{
statements;
}
```
```java
if(condition){
statements;
}else if(condition){
statements;
}else{
statements;
}
```

**Right**:
```java
if (condition) {
	statements;
}
```
```java
if (condition) {
	statements;
} else {
	statements;
}
```
```java
if (condition) {
	statements;
} else if (condition) {
	statements;
} else {
	statements;
}
```

### `while`, `do ... while`, `for`, `foreach`
**Wrong**:
```java
for(initialization;condition;update)
{
statements;
}
```
```java
for(initialization;condition;update);
```
```java
for(initialization:list){
statements;
}
```
```java
while(condition)
{
statements;
}
```
```java
while(condition);
```
```java
do{
statements;
}while(condition);
```

**Right**:
```java
for (initialization; condition; update) {
	statements;
}
```
```java
for (initialization; condition; update);
```
```java
for (initialization : list) {
	statements;
}
```
```java
while (condition) {
	statements;
}
```
```java
while(condition);
```
```java
do {
	statements;
} while (condition);
```

### `switch`
**Wrong**:
```java
switch(n){
case 1:
statements1;
/* falls through */
case 2:
statements2;
break;
case 3:
statements2;
break;
default:
statements;
break;
}
```
**Right**:
```java
switch (n) {
	case 1:
		statements1;
		break;
	case 2:
	case 3:
		statements2;
		break;
	default:
		statements;
}
```