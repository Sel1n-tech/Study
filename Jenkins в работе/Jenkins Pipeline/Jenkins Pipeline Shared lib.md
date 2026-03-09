> _**Данный материл вам поможет орентироваться в примерах и нужен будет вам в будущем,  можете пропустить его сейчас и посмотреть лекцию для начала.**_
> 
>   
> Исходный код можно найти тут:

- [https://github.com/elestopadov/jenkins-shared-libs](https://github.com/elestopadov/jenkins-shared-libs) - это подключаемая библиотека
- [https://github.com/elestopadov/jenkins-course-example/tree/main/shared-lib-use-case](https://github.com/elestopadov/jenkins-course-example/tree/main/shared-lib-use-case) - это то как мы используем код из библиотеки.

### Пример 1 

В примере [https://github.com/elestopadov/jenkins-course-example/blob/main/shared-lib-use-case/Example-1.groovy](https://github.com/elestopadov/jenkins-course-example/blob/main/shared-lib-use-case/Example-1.groovy)

используется код из библиотеки [https://github.com/elestopadov/jenkins-shared-libs/blob/main/src/io/example/Person.groovy](https://github.com/elestopadov/jenkins-shared-libs/blob/main/src/io/example/Person.groovy)

Обратите внимание тут мы при загрузке используем ключевое слово `import` и загружаем конкретный класс `Person`

### Пример 2

В примере [https://github.com/elestopadov/jenkins-course-example/blob/main/shared-lib-use-case/Example-2.groovy](https://github.com/elestopadov/jenkins-course-example/blob/main/shared-lib-use-case/Example-2.groovy)

используется код из библиотеки [https://github.com/elestopadov/jenkins-shared-libs/blob/main/src/io/second/checkoutTools.groovy](https://github.com/elestopadov/jenkins-shared-libs/blob/main/src/io/second/checkoutTools.groovy)

### Пример 3

В примере [https://github.com/elestopadov/jenkins-course-example/blob/main/shared-lib-use-case/Example-3.groovy](https://github.com/elestopadov/jenkins-course-example/blob/main/shared-lib-use-case/Example-3.groovy)

используется код из библиотеки [https://github.com/elestopadov/jenkins-shared-libs/blob/main/src/io/example/ExampleTool.groovy](https://github.com/elestopadov/jenkins-shared-libs/blob/main/src/io/example/ExampleTool.groovy)

### Пример 4

В примере [https://github.com/elestopadov/jenkins-course-example/blob/main/shared-lib-use-case/Example-4.groovy](https://github.com/elestopadov/jenkins-course-example/blob/main/shared-lib-use-case/Example-4.groovy)

используется код из библиотеки [https://github.com/elestopadov/jenkins-shared-libs/blob/main/vars/logs.groovy](https://github.com/elestopadov/jenkins-shared-libs/blob/main/vars/logs.groovy)

### Пример 5

В примере [https://github.com/elestopadov/jenkins-course-example/blob/main/shared-lib-use-case/Example-5.groovy](https://github.com/elestopadov/jenkins-course-example/blob/main/shared-lib-use-case/Example-5.groovy)

используется код из библиотеки [https://github.com/elestopadov/jenkins-shared-libs/blob/main/vars/printMessage.groovy](https://github.com/elestopadov/jenkins-shared-libs/blob/main/vars/printMessage.groovy)

### Пример 6

В примере [https://github.com/elestopadov/jenkins-course-example/blob/main/shared-lib-use-case/Example-6.groovy](https://github.com/elestopadov/jenkins-course-example/blob/main/shared-lib-use-case/Example-6.groovy)

используется код из библиотеки [https://github.com/elestopadov/jenkins-shared-libs/blob/main/vars/buildProject.groovy](https://github.com/elestopadov/jenkins-shared-libs/blob/main/vars/buildProject.groovy)

### Пример 7

В примере [https://github.com/elestopadov/jenkins-course-example/blob/main/shared-lib-use-case/Example-7.groovy](https://github.com/elestopadov/jenkins-course-example/blob/main/shared-lib-use-case/Example-7.groovy)

используется код из библиотеки 

- [https://github.com/elestopadov/jenkins-shared-libs/blob/main/vars/useJson.groovy](https://github.com/elestopadov/jenkins-shared-libs/blob/main/vars/useJson.groovy)
- [https://github.com/elestopadov/jenkins-shared-libs/blob/main/src/io/example/Person.groovy](https://github.com/elestopadov/jenkins-shared-libs/blob/main/src/io/example/Person.groovy)

ресурсы, json данные:

- [https://github.com/elestopadov/jenkins-shared-libs/blob/main/resources/org/json/user.json](https://github.com/elestopadov/jenkins-shared-libs/blob/main/resources/org/json/user.json)

### Пример 8 

В примере [https://github.com/elestopadov/jenkins-course-example/blob/main/shared-lib-use-case/Example-8.groovy](https://github.com/elestopadov/jenkins-course-example/blob/main/shared-lib-use-case/Example-8.groovy)

ресурсы, sh команды в отдельном файле, шаг libraryResource загрузит нам scriptTest.sh: 

[https://github.com/elestopadov/jenkins-shared-libs/blob/main/resources/org/scripts/scriptTest.sh](https://github.com/elestopadov/jenkins-shared-libs/blob/main/resources/org/scripts/scriptTest.sh)

### Пример 9 (загрузка кода напрямую - через load)

В примере [https://github.com/elestopadov/jenkins-course-example/blob/main/shared-lib-use-case/Example-9.groovy](https://github.com/elestopadov/jenkins-course-example/blob/main/shared-lib-use-case/Example-9.groovy)

Загружается код: [https://github.com/elestopadov/jenkins-course-example/blob/main/utils/loop.groovy](https://github.com/elestopadov/jenkins-course-example/blob/main/utils/loop.groovy)

> Обратите внимание это уже не общая библиотека!


## **![](https://lh7-us.googleusercontent.com/quZsOni0GJCXFkgd3u1ro2IR-ejsm_BFjL3LbeR7ztg18ICa-OJ11y2wZtzedP5p4-BFO39d4L5vvkCcOGHaNyf6_t3anqZt0rmXsUaBMWJPYAAsnU0xTLKZQHT2EUD89Dc9EBB94yRvID72NSY-D0_ezg=s2048)**

## Области видимости общих библиотек  
**![](https://lh4.googleusercontent.com/MtydfG06y_XKxG8WRSTUFKcizfzv1g8Him_8ZR_S95Bukz2T3Aw2QPZgndt1B89xLdbMeL4PS0e0SWF8WTvTHQgA5fRrMVTibmDyCLeqze3nN4Iak0vl11GIltKi8ClPppMsaICtAOgwwSr8N-T_fAVdSMPOgMTFyc0v8vre-psC1Zp8mLT9_30xU5CJcrhr=s2048)**

## Загрузка библиотек в сценарий

- Аннотация `@Library`
- Шаг `**library**`
- Директива `**libraries**`

### **Аннотация @Library**

![](https://lh6.googleusercontent.com/N1gxqB44KNkEm2zjdwE40cjzQksVB6x8anwksSSFHHxPbFZLjWgvMhy8pptHozz1hco8RSFnxaW1ssu7jgPLWfPSO7J2r_GA7Y0i1AjMw-djGYH3L2-LltalhqeTdM0g9zwxpmpXe04y19Vh3fa0VWQqCuPrIYmWwgIjS2C_meA0zZQ4KTYpN4AWy_gETaaW=s2048)

- имя библиотеки обязательно
- версия должна сопровождаться знаком `**@**` 
- определенные подмножества методов могут быть импортированы путем включения оператора import в конце аннотации или в следующей строке
- версия может быть тегом, именем ветки или иной спецификацией ревизии в репозитории исходного кода
- оператор **import** не требуется. Если один не указан, все методы будут импортированы
- если оператор **import** не указан, то подчеркивание `**_**` должно быть в конце аннотации 
- несколько имен библиотек (с соответствующими версиями  может быть указано в одной аннотации. Через  запятую.

```kotlin
@Library('test-library') import io.example.Person
```

```kotlin
@Library('test-library') _
```

**Шаг library**

```dart
library 'my-shared-library'
library 'my-shared-library@master'
library('library').com.pipe.Utils.someStaticMethod()
```

**Директива libraries**

```less
libraries { lib(‘test-lib@master’) }
```

![](https://lh7-us.googleusercontent.com/37bmryyoROxNVdChE72VkelYEcKFBLLbMKQNsqFwBxJzULjk_RGMrRvuRPtxic7Hslc_r9ZsOEBl948-X7o6WzQHzmw4_90XUr-d9DsA8nAxB7Pa9YU3yRBvJ1dwfGiahes2UOAJeaWYQAW1tRzqyMBSsA=s2048)### Folder:

Properties

Pipeline Libraries

**Library:**

- **Name:** test-library
- **Default version:** main

**Retrieval method:** Modern SCM

**Source Code Management:** Git

Project Repository: [https://github.com/elestopadov/jenkins-shared-libs.git](https://github.com/elestopadov/jenkins-shared-libs.git)

![](https://ucarecdn.stepik.net/8e92345e-2101-4708-a268-fdcb611de6fc/)

_**Далее на последнем слайде описал специфику трех примеров которые могу вызвать проблемы при запуске**_

## Пример-6

6 задание использует maven

```typescript
@Library('test-library') _

pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Hello Pipeline'
                script {
                    buildProject name: 'TestProject006'
                }
            }
        }
    }
}
```

нас будет интересовать `buildProject name: 'TestProject006'` 

вызывает код из shared-libs тут [https://github.com/elestopadov/jenkins-shared-libs/blob/main/vars/buildProject.groovy](https://github.com/elestopadov/jenkins-shared-libs/blob/main/vars/buildProject.groovy)

обратите внимание что внутри maven

![](https://ucarecdn.stepik.net/2f93883f-3ad4-4c5e-a539-3dec747e3bb0/)

значит что бы заработало нужно добавить maven через tools:

![](https://ucarecdn.stepik.net/64215283-34fa-4d71-bd67-cdc40b2e0e4a/)

И не забыть установить через **tools**  M3 

![](https://ucarecdn.stepik.net/949d008b-b4e9-4a03-9434-057c1579ee0d/)

##   **Пример-7**

 **Пример-7** использует grab и нельзя запускать в песочнице просто так

@Grab(group='com.google.code.gson', module='gson', version='2.8.6') import com.google.gson.Gson

будет ошибка вида:

```yaml
org.jenkinsci.plugins.workflow.cps.CpsCompilationErrorsException: startup failed:
General error during conversion: Annotation Grab cannot be used in the sandbox.
```

![](https://ucarecdn.stepik.net/11c0dae1-e455-4d23-8400-47f5aedfdde4/)

Или ошибка вида когда песочница не используется, но скрипт еще не подвержден:

```less
org.jenkinsci.plugins.scriptsecurity.scripts.UnapprovedUsageException: script not yet approved for use
```

1. Перейти в pipeline 

2. Снять галку песочницы(Use Groovy Sandbox)

3. Появиться подсказка и ссылка на страницу **Script Approval Configuration**

![](https://ucarecdn.stepik.net/de56ca90-453f-4bd3-b768-0dc5d849bca5/)

Нужно подтвердить скрипт тут: [http://jenkins-main.example.ru:8080/scriptApproval/](http://jenkins-main.example.ru:8080/scriptApproval/)

![](https://ucarecdn.stepik.net/591d89cc-41f3-4ab2-b26e-06c26e3a7afd/)

после этого скрипт отработает

![](https://ucarecdn.stepik.net/46eb0171-85e7-43c9-b7ae-d1f4fae699ab/)

## **Пример 9**

**Пример 9** падает с ошибкой потому что использует загрузку через   `load 'utils/loop.groovy'` , что значит что просто так без использования репозитория в sandbox запустить скрипт не получится он просто не загрузит этот скрипт будет ошибка вида:

```swift
java.nio.file.NoSuchFileException: /var/jenkins_home/workspace/shareLib/9/utils/loop.groovy
```

Т.е надо вытянуть все из гита: [https://github.com/elestopadov/jenkins-course-example/blob/main/shared-lib-use-case](https://github.com/elestopadov/jenkins-course-example/blob/main/shared-lib-use-case)

**Pipeline**

**Definition:** _Pipeline script from SCM_

**Repository URL:** [https://github.com/elestopadov/jenkins-course-example.git](https://github.com/elestopadov/jenkins-course-example.git)

**Branch Specifier (blank for 'any'):** */main

**Script Path:** shared-lib-use-case/Example-9.groovy

При такой настройки он склонирует весь код:

![](https://ucarecdn.stepik.net/1cb95bc0-2101-43d9-b30e-e193be49afc0/)

в Build можете открыть Workspace и найти там utils

![](https://ucarecdn.stepik.net/019aef83-2a7b-4740-8119-ebe87aa5abc3/)

и сможет подгрузить `loop.groovy` в результате отработает успешно

![](https://ucarecdn.stepik.net/915218f7-4eb5-4818-9f4a-f104dcc7ab65/)