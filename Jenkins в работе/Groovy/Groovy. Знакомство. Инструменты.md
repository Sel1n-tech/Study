# К примеру установим Groovy под Lubuntu:

## Установка java OpenJDK:

Во-первых, обновите индекс пакета apt с помощью:

```bash
sudo apt update
```

После обновления индекса пакета установите пакет Java OpenJDK по умолчанию с помощью:

```bash
sudo apt install default-jdk
```

Проверьте установку, выполнив следующую команду, которая напечатает версию Java:

```applescript
java -version
```

## Добавление JAVA_HOME

Узнаем где установлена java:

> which - команда **Linux** используется для определения местоположения данного исполняемого файла

```bash
which java
```

![](https://ucarecdn.stepik.net/cae96ee5-849a-481a-a065-b88bc5064ed9/)

А далее узнаем реальный путь: 

> readlink - перейти по символической ссылке и получить информацию о ней

```bash
readlink -f /usr/bin/java
```

![](https://ucarecdn.stepik.net/bb453169-8eca-4df1-8137-420d1d4e4764/)

> В итоге путь будет такой: _**/usr/lib/jvm/java-11-openjdk-amd64/**_

Теперь нужно добавить переменную окружения JAVA_HOME:

В терминале с помощью консольного текстового редактора nano откроем файл:

```bash
nano ~/.bash_profile
```

в этот файл нужно вставить переменую **JAVA_HOME**, и потом добавить в **PATH** через разделитель **:** двоеточие 

> export **JAVA_HOME**=/usr/lib/jvm/java-11-openjdk-amd64/  
> export **PATH**=$PATH**:**$JAVA_HOME/bin

![](https://ucarecdn.stepik.net/295dd692-cc74-4eca-b209-315103c14575/)

Сохраниить мы можем используя горячие клавишы **CTRL + O**, далее жмите Enter изменения запишутся в файл.

![](https://ucarecdn.stepik.net/ef7456b5-a9b1-47c7-a12e-48b9580edff7/)

Выйти из **nano** используем горячие клавиши **CTRL + X**

Обновить изменения в терминале:

```bash
source ~/.bash_profile 
```

После этого проверем доступность JAVA_HOME:

![](https://ucarecdn.stepik.net/da24a2bc-4ac6-46dc-91de-69c1e6ad679b/)

## Установка Groovy

Что бы поставить Groovy для начала поставим sdkman.io, выполните три команды по этапно

```bash
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
sdk version

```

А с помощью SDKMAN установим groovy:

```cmake
sdk install groovy
```

Теперь можно проверить версию 

```applescript
groovy -version
```

Для данного учебного курса подойдет встроеная мини IDE, GroovyConsole:

Для ее запуска в терминале введите команду:

```undefined
groovyConsole
```

# ![](https://ucarecdn.stepik.net/3c1a26f1-e3ff-4eb1-8c06-999ae2f37b8d/)

После прочтения вывода и изменения кода нажмите **Ctrl+W**, чтобы очистить вывод, и еще раз **Ctrl+R**, чтобы запустить код.

# Запуск скрипта из консоли

1. Создайте файл скрипта (с расширением .groovy) с помощью консольного редактора nano:

```nginx
nano hello.groovy
```

2. Внутри сценария введите код вашего первого скрипта:

> println("Hello, world")

3. Сохраните файл( CTRL + O )и выйдите(CTRL + X)

4. Запустим созданый сценарий:

```nginx
groovy hello.groovy
```

# Скрипты & классов

Пример 1. ( public static void main vs script )  
Groovy поддерживает как сценарии, так и классы. Возьмем, к примеру, следующий код **Main.groovy**:

```javascript
class Main {  
    // метод public static void main(String[]) можно использовать в качестве основного метода класса                            
    static void main(String... args) {          
        println 'Groovy world!'                 
    }
}
```

Класс скрипта  
Скрипт всегда компилируется в класс. Компилятор Groovy скомпилирует класс за вас, при этом тело скрипта будет скопировано в метод запуска. Таким образом, предыдущий пример скомпилирован так, как если бы он был следующим:

**Main.groovy**

```java
import org.codehaus.groovy.runtime.InvokerHelper
class Main extends Script { // класс Main расширяет класс groovy.lang.Script.               
    def run() {   // groovy.lang.Script требует, чтобы метод запуска возвращал значение                              
        println 'Hello Groovy!'   // тело скрипта переходит в метод запуска              
    }
    static void main(String[] args) {      // основной метод генерируется автоматически      
        InvokerHelper.runScript(Main, args)     // делегирует выполнение скрипта на метод запуска
    }
}
```

# Общие ссылки:

 Установить Oracle java jdk 11:

[https://www.oracle.com/cis/java/technologies/javase/jdk11-archive-downloads.html](https://www.oracle.com/cis/java/technologies/javase/jdk11-archive-downloads.html)

![](https://ucarecdn.stepik.net/e9a80a27-3eab-450f-af36-95d2a8a44c78/)

Установить groovy разные варианты версий:

[https://groovy.apache.org/download.html#osinstall](https://groovy.apache.org/download.html#osinstall)

![](https://ucarecdn.stepik.net/b7fcd7fc-27ed-4545-b710-b32286e4360e/)

> Groovy lang это динамический язык программирования создан как дополнение к языку Java. Groovy имеет java подобный синтаксксис, компилируется в bytecode от того может напрямую работать с другим java code. 

# Инструменты

В дополнение к groovy установка Groovy поставляется с несколькими полезными инструментами.

##   
1. **groovyc**, компилятор Groovy

**groovyc** — это инструмент командной строки компилятора Groovy. Он позволяет компилировать исходники Groovy в байт-код. Он играет ту же роль, что и javac в мире Java. Самый простой способ скомпилировать сценарий или класс Groovy — запустить следующую команду:

```vbnet
groovyc MyClass.groovy
```

## 2. Groovy Shell

Groovy Shell или groovysh — это приложение командной строки, которое обеспечивает легкий доступ для оценки выражений Groovy, определения классов и выполнения простых экспериментов.

```bash
groovysh --help
```

## 3. GroovyDoc

GroovyDoc — это инструмент, отвечающий за создание документации из вашего кода. Он действует как инструмент Javadoc в мире Java, но способен обрабатывать как файлы groovy, так и файлы java. В дистрибутиве предусмотрено два способа создания документации: из командной строки или из Apache Ant. Другие инструменты сборки, такие как Maven или Gradle, также предлагают оболочки для Groovydoc.