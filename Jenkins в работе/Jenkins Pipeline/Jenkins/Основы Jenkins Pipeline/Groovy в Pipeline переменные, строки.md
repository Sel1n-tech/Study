### Что такое Groovy в Pipeline

Jenkinsfile написан на языке Groovy — динамическом языке программирования для JVM. Groovy похож на Java, но более лаконичный и гибкий.

В декларативном пайплайне мы используем упрощённый DSL (Domain Specific Language), но внутри блоков `steps` и `script` можно писать обычный Groovy-код.

Знание базового Groovy позволяет:

- Создавать переменные и использовать их значения
- Формировать динамические строки
- Делать условия и циклы
- Вызывать функции и обрабатывать данные

### Минимальный пример с переменной

```typescript
pipeline {
    agent any
    stages {
        stage('Example') {
            steps {
                script {
                    def name = 'Jenkins'
                    echo "Hello from ${name}"
                }
            }
        }
    }
}
```

Что здесь происходит:

- `script { }` — специальный блок для написания Groovy-кода внутри декларативного пайплайна
- `def name = 'Jenkins'` — создание переменной с именем `name` и значением `'Jenkins'`
- `"Hello from ${name}"` — строка с интерполяцией, `${name}` заменяется на значение переменной
- `echo` — выводит строку "Hello from Jenkins" в консоль

### Переменные в Groovy

Переменные создаются с помощью ключевого слова `def`:

```java
pipeline {
    agent any
    stages {
        stage('Variables') {
            steps {
                script {
                    // Строковые переменные
                    def appName = 'MyApp'
                    def version = '1.0.0'

                    // Числовые переменные
                    def port = 8080
                    def timeout = 30

                    // Булевы переменные
                    def isProduction = false
                    def enableTests = true

                    echo "Application: ${appName}"
                    echo "Version: ${version}"
                    echo "Port: ${port}"
                }
            }
        }
    }
}
```

Основные типы переменных:

- **Строки** — текстовые значения в одинарных или двойных кавычках
- **Числа** — целые числа или числа с плавающей точкой
- **Булевы значения** — `true` или `false`

Ключевое слово `def` создаёт локальную переменную, которая существует только внутри блока `script`.

### Строки: одинарные vs двойные кавычки

В Groovy есть важное различие между одинарными и двойными кавычками:

```java
pipeline {
    agent any
    stages {
        stage('Strings') {
            steps {
                script {
                    def name = 'World'

                    // Одинарные кавычки - обычная строка
                    def message1 = 'Hello ${name}'
                    echo message1  // Выведет: Hello ${name}

                    // Двойные кавычки - интерполяция работает
                    def message2 = "Hello ${name}"
                    echo message2  // Выведет: Hello World

                    // Можно без фигурных скобок для простых переменных
                    def message3 = "Hello $name"
                    echo message3  // Выведет: Hello World
                }
            }
        }
    }
}
```

Разница:

- **Одинарные кавычки** `'text'` — строка как есть, без обработки переменных
- **Двойные кавычки** `"text"` — строка с интерполяцией, `${variable}` заменяется на значение

Для подстановки переменных используйте двойные кавычки.

### Работа со строками

Groovy предоставляет удобные методы для работы со строками:

```bash
pipeline {
    agent any
    stages {
        stage('String Operations') {
            steps {
                script {
                    def text = 'Jenkins Pipeline'

                    // Длина строки
                    echo "Length: ${text.length()}"

                    // Перевод в верхний регистр
                    echo "Upper: ${text.toUpperCase()}"

                    // Перевод в нижний регистр
                    echo "Lower: ${text.toLowerCase()}"

                    // Замена подстроки
                    def newText = text.replace('Pipeline', 'CI/CD')
                    echo "Replaced: ${newText}"

                    // Разбиение строки
                    def parts = text.split(' ')
                    echo "First word: ${parts[0]}"
                    echo "Second word: ${parts[1]}"
                }
            }
        }
    }
}
```

Полезные методы:

- `length()` — возвращает длину строки
- `toUpperCase()` — переводит в верхний регистр
- `toLowerCase()` — переводит в нижний регистр
- `replace(old, new)` — заменяет подстроку
- `split(separator)` — разбивает строку на массив

### Многострочные строки

Для длинных текстов используются тройные кавычки:

```python
pipeline {
    agent any
    stages {
        stage('Multiline') {
            steps {
                script {
                    def config = '''
                        server:
                          port: 8080
                          host: localhost
                        database:
                          name: mydb
                    '''
                    echo config
                }
            }
        }
    }
}
```

Тройные одинарные кавычки `'''text'''` создают многострочную строку без интерполяции. Для интерполяции используйте тройные двойные кавычки `"""text"""`.

### Более реалистичный пример

Рассмотрим пайплайн, который собирает Docker-образ с динамическим тегом:

```kotlin
pipeline {
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Базовые переменные
                    def appName = 'my-web-app'
                    def registry = 'docker.io/mycompany'
                    def buildNumber = env.BUILD_NUMBER
                    def gitCommit = env.GIT_COMMIT.take(7)

                    // Формируем тег образа
                    def imageTag = "${appName}:${buildNumber}-${gitCommit}"
                    def fullImageName = "${registry}/${imageTag}"

                    echo "Building image: ${fullImageName}"

                    // Собираем образ
                    sh "docker build -t ${fullImageName} ."

                    // Сохраняем имя образа для следующих стейджей
                    env.DOCKER_IMAGE = fullImageName
                }
            }
        }

        stage('Push Image') {
            steps {
                script {
                    echo "Pushing image: ${env.DOCKER_IMAGE}"
                    sh "docker push ${env.DOCKER_IMAGE}"
                }
            }
        }
    }
}
```

В этом примере:

- Создаём переменные для имени приложения, регистри и версии
- `env.BUILD_NUMBER` — встроенная переменная Jenkins с номером билда
- `env.GIT_COMMIT.take(7)` — берём первые 7 символов хеша коммита
- Формируем полное имя образа: `docker.io/mycompany/my-web-app:42-a1b2c3d`
- Используем это имя в командах `docker build` и `docker push`
- Сохраняем значение в `env.DOCKER_IMAGE` для доступа из других стейджей

### Глобальные vs локальные переменные

Переменные, созданные через `def`, локальны и работают только внутри блока `script`:

```typescript
pipeline {
    agent any
    stages {
        stage('Stage 1') {
            steps {
                script {
                    def localVar = 'Hello'
                    echo localVar  // Работает
                }
            }
        }

        stage('Stage 2') {
            steps {
                script {
                    // echo localVar  // Ошибка! Переменная не существует
                }
            }
        }
    }
}
```

Чтобы передать значение между стейджами, используйте `env`:

```typescript
pipeline {
    agent any
    stages {
        stage('Stage 1') {
            steps {
                script {
                    env.SHARED_VAR = 'Hello'
                }
            }
        }

        stage('Stage 2') {
            steps {
                script {
                    echo env.SHARED_VAR  // Работает. Выведет: Hello
                }
            }
        }
    }
}
```

Переменные в `env` доступны во всех стейджах пайплайна.

### Конкатенация строк

Строки можно объединять разными способами:

```java
script {
    def firstName = 'John'
    def lastName = 'Doe'

    // Способ 1: через +
    def fullName1 = firstName + ' ' + lastName

    // Способ 2: через интерполяцию (предпочтительно)
    def fullName2 = "${firstName} ${lastName}"

    // Способ 3: метод concat()
    def fullName3 = firstName.concat(' ').concat(lastName)

    echo fullName2  // John Doe
}
```

Интерполяция с двойными кавычками — самый читаемый способ.

### Практический пример: версионирование

```kotlin
pipeline {
    agent any
    stages {
        stage('Generate Version') {
            steps {
                script {
                    // Компоненты версии
                    def majorVersion = '2'
                    def minorVersion = '5'
                    def patchVersion = env.BUILD_NUMBER
                    def branch = env.BRANCH_NAME ?: 'main'

                    // Формируем версию
                    def version = "${majorVersion}.${minorVersion}.${patchVersion}"

                    // Если не main ветка, добавляем суффикс
                    if (branch != 'main') {
                        version = "${version}-${branch}"
                    }

                    echo "Application version: ${version}"
                    env.APP_VERSION = version
                }
            }
        }

        stage('Build') {
            steps {
                sh "make build VERSION=${env.APP_VERSION}"
            }
        }
    }
}
```

Здесь мы создаём версию приложения в формате `2.5.42` или `2.5.42-develop` для feature-веток, а затем используем её в команде сборки.