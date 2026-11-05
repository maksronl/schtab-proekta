# 🚀 Штаб проекта

**Единое цифровое пространство для проектной деятельности** в школах, IT-Кубах и Кванториумах.

Сервис решает проблему разрозненности инструментов: задачи, файлы, дедлайны и обсуждения — всё в одном месте, с уведомлениями в мессенджере MAX.

> Хакатон «Идея фикс» — команда «Код 35», Вологодская область, г. Вологда.

---

## 🔗 Ссылки

- 🤖 **Бот в MAX:** https://max.ru/ideya_fiks_104_bot
- 💻 **GitHub:** https://github.com/maksronl/schtab-proekta
- 🌐 **Mini App:** открывается из бота или локально на `http://localhost:8000`

---

## 🛠 Технологии

| Слой | Стек |
|---|---|
| Backend | Python 3.11, FastAPI, asyncpg, psycopg2 |
| Frontend | HTML, CSS, Vanilla JS |
| База данных | PostgreSQL 15 |
| Бот | MAX Bot API |
| Инфраструктура | Docker, Docker Compose |

---

## 📦 Функционал

- Канбан-доска: План → В работе → На проверке → Готово
- Роли: учитель и ученик
- Дедлайны с цветовой индикацией
- Файлы к задачам (до 20 МБ) + выгрузка проекта в ZIP
- Шаблоны проектов (игра, исследование, бот, соцпроект, экзамен, медиа, стартап)
- Уведомления в MAX: новая задача, смена статуса, напоминания о дедлайнах
- Приглашения по ID и ссылке-приглашению

---

## 🚀 Инструкция по запуску

### Требования
- Установленный Docker и Docker Compose.
- Свободные порты `8000` (веб) и `5432` (база данных).

### 1. Клонировать репозиторий
```bash
git clone https://github.com/maksronl/schtab-proekta.git
cd schtab-proekta

###2. Создать файл .env

-В корне проекта (рядом с docker-compose.yml) создайте файл .env и добавьте туда токен вашего бота:
env

BOT_TOKEN=ваш_токен_от_MAX
(Без этого токена бот не сможет отправлять уведомления).

###3. Запуск из готовых Docker-образов (.tar)

-В репозитории уже лежат собранные образы. Загрузите их в Docker:
```bash
docker load -i shtab-web.tar
docker load -i shtab-bot.tar

-После этого запустите контейнеры:
```bash
docker-compose up -d

###4. Открыть приложение

-Веб-интерфейс доступен по адресу: http://localhost:8000

---

🖥 Пример запуска через командную строку (без docker-compose)

Если нужно запустить сервисы по отдельности (после загрузки образов):

    Запуск базы данных:

```bash

docker run -d --name shtab-db -e POSTGRES_USER=user -e POSTGRES_PASSWORD=password -e POSTGRES_DB=shtab_db -p 5432:5432 postgres:15-alpine

    Запуск веб-приложения:

```bash

docker run -d --name shtab-web --link shtab-db:db -e DB_HOST=db -e DB_NAME=shtab_db -e DB_USER=user -e DB_PASSWORD=password -p 8000:8000 shtab-web:latest

    Запуск бота:

```bash

docker run -d --name shtab-bot --link shtab-db:db -e DB_HOST=db -e DB_NAME=shtab_db -e DB_USER=user -e DB_PASSWORD=password -e BOT_TOKEN=ваш_токен shtab-bot:latest

