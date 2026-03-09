
Исходный код проекта для сборки: [https://github.com/elestopadov/java-example-apps](https://github.com/elestopadov/java-example-apps)

Перед выполнением задания вам нужно установить плагины:

- [Javadoc Plugin](https://plugins.jenkins.io/javadoc) 
- [Warnings Plugin](https://plugins.jenkins.io/warnings-ng)

> В начале сентября была проблема с **Warnings - сейчас прилетел фикс и проблема решена, установка проходит штатно**

![](https://ucarecdn.stepik.net/604913f0-e849-4bc8-8b04-3b7ca2154ab8/)

![](https://ucarecdn.stepik.net/1d4b5c91-38e1-44c0-a2d1-a38de4bc7642/)

Перед выполнением задания вам нужно установить плагины:

- [Javadoc Plugin](https://plugins.jenkins.io/javadoc)  - это плагин для Jenkins, который позволяет публиковать документацию Java-приложений в виде HTML-файлов. Плагин позволяет настроить параметры генерации документации, а также опубликовать ее на сервере.

Проверяем плагин установлен:

![](https://ucarecdn.stepik.net/368f674a-df07-47ac-b7f4-ff7e0850b5c9/)

Далее нужно создать **New Item >** **Freestyle project**

Настройки для конфигурации сборки для консольного приложения **app-console**

**General:**

- **Discard old builds:**  **![](https://ucarecdn.stepik.net/139b46c7-6734-4e80-9120-84ee0fd557e7/)**
- **Days to keep builds:**  7
- **Max # of builds to keep:** 14

**Source Code Management:**

- **Git:**
    - **Repository URL:**     [https://github.com/elestopadov/java-example-apps.git](https://github.com/elestopadov/java-example-apps.git)
    - **Branch Specifier:**   */main

**Build Environment:**

- Delete workspace before build starts: **![](https://ucarecdn.stepik.net/139b46c7-6734-4e80-9120-84ee0fd557e7/)**

**Build Steps:**

 **Execute shell:**

```bash
cd app-console
javac src/com/evg/*.java -d target/
javadoc src/com/evg/*.java -d target/docs/
ls -lhR
```

  **Execute shell**

```bash
cd app-console/target

java com.evg.AppConsole
```

  **Execute shell**

```bash
cd app-console/target
jar cfe app.jar com.evg.AppConsole com/evg/AppConsole.class
ls
```

  **Execute shell**

```bash
cd app-console/target
java -jar app.jar
```

**Post-build Actions:**

**Archive the artifacts**

- **Files to archive:** app-console/target/app.jar

**Publish JavaDoc**

- **Javadoc directory:**  app-console/target/docs

**E-mail Notification**

- **Recipients: [demo@example.ru](mailto:demo@example.ru)**
Далее в видео что бы у вас заработало публикация отчетов обратите внимание на то что путь сейчас нужно указать как:

`**Post-build Actions - Publish Javadoc:**`

`**Javadoc directory:**`  _calculator/target/reports/apidocs_ 

![](https://ucarecdn.stepik.net/41a13efb-418f-4224-ae0d-155654570cb8/)

Далее нужно создать **New Item >** **Freestyle project**

Настройки для конфигурации сборки для консольного приложения **calculator**

**General:**

- **Discard old builds:**  ****![](https://ucarecdn.stepik.net/139b46c7-6734-4e80-9120-84ee0fd557e7/)****
- **Days to keep builds:**  7
- **Max # of builds to keep:** 14

**Source Code Management:**

- **Git:**
    - **Repository URL:**     [https://github.com/elestopadov/java-example-apps.git](https://github.com/elestopadov/java-example-apps.git)
    - **Branch Specifier:**   */main

**Build Triggers:**

- **Build periodically:** H/50 * * * *

> Предоставляет функцию, подобную cron, для периодического выполнения этого проекта.
> 
> Когда впервые начинают непрерывную интеграцию, они часто настолько привыкли к идее регулярных сборок, например ежевечерних или еженедельных, что используют эту функцию.
> 
> Однако смысл непрерывной интеграции состоит в том, чтобы начать сборку сразу после внесения изменения, чтобы обеспечить быструю обратную связь по изменению. Для этого вам нужно подключить уведомление об изменении SCM к Jenkins.

**Build Environment:**

- **Delete workspace before build starts:** ********![](https://ucarecdn.stepik.net/139b46c7-6734-4e80-9120-84ee0fd557e7/)********

**Build Steps:**

 **Invoke top-level Maven targets:**

- **Maven Version:** M3
- **Goals:** clean package checkstyle:checkstyle
- **POM:** calculator/pom.xml

**Invoke top-level Maven targets:**

- **Maven Version:** M3
- **Goals:** javadoc:javadoc
- **POM:** calculator/pom.xml

**Execute shell:**

```bash
java -jar calculator/target/Calculator-1.0-SNAPSHOT.jar
```

**Post-build Actions:**

**Archive the artifacts**

- **Files to archive:**      calculator/target/Calculator-1.0-SNAPSHOT.jar

> **Archive the artifacts** плагин предназначен для архивирования артефактов. Плагин Archive the artifacts может быть использован для архивирования этого артефакта и отправки его в хранилище артефактов Jenkins. Это позволяет другим пользователям Jenkins получить доступ к этому артефакту и использовать его в своих проектах.

**Publish JUnit test result report**

- **Test report XMLs:**    **/target/surefire-reports/*.xml

> **Publish JUnit test result report** публикуем отчеты о результатах тестирования JUnit в Jenkins, соотвественно дженкинс должен знать путь до отчета.
> 
> Maven Surefire Report Plugin - это плагин, который используется для создания отчетов о результатах тестирования, выполненных с помощью Maven и Surefire. Он позволяет собирать информацию о тестах, ошибках, времени выполнения и других метриках, а затем создавать отчет в формате HTML или XML, который можно просмотреть и проанализировать.
> 
> Этот плагин может быть использован в различных ситуациях, таких как автоматизированное тестирование кода, разработка интеграционных тестов, создание отчетов об ошибках и т.д. Он позволяет ускорить процесс разработки и улучшить качество продукта за счет автоматизации процесса тестирования и предоставления подробной информации о результатах.
> 
> Плагин для генерации отчетов **surefire -** [https://maven.apache.org/surefire/maven-surefire-report-plugin/](https://maven.apache.org/surefire/maven-surefire-report-plugin/). По умолчанию этот плагин генерирует отчеты в формате XML в каталоге `target/surefire-reports`.

**Publish JavaDoc**

- **Javadoc directory:     calculator/target/reports/apidocs**
- **(в видео c**alculator/target/site/apidocs может привести к ошибке используйте выше путь.)

> **Publish JavaDoc** плагин для Jenkins позволяет автоматически генерировать и публиковать документацию для Java-проектов. Он использует информацию из файлов JavaDoc, которые обычно создаются с помощью Apache Maven или Gradle, и генерирует HTML-страницы с документацией для проектов.

**Record compiler warnings and static analysis results**

- **Tool:** CheckStyle

**E-mail Notification**

- **Recipients: [demo@example.ru](mailto:demo@example.ru)**