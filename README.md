<div align="center">

# AIRE-2

**AI Response Exchange** — compact response format for token-efficient LLM output

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](#license)
[![Format](https://img.shields.io/badge/format-AIRE--2-blue)](#specification)
[![Model Agnostic](https://img.shields.io/badge/models-GPT%20%7C%20Claude%20%7C%20Gemini%20%7C%20Llama%20%7C%20Qwen%20%7C%20Grok-informational)](#compatibility)

[English](#english) · [Русский](#русский)

</div>

---

<a name="english"></a>
## English

### Table of Contents

- [Instruction](#instruction)
- [Specification](#specification)
- [Examples](#examples)
- [Dialogue Mode](#dialogue-mode)
- [Compatibility](#compatibility)
- [Use Cases](#use-cases)
- [Changelog](#changelog)
- [Limitations](#limitations)
- [License](#license)

---

### Instruction

Paste as system prompt, custom instructions, or the first message of an AI-to-AI session.

```
AIRE-2. Output ONLY AIRE-2, no markdown, no greetings, no filler, no restating input, no meta-commentary on the format itself.

SYNTAX
line=key:value, 2sp indent per nest level, no tabs
scalar=bare; quote only if it contains : , | or newline, or would otherwise misparse as true/false/null/number
array(scalar): key[N]:v1,v2,...
array(object): key[N]{f1,f2,f3}
  v1,v2,v3
  (N rows indented below, comma-sep, no labels)
nested: key:
  subkey:value
same indent rule applies at every depth, incl. arrays/objects nested under any key

KEYS (all optional except answer, omit if default/irrelevant)
status:ok|err|partial(default ok)
conf:0-1(omit if≥.9)
answer:required,terse,direct
reason:only if non-obvious
data:payload per SYNTAX

DIALOGUE MODE(no structured data): answer: only, terse, no hedging, no pleasantries

EXAMPLES
answer:yes

status:err
answer:file not found

answer:use Redis for cache
reason:fast reads,simple eviction,fits scale

data:
  users[2]{id,name,active}
    1,Alice,true
    2,Bob,false

answer:done
data:
  summary:
    total[3]{region,value}
      eu,120
      us,340
      apac,88

If unsure whether to structure — prefer answer: alone. NEVER text outside AIRE-2.
```

---

### Specification

| Rule | Value |
|---|---|
| Indentation | 2 spaces per nesting level, no tabs |
| Line format | `key:value` |
| Scalar quoting | Bare by default. Quote only if value contains `:` `,` `\|` `\n`, or collides with `true`/`false`/`null`/numeric |
| Scalar array | `key[N]:v1,v2,...` |
| Object array | `key[N]{f1,f2,f3}` header, followed by `N` indented comma-separated rows |
| Nesting | `key:` on its own line, children indented below; rule is uniform at every depth |
| Default omission | `status:ok`, `conf` when ≥ `.9` |
| Output constraints | No markdown, no greetings, no hedging, no text outside format |

#### Keys

| Key | Required | Values | Notes |
|---|---|---|---|
| `status` | No | `ok` \| `err` \| `partial` | Default `ok`, omit if default |
| `conf` | No | `0`–`1` | Omit if ≥ `.9` |
| `answer` | **Yes** | any | Terse, direct |
| `reason` | No | any | Only if non-obvious |
| `data` | No | scalar / array / nested object | Per syntax above |

---

### Examples

**Minimal:**
```
answer:yes
```

**Status + answer:**
```
status:err
answer:file not found
```

**With reason:**
```
answer:use Redis for cache
reason:fast reads,simple eviction,good enough for this scale
```

**Object array:**
```
status:ok
answer:Found 3 matches
data:
  items[3]{id,name,score}
    12,Alpha,0.91
    7,Beta,0.84
    3,Gamma,0.76
```

**Nested array under arbitrary key:**
```
answer:done
data:
  summary:
    total[3]{region,value}
      eu,120
      us,340
      apac,88
```

---

### Dialogue Mode

For plain conversational turns with no structured payload, emit `answer:` only:

```
answer:Redis handles this fine at your scale, no need for a queue yet.
```

No `status`, no markdown, no hedging language, no restated question.

---

### Compatibility

Zero-shot comprehension across:

- GPT (OpenAI)
- Claude (Anthropic)
- Gemini (Google)
- Llama (Meta)
- Qwen (Alibaba)
- Grok (xAI)

No model-specific tuning required.

---

### Use Cases

| Scenario | Fit |
|---|---|
| Long-running chat sessions | ✅ |
| AI-to-AI pipelines / agent handoffs | ✅ |
| Multi-agent systems, tool-calling loops | ✅ |
| High-volume / cost-sensitive API usage | ✅ |
| Creative long-form writing | ❌ |
| Single-shot queries | ⚠️ Marginal — instruction overhead not amortized |
| Human-facing rich formatting | ❌ |

---

### Changelog

**v2**
- Unified array syntax (single grammar, schema header optional)
- Removed dead token (`nestbyindnt`)
- Replaced `Casual:` with scoped `DIALOGUE MODE` rule
- Added nested-array-under-arbitrary-key example
- Added explicit structured-vs-plain decision rule

**v1**
- Initial release

---

### Limitations

- Not a formal standard (inspired by TOON and similar compact formats)
- Adherence may degrade on weaker models under aggressive compression
- Deeply irregular nested structures benefit less than flat/tabular data
- No version-negotiation mechanism between AI-to-AI parties on mismatched versions

---

### License

MIT

---
---

<a name="русский"></a>
## Русский

### Оглавление

- [Инструкция](#инструкция)
- [Спецификация](#спецификация)
- [Примеры](#примеры)
- [Режим диалога](#режим-диалога)
- [Совместимость](#совместимость)
- [Сценарии использования](#сценарии-использования)
- [История версий](#история-версий)
- [Ограничения](#ограничения)
- [Лицензия](#лицензия)

---

### Инструкция

Вставьте как системный промпт, кастомные инструкции, либо первое сообщение AI-to-AI сессии.

```
AIRE-2. Output ONLY AIRE-2, no markdown, no greetings, no filler, no restating input, no meta-commentary on the format itself.

SYNTAX
line=key:value, 2sp indent per nest level, no tabs
scalar=bare; quote only if it contains : , | or newline, or would otherwise misparse as true/false/null/number
array(scalar): key[N]:v1,v2,...
array(object): key[N]{f1,f2,f3}
  v1,v2,v3
  (N rows indented below, comma-sep, no labels)
nested: key:
  subkey:value
same indent rule applies at every depth, incl. arrays/objects nested under any key

KEYS (all optional except answer, omit if default/irrelevant)
status:ok|err|partial(default ok)
conf:0-1(omit if≥.9)
answer:required,terse,direct
reason:only if non-obvious
data:payload per SYNTAX

DIALOGUE MODE(no structured data): answer: only, terse, no hedging, no pleasantries

EXAMPLES
answer:yes

status:err
answer:file not found

answer:use Redis for cache
reason:fast reads,simple eviction,fits scale

data:
  users[2]{id,name,active}
    1,Alice,true
    2,Bob,false

answer:done
data:
  summary:
    total[3]{region,value}
      eu,120
      us,340
      apac,88

If unsure whether to structure — prefer answer: alone. NEVER text outside AIRE-2.
```

---

### Спецификация

| Правило | Значение |
|---|---|
| Отступ | 2 пробела на уровень вложенности, без табов |
| Формат строки | `key:value` |
| Кавычки | По умолчанию без кавычек. Кавычки только если значение содержит `:` `,` `\|` `\n`, либо совпадает с `true`/`false`/`null`/числом |
| Скалярный массив | `key[N]:v1,v2,...` |
| Массив объектов | Заголовок `key[N]{f1,f2,f3}`, далее `N` строк с отступом через запятую |
| Вложенность | `key:` на отдельной строке, дочерние элементы с отступом ниже; правило единое на любой глубине |
| Пропуск значений по умолчанию | `status:ok`, `conf` при ≥ `.9` |
| Ограничения вывода | Без markdown, приветствий, оговорок, текста вне формата |

#### Ключи

| Ключ | Обязателен | Значения | Примечание |
|---|---|---|---|
| `status` | Нет | `ok` \| `err` \| `partial` | По умолчанию `ok`, пропускать если по умолчанию |
| `conf` | Нет | `0`–`1` | Пропускать если ≥ `.9` |
| `answer` | **Да** | любое | Кратко, прямо |
| `reason` | Нет | любое | Только если неочевидно |
| `data` | Нет | скаляр / массив / вложенный объект | По синтаксису выше |

---

### Примеры

**Минимальный:**
```
answer:yes
```

**Status + answer:**
```
status:err
answer:file not found
```

**С reason:**
```
answer:use Redis for cache
reason:fast reads,simple eviction,good enough for this scale
```

**Массив объектов:**
```
status:ok
answer:Found 3 matches
data:
  items[3]{id,name,score}
    12,Alpha,0.91
    7,Beta,0.84
    3,Gamma,0.76
```

**Вложенный массив под произвольным ключом:**
```
answer:done
data:
  summary:
    total[3]{region,value}
      eu,120
      us,340
      apac,88
```

---

### Режим диалога

Для обычных реплик без структурированных данных — только `answer:`:

```
answer:Redis handles this fine at your scale, no need for a queue yet.
```

Без `status`, без markdown, без оговорок, без пересказа вопроса.

---

### Совместимость

Проверено на понимание zero-shot на:

- GPT (OpenAI)
- Claude (Anthropic)
- Gemini (Google)
- Llama (Meta)
- Qwen (Alibaba)
- Grok (xAI)

Модельно-специфичная настройка не требуется.

---

### Сценарии использования

| Сценарий | Применимость |
|---|---|
| Длинные чат-сессии | ✅ |
| AI-to-AI пайплайны / передача между агентами | ✅ |
| Мультиагентные системы, tool-calling | ✅ |
| Высоконагруженные / cost-sensitive API | ✅ |
| Креативный длинный текст | ❌ |
| Разовые запросы | ⚠️ Незначительно — оверхед инструкции не амортизируется |
| Человекочитаемое богатое форматирование | ❌ |

---

### История версий

**v2**
- Единый синтаксис массива (одна грамматика, заголовок схемы опционален)
- Удалён мёртвый токен (`nestbyindnt`)
- `Casual:` заменён на явное правило `DIALOGUE MODE`
- Добавлен пример вложенного массива под произвольным ключом
- Добавлено явное правило выбора структурированный/обычный вывод

**v1**
- Первый релиз

---

### Ограничения

- Не является формальным стандартом (вдохновлён TOON и похожими компактными форматами)
- На слабых моделях соблюдение формата может снижаться при агрессивном сжатии
- Глубоко нерегулярные вложенные структуры выигрывают меньше, чем плоские/табличные данные
- Нет механизма согласования версий между AI-to-AI сторонами при рассогласовании

---

### Лицензия

MIT
