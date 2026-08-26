# Установка requirements-handoff в ChatGPT

`requirements-handoff` предназначен для установки и использования только в ChatGPT.

## Готовая сборка

Скачайте последний ZIP из [GitHub Releases](https://github.com/z03ps00/chatgpt-requirements-handoff/releases/latest). Распаковывать архив перед загрузкой не требуется.

Если в ChatGPT доступен раздел Skills:

1. Откройте боковую панель ChatGPT.
2. Выберите `Plugins`.
3. Откройте вкладку `Skills`.
4. Нажмите `Create`.
5. Выберите `Upload from your computer`.
6. Загрузите ZIP из Release.
7. Просмотрите содержимое и завершите установку.

После установки ChatGPT может автоматически использовать Skill, когда запрос соответствует русскому `description`.

## Интерактивное создание

`Plugins` → `Skills` → `Create` → `Create with chat`

Передайте ZIP и используйте запрос:

```text
Создай Personal Skill из пакета requirements-handoff.
Сохрани имя, русское description, SKILL.md и supporting resources без смыслового упрощения.
Skill предназначен только для ChatGPT.
После создания покажи draft для проверки перед установкой.
```

## Быстрая проверка

```text
Оформи это человеческое описание как требования для передачи разработчику:

Нужно после проведения документа показывать отдельное предупреждение, старое сообщение убрать, но существующий алгоритм проверки не менять. Должно работать и для «Провести и закрыть».
```

Ожидается `Requirements Handoff Contract` с `R-*`, `AC-*`, `NG-*`, `PR-*`, `INV-*`, без подмены требований implementation plan.

## Доступность Skills

Personal Skills доступны не во всех планах и рабочих областях. Интерфейс может отличаться между web, desktop и mobile. Актуальная справка: [Skills in ChatGPT — OpenAI Help Center](https://help.openai.com/en/articles/20001066-skills-in-chatgpt).
