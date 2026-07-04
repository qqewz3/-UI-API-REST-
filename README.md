# UI-API-REST

## Пет-проект: Комплексное UI и API (REST) тестирование платформ Steam & Trello

Репозиторий содержит примеры тестовой документации (UI/UX) и автоматизированных тестовых коллекций (API) для демонстрации практических навыков QA-инженера. Проект моделирует реальные задачи коммерческого тестирования интернет-магазинов и таск-менеджеров.

---

## Используемые технологии и инструменты

- Тест-дизайн: Эквивалентное разделение, Граничные значения, Комбинаторика, Позитивное/Негативное тестирование
- Инструменты: Postman, Google Docs / Sheets, DevTools
- Автоматизация и API: REST API, JavaScript (автотесты в Postman), Newman

---

## Часть 1: UI/UX Тестирование (Платформа Steam)

Разработана гибкая тестовая документация для критически важных модулей интернет-магазина (Регистрация, Поиск и Фильтрация, Корзина покупок, Локализация).

- Чек-лист (Позитивный/Негативный): Компактное покрытие основных сценариев.
- E2E Тест-кейсы: Детализированные сценарии для проверки сложной бизнес-логики.
- Матрицы тест-дизайна: Оптимизация проверок валидации полей ввода.

Ссылка на тестовую документацию:
https://docs.google.com/document/d/1HJwTkUEnaU7tLtiUtwcEI1oCJgta-2DOWd0XzuEk810/edit?tab=t.0
---

## Часть 2: Тестирование API и Автоматизация (Postman + Newman)

В репозитории представлены две экспортированные коллекции Postman. Все запросы покрыты автоматизированными JavaScript-тестами и успешно проходят прогон через Newman.

---

## Запуск API-тестов

### 1. Установка Newman

npm install -g newman

### 2. Настройка ключей

Для запуска тестов необходимо получить API-ключи и токены.

#### Trello

1. Перейдите на страницу: https://trello.com/app-key
2. Скопируйте API Key
3. Нажмите "Token" и скопируйте токен

#### Steam

1. Перейдите на страницу: https://steamcommunity.com/dev/apikey
2. Введите URL сайта (можно localhost)
3. Скопируйте API Key

#### Создание файлов с ключами

В папке environments/ лежат файлы-примеры (trello_example.json и steam_example.json).

Скопируйте их и заполните своими ключами.

Для Windows через командную строку:
copy environments\trello_example.json environments\trello.json
copy environments\steam_example.json environments\steam.json

Или создайте файлы вручную.

Пример для trello.json:
{
  "name": "Trello",
  "values": [
    {
      "key": "API_key",
      "value": "ВАШ_РЕАЛЬНЫЙ_КЛЮЧ",
      "type": "secret",
      "enabled": true
    },
    {
      "key": "API_token",
      "value": "ВАШ_РЕАЛЬНЫЙ_ТОКЕН",
      "type": "secret",
      "enabled": true
    },
    {
      "key": "base_url",
      "value": "https://api.trello.com/1/",
      "type": "default",
      "enabled": true
    }
  ],
  "_postman_variable_scope": "environment"
}

Пример для steam.json:
{
  "name": "Steam",
  "values": [
    {
      "key": "api_key",
      "value": "ВАШ_РЕАЛЬНЫЙ_КЛЮЧ",
      "type": "secret",
      "enabled": true
    },
    {
      "key": "base_url",
      "value": "https://api.steampowered.com",
      "type": "default",
      "enabled": true
    }
  ],
  "_postman_variable_scope": "environment"
}

ВАЖНО: Файлы с реальными ключами НЕ хранятся в репозитории (добавлены в .gitignore).

### 3. Запуск тестов Trello

newman run collections/Trello.postman_collection.json -e environments/trello.json

### 4. Запуск тестов Steam

newman run collections/Steam.postman_collection.json -e environments/steam.json

### 5. Запуск всех тестов

newman run collections/Trello.postman_collection.json -e environments/trello.json && newman run collections/Steam.postman_collection.json -e environments/steam.json

---

## Результаты тестирования

Платформа: Trello
Тестов: 6
Пройдено: 6
Ошибок: 0

Платформа: Steam
Тестов: 3
Пройдено: 3
Ошибок: 0

### Скриншоты успешного прогона

Trello:
./screenshots/trello_success_run.jpg

Steam:
./screenshots/steam_success_run.jpg

---

## Покрытие тестов

### Trello (E2E-сценарий)
- Создание доски
- Создание списка
- Создание карточки
- Обновление карточки (PUT)
- Проверка изменения имени карточки
- Удаление карточки

### Steam
- Получение глобальных достижений игры (Dying Light 2)
- Проверка структуры ответа (массив achievements)
- Валидация формата ID достижений (префикс "ACH_")

---

## Безопасность

- Все API-ключи и токены не хранятся в репозитории
- Файлы с ключами добавлены в .gitignore
- В репозитории лежат только файлы-примеры (*_example.json)
- HTML-отчеты не загружаются в GitHub

---

## Структура проекта

- **collections/** — Postman коллекции
  - `Steam.postman_collection.json`
  - `Trello.postman_collection.json`
- **environments/** — Environment-файлы
  - `trello_example.json` — шаблон для Trello
  - `steam_example.json` — шаблон для Steam
  - `trello.json` — реальный ключ (в .gitignore)
  - `steam.json` — реальный ключ (в .gitignore)
- **screenshots/** — скриншоты результатов
  - `trello_success_run.jpg`
  - `steam_success_run.jpg`
- **reports/** — HTML-отчеты (в .gitignore)
- `.gitignore`
- `README.md`

---

## Что дальше

Планируется:
- Интеграция с GitHub Actions (CI/CD)
- Добавление негативных тест-кейсов
- Параллельный запуск тестов

---

## Автор

Ваше Имя
QA-инженер
GitHub: https://github.com/qqewz3
