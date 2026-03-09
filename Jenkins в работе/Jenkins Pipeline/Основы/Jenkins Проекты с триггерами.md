
> **Зачем в jenkins используют проекты с триггерами и как это вам поможет в работе?**
> 
> Проекты с триггерами в Jenkins используются для запуска сборки проекта при наступлении определенных событий. Например, можно настроить триггер на запуск сборки каждый день в определенное время или при изменении состояния репозитория.
> 
> Использование проектов с триггерами позволяет автоматизировать процесс сборки и сократить время на ручное выполнение задач. Кроме того, это упрощает управление задачами, так как можно настроить запуск сборки только при необходимости, а не каждый раз при создании нового проекта.

Важно перед выполнением поставить плагин [https://plugins.jenkins.io/parameterized-trigger/](https://plugins.jenkins.io/parameterized-trigger/) 

**План занятия:**

1. Пример: Сборка после сборки других проектов

Создаем 3 проекта и делаем зависимость на запуск

- projectFirst
- projectSecond
- projectThird

**Build Triggers**

- Build after other projects are built
- Projects to watch

2 Пример: Триггерная параметризованная сборка в других проектах

1. создайте проект ParamProject

**2.** Далее включить параметры для сборки через опцию![](https://ucarecdn.stepik.net/5c9a1dd9-5e18-4ef4-833a-4df4f510610f/)

И добавить два параметра:

**String Parameter**

- **Name:** PARENT_PROJECT

**String Parameter**

- **Name:** PARENT_BUILD_NUMBER

В разделе Build Steps, добавить Execute Shell и вставить следующий код:

```bash
set +x
echo "Downsteam information: "
echo "\t${PARENT_PROJECT} - ${PARENT_BUILD_NUMBER}"

echo "\nCurrent information: "
echo "\t${JOB_NAME} - ${BUILD_NUMBER}"
```

----------------------------------------  
создайте проект demoTriggersProject

  
 **Build Environment:**  
   **Delete workspace before build starts**

  
**Build steps:**  
   Execute shells:  
      echo "TriggersProject"

  
Post-build action:  
    + **Triggers parameterized build on other projects**  
       Project to build: ParamProject,  
       Triggers when build is: Complete (always trigger)

      + Add Parameters:  
         + Predefined parameters  
           Parameters:  
                       PARENT_PROJECT=${JOB_NAME}  
                       PARENT_BUILD_NUMBER=${BUILD_NUMBER}