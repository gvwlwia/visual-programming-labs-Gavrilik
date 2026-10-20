## Часть 1. Установка и запуск n8n

n8n запущен в Docker из официального образа `n8nio/n8n`.

Подготовил на хосте две папки для volume: `~/n8n-data` и `~/n8n-files`.

Команда запуска:

```bash
docker run -d --name n8n --restart unless-stopped -p 5678:5678 \
  -e TZ="Europe/Minsk" -e GENERIC_TIMEZONE="Europe/Minsk" \
  -e N8N_SECURE_COOKIE=false \
  -v ~/n8n-data:/home/node/.n8n \
  -v ~/n8n-files:/data \
  n8nio/n8n
```

- Первый volume (`~/n8n-data` → `/home/node/.n8n`) хранит базу SQLite, ключ шифрования credentials и сами workflow, поэтому данные не теряются при пересоздании контейнера.
- Второй volume (`~/n8n-files` → `/data`) используется для работы с файлами из workflow.
- Порт 5678 проброшен на хост, интерфейс доступен по http://localhost:5678.
- Переменные `TZ` и `GENERIC_TIMEZONE` задают часовой пояс, чтобы время в расписании и в `timestamp` было корректным.
- `N8N_SECURE_COOKIE=false` позволяет работать по http без HTTPS.

После запуска открыл http://localhost:5678 и зарегистрировал владельца (owner account).

Версия n8n: `<вставь результат docker exec n8n n8n --version>`

![Версия и контейнер](../screenshots/01-version.png)
![Запуск контейнера](../screenshots/02-docker-run.png)
![Интерфейс n8n](../screenshots/03-n8n-ui.png)