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

Чтобы использовать локальный сервер для обработки запросов:

1. [Установите ChatMock](https://github.com/RayBytes/ChatMock).
2. Залогиньтесь:
   ```bash
   python chatmock.py login
   ```

Запустите сервер:

```bash
# если используете локальную репу
python chatmock.py serve --port 8000

# если установлен через Homebrew/pip
chatmock serve --port 8000
```

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

### Философия

**Total Open Codex** — это не просто CLI-агент, а прототип новой парадигмы, которую мы называем **LLMVOS (LLM-based Virtual Operating System)**.  
В LLMVOS роли распределены так:

- **User Space** → языковая модель (LLM), которая может работать как в облаке (OpenAI, Gemini, OpenRouter), так и локально (Ollama, vLLM).  
- **Kernel** → `AgentLoop`, который принимает tool calls от LLM и решает, что с ними делать: выполнить автоматически, запросить подтверждение или отклонить.  
- **Host System** → реальное железо пользователя: файловая система, shell, контейнеры, сеть.

Таким образом, **TotalCodex** превращает ваш компьютер в гибридную ОС нового типа:  
распределённую, модульную и адаптивную. Она может быть децентрализованной (с облачными LLM) или полностью локальной (с личными моделями).  
Главное — интуитивное и интерактивное взаимодействие, где LLM становится приложением-мозгом, а AgentLoop — ядром этой виртуальной ОС.

---

## Итог

**Total Open Codex** — это не просто форк.
Это универсальный агент, который:

* работает где угодно,
* поддерживает всё подряд,
* и превращает твой терминал в **умного напарника по кодингу**. 🚀
