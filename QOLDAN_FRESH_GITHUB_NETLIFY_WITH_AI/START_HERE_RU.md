# QOLDAN v0.3 — НОВЫЙ GitHub + НОВЫЙ Netlify (с нуля)

**Задача:** новый публичный репозиторий, новый проект Netlify, работающий QOLDAN с двумя режимами и AI Scientific Assistant. Никаких старых папок `site`, `dist` или ручных настроек сборки.

## ШАГ 0. Проверка архива

1. Скачай `QOLDAN_FRESH_GITHUB_NETLIFY_WITH_AI.zip` и **распакуй**.
2. Внутри должны лежать файлы `netlify.toml`, `README.md`, `START_HERE_RU.md` и две папки: **`public`** и **`netlify`**.
3. В `public` должны быть `index.html`, `app.js`, `styles.css`, `qoldan-logo.webp`, `favicon.svg`.
4. В `netlify/functions` должен быть `ai.mjs`. **Сохраняй имена и расположение файлов.**
5. API-ключ **не добавляй ни в какой файл**. Если раньше отправлял ключ в чат/Telegram, старый ключ нужно отозвать и использовать новый.

## ШАГ 1. Создать НОВЫЙ репозиторий GitHub

1. Открой https://github.com/new и войди в свой аккаунт.
2. Name: например **`qoldan-launch`** (если занято, `qoldan-learning-2026`).
3. Visibility: **PUBLIC**. Это важно: прежняя ошибка `Unrecognized Git contributor` была связана с приватным репозиторием. В этом проекте секретов нет, ключ находится только в Netlify.
4. Поставь галочку **Add a README file** (будет проще клонировать через GitHub Desktop). Нажми **Create repository**.
5. Нажми зелёную кнопку **Code → Open with GitHub Desktop**, либо установи GitHub Desktop: https://desktop.github.com/ и выбери **File → Clone repository**.
6. После клонирования открой локальную папку репозитория: **Repository → Show in Finder** (macOS) / **Show in Explorer** (Windows).
7. Из распакованного ZIP скопируй **СОДЕРЖИМОЕ архива** в эту папку. Копируй `public`, `netlify`, `netlify.toml`, `README.md`, `START_HERE_RU.md`, `.gitignore` (если виден). Замени автоматически созданный README.
8. Открой GitHub Desktop → посмотри изменения → введи commit message `Initial QOLDAN v0.3 launch` → **Commit to main** → **Push origin**.
9. Открой GitHub в браузере. На главной странице репозитория должны быть **отдельно** видны папки `public/`, `netlify/` и файл `netlify.toml` — это нормально. Если есть единственная лишняя папка `QOLDAN_START_FRESH/` и всё внутри неё, значит файл скопирован уровнем глубже. Перемести **содержимое** на один уровень вверх.

> Если командой занимается Дамир, пусть он делает коммиты через **свой** GitHub-аккаунт. Для публичного репозитория Netlify не применяет ограничение private-repository deploy request policy. Не нужно покупать Pro.

## ШАГ 2. Создать НОВЫЙ проект Netlify

1. Открой https://app.netlify.com/ и войди в свой Netlify-аккаунт.
2. Выбери **Add new project → Import an existing project → GitHub** (интерфейс может называться `Import from Git`).
3. Предоставь Netlify доступ к **новому** репозиторию, если он не появляется в списке GitHub.
4. Выбери `qoldan-launch`. Проверь настройки:

| Поле | Значение |
|---|---|
| Production branch | `main` |
| Base directory | **пусто** |
| Build command | **пусто** (без `npm run build`) |
| Publish directory | **`public`** |
| Functions directory | `netlify/functions` (уже записано в `netlify.toml`) |

5. Нажми **Deploy / Deploy site**. В репозитории уже есть `public/index.html`; папку `site` Netlify искать не будет.
6. Дождись статуса **Published**. Открой новый URL `https://...netlify.app`.
7. Если нужно новое короткое имя, открой **Project configuration → Domain management** и поменяй site name (если имя свободно).

**Важно:** для полного AI-проекта нужно подключение через GitHub → Netlify; одной загрузки `public` через Netlify Drop недостаточно, поскольку серверная функция отдельно не развернётся.

## ШАГ 3. Добавить OpenRouter API-ключ БЕЗ GitHub

1. Убедись, что используешь **новый секретный ключ**, а старый, который когда-то отправлялся в чат, отозван: https://openrouter.ai/keys.
2. На Netlify открой новый проект → **Project configuration → Environment variables → Add a variable**.
3. Key / name: **`OPENROUTER_API_KEY`** (точно так, заглавными буквами).
4. Value: **твой новый ключ**. Вставь его здесь, НЕ в GitHub. Если доступен переключатель `Contains secret values`, включи его.
5. Scope: на Free-плане оставь **All scopes / Default** (функция сможет прочитать ключ). Сохрани.
6. Открой **Deploys → Trigger deploy → Deploy project** (или **Deploy site**). Это необходимо, чтобы новое значение применилось.
7. После публикации открой `https://ТВОЙ-САЙТ.netlify.app/.netlify/functions/ai` в браузере. **405 / Method not allowed — ХОРОШО**: функция существует и ждёт POST. **404 — ПЛОХО**: функция не опубликована, проверь наличие `netlify/functions/ai.mjs` в GitHub и Deploy summary Netlify.
8. Вернись на главную страницу. Explorer или Researcher → Science. В Researcher заполни короткое научное объяснение → **Check reasoning**. AI должен дать ответ. Убедись, что ответ не является имитацией / заранее написанной фразой.

Модель задана как **`openrouter/free`** — бесплатный маршрутизатор OpenRouter. У бесплатного OpenRouter есть лимиты (обычно 50 запросов в день при отсутствии покупок кредитов); он может быть занят или временно недоступен. AI здесь **дополнительный**, сама миссия работает и без него.

## ШАГ 4. Контрольный тест (на телефоне и компьютере)

- [ ] Главная страница открывается без 404, логотип виден.
- [ ] Explorer Mode позволяет пройти миссию без длинного эссе.
- [ ] Researcher Mode содержит Scientific Background, Logic Plan, расчёты и Justification.
- [ ] В основной миссии 3 Ω → перегрузка; 4 Ω → 80 минут; **6 Ω → успех**; 8 Ω → недостаточно мощности.
- [ ] Transfer challenge с **8 Ω** проходит успешно.
- [ ] Кнопка AI `Check reasoning` возвращает живой ответ через OpenRouter (после настройки API).
- [ ] Можно экспортировать анонимный отчёт.
- [ ] Сайт открывается у человека, который НЕ вошёл в GitHub или Netlify.

## Если появляется ошибка

| Сообщение | Причина / что делать |
|---|---|
| `Deploy directory 'site' does not exist` | На новом проекте НЕ должно быть `site`. Проверь, что выбран новый GitHub-репозиторий и `netlify.toml` содержит `publish = "public"`. |
| `Deploy directory 'public' does not exist` | В GitHub файлы лежат не в корне, а в лишней вложенной папке. В корне репозитория должны быть `public/` и `netlify.toml`. |
| `Unrecognized Git contributor` | Убедись, что **НОВЫЙ** репозиторий Public, а не Private; в Netlify подключён именно он. Проверь, что GitHub-аккаунт авторизован в Netlify. |
| Homepage 404 | Смотри Deploy file explorer: в `public` должен находиться `index.html`. |
| AI API 404 | Не загрузилась функция `netlify/functions/ai.mjs`; нужен деплой через GitHub, не только Drop. |
| AI API GET 405 | **Норма** — функция есть, но работает по POST. |
| AI says “not configured” / HTTP 503 | `OPENROUTER_API_KEY` отсутствует, указан неверно или изменения ещё не задеплоены. |
| AI quota / 429 | Лимит бесплатной модели OpenRouter. Подожди обновления квоты, миссия работает без ИИ. |
| AI provider / 502 | Ошибка либо перегрузка модели; перепроверь OpenRouter и повтори позже. |
| CSS / images missing | Из папки `public/` не скопированы `styles.css` или `qoldan-logo.webp`. |

## Для безопасности и заявки MIT Solve

- В коде и архиве **нет настоящего API-ключа**, и не должно быть.
- Сайт публичный, поэтому не отправляйте реальные имена, контакты, оценки или другие чувствительные данные несовершеннолетних в чат с AI.
- Сохранённые результаты находятся в `localStorage` конкретного браузера. У команды пока нет автоматической базы данных пользовательских результатов.
- Рубрика и AI feedback — формативное обучение, **не официальная оценка**. Для анализа качества AI используйте проверку учителем.
- Лимит запросов в серверной функции рассчитан только на небольшой тестовый пилот, не защищает от распределённого злоупотребления. Для большого открытого запуска потребуются более строгие лимиты.

**Готово:** в следующий раз просто меняешь файлы в `public/` или `netlify/functions/` → GitHub Desktop: Commit → Push → Netlify автоматически обновляет сайт.
