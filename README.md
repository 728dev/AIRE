<p align="center">
  <strong>AIRE — AI Response Exchange</strong><br>
  Ultra-compact instructions for token-efficient LLM responses
</p>

<p align="center">
  <a href="#english-version">English</a> · 
  <a href="#русская-версия">Русский</a>
</p>

---

<a id="english-version"></a>

# English Version

**AIRE** provides ready-to-use instructions that can be applied as a **system prompt** or as **custom response instructions** for any modern LLM.  
The goal is to significantly reduce token usage in both structured outputs and ordinary conversation while remaining understandable by virtually any model.

---

## Instructions (copy & paste)

```text
RespONLY in AIRE.Nothing else.English only.
AIRE:2spindnt key:val noquotesunless:|,nl|true/false/null/num
unifarr name[N]{f1,f2}:row primarr name[N]:v1,v2 nestbyindnt
omitdefs(status=ok+conf≥.9)
topkeys(use needed):status:ok|err|partial conf:0-1 answer:main reason:shortopt data:payload
Casual:answer max short.reason only if valuable.no fluff/polite/markdown.
ex:status:ok
answer:40-60% on tabular,low on prose
NEVER extra text.PureAIRE only.
```

Use the block above as a **system prompt** or paste it into custom instructions / response format settings of your model.

---

## What is AIRE?

AIRE is a lightweight response format combined with highly compressed instructions. It reduces token consumption on structured data and everyday dialogue without requiring model-specific features or long explanations.

### Key Advantages

- Token savings on structured data and casual chat
- Cross-model compatible (GPT, Claude, Gemini, Llama, Qwen, Grok and others)
- Zero-shot friendly — models understand the format from the compact instruction
- Hybrid design: clean tabular data **and** short conversational answers
- Strict anti-fluff rules force concise, high-signal replies
- English-only for maximum tokenizer efficiency on most models
- Extremely short instruction block (minimal overhead)

---

## Approximate Token Savings

| Task Type                          | Typical Savings | Notes                                      |
|------------------------------------|-----------------|--------------------------------------------|
| Uniform tabular / list of objects  | **40–55%**      | Best case. Schema declared once            |
| Nested structured data             | **25–40%**      | Better than pretty JSON/YAML               |
| Mixed structured + text            | **30–45%**      | Depends on structured portion ratio        |
| Casual conversation                | **25–45%**      | Mainly from removing fluff & verbosity     |
| Pure long-form prose               | **10–25%**      | Limited gain — mostly style enforcement    |
| Average across mixed workloads     | **30–40%**      | Realistic overall expectation              |

Savings are measured against typical verbose model behavior (polite, well-formatted, explanatory answers). Against already-minimal JSON the gains are lower.

---

## Format Overview

**Minimal valid responses:**

```text
answer:yes
```

```text
status:ok
answer:Found 3 matches
data:
  items[3]{id,name,score}:
    12,Alpha,0.91
    7,Beta,0.84
    3,Gamma,0.76
```

```text
answer:use Redis for cache
reason:fast reads,simple eviction,good enough for this scale
```

### Core Rules

- 2-space indentation
- `key: value`
- Uniform arrays of objects use the compact tabular form
- Omit default fields (`status: ok`, high confidence)
- No markdown, no polite phrases, no extra text outside the format
- Prefer English

---

## When to Use

**Good fit**
- Multi-agent systems
- High-volume API usage
- Tool-calling loops
- Cost-sensitive applications
- Forcing concise assistant behavior

**Less ideal**
- Creative long-form writing
- Cases where rich formatting or very natural tone is required

---

## Limitations

- Not a formal standard (inspired by TOON and similar formats)
- Extreme compression of the instruction can slightly reduce adherence on weaker models
- Deeply irregular nested structures benefit less than flat/tabular data
- Savings depend on how verbose the baseline model behavior is

---

## License

MIT

---

<br><br>

<p align="center">
  <strong>AIRE — AI Response Exchange</strong><br>
  Ультра-компактные инструкции для токен-эффективных ответов LLM
</p>

<p align="center">
  <a href="#english-version">English</a> · 
  <a href="#русская-версия">Русский</a>
</p>

---

<a id="русская-версия"></a>

# Русская версия

**AIRE** — готовые инструкции, которые можно использовать как **системный промпт** или как **пользовательские / кастомные инструкции для формата ответа** модели.  
Цель — существенно снизить расход токенов как на структурированных данных, так и в обычном диалоге, оставаясь понятным практически любой современной LLM.

---

## Инструкции (скопировать и вставить)

```text
RespONLY in AIRE.Nothing else.English only.
AIRE:2spindnt key:val noquotesunless:|,nl|true/false/null/num
unifarr name[N]{f1,f2}:row primarr name[N]:v1,v2 nestbyindnt
omitdefs(status=ok+conf≥.9)
topkeys(use needed):status:ok|err|partial conf:0-1 answer:main reason:shortopt data:payload
Casual:answer max short.reason only if valuable.no fluff/polite/markdown.
ex:status:ok
answer:40-60% on tabular,low on prose
NEVER extra text.PureAIRE only.
```

Используйте блок выше как **системный промпт** или вставьте его в пользовательские инструкции / настройки формата ответа вашей модели.

---

## Что такое AIRE?

AIRE — лёгкий формат ответов в сочетании с сильно сжатыми инструкциями. Снижает расход токенов на структурированных данных и в повседневном диалоге без необходимости в модельно-специфичных возможностях или длинных объяснениях.

### Основные преимущества

- Экономия токенов на структурированных данных и обычной беседе
- Кросс-модельная совместимость (GPT, Claude, Gemini, Llama, Qwen, Grok и другие)
- Работает zero-shot — модели понимают формат из компактной инструкции
- Гибридный дизайн: чистые табличные данные **и** короткие разговорные ответы
- Жёсткие правила против «воды» заставляют отвечать коротко и по делу
- Только английский — максимальная эффективность токенизаторов на большинстве моделей
- Очень короткий блок инструкций (минимальные накладные расходы)

---

## Примерная экономия токенов

| Тип задачи                              | Типичная экономия | Комментарий                                      |
|-----------------------------------------|-------------------|--------------------------------------------------|
| Однородные таблицы / списки объектов    | **40–55%**        | Лучший случай. Схема объявляется один раз        |
| Вложенные структурированные данные      | **25–40%**        | Лучше, чем pretty JSON/YAML                      |
| Смешанные структурированные + текст     | **30–45%**        | Зависит от доли структурированной части          |
| Обычная беседа                          | **25–45%**        | В основном за счёт удаления воды и многословия   |
| Чистый длинный текст                    | **10–25%**        | Ограниченный выигрыш — в основном контроль стиля |
| Среднее по смешанным нагрузкам          | **30–40%**        | Реалистичное общее ожидание                      |

Экономия считается относительно типичного многословного поведения моделей (вежливость, форматирование, развёрнутые объяснения). По сравнению с уже минимальным JSON выигрыш меньше.

---

## Обзор формата

**Минимально валидные ответы:**

```text
answer:yes
```

```text
status:ok
answer:Found 3 matches
data:
  items[3]{id,name,score}:
    12,Alpha,0.91
    7,Beta,0.84
    3,Gamma,0.76
```

```text
answer:use Redis for cache
reason:fast reads,simple eviction,good enough for this scale
```

### Основные правила

- Отступ — 2 пробела
- `key: value`
- Однородные массивы объектов используют компактную табличную форму
- Пропускать поля по умолчанию (`status: ok`, высокая уверенность)
- Без markdown, вежливых фраз и любого текста вне формата
- Предпочитать английский

---

## Когда использовать

**Хорошо подходит**
- Мульти-агентные системы
- Высоконагруженные API
- Циклы tool-calling
- Приложения, чувствительные к стоимости
- Принуждение ассистента к кратким ответам

**Менее подходит**
- Креативный длинный текст
- Случаи, где нужно богатое форматирование или очень естественный тон

---

## Ограничения

- Не является формальным стандартом (вдохновлён TOON и похожими форматами)
- Сильное сжатие инструкций может немного снижать соблюдение формата на более слабых моделях
- Глубоко нерегулярные вложенные структуры выигрывают меньше, чем плоские/табличные данные
- Экономия зависит от того, насколько многословно ведёт себя модель в обычном режиме

---

## Лицензия

MIT


<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=tzuxi728.AIRE&left_text=Repo+Views&left_color=555&right_color=0e75b6" alt="Views" />
</p>
