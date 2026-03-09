Исходный код можно найти тут: [https://github.com/elestopadov/jenkins-example-app](https://github.com/elestopadov/jenkins-example-app)

План занятие:

1. Рассмотреть основные действия над проектом jenkins
2. Рассмотреть статусы завершения проектов jenkins
3. Подробнее рассмотреть настройки конфигураций Freestyle project

Если вы совсем новичок, что бы лучше запомнить материал повторяйте на практике и выполните лабораторные работы к этому занятию.

![[Pasted image 20260309010556.png]]

![[Pasted image 20260309010713.png]]
![[Pasted image 20260309010740.png]]
![[Pasted image 20260309010801.png]]

## **Build Status**:  Successful ![](https://ucarecdn.stepik.net/6897a6ac-8f4d-4bc4-a6d9-ea560a10d5b6/)

Создаем freestyle project

1. В меню слева выбираем пункт [New Item]
2. В поле **Enter an item name** вводим имя _"ExampleStatus"_
3. Далее выбираем тип проекта _**Freestyle Project**_, и жмем **[OK]**
4. В разделе **Build**, добавим шаг кликнув по кнопке **[Add build step]** с типом "Execute Shell"
5. В поле **Command** мы можем вводить команды shell, т.е это обычные команды терминала линукс.
6. Давайте введем следующие команды.
    - ```bash
        echo "RUN"
        /bin/sleep 20
        echo "FINISHED"
        ```
        
7. Сохраним проект **[SAVE]**, когда мы сохраняем проект мы автоматически оказываемся в разделе Status
8. Запустим проект,  находясь внутри проекта через пункт меню ![](https://ucarecdn.stepik.net/1ae4c4b1-14bc-4a97-88d7-296a833c71eb/)
9. После того как сборка отработает в должны увидить информацию о сборке в "Build History
    - ![](https://ucarecdn.stepik.net/f160bbfc-0ad9-41f6-9372-e6fb53eeab9d/)
        
10.  ![](https://ucarecdn.stepik.net/6897a6ac-8f4d-4bc4-a6d9-ea560a10d5b6/) **Successful -** Сборка не содержит ошибок компиляции. (она же **Stable** - сборка прошла успешно)

##  **Build Status**:  Unstable ![](https://ucarecdn.stepik.net/36883a0f-a072-4c86-bc42-ce19340bc331/)  

1. Переходим в созданый проект из прошлого раздела это _"ExampleStatus"_
2. Открываем секцию **Build**
3. В поле **Command**:
    - ```bash
        echo "RUN"
        /bin/sleep 20
        echo "FINISHED"
        exit 200
        ```
        
4. Нажмите **[Advanced]**

![](https://ucarecdn.stepik.net/8d46f283-f2c5-4258-8908-ab93044e80f7/)

1. Тогда отобразится еще одна настройка "Exit code to set build unstable", добавьте туда значение:  _200_

![](https://ucarecdn.stepik.net/2173b79c-6ecb-4412-9ab2-2d60ff7636c6/)

1. Нажимаем **[Save]**
2. Запускаем сборку через пункт меню **[Build Now]**
3. Cборка отработает в должны увидить информацию о сборке в "Build History"

![](https://ucarecdn.stepik.net/d1c38ed5-9b71-4a6a-9d33-41374c689dd4/)

1. ![](https://ucarecdn.stepik.net/36883a0f-a072-4c86-bc42-ce19340bc331/) **Unstable** - в билде были ошибки, но они не были критичными.

##  **Build Status**: ​​​​​​ **Aborted**   ![](https://ucarecdn.stepik.net/1634695e-45ca-43e2-93a8-f8a9e579778f/)

1. Переходим в созданый проект из прошлого раздела это _"ExampleStatus"_
2. Открываем секцию **Build > Execute shell**
3. В поле **Command**:
    - ```bash
        echo "RUN"
        /bin/sleep 90
        echo "FINISHED"
        ```
        
4. Нажмите **[Advanced]**
5. Очищайте поле "Exit code to set build unstable"
6. Нажимаем **[Save]**
7. Запускаем сборку через пункт меню **[Build Now]**
8. И сразу смотрите "Build History" вам нужно успеть превать сборку во время выполнения
9. нажав на [X], а далее в вплывающем диалоге нажать **[OK]** 
    - ![](https://ucarecdn.stepik.net/4c4125d4-7eb8-4fe4-924c-ae5c80f84e02/)
        
10. Остановив сборку мы получаем нужный статус:

![](https://ucarecdn.stepik.net/3447ab68-5b93-48b4-ad8d-6e805836fa48/)

1. ![](https://ucarecdn.stepik.net/1634695e-45ca-43e2-93a8-f8a9e579778f/) **Aborted** - сборка была прервана до того, как она достигла ожидаемого конца.

##   **Build Status**: ​​​​​​**Failed** ![](https://ucarecdn.stepik.net/be427459-e207-4cbc-b864-be77338f7358/)

1. Переходим в созданый проект из прошлого раздела это _"ExampleStatus"_
2. Открываем секцию **Build > Execute shell**
3. В поле **Command**:
    - ```bash
        echo "RUN"
        exit 2
        ```
        
4. Нажимаем **[Save]**
5. Запускаем сборку  **[Build Now]**
6. Cборка упадет с ошибкой в "Build History"
    - ![](https://ucarecdn.stepik.net/2b6b9c74-fe5a-4540-8ff1-6558bca30bd3/)
        
7. ![](https://ucarecdn.stepik.net/be427459-e207-4cbc-b864-be77338f7358/) **Failed** - в сборке произошла фатальная ошибка.