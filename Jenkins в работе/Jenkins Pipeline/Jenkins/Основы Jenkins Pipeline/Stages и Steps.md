### Что такое Stages

Стейдж (stage) — это логический блок работы в пайплайне. Он объединяет несколько шагов под одним понятным названием. Стейджи помогают разделить процесс CI/CD на этапы и делают пайплайн наглядным.

Каждый стейдж отображается в интерфейсе Jenkins как отдельный элемент. Если стейдж выполнился успешно — он зелёный, если упал — красный. Это позволяет сразу увидеть, на каком этапе возникла проблема.

Стейджи выполняются последовательно, один за другим. Если какой-то стейдж завершается с ошибкой, следующие стейджи не запускаются (если не настроено иначе).

### Минимальный пример

```typescript
pipeline {
    agent any
    stages {
        stage('First Stage') {
            steps {
                echo 'This is step one'
            }
        }
    }
}
```

Что здесь происходит:

- `stages { }` — контейнер для всех стейджей
- `stage('First Stage') { }` — один стейдж с названием "First Stage"
- `steps { }` — блок, в котором перечислены все шаги этого стейджа
- `echo 'This is step one'` — единственный шаг, который выводит текст

### Анатомия stages и steps

Рассмотрим пример с несколькими стейджами и разными типами шагов:

```typescript
pipeline {
    agent any

    stages {
        // Стейдж 1: Подготовка
        stage('Prepare') {
            steps {
                echo 'Preparing workspace...'
                sh 'mkdir -p build'
            }
        }

        // Стейдж 2: Сборка
        stage('Build') {
            steps {
                echo 'Building application...'
                sh 'gcc main.c -o app'
            }
        }

        // Стейдж 3: Проверка
        stage('Verify') {
            steps {
                echo 'Running verification...'
                sh './app --version'
            }
        }
    }
}
```

Разберём каждый элемент:

1. **stage('Prepare')** — стейдж подготовки, создаёт директорию build
2. **stage('Build')** — стейдж сборки, компилирует C-программу
3. **stage('Verify')** — стейдж проверки, запускает собранное приложение

Внутри каждого стейджа блок `steps { }` содержит команды. Команды выполняются строго по порядку, сверху вниз.

### Типы шагов (steps)

Jenkins предоставляет множество встроенных команд для блока `steps`. Рассмотрим самые распространённые:

```typescript
pipeline {
    agent any
    stages {
        stage('Different Steps') {
            steps {
                // Вывод текста
                echo 'Hello from pipeline'

                // Выполнение shell-команды (Linux/Mac)
                sh 'ls -la'

                // Выполнение batch-команды (Windows)
                bat 'dir'

                // Выполнение PowerShell (Windows)
                powershell 'Get-ChildItem'

                // Пауза (в секундах)
                sleep 5

                // Вывод сообщения об ошибке и остановка
                error 'Something went wrong!'
            }
        }
    }
}
```

Основные типы шагов:

- `echo` — вывод текста в консоль билда
- `sh` — выполнение команд bash/sh (для Linux и MacOS)
- `bat` — выполнение batch-скриптов (для Windows)
- `powershell` — выполнение PowerShell команд (для Windows)
- `sleep` — задержка выполнения на указанное количество секунд
- `error` — принудительная остановка пайплайна с сообщением об ошибке

### Более реалистичный пример

Рассмотрим пайплайн для Python-приложения с тестами:

```typescript
pipeline {
    agent any

    stages {
        stage('Setup') {
            steps {
                echo 'Setting up virtual environment...'
                sh 'python3 -m venv venv'
                sh '. venv/bin/activate'
            }
        }

        stage('Install') {
            steps {
                echo 'Installing dependencies...'
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Lint') {
            steps {
                echo 'Running code quality checks...'
                sh 'flake8 src/'
                sh 'pylint src/'
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                sh 'pytest tests/ -v'
            }
        }

        stage('Package') {
            steps {
                echo 'Creating distribution package...'
                sh 'python setup.py sdist bdist_wheel'
            }
        }
    }
}
```

В этом примере пайплайн разделён на логические этапы:

- **Setup** — создание виртуального окружения Python
- **Install** — установка зависимостей из requirements.txt
- **Lint** — проверка качества кода с помощью flake8 и pylint (два шага в одном стейдже)
- **Test** — запуск тестов через pytest
- **Package** — создание дистрибутива приложения

Обратите внимание, что в стейдже Lint мы используем два шага подряд. Оба должны выполниться успешно, иначе весь стейдж будет помечен как провалившийся.

### Именование стейджей

Названия стейджей должны быть понятными и отражать суть выполняемой работы. Хорошие примеры:

- Build, Test, Deploy — классические названия
- Compile Sources, Run Unit Tests, Push to Registry — более детальные
- Checkout Code, Install Dependencies, Lint Code — пошаговые действия

Плохие примеры:

- Stage 1, Stage 2 — неинформативно
- Do Stuff, Work, Process — слишком абстрактно
- asdfgh — совсем непонятно

### Порядок выполнения

Важно понимать последовательность:

```vbnet
Пайплайн запускается
    ↓
Выполняется Stage 1
    ↓
    Выполняется Step 1.1
    ↓
    Выполняется Step 1.2
    ↓
    Выполняется Step 1.3
    ↓
Стейдж 1 завершён успешно
    ↓
Выполняется Stage 2
    ↓
    Выполняется Step 2.1
    ↓
    Step 2.1 упал с ошибкой
    ↓
Stage 2 провален
    ↓
Пайплайн остановлен (Stage 3 не запускается)
```

Если хотя бы один шаг внутри стейджа падает с ошибкой, весь стейдж считается проваленным. Последующие стейджи по умолчанию не выполняются.