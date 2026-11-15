# Ansible Playbooks
Коллекция production-ready плейбуков для автоматизации Linux-серверов.

##   Структура

| Папка | Назначение |
|-------|------------|
| `inventory/` | Инвентарь хостов (production, staging) |
| `playbooks/` | Плейбуки для настройки серверов |
| `roles/` | Переиспользуемые роли |

##    Плейбуки

### 01-hello-world.yml
Тестовый плейбук: проверка подключения, сбор фактов, вывод uptime.

### 02-server-setup.yml
Базовая настройка сервера: установка пакетов, создание пользователя, настройка бэкапов.

##   Использование

```bash
ansible all -m ping
ansible-playbook playbooks/01-hello-world.yml

