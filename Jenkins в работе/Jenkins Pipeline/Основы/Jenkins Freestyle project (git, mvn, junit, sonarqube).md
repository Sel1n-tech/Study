# **SonarQube**

Статический анализ кода - это процесс анализа программного кода без его выполнения на компьютере. Он позволяет обнаруживать ошибки и уязвимости в коде, а также оптимизировать его производительность. Статический анализ может проводиться с помощью различных инструментов, таких как SonarQube, Findbugs, PMD и др.

Основные особенности статического анализа кода включают в себя:

1. Обнаружение ошибок и уязвимостей в коде: Статический анализ позволяет обнаружить ошибки, которые могут привести к сбоям в работе программы или к уязвимостям системы безопасности.
    
2. Оптимизация производительности кода: Статический анализ помогает выявить неэффективный код и оптимизировать его, что может повысить производительность приложения.
    
3. Автоматизация процесса анализа: Статический анализ можно автоматизировать с помощью специальных инструментов, что позволяет ускорить процесс анализа и уменьшить вероятность ошибок.
    
4. Совместимость с различными языками программирования: Большинство инструментов статического анализа поддерживают множество языков программирования, что делает их универсальными и подходящими для широкого круга проектов.
    
5. Улучшение качества кода: Статический анализ способствует улучшению качества кода, поскольку он помогает выявить ошибки и несоответствия стандартам кодирования, что в свою очередь повышает надежность и безопасность приложения.
    

Существует множество инструментов для проведения статического анализа кода. Некоторые из них:

- SonarQube
- Findbugs
- PMD
- CheckStyle
- PVS-Studio

**SonarQube** - это инструмент для статического анализа кода, который помогает обнаруживать ошибки, уязвимости и другие проблемы в коде. Он использует различные технологии, такие как анализ потока данных, анализ безопасности и анализ производительности, чтобы помочь разработчикам улучшить качество своего кода. **SonarQube** может быть использован как на этапе разработки, так и на этапе тестирования и развертывания кода.

**Интеграция SonarQube с Jenkins** позволяет автоматически собирать код, анализировать его с помощью **SonarQube** и отправлять результаты анализа обратно в **Jenkins**. Это позволяет разработчикам быстро получать информацию о качестве кода и исправлять ошибки до того, как они будут запущены в производство.

Сервер **SonarQube** запускает следующие процессы:

- Веб-сервер, обслуживающий пользовательский интерфейс SonarQube.
- Поисковый сервер на основе Elasticsearch.
- Вычислительный механизм, отвечающий за обработку отчетов анализа кода и сохранение их в базе данных SonarQube.

- [https://docs.sonarqube.org/latest/setup/install-server/#header-4](https://docs.sonarqube.org/latest/setup/install-server/#header-4)
- [https://hub.docker.com/_/sonarqube](https://hub.docker.com/_/sonarqube)

## SonarQube Scanner

**SonarQube Scanner** - это инструмент, который используется для сканирования кода и отправки результатов анализа в SonarQube. Он может быть установлен на любой компьютер, на котором есть Java, и используется для сканирования проектов, которые затем анализируются с помощью SonarQube.

- [https://plugins.jenkins.io/sonar/](https://plugins.jenkins.io/sonar/) 
- [https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/sonarscanner-for-maven/](https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/sonarscanner-for-maven/)
- [https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/jenkins-extension-sonarqube/](https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/jenkins-extension-sonarqube/)
- [https://docs.sonarsource.com/sonarqube/9.9/analyzing-source-code/analysis-parameters/](https://docs.sonarsource.com/sonarqube/9.9/analyzing-source-code/analysis-parameters/)

Далее переходим к практике, переходите к следующей странице..

> обратите внимание что **jenkins_net**, была создана когда вы запускали установку jenkins [тут](https://stepik.org/lesson/686367/step/7?unit=685462)

0. Установить плагин для Jenkins - SonarQube Scanner for Jenkins

![](https://ucarecdn.stepik.net/f3129e45-1795-437d-82b9-a4da0a226249/)

1. Docker hub сайт **https://hub.docker.com/_/sonarqube**   (**тэг будет:** 9.9.1-community)  
2. Скачиваем image

```nginx
docker pull sonarqube:9.9.1-community
```

3. Запускаем SonarQube 

```applescript
docker run --rm --detach \
 --net jenkins_net --ip 172.10.0.5  \
 --publish 9000:9000 \
 --volume sonarqube_extensions:/opt/sonarqube/extensions \
 --volume sonarqube_data:/opt/sonarqube/data \
 --volume sonarqube_logs:/opt/sonarqube/logs \
 --name sonar \
 sonarqube:9.9.1-community
```

4. Контейнер запускается не моментально, нужно подождать некоторое время, а далее переходим на сайт с **SonarQube**: **172.10.0.5:9000** , логин и пароль для входа `admin / admin`  
5. Посмотрим утилизации ресурсов (прервать горячие клавиши `**CTRL + C**`):

```nginx
docker stats
```

6. Создание токена для SonarQube через веб интерфейс. 

`My Account > Security > Generate Tokens`

![](https://ucarecdn.stepik.net/7c13316e-b993-40d4-a230-09ad131afbcd/)

9.  Добавляем токен в Jenkins. **`Manage Jenkins > Credentials`**

    **Server authentication token:**   
        **Kind:** Secret text  
        **Scope:** Global  
        **ID:** sonar_token  
        **Description:** SonarQube token

![](https://ucarecdn.stepik.net/7f80031f-d881-40ab-9c31-c14c612b1672/)

после создания будет выглядеть примерно так:

![](https://ucarecdn.stepik.net/d5138bb1-5f26-4479-b8ee-129eae5899ff/)

10. Переходим в **`Manage Jenkins > System`**

Находим раздел **SonarQuber Servers** > Add SonarQube

- ![](https://ucarecdn.stepik.net/3e78294a-e0eb-4626-890a-cc04079bdc97/)
- **Name:** Sonar
- **Server URL:** [http://172.10.0.5:9000](http://172.10.0.5:9000/)
- **Server authentication token:** sonar_token (тут просто выбираем ранее credential- secret text)

## ![](https://ucarecdn.stepik.net/42569414-a2cd-47fc-9eda-ba7650872751/)

## Пример 1:  Jenkins Freestyle запуск через Maven цель статический анализ кода SonarQube

**General:**

- **Discard old builds:**  ****![](https://ucarecdn.stepik.net/139b46c7-6734-4e80-9120-84ee0fd557e7/)****
- **Days to keep builds:**  7
- **Max # of builds to keep:** 14

**Source Code Management:**

- **Git:**
    - **Repository URL:**     [https://github.com/elestopadov/java-example-apps.git](https://github.com/elestopadov/java-example-apps.git)
    - **Branch Specifier:**   */main

**Build Environment:**

- **Delete workspace before build starts:** ********![](https://ucarecdn.stepik.net/139b46c7-6734-4e80-9120-84ee0fd557e7/)********
- ![](https://ucarecdn.stepik.net/653fd6c3-ced7-47c3-9e0f-c2f0ec1b72c8/) - и выпадающем списке не забываем указать токен если не указать будет ошибка вида:
- ![](https://ucarecdn.stepik.net/8eb8268e-b7c6-4542-a2ad-7936db0d305f/)

**Build Steps:**

 **Invoke top-level Maven targets:**

- **Maven Version:** M3
- **Goals:** clean package sonar:sonar
- **POM:** my-app/pom.xml

**Post-build Actions:**

  **Publish JUnit test result report**

- **Test report XMLs:**    **/target/surefire-reports/*.xml
## Пример 2: Jenkins Freestyle интеграция через плагин SonarQube Scanner.

Для начала вам надо установить **SonarQube Scanner.**

1. Перейти в `**Dashboard > Manage Jenkins > Tools**`
2. Найти раздел `**SonarQube Scanner installations**` и нажать **[Add SonarQube Scanner]**

- **Name:** sonar_scanner
- **Version:** SonarQube Scanner 5.0.1.3006
- Нажать **[apply]**

Будет выглядить так:

![](https://ucarecdn.stepik.net/a40210fa-c49a-4a61-ab95-487b269a9601/)

**General:**

- **Discard old builds:**  ****![](https://ucarecdn.stepik.net/139b46c7-6734-4e80-9120-84ee0fd557e7/)****
- **Days to keep builds:**  7
- **Max # of builds to keep:** 14

**Source Code Management:**

- **Git:**
    - **Repository URL:**     [https://github.com/elestopadov/java-example-apps.git](https://github.com/elestopadov/java-example-apps.git)
    - **Branch Specifier:**   */main

**Build Environment:**

- **Delete workspace before build starts:** ********![](https://ucarecdn.stepik.net/139b46c7-6734-4e80-9120-84ee0fd557e7/)********

**Build Steps:**

 **Invoke top-level Maven targets:**

- **Maven Version:** M3
- **Goals:** clean package 
- **POM:** my-app-two/pom.xml

**Execute SonarQube Scanner****:**

- **Task to run:** scan (может поля отсутствовать)
- **Analysis properties:**

```ini
sonar.projectKey=my-app-two
sonar.projectName=my-app-two
sonar.projectVersion=1.0
sonar.language=java
sonar.sources=my-app-two/src
sonar.java.binaries=my-app-two/target/classes
sonar.surefire.reportsPath=my-app-two/target/surefire-reports
sonar.sourceEncoding=UTF-8
```

![](https://ucarecdn.stepik.net/1440508a-d578-4bf9-acdb-1192f37483aa/)

**Publish JUnit test result report**

- **Test report XMLs:**    **/target/surefire-reports/*.xml
Настройки для интеграции через плагин SonarQube

Execute SonarQube Scanner

**Analysis properties**:

```ini
sonar.projectKey=Jenkins-test
sonar.projectName=Jenkins-test
sonar.projectVersion=1.0
sonar.language=java
sonar.sources=my-app-jenkins/src
sonar.java.binaries=my-app-jenkins/target/classes
sonar.surefire.reportsPath=my-app-jenkins/target/surefire-reports
sonar.sourceEncoding=UTF-8
```

Подробнее можно почитать тут: [https://docs.sonarqube.org/latest/analysis/analysis-parameters/](https://docs.sonarqube.org/latest/analysis/analysis-parameters/)

