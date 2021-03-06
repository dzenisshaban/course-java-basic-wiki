# Java IO
Отличительной чертой многих языков программирования является работа с файлами и потоками. В Java основной функционал работы с потоками сосредоточен в классах из пакета `java.io`.

Ключевым понятием здесь является понятие **потока**. Хотя понятие "поток" в программировании довольно перегружено и может обозначать множество различных концепций. В данном случае применительно к работе с файлами и вводом-выводом будет говориться о **потоке** (**stream**), как об абстракции, которая используется для чтения или записи информации (файлов, сокетов, текста консоли и т.д.).

**Поток** связан с реальным физическим устройством с помощью системы ввода-вывода Java. Может быть определен поток, который связан с файлом и через который можно вести чтение или запись файла. Это также может быть поток, связанный с сетевым сокетом, с помощью которого можно получить или отправить данные в сети. Все эти задачи: чтение и запись различных файлов, обмен информацией по сети, ввод-ввывод в консоли решаются в Java с помощью потоков.

![Java IO](res/img/java/io/java-io.png)

Объект, из которого можно считать данные, называется **потоком ввода**, а объект, в который можно записывать данные, - **потоком вывода**. Например, если надо считать содержание файла, то применяется поток ввода, а если надо записать в файл - то поток вывода.

В основе всех классов, управляющих **потоками байтов**, находятся два абстрактных класса: `InputStream` (представляющий потоки ввода) и `OutputStream` (представляющий потоки вывода)

Но поскольку работать с байтами не очень удобно, то для работы с **потоками символов** были добавлены абстрактные классы `Reader` (для чтения потоков символов) и `Writer` (для записи потоков символов).

Все остальные классы, работающие с потоками, являются наследниками этих абстрактных классов. Основные классы потоков:

||Byte Based || Character Based ||
| :-: |-|-|-|-|
|**Type**|**Input**|**Output**|**Input**|**Output**|
|Basic|InputStream|OutputStream|Reader/InputStreamReader|Writer/OutputStreamWriter|
|Arrays|ByteArrayInputStream|ByteArrayOutputStream|CharArrayReader|CharArrayWriter|
|Files|FileInputStream|RandomAccessFile|FileOutputStream|RandomAccessFile|	FileReader	FileWriter
|Pipes|PipedInputStream|PipedOutputStream|PipedReader|PipedWriter|
|Buffering|BufferedInputStream|BufferedOutputStream|BufferedReader|BufferedWriter|
|Filtering|FilterInputStream|FilterOutputStream|FilterReader|FilterWriter|
|Parsing|PushbackInputStream/StreamTokenizer||PushbackReader/LineNumberReader||	 
|Strings|||StringReader|StringWriter|
|Data|DataInputStream|DataOutputStream|||	 	
|Data-Formatted||PrintStream||PrintWriter|
|Objects|ObjectInputStream|ObjectOutputStream|||	 	 
|Utilities|SequenceInputStream||||
 	 	 

## Абстрактный класс `InputStream`
Класс `InputStream` является базовым для всех классов, управляющих байтовыми потоками ввода. Рассмотрим его основные методы:
- `int available()` возвращает количество байтов, доступных для чтения в потоке
- `void close()` закрывает поток
- `int read()` возвращает целочисленное представление следующего байта в потоке. Когда в потоке не останется доступных для чтения байтов, данный метод возвратит число `-1`
- `int read(byte[] buffer)` считывает байты из потока в массив `buffer`. После чтения возвращает число считанных байтов. Если ни одного байта не было считано, то возвращается число `-1`
- `int read(byte[] buffer, int offset, int length)` считывает некоторое количество байтов, равное `length`, из потока в массив `buffer`. При этом считанные байты помещаются в массиве, начиная со смещения `offset`, то есть с элемента `buffer[offset]`. Метод возвращает число успешно прочитанных байтов.
- `long skip(long number)` пропускает в потоке при чтении некоторое количество байт, которое равно `number`


## Абстрактный класс `OutputStream`
Класс `OutputStream` является базовым классом для всех классов, которые работают с бинарными потоками записи. Свою функциональность он реализует через следующие методы:
- `void close()` закрывает поток
- `void flush()` очищает буфер вывода, записывая все его содержимое
- `void write(int b)` записывает в выходной поток один байт, который представлен целочисленным параметром `b`
- `void write(byte[] buffer)` записывает в выходной поток массив байтов `buffer`
- `void write(byte[] buffer, int offset, int length)` записывает в выходной поток некоторое число байтов, равное `length`, из массива `buffer`, начиная со смещения `offset`, то есть с элемента `buffer[offset]`


## Абстрактный класс `Reader`
Абстрактный класс `Reader` предоставляет функционал для чтения текстовой информации. Рассмотрим его основные методы:
- `absract void close()` закрывает поток ввода
- `int read()` возвращает целочисленное представление следующего символа в потоке. Если таких символов нет, и достигнут конец файла, то возвращается число `-1`
- `int read(char[] buffer)` считывает в массив `buffer` из потока символы, количество которых равно длине массива `buffer`. Возвращает количество успешно считанных символов. При достижении конца файла возвращает `-1`
- `int read(CharBuffer buffer)` считывает в объект `CharBuffer` из потока символы. Возвращает количество успешно считанных символов. При достижении конца файла возвращает `-1`
- `absract int read(char[] buffer, int offset, int count)` считывает в массив `buffer`, начиная со смещения `offset`, из потока символы, количество которых равно `count`
- `long skip(long count)` пропускает количество символов, равное `count`. Возвращает число успешно пропущенных символов


## Абстрактный класс `Writer`
Класс `Writer` определяет функционал для всех символьных потоков вывода. Его основные методы:
- `Writer append(char c)` добавляет в конец выходного потока символ `c`. Возвращает объект `Writer`
- `Writer append(CharSequence chars)` добавляет в конец выходного потока набор символов `chars`. Возвращает объект `Writer`
- `abstract void close()` закрывает поток
- `abstract void flush()` очищает буферы потока
- `void write(int c)` записывает в поток один символ, который имеет целочисленное представление
- `void write(char[] buffer)` записывает в поток массив символов
- `absract void write(char[] buffer, int off, int len) ` записывает в поток только несколько символов из массива `buffer`. Причем количество символов равно `len`, а отбор символов из массива начинается с индекса `off`
- `void write(String str)` записывает в поток строку
- `void write(String str, int off, int len)` записывает в поток из строки некоторое количество символов, которое равно `len`, причем отбор символов из строки начинается с индекса `off`