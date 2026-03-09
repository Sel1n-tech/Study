**Pull** **Request** **(****PR****)** — это запрос на слияние изменений из одной ветки в другую (либо из fork-репозитория в родительский репозиторий). Это не просто технический процесс, а **способ общения команды** о коде.

**Pull Request (PR)** в GitHub **= Merge Request (MR)** в GitLab

## Варианты реализации

- Через fork репозитория
- Через отдельные ветки в общем репозитории

## **Зачем нужны PR?**

- **Контроль качества** — код проверяют перед слиянием
- **Обучение команды** — все видят как пишут другие
- **Документирование** — обсуждение решений сохраняется
- **База знаний** — история принятых решений

**PR** похож на подачу документов на согласование. Вы сделали работу, но нужно чтобы её проверили и утвердили.

## Полезные ссылки

- Обсуждение Pull Request на StackOverflow: [https://ru.stackoverflow.com/questions/134183/Что-такое-pull-request](https://ru.stackoverflow.com/questions/134183/%D0%A7%D1%82%D0%BE-%D1%82%D0%B0%D0%BA%D0%BE%D0%B5-pull-request)
- Статья "[Как создать pull request на GitHub](https://arenda-server.cloud/blog/kak-sozdat-pull-request-na-github/)"
- Статья на Хабре: [https://habr.com/ru/articles/125999/](https://habr.com/ru/articles/125999/)




## Пошаговая настройка: от форка до PR

Давайте разберём весь процесс по шагам. Допустим, вы хотите внести изменения в проект мониторинга серверов.

### Шаг 1: Создание fork

Заходите на GitHub к нужному репозиторию и нажимаете кнопку “Fork” в правом верхнем углу. Это создаст копию проекта в вашем аккаунте.

### Шаг 2: Клонирование на локальную машину

`   # Клонируем ваш fork   git clone https://github.com/YOUR_USERNAME/project-name.git   cd project-name`

`   # Добавляем оригинальный репозиторий как upstream   git remote add upstream https://github.com/ORIGINAL_OWNER/project-name.git   `

`# Проверяем, что всё настроено правильно   git remote -v   `

### Шаг 3: Создание новой ветки

`   # Обновляем основную ветку   git checkout main   git pull upstream main`

`   # Создаём новую ветку для изменений   git checkout -b fix-server-monitoring-bug   `

`# Или более описательное название   git checkout -b add-nginx-config-validation   `

### Шаг 4: Внесение изменений и коммиты

Вносите свои изменения в код. Например, исправляете баг в скрипте мониторинга или добавляете новую функцию.

`   # Добавляем изменения   git add .`

`   # Создаём коммит с описательным сообщением   git commit -m "Fix memory leak in server monitoring script  - Fixed buffer overflow in memory usage calculation   - Added proper error handling for disk space checks   - Updated documentation with new configuration options"   `

`# Загружаем изменения в свой fork   git push origin fix-server-monitoring-bug   `

### Шаг 5: Создание Pull Request

Идёте на GitHub, переходите в свой fork. Должна появиться жёлтая плашка с предложением создать pull request. Нажимаете “Compare & pull request”.

## Примеры и кейсы из практики

Приведу несколько реальных сценариев, с которыми вы можете столкнуться:

### Сценарий 1: Исправление бага в Ansible роли

Вы используете популярную Ansible роль для настройки Nginx на своём [выделенном сервере](https://arenda-server.cloud/dedicated), но обнаружили, что она не работает с новой версией Ubuntu. Исправили баг локально, теперь хотите поделиться исправлением.

`    # В файле tasks/main.yml исправляем условие   - name: Install Nginx   apt:   name: nginx   state: present   when: ansible_distribution_version is version('20.04', '>=')    `

**Хороший PR:** Описываете проблему, показываете, как воспроизвести баг, предлагаете решение с тестами.

**Плохой PR:** Просто “Fixed bug” без объяснений.

### Сценарий 2: Добавление новой функции в мониторинг

Вы добавили поддержку мониторинга Docker контейнеров в существующий скрипт мониторинга серверов:

`   #!/bin/bash   # Новая функция для мониторинга Docker   check_docker_containers() {   local running_containers=$(docker ps -q | wc -l)   local total_containers=$(docker ps -a -q | wc -l)`

`   echo "Docker containers: $running_containers/$total_containers running"  if [ $running_containers -eq 0 ]; then   echo "WARNING: No Docker containers are running!"   return 1   fi   `

`return 0   }   `

### Таблица сравнения подходов к PR

|Критерий|Хороший PR|Плохой PR|
|---|---|---|
|Название|Add Docker monitoring to server health check|Update|
|Описание|Детальное объяснение проблемы и решения|Просто “Fixed some stuff”|
|Размер|Одна логическая функция|Множество несвязанных изменений|
|Тесты|Включены и проходят|Отсутствуют или сломаны|
|Документация|Обновлена при необходимости|Устарела|

## Полезные команды и скрипты

Вот набор команд, которые помогут вам в повседневной работе с PR:

`   # Синхронизация с upstream перед созданием новой ветки   git fetch upstream   git checkout main   git merge upstream/main   git push origin main`

`   # Создание ветки с автоматической привязкой к remote   git checkout -b feature-branch   git push -u origin feature-branch  # Интерактивный rebase для "причёсывания" коммитов   git rebase -i HEAD~3  # Принудительная отправка после rebase (осторожно!)   git push --force-with-lease  # Просмотр различий между ветками   git diff main..feature-branch   `

`# Проверка статуса всех веток   git branch -vv   `

### Полезный скрипт для автоматизации

`   #!/bin/bash   # create-pr-branch.sh - автоматизация создания ветки для PR`

`   if [ $# -eq 0 ]; then   echo "Usage: $0 "   exit 1   fi  BRANCH_NAME=$1  # Обновляем main   git checkout main   git pull upstream main  # Создаём новую ветку   git checkout -b $BRANCH_NAME  # Настраиваем отслеживание   git push -u origin $BRANCH_NAME   `

`echo "Branch $BRANCH_NAME created and ready for work!"   `

## Продвинутые техники и автоматизация

### GitHub CLI для автоматизации

GitHub CLI ([https://cli.github.com/](https://cli.github.com/)) позволяет создавать PR прямо из командной строки:

`   # Установка GitHub CLI (Ubuntu/Debian)   sudo apt install gh`

`   # Авторизация   gh auth login  # Создание PR   gh pr create --title "Add Docker monitoring support" --body "Adds comprehensive Docker container monitoring to the existing server health check script"  # Просмотр статуса PR   gh pr status   `

`# Просмотр и код-ревью   gh pr view 42   gh pr review 42 --approve   `

### Интеграция с CI/CD

Современные проекты часто используют GitHub Actions для автоматической проверки PR:

`   # .github/workflows/pr-check.yml   name: PR Check   on:   pull_request:   branches: [ main ]`

`jobs:   test:   runs-on: ubuntu-latest   steps:   - uses: actions/checkout@v3   - name: Setup Python   uses: actions/setup-python@v3   with:   python-version: 3.9   - name: Install dependencies   run: |   pip install -r requirements.txt   pip install pytest   - name: Run tests   run: pytest tests/   `

## Альтернативные решения и инструменты

Хотя GitHub — самая популярная платформа, существуют альтернативы:

- **GitLab** — использует merge requests вместо pull requests
- **Bitbucket** — также поддерживает pull requests
- **Gitea** — self-hosted альтернатива с похожим функционалом
- **Gerrit** — более сложная система код-ревью, популярная в enterprise

### Сравнение workflow

|Платформа|Название|Особенности|
|---|---|---|
|GitHub|Pull Request|Простой workflow, отличная интеграция|
|GitLab|Merge Request|Встроенный CI/CD, больше возможностей|
|Gerrit|Change|Patch-based workflow, сложнее в освоении|

## Статистика и интересные факты

По данным GitHub, в 2023 году:

- Создано более 200 миллионов pull requests
- Среднее время от создания PR до merge — 3.5 дня
- Самые активные языки по количеству PR: JavaScript, Python, Java
- 85% PR в открытых проектах создаются участниками, не являющимися основными maintainer’ами

Интересный факт: самый большой PR в истории GitHub содержал более 1 миллиона изменений строк (это был автоматический рефакторинг в проекте Chromium).

## Нестандартные способы использования

### PR для документации и инфраструктуры

PR можно использовать не только для кода, но и для:

- **Infrastructure as Code** — изменения в Terraform, Ansible, Kubernetes манифестах
- **Документация** — обновления README, wiki, комментарии в коде
- **Конфигурации** — настройки CI/CD, линтеры, pre-commit hooks

### Автоматизация развёртывания

Многие команды используют PR для автоматизации развёртывания на серверах:

`   # Пример workflow для автоматического деплоя   name: Deploy to staging   on:   pull_request:   branches: [ main ]`

`jobs:   deploy:   runs-on: ubuntu-latest   steps:   - name: Deploy to staging server   run: |   ssh user@staging-server.example.com "   cd /opt/app &&   git pull origin ${GITHUB_HEAD_REF} &&   docker-compose restart   "   `

## Заключение и рекомендации

Pull request — это не просто техническая возможность, это целая культура разработки. Если вы администрируете серверы, автоматизируете инфраструктуру или разрабатываете скрипты, умение создавать качественные PR открывает множество возможностей:

- **Участие в open-source проектах** — исправляйте баги в инструментах, которые используете
- **Командная работа** — синхронизируйте изменения конфигураций с коллегами
- **Контроль качества** — получайте ревью на свои скрипты и автоматизацию
- **Обучение** — изучайте чужой код через участие в проектах

Главные принципы хорошего PR:

- **Атомарность** — один PR = одна логическая функция
- **Описательность** — объясняйте, что и почему вы делаете
- **Тестируемость** — включайте тесты и проверки
- **Документированность** — обновляйте документацию при необходимости