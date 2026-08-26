<div align="center">

# ChatGPT Requirements Handoff

**ChatGPT Skill для перевода человеческого ТЗ в инженерный контракт требований**

Превращает переписку, задачу из трекера, письмо, заметки или расшифровку встречи в структурированный `Requirements Handoff Contract` для передачи разработчику или на следующий AI-этап.

[![ChatGPT Skill](https://img.shields.io/badge/ChatGPT-Skill-10a37f.svg)](#установка-в-chatgpt)
[![Runtime](https://img.shields.io/badge/runtime-English-informational.svg)](#почему-skill-внутри-на-английском)
[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg)](LICENSE)
[![GitHub](https://img.shields.io/badge/author-z03ps00-black.svg)](https://github.com/z03ps00)

</div>

---

## Зачем это нужно

Обычное ТЗ редко выглядит как готовая спецификация. Чаще это задача из трекера, несколько комментариев и фразы вроде:

> Нужно после проведения показать предупреждение. Старое сообщение убрать, но саму проверку не менять. И проверить «Провести и закрыть».

Для человека контекст обычно понятен. Следующая AI-модель может смешать требование с предположением, выбрать реализацию за аналитика или потерять ограничение из середины переписки.

Skill даёт ChatGPT одну задачу: привести исходный материал к нейтральному контракту требований до технического проектирования.

```text
Человеческое ТЗ
      ↓
ChatGPT + requirements-handoff
      ↓
Requirements Handoff Contract
      ↓
разработчик / OpenSpec / Plan Mode / AI coding-agent
```

Сам Skill предназначен только для ChatGPT. Результат его работы остаётся нейтральным и может передаваться дальше в любой инженерный workflow.

## Что делает Skill

ChatGPT отдельно фиксирует:

- цель и scope;
- текущее и требуемое поведение;
- требования `R-*`;
- сценарии `S-*`;
- критерии приёмки `AC-*`;
- `NG-*` — что не входит в задачу;
- `PR-*` — что нельзя сломать;
- `INV-*` — технические вопросы для исследования;
- `Q-*` — незакрытые бизнес-вопросы;
- ограничения, точные значения, риски, решения и источники;
- трассировку требований до проверки результата.

Главное правило:

```text
WHAT ≠ HOW
```

Контракт фиксирует требуемое поведение, ограничения и проверку. Он не должен без основания навязывать процедуру, модуль, событие формы, архитектуру, API или другой способ реализации.

## Почему Skill внутри на английском

Начиная с `v1.1.0`, рабочие инструкции `SKILL.md`, `references/`, шаблон и пример написаны на английском. Это уменьшает объём runtime-контекста и делает инструкции более компактными для модели.

Поле `description` в YAML оставлено на русском, чтобы Skill хорошо находился по русским запросам. Сам `Requirements Handoff Contract` по умолчанию формируется на языке пользователя, поэтому русское ТЗ даёт русскую спецификацию.

README и инструкция установки остаются на русском, потому что предназначены для человека, а не для runtime-контекста Skill.

## Что получается на выходе

Сокращённый пример:

```markdown
# Requirements Handoff Contract — payment-warning

## 0. Status
READY

## R-001 — Предупреждение после проведения
**Условие:** документ успешно проведён и контроль обнаружил нарушение.
**Требование:** показать отдельное предупреждение.
**Ожидаемый результат:** одно предупреждение за одно проведение.

## PR-001 — Существующая проверка
Алгоритм определения нарушения должен продолжить работать без изменений.

## INV-001
Определить корректную точку реализации нового способа информирования.
```

Полный runtime-пример: [`examples/example-payment-warning.md`](examples/example-payment-warning.md).

## Установка в ChatGPT

Готовая сборка `v1.1.0` находится прямо в репозитории: [скачать ZIP](dist/requirements-handoff-chatgpt-skill-v1.1.0.zip). Рядом лежит [SHA-256](dist/requirements-handoff-chatgpt-skill-v1.1.0.zip.sha256).

Для следующих версий подготовлен workflow [`Publish ChatGPT Skill release`](.github/workflows/release-skill.yml). Его ручной запуск через GitHub Actions создаёт/обновляет Release и прикладывает ZIP вместе с checksum.

Далее в ChatGPT:

1. Откройте **Plugins**.
2. Перейдите в **Skills**.
3. Нажмите **Create**.
4. Выберите **Upload from your computer**.
5. Загрузите ZIP.

Подробная инструкция: [`INSTALL_CHATGPT.md`](INSTALL_CHATGPT.md).

Доступность Personal Skills зависит от плана и workspace. Актуальная справка: [Skills in ChatGPT — OpenAI Help Center](https://help.openai.com/en/articles/20001066-skills-in-chatgpt).

## Использование

После установки достаточно обычного запроса:

```text
Оформи эту переписку как ТЗ для разработчика.
```

```text
Сделай из этой задачи handoff для AI-агента.
```

```text
Формализуй требования и отдели технические предположения.
```

Skill сам применит формат Contract и проверит результат перед выдачей.

## Структура

```text
chatgpt-requirements-handoff/
├── SKILL.md
├── README.md
├── INSTALL_CHATGPT.md
├── LICENSE
├── references/
│   ├── contract-format.md
│   ├── normalization-rules.md
│   └── quality-gates.md
├── assets/
│   └── requirements-handoff-template.md
├── examples/
│   └── example-payment-warning.md
├── dist/
│   ├── requirements-handoff-chatgpt-skill-v1.1.0.zip
│   └── requirements-handoff-chatgpt-skill-v1.1.0.zip.sha256
└── .github/workflows/
    └── release-skill.yml
```

`SKILL.md` содержит основной workflow и триггеры ChatGPT. Supporting resources загружаются только когда нужны. GitHub Actions умеет собирать установочный ZIP для версии из `metadata.version` и публиковать его в Releases вместе с SHA-256.

## Что Skill намеренно не делает

`requirements-handoff` не является coding-agent, архитектурным агентом или implementation planner. Он не заменяет OpenSpec или Plan Mode.

```text
Human language
      ↓
ChatGPT Skill
      ↓
Engineering requirements
      ↓
Research / Design / Plan / Code
```

## Лицензия

Проект распространяется по [MIT License](LICENSE).

---

<div align="center">

Сделано для более надёжной передачи требований из ChatGPT в разработку · MIT · [z03ps00](https://github.com/z03ps00)

</div>
