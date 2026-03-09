**Цель:** _изучить возможность интеграции Jenkins с JFrog Artifactory, плюс рассмотреть возможность публикации war-file в application server Tomcat 9 по средствам Jenkins._

- **системы контроля версий** - GIT (github)
- **система сборки приложений** - Maven
- **фреймворка модульных тестов** - JUNIT
- **менеджер репозиториев** - JFrog Artifactory Community Edition 

Данный урок будет состоять из нескольких этапов (я подразумеваю то что вы выполнили прошлые уроки и вас установлен Jenkins, docker, Parameterized Trigger plugin, и.т.д ;)

> Установите плагин "**Deploy to container**" для **jenkins**  [https://plugins.jenkins.io/deploy/](https://plugins.jenkins.io/deploy/)
> 
> ![](https://ucarecdn.stepik.net/a1b68ec6-8511-4012-9926-ab6f3f633ceb/)

1. Установка и конфигурирование **Application Server - Tomcat** в Docker контейнере.
2. Установка и конфигурирование **JFrog Artifactory** в Docker контейнере.
## Установка и конфигурирование Application Server - Tomcat в Docker контейнере.

**Внимание**: _это краткая текстовая версия видео урока, я привожу ее что бы вы могли удобно копировать команды и видеть общий план при повторении, видео урок следует сразу за этим шагом._

1. Создайте директорию docker_tomcat, перейдите в нее и создайте там текстовый файл Dockerfile:

```bash
mkdir docker_tomcat
cd docker_tomcat
touch Dockerfile
```

2. В докерфайл вам нужно добавить следующий код:

**Dockerfile**:

```swift
FROM tomcat:9.0-jre8-alpine
RUN sed -i 's/8080/8050/' /usr/local/tomcat/conf/server.xml 
RUN sed -i '19d' /usr/local/tomcat/webapps/host-manager/META-INF/context.xml
RUN sed -i '19d' /usr/local/tomcat/webapps/host-manager/META-INF/context.xml
RUN sed -i '19d' /usr/local/tomcat/webapps/manager/META-INF/context.xml
RUN sed -i '19d' /usr/local/tomcat/webapps/manager/META-INF/context.xml
RUN sed -i '/<\/tomcat-users>/d' /usr/local/tomcat/conf/tomcat-users.xml
RUN echo -e "<role rolename=\"manager-gui\"/>\n<role rolename=\"manager-script\"/>\n<user username=\"admin\" password=\"1234\" roles=\"manager-gui, manager-script\"/>\n </tomcat-users>" >> /usr/local/tomcat/conf/tomcat-users.xml
```

> **Команда FROM** в Dockerfile используется для указания базового образа, который будет использоваться при создании нового контейнера. 
> 
> **Команда** **RUN** в Dockerfile используется для выполнения команд внутри контейнера во время его сборки.
> 
> Sed (Stream Editor) - это утилита командной строки, которая используется для редактирования текстовых файлов в Linux. Она позволяет выполнять простые операции замены, удаления или вставки строк в файле.

3. Далее cоберем и запустим контейнер, запустите следующие команды в терминале:

> Команда `docker build` используется для создания нового образа Docker

```bash
docker build -t mtomcat/tomcat .
```

```nginx
docker images
```

```bash
docker run --rm -d -p 8050:8050 --name tomcat9 --net jenkins_net --ip 172.10.0.9 mtomcat/tomcat
```

4. В результате вы создадите образ mtomcat/tomcat, а на базе данного образа будет создан докер контейнер.

5. Можете открыть страницу [http://172.10.0.9:8050/](http://localhost:8050/) 

![](https://ucarecdn.stepik.net/92dd5c1d-c31b-412c-94cc-0acf6de68436/)

6. Для деплоя приложения на Tomcat, так же нужен Jenkins plugin , установите на Jenkins [Deploy to container](https://plugins.jenkins.io/deploy/)

![](https://ucarecdn.stepik.net/0bb01b44-cdb7-4ec4-b5b2-909254742c5a/)

## Установка и конфигурирование JFrog Artifactory в Docker контейнере.

**Внимание**: _это краткая текстовая версия видео урока, я привожу ее что бы вы могли удобно копировать команды и видить общий план при повторении, видео урок следует сразу за этим шагом._

**JFrog Artifactory** - приложение, используемое для хранения результатов сборки программного обеспечения, а так же для распространения и развертывания. (поддерживает разные форматы пакетов, jar, war, npm, docker)

**0.** для загрузки образа Docker из удаленного репозитория (jfrog репозитория). 

```bash
docker pull releases-docker.jfrog.io/jfrog/artifactory-oss:7.63.12
```

**1.** Запустите контейнер **Artifactory**  

```css
docker run --rm --detach \
 --net jenkins_net --ip 172.10.0.10 -p 8081:8081 -p 8082:8082  \
 --volume artifactory_var:/var/opt/jfrog/artifactory \
 --name artifactory \
 releases-docker.jfrog.io/jfrog/artifactory-oss:7.63.12
```

Обратите внимание на запуск контейнера будет затрачено некоторое время

![](https://ucarecdn.stepik.net/ea3d13af-78db-40d2-a452-e9bf83fcc110/)

и когда будет загрузка вы увидите :

![](https://ucarecdn.stepik.net/6b5305a1-456d-4ab0-aaaf-89aa44947729/)

**2.** Получите доступ к **Artifactory** из своего браузера. Например, на вашем локальном компьютере (**[http://172.10.0.10:8082/ui/](http://172.10.0.10:8082/ui/)** ): 

![](https://ucarecdn.stepik.net/38b30e1b-5299-4d14-bcb1-712c7dbc3f2c/)

 3. Войти в систему можно под: 

- **Username**:   _admin_
- **Password**:   _password_

![](https://ucarecdn.stepik.net/84fd09fa-71e6-4d67-825d-e5325124710b/)

> Qwert123!

4. Для интеграции **Jenkins & Artifactory** нам нужен установить плагин для Jenkins ( [https://plugins.jenkins.io/artifactory/](https://plugins.jenkins.io/artifactory/) )
## Настройка интеграции **Jenkins & Artifactory через plugin.** 

Для интеграции **Jenkins & Artifactory** нам нужен установить плагин для Jenkins ( [https://plugins.jenkins.io/artifactory/](https://plugins.jenkins.io/artifactory/) )

`Artifactory` , JFrog Plugin

![](https://ucarecdn.stepik.net/7125eb71-ffe0-491e-9e9a-d9320eaa3839/)

- [https://jfrog.com/help/r/jfrog-rest-apis/introduction-to-the-artifactory-rest-apis](https://jfrog.com/help/r/jfrog-rest-apis/introduction-to-the-artifactory-rest-apis)

После установки плагина нужно настроить JFrog в Jenkins, это можно сделать перейдя в  

**Dashboard > Manage Jenkins > System**, далее нужно найти раздел **JFrog** выглядит примерно так:

![](https://ucarecdn.stepik.net/e4d015a0-3040-4688-9e2a-52415371c2f9/)          ![](https://ucarecdn.stepik.net/ac2401d8-45b2-4244-92e3-42a6294c0cc3/)

 **JFrog instance details**

- ![](https://ucarecdn.stepik.net/bb412107-e99c-4b34-9f90-0c223601c48c/)
- **Instance ID**:  jfrog-artifactory
- **JFrog Platform URL:**  [http://172.10.0.10:8081](http://172.10.0.10:8081/)

**Default Deployer Credentials**

Добавить Credentials - Username with password

- **Username:** admin
- **Password:** Qwert123!
- **ID:** jfrog_login

![](https://ucarecdn.stepik.net/b7193caa-a5ba-46d5-b3c8-4e5aed84e1a1/)

Обращайте внимание на пробельные символы,  можно скопировать с лишним символом пробела и получить ошибку вида:

![](https://ucarecdn.stepik.net/689b04e2-3813-4771-be95-9c5c8b1cd790/)1. Создайте проект

- **Project Name:** first
- **Project Key:** firstkey
    

2. Создать локальный репозиторий внутри созданого проекта **[Add Repositories] > [Local repository]**

- **Repository Key**: firstkey-one
- **Type:** Generic
- **Environments:** DEV

![](https://ucarecdn.stepik.net/b84860f8-3bb9-4a5f-8cc5-6a4563a4c792/) 3. Информацию о артефактах можно увидить тут:

![](https://ucarecdn.stepik.net/55423868-5f38-4c69-8ada-f0beb93dac9f/)
> **Цель:** _изучить возможность интеграции Jenkins с JFrog Artifactory, плюс рассмотреть возможность публикации war-file в application server Tomcat 9 по средствам Jenkins._

План занятия: 

- Создать Folder с именем labsJfrog
- Создать web-app-package для сборки war-file
- Создать web-app-deploy-to-dev для доставки приложения на application server tomcat 9 

Для начала создайте  folder:

1. Создать **New Item >** ![](https://ucarecdn.stepik.net/793eb838-afcf-4c22-9d62-b9a0bf730b70/)**Folder**, с именем `labsJfrog`
2. Перейти в `**labsJfrog**`

> Далее описаны действия по созданию двух freestyle проектов.


## ![](https://ucarecdn.stepik.net/2f44606f-5070-4b77-a439-6552e2b93f70/) web-app-package

Далее нужно создать **New Item >** **Freestyle project**, с именем `web-app-package`

> **web-app-package -** будет получать исходный код веб-приложения из git, далее будет происходить сборка и собраный war-file будет опубликован в JFrog-artifactory в артифактах.
> 
> А после сборки будет запущен другой проект **web-app-deploy-to-dev** который будет осуществлять доставку, настройка **web-app-deploy-to-dev** проекта будет доступна на следующей странице.

Настройки для конфигурации сборки будут такими:

**Source Code Management:**

- **Git:**
    - **Repository URL:**     [https://github.com/elestopadov/java-example-apps.git](https://github.com/elestopadov/java-example-apps.git)
    - **Branch Specifier:**   */main

**Build Environment:**

- **Delete workspace before build starts:** **![](https://ucarecdn.stepik.net/139b46c7-6734-4e80-9120-84ee0fd557e7/)**
- ![](https://ucarecdn.stepik.net/53f38cee-ba56-454a-b389-4125b1c05738/)
    - #### Artifactory Configuration
        
        `​​​​​​в разделе **​Upload Details** находим **Upload spec source**`
        
        - добавить код в **Spec**
            
            ```bash
            {
                "files": [
                    {
                        "pattern": "web-app/target/*.war",
                        "target": "firstkey-firstkey-one/${BUILD_NUMBER}/"
                    }
                ]
            }
            ```
            

**Build Steps:**

**Invoke top-level Maven targets**

- **Maven Version:** M3 (тут вы указываете свою версию мавен которую добавили в tools )
- **Goals:** clean package
- **POM:** web-app/pom.xml

**Post-build Actions:**

> (обратите внимание что данная настройка будет запускать другой проект, потому если вы хотите просто собрать и опубликовать war-файл в артивактори, то можно не добавлять эту опциию сразу)
> 
> Важно перед выполнением поставить плагин [https://plugins.jenkins.io/parameterized-trigger/](https://plugins.jenkins.io/parameterized-trigger/) 

_**Trigger parameterized build on other projects**_

- **Projects to build**: web-app-deploy-to-dev
- **Trigger when build is**: Stable
    
- **Predefined parameters**:
    - **Parameters:**
    - ```ini
        PARENT_BUILD=${BUILD_NUMBER}
        ```
    ## ![](https://ucarecdn.stepik.net/2f44606f-5070-4b77-a439-6552e2b93f70/) web-app-deploy-to-dev

> **web-app-deploy-to-dev -** доставка приложения на application server Tomcat 9 (запускать данный проект будет **web-app-package)**

Далее нужно создать **New Item >** **Freestyle project**, с именем `web-app-deploy-to-dev`

**General:**

![](https://ucarecdn.stepik.net/7fb5739f-a7db-45e7-a7fb-3023a04a69ca/)

**String Parameter**

- **Name:** PARENT_BUILD

**Build Environment:**

- **Delete workspace before build starts:** ****![](https://ucarecdn.stepik.net/139b46c7-6734-4e80-9120-84ee0fd557e7/)****
- ![](https://ucarecdn.stepik.net/53f38cee-ba56-454a-b389-4125b1c05738/)
    - #### Artifactory Configuration
        
        `​​​​​​в разделе **​Download Details** находим **Download spec source**`
        
        - добавить код в **Spec**
            
            ```bash
            {
                "files": [
                    {
                        "pattern": "firstkey-firstkey-one/${PARENT_BUILD}/web-app.war",
                        "target": "download/"
                    }
                ]
            }
            ```
            

**Post-build Actions:**

![](https://ucarecdn.stepik.net/14cc35c1-9116-41f1-99ed-a3ed8394a897/)

- **WAR/EAR files:**  _download/${PARENT_BUILD}/web-app.war_
- В разделе **Containers**, добавить Tomcat 9.x remote и настроить так:
- ![](https://ucarecdn.stepik.net/4dc33b4e-38ce-4d39-a3be-9d095439e830/)
    - **Credentials:** Username with password (tomcat login: admin/1234)
    - **Tomcat URL:** [http://172.10.0.9:8050](http://172.10.0.9:8050/)