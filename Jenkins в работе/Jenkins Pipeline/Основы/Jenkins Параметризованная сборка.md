> **Зачем использовать параметризованную сборку Jenkins и как это воообще вам поможет в работе?** 
> 
> Параметризованная сборка в Jenkins используется для автоматизации процесса сборки проектов. Она позволяет создавать различные конфигурации сборки в зависимости от различных параметров, таких как версия используемого языка программирования, параметры компилятора, настройки среды и т.д.
> 
> Это позволяет сократить время на настройку сборки каждого проекта и ускорить процесс сборки. Кроме того, параметризованная сборка позволяет более гибко настраивать параметры сборки, что может быть полезно при работе с различными проектами и командами разработчиков.

Установим плагин 

**[https://plugins.jenkins.io/ansicolor/](https://plugins.jenkins.io/ansicolor/)**

Jenkins переменные среды (Environment Variables) - это переменные окружения, которые можно использовать при настройке проектов в Jenkins. Они позволяют задавать различные параметры и настройки для каждого проекта, что делает работу с Jenkins более гибкой и удобной.

[http://jenkins-main.example.ru:8080/env-vars.html/](http://jenkins-main.example.ru:8080/env-vars.html/)

В Jenkins переменные среды используются для хранения различных параметров и настроек, которые могут потребоваться при сборке проектов. Чтобы получить доступ к этим параметрам, необходимо использовать специальные переменные окружения.

Одним из наиболее распространенных способов получения доступа к параметрам в Jenkins является использование переменных окружения JOB_NAME и JOB_DISPLAY_NAME.

Переменная JOB_NAME содержит имя текущего задания сборки, которое отображается в списке заданий Jenkins. 

Вы можете попробовать отобразить данные переменные если создадите freestyle project .

В разделе `**Build Steps**` добавьте **Execute shell** и введите следующий скрипт для распечатки переменных.

```bash
echo "BUILD_URL ->->-> " $BUILD_URL

echo "GIT_COMMIT ->->-> "  $GIT_COMMIT

echo "JOB_NAME ->->-> "  $JOB_NAME

echo "BUILD_NUMBER ->->-> "  $BUILD_NUMBER
echo "BUILD_ID ->->-> "  $BUILD_ID
echo "BUILD_DISPLAY_NAME ->->-> "  $BUILD_DISPLAY_NAME

echo "WORKSPACE ->->->"   $WORKSPACE


echo "JENKINS_HOME ->->-> "  $JENKINS_HOME
echo "JENKINS_URL ->->-> "  $JENKINS_URL

echo "JOB_URL ->->-> "  $JOB_URL
```

1. Создайте с именем **FreestyleParametrezied,** и типо FreeStyle project

2. В `**General**` добавьте возможность добавлять параметры: ![](https://ucarecdn.stepik.net/dceedba4-e7df-4c39-82a9-e05233776ed3/)

3. Далее нужно добавить параметры:

> тут важны имена, потому что эти переменные будут распечатаны скриптом приведеным ниже, так же смотрите видео урок что бы проще было понять.

- Boolean Parameter
    - **Name:** BooleanParameter
- Choice Parameter
    - **Name:** ChoiceParameter
    - ![](https://ucarecdn.stepik.net/2184989e-35a7-46aa-9a17-924b5ad0cc23/)
- Credentials Parameter
    - **Name:** CredentialsParameter
- File Parameter
    - **File location**: FileParameter
- Multi-line String Parameter
    - **Name:** MultiStringParameter
- Password Parameter
    - **Name:** PasswordParameter
- String Parameter
    - **Name:** StringParameter

4. В разделе `**Build Environment**` выбрать:

![](https://ucarecdn.stepik.net/0cd73084-4ab3-4c74-8554-698b599b1a01/)

5. В разделе `**Build Steps**` добавьте **Execute shell** и введите следующий скрипт для распечатки вводимых переменых.

```nginx
set +x

info() {
	echo "\033[42m[INFO] \033[0m $1"
}

result(){
	echo "\033[44m[RESULT] \033[0m \n$1\n"
}

info "This is result:"

result "*1 Boolean Parameter is equal [ ${BooleanParameter} ] *"

result "*2 ChoiceParameter is equal [ ${ChoiceParameter} ] *"

result "*3 CredentialsParameter is equal [ ${CredentialsParameter} ] *"

result "*4 FileParameter is equal [ ${FileParameter} ] *"

result "*5 Multi-line string parameter is equal [ ${MultiStringParameter} ] *"

result "*6 Password Parameter is equal [ ${PasswordParameter} ] *"

result "*7 String Parameter is equal [ ${StringParameter} ] *"

echo "\033[37;42m - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - \033[0m"
```

В результате вы должны получить следующий результат в Console Output:

![](https://ucarecdn.stepik.net/b2925541-4742-4626-8f2c-836c21334bdf/)