# Total Open Codex

**Total Open Codex (TOC)** — это наш расширенный форк Open Codex CLI, который мы сделали удобным, гибким и универсальным.

Главная идея проста:

* Один агент, который запускается прямо в терминале.
* Поддержка **множества AI-провайдеров** (OpenAI, OpenRouter, Gemini, Ollama, XAI).
* Возможность работать как через API-ключи, так и полностью **локально** (без интернета).
* Поддержка **toolchains** (шелл-команды, работа с файлами, контейнеры и т. д.) даже на смартфоне в Termux.

---

## Отличия Total Open Codex от оригинала

* Расширенная поддержка провайдеров: можно легко переключаться между OpenAI, OpenRouter, Gemini и локальными моделями.
* Простые **alias-пресеты** для переключения между конфигами (`codex-openai`, `codex-openrouter` и т. д.).
* Возможность работы через **ChatMock**, чтобы запускать агента на локальном сервере и тестировать без API-ключей.
* Работает даже в **Termux на Android** — полноценный агент в кармане.

---

## Установка

```bash
git clone https://github.com/Endorpheen/open-codex.git
cd open-codex/codex-cli
npm install
npm run build
```

---

## Конфигурация

Файл конфигурации хранится в `~/.codex/config.json`.
Для удобства мы используем **несколько пресетов**:

`~/.codex/config-openai.json`

```json
{
  "provider": "openai",
  "model": "gpt-5",
  "approvalMode": "full-auto"
}
```

`~/.codex/config-openrouter.json`

```json
{
  "provider": "openrouter",
  "model": "openrouter/sonoma-sky-alpha",
  "approvalMode": "full-auto"
}
```

Алиасы в `~/.bashrc` или `~/.zshrc`:

```bash
alias codex-openai='cp ~/.codex/config-openai.json ~/.codex/config.json && open-codex'
alias codex-openrouter='cp ~/.codex/config-openrouter.json ~/.codex/config.json && open-codex'
```

---

## Работа с ChatMock

Чтобы использовать **локальный сервер** для обработки запросов:

1. Установите [ChatMock](https://github.com/openai/chatmock).
2. Запустите сервер:

   ```bash
   chatmock serve --port 8000
   ```
3. В новой сессии установите переменные окружения:

   ```bash
   export OPENAI_BASE_URL="http://127.0.0.1:8000/v1"
   export OPENAI_API_KEY="dummy_key"
   ```
4. Запустите Codex:

   ```bash
   node dist/cli.js -m gpt-5
   ```

Теперь агент будет подключаться к локальному ChatMock и использовать его как бэкенд.

---

## Примеры запуска

```bash
codex-openai
codex-openrouter
```

Или напрямую:

```bash
open-codex "создай тесты для utils/date.ts"
open-codex -m openrouter/sonoma-sky-alpha "объясни этот код"
```

---

## Поддерживаемые сценарии

* Автогенерация кода и тестов.
* Запуск shell-команд и работа с файлами.
* Использование разных LLM-провайдеров.
* Полностью оффлайн-режим через локальные модели (Ollama/DeepSeek).
* Запуск на **ПК и смартфоне**.

---

## Итог

**Total Open Codex** — это не просто форк.
Это универсальный агент, который:

* работает где угодно,
* поддерживает всё подряд,
* и превращает твой терминал в **умного напарника по кодингу**. 🚀
