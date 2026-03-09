> внимание: контейнер с JFrog Artifactory убедитесь что остановлен. Что бы экономить ресурсы компьютера.
> 
>  [https://github.com/jenkins-infra/helpdesk/issues/3742](https://github.com/jenkins-infra/helpdesk/issues/3742) Nexus Platform плагин пока сломали, надеюсь что скоро починят
> 
> ![](https://ucarecdn.stepik.net/c5ef80b2-83bc-45fc-8c48-3de6c5ec529a/)

**Цель**: на практическом примере показать интеграцию нескольких инструментов с Jenkins таких как:

- **системы контроля версий** - GIT (github)
- **система сборки приложений** - Maven
- **менеджер репозиториев** - Sonatype Nexus3 
- **сервер приложений** - Tomcat 9

> **Какие причины есть для интеграции Jenkins и Nexus3 и как это воообще вам поможет в работе?** 
> 
> - **Управление зависимостями:** Jenkins может использовать Nexus 3 для управления зависимостями, которые он использует при сборке проектов. Это позволяет Jenkins автоматически загружать нужные зависимости, что упрощает процесс сборки и уменьшает вероятность ошибок.
> - **Автоматизация обновлений:** Nexus 3 может автоматически обновлять зависимости в Jenkins, что позволяет Jenkins использовать самые последние версии зависимостей.
> - **Управление артефактами:** Nexus 3 можно использовать для хранения всех артефактов, создаваемых Jenkins, таких как файлы сборки, отчеты о тестировании и т.д. Это позволяет упростить управление артефактами и уменьшить вероятность потери данных.  
>      

Данный урок будет состоять из нескольких этапов (я подразумеваю то что вы выполнили прошлые уроки и вас установлен Jenkins, Docker, и.т.д ;)

0. Вам нужно установить tomcat в контейнере и запустить. Можете воспользоваться уроком [1.14 Установка и конфигурирование Application Server - Tomcat в Docker контейнере.](https://stepik.org/lesson/686375/step/2?unit=685470)

1. Установка и конфигурирование **Sonatype Nexus3** в Docker контейнере.

2. Создаем **Freestyle project: package-upload-nexus3** ( в проекте собираем приложение и публикуем в Nexus3)

3. Создаем **Freestyle project: nexus-deploy-tomcat** ( скачиваем приложение с помощью плагина HTTP Request из Nexus3 и публикуем в Tomcat)
## Установка и конфигурирование Sonatype Nexus3 в Docker контейнере.

**(обновил курс под новый интерфейс Jenkins, + тут новая версия урока используется сеть jenkins_net статическим ip, ранее было host.)**

Sonatype Nexus3 — это бесплатная платформа с открытым исходным кодом для управления пакетами, версиями и зависимостями, которая позволяет разработчикам создавать, публиковать и получать доступ к программным пакетам и библиотекам. 

Nexus3 один из самых популярных репозиториев артефактов, используемых не только в сообществе Java.

Nexus3 позволяет управлять версиями, публиковать пакеты, отслеживать зависимости, тестировать и развертывать приложения, а также обеспечивает безопасность и контроль доступа к пакетам.

С помощью Nexus разработчики могут хранить и управлять зависимостями java (maven), docker images , python, npm, go. (подобронее о форматах тут: [https://help.sonatype.com/repomanager3/nexus-repository-administration/formats](https://help.sonatype.com/repomanager3/nexus-repository-administration/formats) )

![](https://ucarecdn.stepik.net/33a895b0-f25f-42dd-9f38-a74e437c77df/)

Sonatype Nexus 3 имеет следующие особенности:

- Управление версиями: Nexus 3 позволяет хранить и управлять версиями программных пакетов, что позволяет разработчикам быстро получать доступ к последним версиям зависимостей и легко откатываться к предыдущим версиям при необходимости.
- Публикация пакетов: Nexus 3 предоставляет возможность публиковать пакеты на платформе, что позволяет другим разработчикам получать доступ к этим пакетам и использовать их в своих проектах.
- Контроль зависимостей: Nexus 3 обеспечивает отслеживание зависимостей между пакетами, что позволяет выявлять конфликты и проблемы с зависимостями.
- Безопасность и контроль доступа: Nexus 3 обеспечивает безопасность и контроль доступа к публичным репозиториям пакетов, что помогает защитить конфиденциальные данные и предотвратить несанкционированный доступ.

Nexus3 страница на [DockerHub](https://hub.docker.com/r/sonatype/nexus3/)

> **далее в видео демонстрации установки, вы можете заметить что версия там будет 3.59.0, но я там нашел проблему с работой rest api, под 3.58.1 она не воспроизводится и потому используйте именно эту версию 3.58.1.**
> 
> **3.58.1 сломана не поднимается, используем 3.85.0 последний свежий релиз.**

1. Скачать образ контейнера **Nexus**:

```bash
docker pull sonatype/nexus3:3.85.0
```

2. Запустите контейнер(убедитесь что вы остановили контейнер с JFrog Artifactory, они занимают одинаковые порты с Nexus):

```applescript
docker run --rm --detach \
 --net jenkins_net --ip 172.10.0.12  \
 --publish 8081:8081 \
 --volume nexus-data:/nexus-data \
 --name nexus-repo \
 sonatype/nexus3:3.85.0
```

3. Откройте веб-интерфейс nexus3: [http://172.10.0.12:8081/](http://172.10.0.12:8081/)

Посмотреть пароль для admin ([https://help.sonatype.com/repomanager3/installation-and-upgrades/accessing-the-user-interface](https://help.sonatype.com/repomanager3/installation-and-upgrades/accessing-the-user-interface)):

```bash
docker exec nexus-repo cat /nexus-data/admin.password
```

4. Установить плагин интеграции Jenkins & Nexus ( [https://plugins.jenkins.io/nexus-jenkins-plugin/](https://plugins.jenkins.io/nexus-jenkins-plugin/)  сейчас там есть ишью и он находится на рассмотрение, можно установить плагин руками предварительно [скачав от сюда](https://help.sonatype.com/en/download-and-compatibility.html), далее будет короткое видео по шагам) 

> прямая ссылка: 
> 
> [https://cdn.download.sonatype.com/repository/downloads-prod-group/jenkins/nexus-jenkins-plugin-3.29.0-01.hpi](https://cdn.download.sonatype.com/repository/downloads-prod-group/jenkins/nexus-jenkins-plugin-3.29.0-01.hpi)
> 
> или если вас что то блокирует(я скачал и выложил - яндекс диск)
> 
> [https://disk.yandex.ru/d/7gifDDCKwPdlSw](https://disk.yandex.ru/d/7gifDDCKwPdlSw)

> В качестве дополнительной информации при тесте подключение из jenkins к nexus (в `Dashboard > Manage Jenkins > System  | **Nexus Repository Manager Servers**` ) 
> 
> **Обратите внимание при дальшей настройки возможна ошибка с лишними пробелами будет ошибка вида, сложно понять в чем проблема потому что пробел не видно.** 

![](https://ucarecdn.stepik.net/385f863e-a758-4ace-a5fe-4f8871486e9a/)
Установите плагин - [https://plugins.jenkins.io/http_request/](https://plugins.jenkins.io/http_request/)

![](https://ucarecdn.stepik.net/67eb83c9-bd2f-4281-9b42-bdba00fa2eea/)

Установите плагин "**Deploy to container**" для **jenkins**  [https://plugins.jenkins.io/deploy/](https://plugins.jenkins.io/deploy/)

![](https://ucarecdn.stepik.net/a1b68ec6-8511-4012-9926-ab6f3f633ceb/)

Documentation Nexus3(rest api): [https://help.sonatype.com/repomanager3/integrations/rest-and-integration-api/search-api#SearchAPI-DownloadingtheLatestVersionofanAsset](https://help.sonatype.com/repomanager3/integrations/rest-and-integration-api/search-api#SearchAPI-DownloadingtheLatestVersionofanAsset)

![](https://ucarecdn.stepik.net/2f44606f-5070-4b77-a439-6552e2b93f70/)**Freestyle project:** package-upload-nexus

**Source Code Management:**

- **Git:**
    - **Repository URL:**     [https://github.com/elestopadov/java-example-apps.git](https://github.com/elestopadov/java-example-apps.git)
    - **Branch Specifier:**   */main

**Build Environment:**

![](https://ucarecdn.stepik.net/0d7518e5-3599-4376-bafe-a42e0e1aca75/)

**Build Steps:**

![](https://ucarecdn.stepik.net/22be3cdb-ec1e-4129-aef3-e3e16d24e1e2/)

- **Maven Version:** M3
- **Goals:** clean package 
- **POM:** web-app/pom.xml

![](https://ucarecdn.stepik.net/64035d97-912e-4ddb-8614-3dd1f3563780/)

- **Nexus Instance:** nexus_3.
- **Nexus Repository:** app-repo
- [Add Package] > Packages
    -   
        ![](https://ucarecdn.stepik.net/d5581414-ac29-4888-ae20-869318dc75a8/)
        - **Group:** my-webapp
            
        - **Artifact:** web-app
            
        - **Version:** $BUILD_NUMBER
            
        - **Packaging:** war
            
    - [Add Artifacts Path] > Artifacts
        - ![](https://ucarecdn.stepik.net/7dada32a-fa7b-4a21-9472-25434f168190/)
            - **File Path:** web-app/target/web-app.war

 ![](https://ucarecdn.stepik.net/2f44606f-5070-4b77-a439-6552e2b93f70/)**Freestyle project:** webapp-deploy-tomcat

**Build Environment:**

![](https://ucarecdn.stepik.net/0d7518e5-3599-4376-bafe-a42e0e1aca75/)

**Build Steps:**

![](https://ucarecdn.stepik.net/8f8b7ba9-7880-4697-bf15-4a4327a74e44/)

- **URL:** 
    
    ```bash
    http://172.10.0.12:8081/service/rest/v1/search/assets/download?sort=version&repository=app-repo&group=my-webapp&name=web-app&maven.extension=war
    ```
    
- **HTTP mode:** GET

![](https://ucarecdn.stepik.net/84d6771a-946f-4ca0-b557-2fd9fe9f57d6/)

**Response**

**Output response to file:** web-app.war

**Post-build Actions:**

![](https://ucarecdn.stepik.net/a1fc8c91-b2a6-4b0f-944a-f3944a85458e/)

**WAR/EAR files:** web-app.war

![](https://ucarecdn.stepik.net/53fb2b82-792f-4a4d-be49-5aa39de1793a/)

**Credentials:** admin/1234

**Tomcat URL:** [http://172.10.0.9:8050/](http://172.10.0.9:8050/)