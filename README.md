# Ansible Playbooks 

Коллекция production-ready плейбуков и ролей для автоматизации Linux-серверов.
Создано в рамках обучения DevOps-инженерии.

##  Структура

| Папка | Назначение |
|-------|------------|
| `inventory/` | Инвентарь окружений (staging, production) + group_vars |
| `playbooks/` | Плейбуки: от hello-world до multi-env деплоя |
| `roles/nginx/` | Переиспользуемая роль nginx (templates, handlers, tags) |

##  Плейбуки

| Файл | Что делает |
|------|-----------|
| `01-hello-world.yml` | Проверка подключения, сбор фактов, uptime |
| `02-server-setup.yml` | Базовая настройка: пакеты, пользователь, бэкапы, cron |
| `03-nginx-role.yml` | Деплой nginx через роль с шаблоном Jinja2 |
| `04-multi-env-nginx.yml` | Деплой в staging/production с разными переменными |
| `05-tags-conditions.yml` | Гибкий деплой: теги (--tags) и условия (when) |

##  Использование

    # Проверка подключения
    ansible all -m ping

    # Деплой в staging
    ansible-playbook -i inventory/staging playbooks/04-multi-env-nginx.yml

    # Только конфиг nginx (без переустановки пакетов)
    ansible-playbook -i inventory/production playbooks/05-tags-conditions.yml --tags config

##  Ключевые концепции

- **Идемпотентность**: повторный запуск не меняет уже настроенное
- **Роли**: переиспользуемые модули конфигурации
- **Шаблоны Jinja2**: динамические конфиги с переменными
- **Handlers**: перезапуск служб только при изменениях
- **group_vars**: разные переменные для staging/production
- **Tags + when**: гибкое выборочное выполнение



