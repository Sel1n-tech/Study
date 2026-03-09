### Что такое Agent

Агент — это машина или окружение, где выполняется ваш пайплайн. Когда вы запускаете джобу в Jenkins, код не выполняется в самом Jenkins-сервере. Вместо этого Jenkins отправляет задачи на агент, который делает всю работу.

Агент может быть:

- Физическим или виртуальным сервером
- Docker-контейнером
- Облачной машиной 
- Тем же сервером, где установлен Jenkins (встроенный агент)

Директива `agent` обязательна в каждом декларативном пайплайне. Она указывает, где выполнять код.

### Минимальный пример

```typescript
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building on some agent...'
            }
        }
    }
}
```

Что здесь происходит:

- `agent any` — говорит Jenkins выполнить пайплайн на любом доступном агенте
- Jenkins сам выберет свободный агент из пула
- Все стейджи будут выполнены на этом агенте

### Типы агентов

Jenkins поддерживает несколько способов указать агент:

```typescript
pipeline {
    // 1. Любой доступный агент
    agent any

    stages {
        stage('Example') {
            steps {
                echo 'Running on any agent'
            }
        }
    }
}
```

```typescript
pipeline {
    // 2. Без агента (нужно указывать в каждом стейдже)
    agent none

    stages {
        stage('Build') {
            agent any
            steps {
                echo 'This stage runs on an agent'
            }
        }
    }
}
```

```javascript
pipeline {
    // 3. Агент с конкретной меткой
    agent {
        label 'linux'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Running on agent with label "linux"'
            }
        }
    }
}
```

```javascript
pipeline {
    // 4. Docker-контейнер как агент
    agent {
        docker {
            image 'node:18'
        }
    }

    stages {
        stage('Build') {
            steps {
                sh 'node --version'
            }
        }
    }
}
```

Основные варианты:

- `agent any` — выполнить на любом свободном агенте
- `agent none` — не назначать агент на уровне пайплайна (нужно указать в каждом стейдже)
- `agent { label 'name' }` — выполнить на агенте с определённой меткой
- `agent { docker { image 'name' } }` — выполнить внутри Docker-контейнера

### Agent на уровне пайплайна и стейджа

Агент можно указать для всего пайплайна или для отдельных стейджей:

```javascript
pipeline {
    // Агент для всего пайплайна
    agent {
        label 'linux'
    }

    stages {
        stage('Build') {
            steps {
                // Выполняется на агенте 'linux'
                sh 'make build'
            }
        }

        stage('Test on Docker') {
            // Переопределяем агент для этого стейджа
            agent {
                docker {
                    image 'python:3.9'
                }
            }
            steps {
                // Выполняется в Docker-контейнере с Python
                sh 'python --version'
                sh 'pytest tests/'
            }
        }

        stage('Deploy') {
            steps {
                // Снова на агенте 'linux'
                sh 'make deploy'
            }
        }
    }
}
```

- Стейджи Build и Deploy выполняются на агенте с меткой `linux`
- Стейдж Test on Docker переопределяет агент и запускается в Docker-контейнере
- После завершения стейджа Test on Docker выполнение возвращается к основному агенту

### Что такое Node

Нода — это физическая или виртуальная машина, подключённая к Jenkins. Каждый агент работает на какой-то ноде.

В декларативном пайплайне термины "агент" и "нода" часто используются взаимозаменяемо, но есть нюанс:

- **Node** — это машина в системе Jenkins
- **Agent** — это программа на ноде, которая выполняет задачи

В интерфейсе Jenkins вы увидите раздел "Manage Nodes", где перечислены все подключённые машины. Каждая нода может иметь метки (labels), которые используются в директиве `agent { label 'name' }`.

### Более реалистичный пример

Рассмотрим пайплайн для веб-приложения, которое собирается на Linux, а тесты UI запускаются на Windows:

```javascript
pipeline {
    agent none  // Не используем общий агент

    stages {
        stage('Build Backend') {
            agent {
                label 'linux-docker'
            }
            steps {
                echo 'Building Go application...'
                sh 'go build -o app ./cmd/server'
            }
        }

        stage('Test Backend') {
            agent {
                docker {
                    image 'golang:1.21'
                    label 'linux-docker'
                }
            }
            steps {
                echo 'Running Go tests...'
                sh 'go test ./...'
            }
        }

        stage('Build Frontend') {
            agent {
                docker {
                    image 'node:18'
                }
            }
            steps {
                echo 'Building React application...'
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('UI Tests') {
            agent {
                label 'windows-chrome'
            }
            steps {
                echo 'Running Selenium tests...'
                bat 'run-ui-tests.bat'
            }
        }
    }
}
```

В этом примере:

- **Build Backend** — выполняется на Linux-ноде с Docker
- **Test Backend** — запускается в Docker-контейнере с Go
- **Build Frontend** — выполняется в контейнере с Node.js
- **UI Tests** — запускается на Windows-машине с установленным Chrome

Каждый стейдж использует подходящее окружение для своей задачи.

### Метки (Labels)

Метки помогают организовать ноды по характеристикам. Примеры меток:

- `linux`, `windows`, `macos` — по операционной системе
- `docker` — на ноде установлен Docker
- `gpu` — нода с видеокартой для ML-задач
- `prod`, `staging` — по окружению
- `high-memory` — нода с большим количеством RAM

Метки назначаются администратором Jenkins в настройках нод. В пайплайне вы просто используете их:

```csharp
agent {
    label 'linux && docker'  // Нода с обеими метками
}
```

### Workspace (воркспейс)

Когда пайплайн запускается на агенте, Jenkins создаёт воркспейс — директорию, где будет выполняться код. В этой директории клонируется репозиторий, создаются артефакты и выполняются команды.

Путь к воркспейсу обычно выглядит так:

```swift
/var/jenkins_home/workspace/my-job-name/
```

Внутри пайплайна все команды `sh` выполняются относительно этой директории.

### Визуальная схема работы агентов

```less
Jenkins Master (сервер)
    │
    ├─→ Agent 1 (Linux, label: 'linux')
    │   └── Workspace: /home/jenkins/workspace/job-1/
    │
    ├─→ Agent 2 (Windows, label: 'windows')
    │   └── Workspace: C:\Jenkins\workspace\job-2\
    │
    └─→ Agent 3 (Docker Host, label: 'docker')
        └── Запускает контейнеры для пайплайнов
```