# Управление зависимостями с помощью Grape

## Добавить зависимость

**Grape** — это менеджер зависимостей JAR, встроенный в Groovy. **Grape** позволяет быстро добавлять зависимости репозитория maven в путь к классам, что еще больше упрощает написание сценариев.

Grape (адаптируемый механизм упаковки Groovy) — это инфраструктура, позволяющая выполнять вызовы **grab()** в Groovy, наборе классов, использующих **Ivy** (agile dependency manager) для создания модульной системы, управляемой репозиторием, для Groovy. Это позволяет разработчику написать сценарий с практически произвольными требованиями к библиотеке.

Grape во время выполнения загружает по мере необходимости и связывает названные библиотеки и все зависимости, образуя транзитивное замыкание, когда скрипт запускается из существующих репозиториев, таких как Maven Central.

Grape следует соглашениям Ivy для идентификации версии модуля с изменением имени.

**group** — из какой группы модулей происходит модуль. Преобразует непосредственно в Maven groupId или Ivy Organization. Любая группа, соответствующая /groovy[x][\..*]^/, зарезервирована и может иметь особое значение для поддерживаемых groovy модулей.

**module** - имя модуля для загрузки. Преобразуется непосредственно в артефакт Maven или артефакт Ivy.

**version** — версия используемого модуля. Либо буквальная версия «1.1-RC3», либо Ivy Range «[2.2.1,)», что означает 2.2.1 или любую более позднюю версию).

**classifier** — необязательный классификатор для использования (например, jdk15)

Загруженные модули будут храниться в соответствии со стандартным механизмом Ivy с корнем кеша ~/.groovy/grapes.

## Самое простое использование, нужно добавить:

**@Grab** аннотацию к вашему сценарию: 

```sql
@Grab(group='com.xlson.groovycsv', module='groovycsv', version='1.3')
import static com.xlson.groovycsv.CsvParser.parseCsv
```

@Grab также поддерживает сокращенную запись:

```java
@Grab('com.xlson.groovycsv:groovycsv:1.3')
```

Обратите внимание, что здесь мы используем аннотированный импорт, что является рекомендуемым способом. Вы также можете искать зависимости на mvnrepository.com , и он предоставит вам форму аннотации @Grab для записи pom.xml.

## Классификаторы Maven

Некоторым зависимостям maven нужны классификаторы, чтобы их можно было разрешить. Вы можете исправить это следующим образом:

```java
@Grab(group='net.sf.json-lib', module='json-lib', version='2.2.3', classifier='jdk11')
```

## Использование Grape из Groovy Shell

Из **groovysh** используйте вариант вызова метода:

```java
groovy.grape.Grape.grab(group:'com.xlson.groovycsv', module:'groovycsv', version:'1.3')
```

## Полезные команды для grape:

Что бы посмотреть уже загруженные библиотеки в терминале введите команду: 

```nginx
grape list
```

![](https://ucarecdn.stepik.net/ed894402-45e4-40bf-b7d9-9e85c526f6c2/)

 А удалить загруженную библиотеку можно командой:

```php-template
grape uninstall <nameLib>
```

# CSV

**CSV (Comma Separated Values)** — это формат данных, который используется для представления табличных данных в виде простого текстового файла. В CSV-файлах значения разделяются запятыми, а строки заканчиваются символами перевода строки.

**Основные особенности формата CSV:**

- Значения в ячейках таблицы разделяются запятой или другим разделителем.
- Строки таблицы заканчиваются символом перевода строки (Enter).
- Каждая строка таблицы представляет собой запись.
- Первая строка может содержать заголовки столбцов таблицы.

CSV является одним из самых популярных форматов обмена данными между различными программами и системами. Он поддерживается большинством электронных таблиц, баз данных и других приложений.

Для создания и редактирования CSV-файлов можно использовать любой текстовый редактор. 

Пример того, как может выглядеть файл CSV:

```delphi
Name, Age, City
John Doe, 21, Moscow
Jane Smith, 25, Los Angeles
```

> В этом примере  "Name", "Age", "City" — это заголовки или имена полей. Под каждым заголовком указаны значения, соответствующие этим полям.

Вот несколько примеров использования CSV:

- Экспорт данных из базы данных или электронной таблицы в CSV-файл для последующего анализа или импорта в другую систему.
- Импорт данных из CSV-файла в базу данных или электронную таблицу для обработки или анализа.
- Обмен данными между различными приложениями и системами, которые поддерживают формат CSV.

Формат CSV является простым и удобным способом обмена данными, который широко используется в различных областях, таких как бизнес, наука, образование и другие.

Рассмотрим простой пример для разбора csv файла:

```php
// загружаем библиотеку обработки csv
@Grab('com.xlson.groovycsv:groovycsv:1.3') 
import static com.xlson.groovycsv.CsvParser.parseCsv

// Задаем в переменной csv"
def csvText = '''name,lastName,phone
Dmitro,Petrov,+79343943
Alex,Fox,898734923
Mari,Lee,798743023
Skali,Wood,89873242432'''

def data = parseCsv(csvText) // разбираем csv
println("NAME | \t | LastName | \t | PHONE \n")
for(line in data) { // выбираем по строке из общего количества данных
    printf("%-12s %-12s %-12s\n", "$line.name", "$line.lastName",  "$line.phone")
}
```

А теперь выполним разбор из csv файла, тут нам потребуется сам файл **example.csv** , создайте его и скопируйте в него текст

**example.csv:**

```bash
6523,"00A","heliport","Total Rf Heliport",40.07080078125,-74.93360137939453,11,"NA","US","US-PA","Bensalem","no","00A",,"00A",,,
323361,"00AA","small_airport","Aero B Ranch Airport",38.704022,-101.473911,3435,"NA","US","US-KS","Leoti","no","00AA",,"00AA",,,
6524,"00AK","small_airport","Lowell Field",59.947733,-151.692524,450,"NA","US","US-AK","Anchor Point","no","00AK",,"00AK",,,
6525,"00AL","small_airport","Epps Airpark",34.86479949951172,-86.77030181884766,820,"NA","US","US-AL","Harvest","no","00AL",,"00AL",,,
6526,"00AR","closed","Newport Hospital & Clinic Heliport",35.6087,-91.254898,237,"NA","US","US-AR","Newport","no",,,,,,"00AR"
322127,"00AS","small_airport","Fulton Airport",34.9428028,-97.8180194,1100,"NA","US","US-OK","Alex","no","00AS",,"00AS",,,
6527,"00AZ","small_airport","Cordes Airport",34.305599212646484,-112.16500091552734,3810,"NA","US","US-AZ","Cordes","no","00AZ",,"00AZ",,,
6528,"00CA","small_airport","Goldstone (GTS) Airport",35.35474,-116.885329,3038,"NA","US","US-CA","Barstow","no","00CA",,"00CA",,,
324424,"00CL","small_airport","Williams Ag Airport",39.427188,-121.763427,87,"NA","US","US-CA","Biggs","no","00CL",,"00CL",,,
322658,"00CN","heliport","Kitchen Creek Helibase Heliport",32.7273736,-116.4597417,3350,"NA","US","US-CA","Pine Valley","no","00CN",,"00CN",,,
6529,"00CO","closed","Cass Field",40.622202,-104.344002,4830,"NA","US","US-CO","Briggsdale","no",,,,,,"00CO"
6531,"00FA","small_airport","Grass Patch Airport",28.64550018310547,-82.21900177001953,53,"NA","US","US-FL","Bushnell","no","00FA",,"00FA",,,
6532,"00FD","heliport","Ringhaver Heliport",28.846599578857422,-82.34539794921875,25,"NA","US","US-FL","Riverview","no","00FD",,"00FD",,,
6533,"00FL","small_airport","River Oak Airport",27.230899810791016,-80.96920013427734,35,"NA","US","US-FL","Okeechobee","no","00FL",,"00FL",,,
6534,"00GA","small_airport","Lt World Airport",33.76750183105469,-84.06829833984375,700,"NA","US","US-GA","Lithonia","no","00GA",,"00GA",,,
6535,"00GE","heliport","Caffrey Heliport",33.887982,-84.736983,957,"NA","US","US-GA","Hiram","no","00GE",,"00GE",,,
6536,"00HI","heliport","Kaupulehu Heliport",19.832881,-155.978347,43,"OC","US","US-HI","Kailua-Kona","no","00HI",,"00HI",,,
```

Создайте файл скрипта на Groovy-lang, назовем **workCsv.groovy**:

```java
@Grab('com.xlson.groovycsv:groovycsv:1.3') /// загружаем библиотеку обработки csv
import static com.xlson.groovycsv.CsvParser.parseCsv

loadFile = new File('example.csv')
def csv_content = loadFile.getText('utf-8')

def dataAll = parseCsv(csv_content, separator: ',', readFirstLine: true)
for (line in dataAll) {
    println line[2] + " | " + line[3]
}
```

В результате теперь вы можете разбирать любые csv файлы, главное понять общую концепцию.

## Обработка XML  
Разбор XML

Наиболее часто используемый подход для анализа XML с помощью Groovy заключается в использовании одного из следующих способов:

- groovy.xml.XmlParser
- groovy.xml.XmlSlurper

Оба имеют одинаковый подход к анализу xml. Оба поставляются с набором перегруженных методов синтаксического анализа, а также некоторыми специальными методами, такими как parseText, parseFile и другими. В следующем примере мы будем использовать метод parseText. Он анализирует строку XML и рекурсивно преобразует ее в список или карту объектов.

Давайте сначала посмотрим на сходство между XMLParser и XMLSlurper:

- Оба основаны на SAX, поэтому оба требуют мало памяти.
- Оба могут обновлять/преобразовывать XML

Но у них есть отличия:

- XmlSlurper лениво оценивает структуру. Поэтому, если вы обновите xml, вам придется снова оценивать все дерево.
- XmlSlurper возвращает экземпляры GPathResult при разборе XML
- XmlParser возвращает объекты Node при разборе XML

 Пример чтения xml двумя парсерами:

```python
def text = '''
    <list>
        <technology>
            <name>Groovy Lang</name>
        </technology>
    </list>
'''
// XmlSlurper
def list = new XmlSlurper().parseText(text)
println list.technology.name

// XmlParser
def l = new XmlParser().parseText(text)
println l.technology.name.text()
```

### Когда использовать XmlSlurper или XmlParser?

- Если вы хотите преобразовать существующий документ в другой, вам подойдет XmlSlurper.
- Если вы хотите одновременно обновлять и читать, XmlParser — лучший выбор.

Обоснование этого заключается в том, что каждый раз, когда вы создаете узел с помощью XmlSlurper, он будет недоступен, пока вы снова не проанализируете документ с помощью другого экземпляра XmlSlurper. Нужно прочитать всего несколько нод. XmlSlurper для вас.

Если вам просто нужно прочитать несколько узлов, XmlSlurper должен быть вашим выбором, так как ему не нужно будет создавать полную структуру в памяти.

В целом оба класса работают одинаково. Даже способ использования выражений GPath с ними одинаков (оба используют выражения widthFirst() и depthFirst()). Так что я думаю, это зависит от частоты записи/чтения.

## Создание XML

Наиболее часто используемый подход для создания XML с помощью Groovy заключается в использовании одного из классов:

- groovy.xml.MarkupBuilder
- groovy.xml.StreamingMarkupBuilder

Вот пример использования Groovy MarkupBuilder для создания нового XML-файла:

Создание XML с помощью MarkupBuilder

```less
@Grab('org.codehaus.groovy:groovy-xml:3.0.9')
import groovy.xml.MarkupBuilder

def writer = new FileWriter("../groovy/data.xml" ) // изменить путь до места куда у вас есть доступа
def xml = new MarkupBuilder(writer)


xml.records() { 
    car(name: 'HSV Maloo', make: 'Holden', year: 2006) {
        country('Australia')
        record(type: 'speed', 'Production Pickup Truck with speed of 271kph')
    }
    car(name: 'Royale', make: 'Bugatti', year: 1931) {
        country('France')
        record(type: 'price', 'Most Valuable Car at $15 million')
    }
}
```

В результате мы получаем файл **data.xml** такого содержания:

![](https://ucarecdn.stepik.net/f578e29b-2c0a-42ba-9f13-32c391cc1acb/)

# Парсинг и создание JSON

Groovy поставляется со встроенной поддержкой преобразования между объектами Groovy и JSON. Классы, предназначенные для сериализации и синтаксического анализа JSON, находятся в пакете **groovy.json**

**JsonSlurper** — это класс, который анализирует текст JSON или содержимое для чтения в структуры данных (объекты) Groovy, такие как карты, списки и примитивные типы, такие как Integer, Double, Boolean и String.

Класс поставляется с набором перегруженных методов синтаксического анализа, а также некоторыми специальными методами, такими как parseText, parseFile и другими. В следующем примере мы будем использовать метод parseText. Он анализирует строку JSON и рекурсивно преобразует ее в список или карту объектов. Другие методы parse* аналогичны тем, что возвращают строку JSON, но для других типов параметров.

```scala
import groovy.json.JsonSlurper // сделайте импорт JsonSlurper

def jsonSlurper = new JsonSlurper() // создаем объект JsonSlurper

// Затем мы используем функцию parseText класса JsonSlurper для анализа некоторого текста JSON.
def object = jsonSlurper.parseText('{ "name": "Evgeniy Lestopadov" } ')

// Когда мы получаем объект, мы можем получить доступ к значениям в строке JSON через ключ.
println object.getClass()  // class org.apache.groovy.json.internal.LazyMap
println object         // [name:Evgeniy Lestopadov]
println object.name    // Evgeniy Lestopadov
```

Обратите внимание, что в результате получается простая карта, и с ней можно обращаться как с обычным экземпляром объекта Groovy. JsonSlurper анализирует заданный JSON в соответствии со стандартом обмена JSON ECMA-404, а также поддерживает комментарии и даты JavaScript.

В дополнение к картам JsonSlurper поддерживает массивы JSON, которые преобразуются в списки:

```java
import groovy.json.JsonSlurper // сделайте импорт JsonSlurper

def jsonSlurper = new JsonSlurper() // создаем объект JsonSlurper
def object = jsonSlurper.parseText('{ "myList": [4, 8, 15, 16, 23, 42] }')

println object.getClass() // class org.apache.groovy.json.internal.LazyMap
println object.myList   //[4, 8, 15, 16, 23, 42]
```

Стандарт JSON поддерживает следующие примитивные типы данных: string, number, object, true, false,  null.

JsonSlurper преобразует эти типы JSON в соответствующие типы Groovy. 

|JSON|Groovy|
|---|---|
|string|`java.lang.String`|
|number|`java.lang.BigDecimal` or `java.lang.Integer`|
|object|`java.util.LinkedHashMap`|
|array|`java.util.ArrayList`|
|true|`true`|
|false|`false`|
|null|`null`|
|date|`java.util.Date`|

## JsonOutput

JsonOutput отвечает за сериализацию объектов Groovy в строки JSON. Его можно рассматривать как объект для JsonSlurper, который является синтаксическим анализатором JSON.

JsonOutput поставляется с перегруженными статическими методами toJson. Каждая реализация toJson принимает разные типы параметров. Статические методы можно использовать либо напрямую, либо путем импорта методов с помощью оператора статического импорта.

```java
import groovy.json.JsonOutput // сделайте импортJsonOutput
def json = JsonOutput.toJson([name: 'John Doe', age: 42])

println json // {"name":"John Doe","age":42}
 
```

JsonOutput не только поддерживает примитивные типы данных, карты или списки для сериализации в JSON, он идет еще дальше и даже поддерживает сериализацию POGO, то есть обычных объектов Groovy:

```java
import groovy.json.JsonOutput // сделайте импортJsonOutput
class Person { String name }

def json = JsonOutput.toJson([ new Person(name: 'Petro'), new Person(name: 'Valera') ])

println json // [{"name":"Petro"},{"name":"Valera"}]
 
```

Другой способ создать JSON из Groovy — использовать JsonBuilder или StreamingJsonBuilder. Оба компоновщика предоставляют DSL, который позволяет сформулировать граф объектов, который затем преобразуется в JSON.
# Обработка YAML

Groovy имеет необязательный модуль groovy-yaml, который обеспечивает поддержку преобразования между объектами Groovy и YAML. Классы, посвященные сериализации и синтаксическому анализу YAML, находятся в пакете **groovy.yaml**

YamlSlurper — это класс, который анализирует текст YAML или содержимое для чтения в структуры данных (объекты) Groovy, такие как карты, списки и примитивные типы, такие как Integer, Double, Boolean и String.

Класс поставляется с набором перегруженных методов синтаксического анализа, а также некоторыми специальными методами, такими как parseText и другие. В следующем примере мы будем использовать метод parseText. Он анализирует строку YAML и рекурсивно преобразует ее в список или карту объектов. Другие методы parse* похожи тем, что возвращают строку YAML, но для других типов параметров.

```java
import groovy.yaml.YamlSlurper
def ys = new YamlSlurper()

def yaml = ys.parseText '''
language: groovy
sudo: required
dist: latest

matrix:
  include:
    - jdk: openjdk11
    - jdk: oraclejdk10
    - jdk: oraclejdk9

'''

println yaml.language             // groovy
println yaml.sudo                 // required
println yaml.dist                 // latest
println yaml.matrix.include.jdk   // [openjdk11, oraclejdk10, oraclejdk9]
```

Обратите внимание, что в результате получается простая карта, и с ней можно обращаться как с обычным экземпляром объекта Groovy. YamlSlurper анализирует данный YAML в соответствии с определением YAML Ain’t Markup Language (YAML™).

Поскольку YamlSlurper возвращает чистые экземпляры объектов Groovy без каких-либо специальных классов YAML, его использование прозрачно.

## Создаем YAML из Groovy lang

Другой способ создать YAML из Groovy — использовать YamlBuilder. Построитель предоставляет DSL, который позволяет сформулировать граф объектов, который затем преобразуется в YAML.

```go
import groovy.yaml.YamlBuilder

def builder = new YamlBuilder()
builder.records {
    car {
        name 'Stuff'
        make 'RU'
        year 2026
        country 'Russia'
        homepage new URL('http://stepik.org')
        record {
            type '0003'
            description 'production 007'
        }
    }
}

println builder.toString()
```

В результате получаем yaml вида:

![](https://ucarecdn.stepik.net/dc9f8f38-a07a-46b6-bd3e-9fe3761c5164/)


