# Ansible Playbooks 

![Ansible Lint CI](https://github.com/s1l-d/ansible-playbooks/actions/workflows/ansible-lint.yml/badge.svg)

Коллекция production-ready плейбуков и ролей для автоматизации Linux-серверов.
Создано в рамках обучения DevOps-инженерии.

##  Структура

| Папка | Назначение |
|-------|------------|
| `inventory/` | Инвентарь окружений (staging, production) + group_vars |
| `playbooks/` | Плейбуки: от hello-world до деплоя с Vault |
| `roles/nginx/` | Переиспользуемая роль nginx (templates, handlers, tags) |
| `vault/` | Зашифрованные секреты (Ansible Vault, AES256) |

##  Плейбуки

| Файл | Что делает |
|------|-----------|
| `01-hello-world.yml` | Проверка подключения, сбор фактов, uptime |
| `02-server-setup.yml` | Базовая настройка: пакеты, пользователь, бэкапы, cron |
| `03-nginx-role.yml` | Деплой nginx через роль с шаблоном Jinja2 |
| `04-multi-env-nginx.yml` | Деплой в staging/production с разными переменными |
| `05-tags-conditions.yml` | Гибкий деплой: теги (--tags) и условия (when) |
| `06-vault-secrets.yml` | Деплой секретов из Ansible Vault (AES256, no_log) |

##  Использование

    # Проверка подключения
    ansible all -m ping

    # Деплой в staging
    ansible-playbook -i inventory/staging playbooks/04-multi-env-nginx.yml

    # Только конфиг nginx (без переустановки пакетов)
    ansible-playbook -i inventory/production playbooks/05-tags-conditions.yml --tags config

    # Деплой секретов (спросит vault-пароль)
    ansible-playbook -i inventory/staging playbooks/06-vault-secrets.yml --ask-vault-pass

##  Секреты (Ansible Vault)

Пароли и API-ключи хранятся в `vault/secrets.yml` в зашифрованном виде (AES256).
Зашифрованный файл можно безопасно коммитить в публичный репозиторий.

**Полезные команды:**

    # Создать новый зашифрованный файл
    ansible-vault create vault/new-secrets.yml

    # Посмотреть содержимое
    ansible-vault view vault/secrets.yml

    # Отредактировать
    ansible-vault edit vault/secrets.yml

    # Сменить пароль
    ansible-vault rekey vault/secrets.yml

##  Ключевые концепции

- **Идемпотентность**: повторный запуск не меняет уже настроенное
- **Роли**: переиспользуемые модули конфигурации (tasks, handlers, templates, defaults)
- **Шаблоны Jinja2**: динамические конфиги с переменными
- **Handlers**: перезапуск служб только при изменениях (notify)
- **group_vars**: разные переменные для staging/production
- **Tags + when**: гибкое выборочное выполнение задач
- **Ansible Vault**: безопасное хранение секретов в git (AES256)
- **CI**: автоматическая проверка плейбуков через ansible-lint в GitHub Actions

##  CI/CD

Автоматическая проверка кода при каждом push через **GitHub Actions**:
- Линтинг всех плейбуков и ролей через `ansible-lint`
- Статус отображается в бейдже вверху README


Стек: Linux • Docker • GitHub Actions • Git • Ansible • bash • systemd