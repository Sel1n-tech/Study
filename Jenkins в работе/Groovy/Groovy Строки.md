# Введение

Текстовые литералы представлены в виде цепочки символов, называемых строками.

В Groovy существует два типа строк:

- строки в одинарных кавычках ( Java Strings )
- GStrings — в двойных кавычках( Groovy Strings)

Groovy позволяет создавать экземпляры java.lang.String объектов, а также GStrings ( groovy.lang.GString), которые в других языках программирования также называются интерполированными строками .

```ini
jstring= 'Java String' 
gString = "Groovy String + ${jstring}!"
```

В Groovy существуют различные способы записи строк. Вот некоторые из них:

- Интерполяция строк: Это процесс включения значений переменных в строки. В Groovy это можно сделать с помощью `${}` или `${…}`
- Конкатенация строк: Соединение двух или более строк в одну. В Groovy это делается с помощью оператора `+`
- Форматирование строк: Groovy поддерживает стандартный метод `String.format()`, который позволяет форматировать строки на основе аргументов.
- Многострочные строки: Groovy позволяет использовать многострочные строки, используя тройные кавычки `'''`или `"""`

Это лишь некоторые из возможных способов работы со строками в Groovy. В зависимости от конкретной задачи, можно выбрать наиболее подходящий способ.

## **Конкатенация строк**

**Конкатенация в программировании** - это операция соединения (составления) строк или других последовательностей символов. Обычно для конкатенации строк используется оператор + или специальные методы.

Все строки Groovy можно объединить с помощью оператора `**+**`

```go
println "Hello world " + "100500" // конкатенация
```

## **Интерполяция строк**

В программировании интерполяция строк (интерполяция переменных, подстановка переменных или раскрытие переменных) - это процесс оценки строкового литерала, содержащего один или несколько заполнителей, в результате чего они заменяются соответствующими значениями. 

Интерполяция строк обеспечивает более простое и интуитивно понятное форматирование строк и спецификацию содержимого по сравнению с конкатенацией строк. 

Существует _два основных типа алгоритмов раскрытия_ переменных для интерполяции переменных:

Замена и раскрытие заполнителей: создание новой строки из исходной с помощью операций поиска-замены. Найдите ссылку на переменную (заполнитель), замените ее значением переменной. Этот алгоритм не предлагает стратегии кэширования.

Разделить и объединить строку: разделить строку на массив и объединить ее с соответствующим массивом значений; затем соедините элементы конкатенацией. Разделенную строку можно кэшировать для повторного использования.

В Groovy интерполированные строки известны как GStrings

```java
def quality = 'superhero'

def test= "DevOps - is ${quality}"
```

# Виды строк

Перед вами основные виды строк груви,

![](https://ucarecdn.stepik.net/e0d88d44-f74c-44ed-adcb-10b2757b4a6f/)

## Строка в одинарных кавычках

Строки в одинарных кавычках представляют собой серию символов, заключенных в одинарные кавычки:

`**'**a single-quoted string**'**`

Строки в одинарных кавычках являются простыми **java.lang.String** и не поддерживают интерполяцию.

## Строка в тройных одинарных кавычках

Строки с тройными одинарными кавычками представляют собой серию символов, окруженных тройками одинарных кавычек:

`**'''**a single-quoted string**'''**`

## Строка в двойных кавычках

Строки, заключенные в двойные кавычки, представляют собой серию символов, заключенных в двойные кавычки:

`**"**a double-quoted string**"**`

Строки в двойных кавычках являются простыми java.lang.String, если нет интерполированного выражения, но являются **groovy.lang.GString** экземплярами, если интерполяция присутствует.

Чтобы избежать двойных кавычек, вы можете использовать символ обратной косой черты:  **\"**

##  Строка в тройных кавычках

`**"""**a double-quoted string**"""**`

## Строка в тройных одинарных кавычках '''

![](https://lh5.googleusercontent.com/1ebOE-xei_o9o6rkwIMOvb24oM-6pQVn_U5DWn2cuRIXh2xF43tOnzSB2uy0Wecp04xBjRpjXA7jZfInCNhi7U4bK-t__6M5Af0coAZq7uEp2_k3FiN9OXGN7dg-AY68_fHITpONIVlz6oNrdZCgNQ)

![](https://lh5.googleusercontent.com/rzeWv7xG3QUdG8p-sn3neFtXZOfYZEbdO5qpUx1wxanvmjh8kTFsh2moVdyQH4_bT5X-rv0K_80zlfqErThq5bxj3asjndiYMfsmOtSRIzSiRWv1DTHt7F-alsEBWJPJnYdWno2FVaISop7Qii1jUw)

Строка в тройных одинарных кавычках

Строки с тройными одинарными кавычками представляют собой серию символов, окруженных тройками одинарных кавычек:

`'''a triple-single-quoted string'''`

Строки в тройных одинарных кавычках являются простыми java.lang.Stringи не поддерживают интерполяцию.

Строки в тройных одинарных кавычках могут занимать несколько строк. Содержимое строки может пересекать границы строки без необходимости разбивать строку на несколько частей и без конкатенации или escape-символов новой строки:

```python
def aMultilineString = '''line one

line two

line three'''
```

## **Экранирование специальных символов**

Вы можете избежать одинарных кавычек с помощью символа обратной косой черты, чтобы избежать завершения строкового литерала:

'an escaped single quote: \' needs a backslash'

А экранировать сам escape-символ можно с помощью двойной обратной косой черты:

'an escaped escape character: \\ needs a double backslash'

### **Экранирование специальных символов**

![](https://ucarecdn.stepik.net/82f98dfd-7f84-4f76-b4e7-4be9c8808a1b/)

##  **Escape-последовательность Unicode**

Для символов, которых нет на клавиатуре, вы можете использовать escape-последовательности Unicode: обратную косую черту, за которой следует «u», а затем 4 шестнадцатеричных цифры.

Например, символ валюты евро может быть представлен следующим образом:

println 'Japan currency symbol: \u00A5'

###  **Экранируем кавычку в кавычках**

![](https://lh3.googleusercontent.com/PqsubU1QtpHM_QHawAdULiUs0jiHfZ2ix0s2Jran8BGiyRc7CzzKyDefpSZt0aw9IXDmpWQYbWQVRCb9YtrXvsbgOaqmCxt0R0D3fh0gEeNWRfpwGHOphHVtvP45HsIMnqA6kbUrZXi99Klj8xt0uw)

### **Экранируем слэш \**

![](https://lh3.googleusercontent.com/Uunvk0qozz598-F6t24Hk_IZbW82ociAI-rEhnsguPldrOB-PV7XoJzML1cjieM9HFZ7t320xbNUaw12MU3pcaJr8F1-qEtsMZGYRZnrpXX6FVd2oWb4epXRTyxYiATj-4Vu4QZ1c8V8kGC0Fs5fJw)

###  **Escape-последовательность Unicode:**

![](https://lh4.googleusercontent.com/dWvChn1qwmjisdCPhSMOUGL_yWbCReguo9aCh9le4JUeZIoIFg-3E_64aNTKec2mVn4yGKAVS90QO59xwL5jBX7e-H4Di7z55xDsQuL7zvXxzEFAYzjcUYY87ROmHIOgzxXnhqeu5C9sQivI8g5izQ)

#  Characters

В отличие от Java, в Groovy нет явного символьного литерала. Однако вы можете явно указать, что строка Groovy является фактическим символом, тремя различными способами:

```java
char c1 = 'X' 

def c2 = 'Y' 

def c3 = (char)'Z'
```

# Индексация

  
Поскольку String являются упорядоченными последовательностями символов, мы получаем доступ к отдельным  
символ по его положению в String . Это дается индексной позицией.

Обратите внимание:  эти позиции могут указывать либо один символ, либо подмножество символов.

В любом случае возвращается строковое значение. Строковые индексы начинаются с нуля и заканчиваются на  
на единицу меньше длины строки. Groovy также позволяет использовать отрицательные индексы [-1] (назад от конца строки)

```java
def step = 'Study Stepik'
println step[4]     // y 
println step[-1]    // k 
```

# Нарезка строк

Подмножества строк также могут быть выражены с помощью slicing(нарезка). Срез позволяет нам извлечь часть строки.  
Рассмотрим следующий пример String, вместе с некоторые примеры индексации и нарезки.

```java
def step = 'Study Stepik'

println step[2..4]  // срез udy
println step[1..<3] // срез tu
println step[4..2]  // обратный срез
println step[4, 1, 6] // избирательная нарезка ytS
```

Здесь выражение **2..4** — это диапазон индекса с 2 по 4 включительно.

Диапазон, обозначенный как **1..<3,** является исключительным диапазоном и включает все значения, начинающиеся с 1 и заканчивающиеся индексом меньше 3.

# Основные операции над строками

Основные операции со строками включают:

- `+` конкатенацию двух строк String s,
- `*` дублирование String s
- `size(), length()` определение длины **String**
- метод **-** минус (перегруженный **-** оператор) удаляет первое вхождение подстроки. 
- метод **count()** определяет количество вхождений подстроки,
- метод **contains()** определяет, содержит ли строка заданную подстроку. 

В Groovy длина строки может быть получена с помощью метода size() или length():

```rust
def str = "HeLLo"
println str.size()   // Выведет длину строки
println str.length()   // Выведет длину строки
```

![](https://ucarecdn.stepik.net/7e06b9dc-442f-46b6-9bcf-c5c384849c0d/)

## Разница size & length 

- `**size()**`  метод, указанный в **java.util.Collection**, который затем наследуется каждой структурой данных в стандартной библиотеке. Так как это **java.util.Collection** то будет более логично применять его больше в коллекциях, чем для строк, хотя он отрабатывает для строк нормально.
- **`length()`** это метод **java.lang.String**, который представляет собой тонкую оболочку для char[]. И будет возможно применить метод length() только для строк, а если вы попробуете применить его для коллекций то будет выбрашено исключение вида: `groovy.lang.MissingMethodException: No signature of method: java.util.ArrayList.length() is applicable for argument types: () values: []`

Вот пример:

```go
def str = "HeLLo"
println "string.size(): " + str.size()   // Выведет длину строки
println "string.length(): " + str.length()   // Выведет длину строки

def myList = [0, 1, 2, 3, 4];
println "myList.size(): " +  myList.size() 
//println "myList.length(): " + myList.length() // можете расскоментировать и увидите ошибку описаную выше
```

Рассмотрим примеры:

```java
def baseop = 'Study Stepik'

println 'Hello' + 'world!' // Helloworld!
println 'hi' * 3           // hihihi
println baseop - 'Step'   // Study ik
println "baseop.size(): " + baseop.size()         // 12
println "baseop.length(): " + baseop.length()       // 12
println "baseop.count('t') " + baseop.count('t')     //  2
println "baseop.contains('ik'): " + baseop.contains('ik')  // true
```

![](https://ucarecdn.stepik.net/16a90fec-2e61-45f4-8c1e-50920faa003e/)

первые три примера иллюстрируют перегрузку операторов: **+ * -**

Groovy String являются неизменяемыми  их нельзя изменить. Мы создаем новый объект String, индексируя, разрезая и объединяя другие объекты String. 

Список методов для строк можете найти по адресу: [https://groovy-lang.org/gdk.html](https://groovy-lang.org/gdk.html)

![](https://ucarecdn.stepik.net/04eaf080-22c8-40a5-975c-b0906d3990a5/)

# Cравнение строк

Groovy поддерживает методы сравнения String.

- Операторы представляют собой перегруженные версии именованных методов.
- Таким образом, мы сравните два объекта String, используя **str1 == str2** , помня, что это  **str1.equals(str2)**
- Точно так же оператор, обозначенный как **str1 <=> str2** представляет **str1.compareTo(str2)** 
- Этот метод возвращает **-1**, если str1 предшествует str2 , либо возвращает 1, если str1 следует за str2, и 0, если str1 и str2 совпадают. Это может использоваться для сортировки серии String s. 

Сравнение строк является лексикографическим, поэтому прописные буквы предшествуют строчным буквам в наборе символов.

```go
println 'Stepik' <=> 'Stepik'  // 0
println 'A' <=> 'Stepik'       // -1
println 'stepik' <=> 'Stepik'  //  1
println 'stepik'.compareTo('Stepik') // 32
```

## center() 

Возвращает новую строку длиной numberOfChars, состоящую из получателя, дополненного слева и справа пробелами.

```java
String a = "this is center"; 
println(a.center(80)); 
```

## ![](https://ucarecdn.stepik.net/2de5853a-3533-4874-8cd2-95e18cf5024c/)

## compareToIgnoreCase()

Сравнивает две строки лексикографически, игнорируя различия в регистре. ( возвращает отрицательное целое число, ноль или положительное целое число, поскольку указанная строка больше, равна или меньше этой строки, игнорируя особенности регистра.)

```arduino
String str1 = "This Is Demo"; 
String str2 = "THIS IS DEMO"; 
String str3 = "THIS Is Demo test";

println str1.compareToIgnoreCase(str2); 
println str2.compareToIgnoreCase(str3); 
println str3.compareToIgnoreCase(str1);
```

![](https://ucarecdn.stepik.net/7075cfbc-0d34-4cd9-bbd1-337b94ba12a2/)

## concat()

Объединяет указанную строку с концом этой строки.

```arduino
String str1 = "This is "
str1 = str1.concat("DEMO")

println str1
```

## ![](https://ucarecdn.stepik.net/b7d4e215-9f22-4311-b6e0-e724b90d2539/)

## eachMatch()

Обрабатывает каждую группу регулярных выражений, соответствующую подстроке заданной строки.

```typescript
String str1 = "This is DEmos"

str1.eachMatch("i") {
    symbol -> println symbol
}
```

## ![](https://ucarecdn.stepik.net/4f5249ba-99ce-4faf-9f1a-7a6f2b1c3b20/)

## endsWith()

Проверяет, заканчивается ли эта строка указанным суффиксом.(вернет логическое значение **true/false**)

```arduino
String s = "This is demo"

println s.endsWith("o")
println s.endsWith("demo")
println "this is test".endsWith("est")
```

## ![](https://ucarecdn.stepik.net/78281a30-13ed-418d-945f-13d3b1897ff7/)

## equalsIgnoreCase()

Сравнивает эту строку с другой строкой, игнорируя рассмотрение регистра ( возвращает true, если аргумент не равен нулю и строки равны, игнорируя регистр; ложь в противном случае.)

```arduino
String str1 = "Hello"; 
String str2 = "HELLO"; 

println str1.equalsIgnoreCase(str2)
```

## ![](https://ucarecdn.stepik.net/000a0516-3fbe-43f1-9905-8c0a22bb4ef1/)

## getAt()

Возвращает символ в позиции индекса

```arduino
String str1 = "This is groovy lang!"; 

println str1.getAt(8)
println str1.getAt(0)
println str1.getAt(-1)
```

## ![](https://ucarecdn.stepik.net/0cfd5ed2-f3d1-4f8a-8a35-e48c56be5b13/)

## indexOf()

Возвращает индекс первого вхождения указанной подстроки в этой строке.

```arduino
String str1 = "This is groovy lang!"; 

println str1.indexOf('T')
println str1.indexOf('i')

// int indexOf(string str, int fromIndex) 
println str1.indexOf("oo", 5)
```

## ![](https://ucarecdn.stepik.net/41cf3e46-6916-4472-8df4-35f60318fda8/)

## minus()

Удаляет часть значения из строки.

```arduino
String str1 = "The price is \$9"

println str1.minus("\$9")
```

## ![](https://ucarecdn.stepik.net/a80d920d-1e53-4234-b31d-e0bc9faf106d/)

## next()

Вызывается оператором ++ для класса String. Он увеличивает последний символ в данной строке.

```vbnet
String str1 = "The price is 105"

println "A".next()
println "this is groovy".next()
println "The price is 101".next()
println str1.next()
```

## ![](https://ucarecdn.stepik.net/ea517eb0-bec0-4c3d-a299-f6c717ac4781/)

## plus()

Добавляет строку

```arduino
String str1 = "hello"

println str1.plus(" world")
```

## ![](https://ucarecdn.stepik.net/a00932c7-ed48-4983-8c5e-15dcc7a14bd6/)

## replaceall()

Заменяет все вхождения захваченной группы результатом замыкания этого текста.

String str1 = "This is groovy lang"  
println str1  
println str1.replaceAll("is","EE")

![](https://ucarecdn.stepik.net/04a17b96-995b-4892-9af4-54285c721caf/)

## reverse()

Создает новую строку, обратную этой строке.

```arduino
String str1 = "This is groovy lang"
println str1
println str1.reverse()
```

![](https://ucarecdn.stepik.net/caf6400b-e696-4507-8b24-5d15457a9f87/)

## split()

Разбивает эту строку вокруг совпадений данного регулярного выражения.

```arduino
String str1 = "This is groovy-lang"
println str1.split('-')
println str1.split('-')[0]
println str1.split('-')[1]
```

## ![](https://ucarecdn.stepik.net/8f1228dd-181a-4268-8db4-d560334004ee/)

## substring()

Метод substring вернет часть строки. ( Возвращает новую строку, которая является подстрокой этой строки. )

Если даны два параметра, они определяют диапазон символов (начало включено, конец исключен). Если указан только один параметр, это начало подстроки.

Индексация начинается с 0, поэтому `string.s**ubstring(0,3)**` означает первые 3 символа. а `string**.substring(4,7)**` означает номер последующие. А вот вам другой пример попробуйте сами выполнить код:

```arduino
String str1 = "This is groovy lang"
println str1
println str1.substring(2)
println str1.substring(8, 15)
```

## ![](https://ucarecdn.stepik.net/29856675-51c1-4c4e-97cc-0d4222f34866/)

## toUpperCase()

Преобразует все символы в этой строке в верхний регистр.

```go
println "Hello World".toUpperCase()
```

## ![](https://ucarecdn.stepik.net/7b45163a-2883-40da-8e36-6f17fd753f9a/)

## toLowerCase()

Преобразует все символы в этой строке в нижний регистр.

```arduino
String str1 = "This Is Groovy Lang"

println str1.toLowerCase()
```

 ![](https://ucarecdn.stepik.net/041f1ae7-7dbf-474a-b29b-d096cc900077/)

## Ключевые моменты которые стоить запомнить:

- Строки, созданные с помощью одинарной кавычки ('), не поддерживают интерполяцию
- Слэши и _тройные или двойными кавычками_ могут быть многострочными
- Многострочные строки содержат пробельные символы из-за отступа кода
- Обратный слэш (\) используется для экранирования специальных символов в каждом типе, кроме строки с слэша доллара, где мы должны использовать доллар ($) для экранирования