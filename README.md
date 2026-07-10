# TICAP — Time Capital Allocation System

**EN below · [Русская версия ↓](#ticap--система-аллокации-временного-капитала)**

> The tracker is for time you invest. Time you live doesn't need accounting.

**Live app:** https://memloop.github.io/ticap/ · installable PWA · works offline · zero data collection · auto-detects RU/EN

---

## What it is

TICAP is not a habit tracker. It's a personal **time-capital allocation system**: a method (and a tool built around it) that treats your hours the way an investor treats capital — every invested hour either **compounds** into skill, income, or health, or it's simply spent.

Habit trackers die because they try to account for your whole life. TICAP deliberately covers only the **investment contour** (~10–15 hours a week) and leaves the rest of life alone. That boundary is the core design decision.

## Three failure modes it targets

Most people don't lack plans — they lack a mechanism that survives contact with a real week. TICAP is built against three specific failure modes, each with its own mechanic:

1. **Knowing without doing** → 30-minute checkpoints (minimal entry cost), instant reward loop (sound → bar → confetti → stats), weekly quests that translate a distant goal into "what to do before the week closes".
2. **Doing but scattering** → a strictly single Experimental slot, budgeted allocations with mandatory retros, kill criteria written before the start, a capacity reminder when you open a 4th+ active allocation.
3. **Focused but taking long breaks** → an honest week history (an empty week is a ✗, not silence) and a **pause protocol**: declared in advance, with a reason (illness / force majeure / chronic flare-up), a return date ≤14 days, once per season. Paused weeks show ⏸ — the streak waits instead of dying.

## Core concepts

**Delta Unit (DU).** `1 DU = 100 hours`, tracked in 30-minute checkpoints. *Delta* means the before→after difference: you measure what accrued, not what was spent. Scouting a new direction costs 0.1–0.2 DU; a full DU is enough data to judge a direction.

**Allocation.** A budgeted investment of time into one direction ("Master a craft · 2 DU"). Not a task and not a habit: an allocation has an estimate, a bar and a mandatory retro. The bar ripens from gold to teal as it fills. Finishing under budget is a win — close early with **✓**; a direction that stalls gets **kill**. The **×1.5 rule**: if an allocation drags 1.5× past its plan, close it — the direction is stalling.

**Three levels.** **Core** — long-term assets (skills, cash flow, infrastructure), never cut. **Experimental** — strictly one slot. **Body** — the carrier: an hour worked in pain yields 40–60% of nominal, so the carrier is serviced before the portfolio.

**Selection cycle.** Bar filled (or closed early) → a short retro: *what actually accrued?* Three outcomes — **Double** (works → next iteration is bigger), **Pivot** (same direction, new approach), **Kill** (end it honestly). Kill is a routine selection operation, not a failure.

**Yearly capacity math.** At 12–15 h/week the year holds ~6–8 DU gross. Cross-season Core (language, body, cash flow) eats about half of it continuously — **2–3 DU remain for new directions**. That's why the scarce resource is slots, not hours.

**Seasons.** A 30/60/90-day run with **one binary goal** (verifiable fact + number + deadline — a stranger must be able to say yes/no at the end). Weeks run **from the start date** (start on Thursday → weeks close every Thursday, automatically). The season plan is tracks with weekly quotas, grouped by level: **Season goal / Core / Experimental / Body** — each track is a quest; the week is won when **all quests + the outgoing-actions quota** are closed. *Outgoing* = touches of the outer world where rejection is possible (applications, pitches, publications). Closed quotas slide into a collapsible archive with a one-line micro-retro; consecutive won weeks build a streak. A track can be bound to an allocation: one +30 tap feeds both layers, and when the bound allocation fills, its retro opens right inside the season view.

## Features

- **Single-file PWA** — the entire app is one `index.html`: no build step, no framework, zero dependencies. Installable, offline-first.
- **Privacy by design** — no server, no accounts, no analytics. Data lives in `localStorage` on your device only; backup is a JSON file you export wherever you want.
- **RU/EN auto-detection** by system language + manual switch; **dark / light** themes (deep parchment-and-bronze light mode).
- **Synthesized sound** (Web Audio, zero audio files): checkpoints are a formant-synthesized vocal "yeah!" that rises in pitch with the bar — a duet past 60%, a trio past 85%; completion resolves in a full IV→V→I piano cadence with convolution reverb; kill gets a low descending tone. Mutable.
- **Canvas confetti** on completed bars and weekly quests.
- **Drag & drop everywhere** — cards within blocks and the blocks themselves (allocations by level, season tracks by level), with edge auto-scroll, built on raw pointer events.
- **Motion system** — FLIP-animated progress bars, one-time card entries, spring toasts; respects `prefers-reduced-motion`.
- **PWA-safe confirmations** — destructive actions use two-tap arming instead of native dialogs (which installed PWAs may silently suppress).
- **Onboarding** — five cards on first launch, reopenable via `?`; a full system flowchart lives in the reference tab.

## Quick start

1. Open https://memloop.github.io/ticap/ on your phone.
2. Install it (browser menu → *Add to Home Screen*).
3. Pass the 5-card onboarding.
4. Open your first allocation (0.1–0.2 DU for scouting), work 30 minutes, tap **+30**.
5. Add the Season once tapping is a habit — not before.

## Architecture notes

Vanilla JS, ~1,900 lines, one file. State is a single serializable object (allocations / season / seasons archive / outgoing timestamps) persisted to `localStorage` with schema migrations on load (level system, rolling weeks, pause history all migrate old data in place). UI re-renders from state; a lightweight FLIP pass animates bar widths between renders and mounts new cards only once. i18n is a two-locale dictionary; the reference tab — including the SVG system flowchart — ships in both languages and is themed via CSS variables. Sound is synthesized per event: piano from oscillator partials with a darkening filter, the checkpoint voice from a sawtooth source through three band-pass formant filters, all through a runtime-generated convolution reverb.

## Process

Designed, specified and product-managed by **Memloop**; implemented in an iterative dialogue with **Claude** (Anthropic). Every mechanic went through real daily usage plus external testing, and the big ones were redesigned from that feedback: rolling weeks instead of calendar weeks, quest closing rules ("hours must have somewhere to accrue"), inline allocation retro in the season view, the four-level track system, the pause protocol with its anti-abuse constraints. The system itself — "Karta" — existed before the app; the app is its instrument.

---
---

# TICAP — система аллокации временного капитала

> Трекер для времени, которое ты вкладываешь. Время, которое ты живёшь, в учёте не нуждается.

**Приложение:** https://memloop.github.io/ticap/ · устанавливается как PWA · работает офлайн · ноль сбора данных · язык RU/EN определяется автоматически

## Что это

TICAP — не трекер привычек. Это личная **система аллокации временного капитала**: методология (и инструмент вокруг неё), которая относится к часам как инвестор к капиталу — каждый вложенный час либо **накапливается** в навык, доход или здоровье, либо просто потрачен.

Трекеры привычек умирают, потому что пытаются учитывать всю жизнь. TICAP сознательно покрывает только **инвестиционный контур** (~10–15 часов в неделю) и не заходит на остальную территорию. Эта граница — главное дизайн-решение системы.

## Три режима отказа, против которых построена система

Людям не не хватает планов — не хватает механизма, который переживает столкновение с реальной неделей. TICAP собран против трёх конкретных режимов отказа, у каждого своя механика:

1. **Знаю, но не делаю** → чекпоинты по 30 минут (минимальный порог входа), мгновенная петля награды (звук → шкала → салют → статистика), недельные квесты, переводящие далёкую цель в «что сделать до закрытия недели».
2. **Делаю, но распыляюсь** → строго один слот Эксперимента, аллокации со сметой и обязательным ретро, kill-критерии до старта, напоминание о ёмкости при 4+ активных аллокациях.
3. **Не распыляюсь, но беру большие паузы** → честная история недель (пустая неделя — это ✗, а не тишина) и **протокол паузы**: объявляется заранее, с причиной (болезнь / форс-мажор / обострение), датой возврата ≤14 дней, один раз за сезон. Недели паузы — ⏸: серия ждёт, а не умирает.

## Ядро системы

**Дельта-Единица (ДЕ).** `1 ДЕ = 100 часов`, учёт чекпоинтами по 30 минут. Дельта — разница «было → стало»: измеряется приращение, а не потраченное время. Разведка нового направления — 0,1–0,2 ДЕ; полная ДЕ — достаточно данных для оценки направления.

**Аллокация.** Вложение времени в одно направление с бюджетом («Освоить профессию · 2 ДЕ»). Не задача и не привычка: у аллокации есть смета, шкала и обязательное ретро. Шкала зреет от золота к бирюзе. Закрыть раньше сметы — победа (кнопка **✓**), буксующее направление — **kill**. **Правило ×1,5:** тянется в полтора раза дольше плана — закрывай, направление буксует.

**Три уровня.** **Ядро (Core)** — долгие активы: навыки, денежный поток, инфраструктура; не отсекается. **Эксперимент** — строго один слот. **Носитель** — тело: час на фоне боли даёт 40–60% номинала, поэтому носитель обслуживается до портфеля.

**Цикл отбора.** Шкала заполнилась (или закрыта досрочно) → короткое ретро: *что реально приросло?* Три исхода: **Удвоить** / **Пивот** / **Закрыть**. Kill — штатная операция отбора, не провал.

**Экономика года.** При 12–15 ч/нед год вмещает ~6–8 ДЕ валом. Сквозной Core (язык, тело, поток) постоянно съедает около половины — **на новые направления остаётся 2–3 ДЕ**. Поэтому дефицит — слоты, а не часы.

**Сезоны.** Забег на 30/60/90 дней с **одной бинарной целью** (факт + число + дедлайн — посторонний в конце скажет «да» или «нет»). Недели идут **от даты старта** (стартовал в четверг — закрываются каждый четверг, автоматически). План сезона — треки с недельными нормами по уровням: **Цель сезона / Ядро / Эксперимент / Носитель**; каждый трек — квест, неделя выиграна, когда закрыты **все квесты + норма исходящих**. *Исходящие* — касания мира, где возможен отказ: отклики, питчи, публикации. Закрытые нормы уезжают в сворачиваемый архив с микро-ретро одной строкой; выигранные недели подряд — серия. Трек можно привязать к аллокации: один тап +30 кормит оба слоя, а когда привязанная аллокация заполняется — её ретро открывается прямо в сезоне.

## Возможности

- **PWA в одном файле** — всё приложение это один `index.html`: без сборки, фреймворков и зависимостей; устанавливается, работает офлайн.
- **Privacy by design** — нет сервера, аккаунтов и аналитики. Данные живут в `localStorage` устройства; бэкап — JSON-файл, который ты сам сохраняешь куда хочешь.
- **RU/EN автоопределение** по языку системы + ручной переключатель; **тёмная / светлая** темы (светлая — глубокий пергамент с бронзой).
- **Синтезированный звук** (Web Audio, без единого аудиофайла): чекпоинт — формантный голосовой «еее!», поднимающийся с прогрессом шкалы (после 60% — дуэт, после 85% — трио); заполнение — полная фортепианная каденция IV→V→I со свёрточным ревербом; у kill — низкий нисходящий тон. Отключается.
- **Салют** на заполненных шкалах и закрытых квестах.
- **Drag-and-drop всего** — карточки внутри блоков и сами блоки, с автоскроллом у краёв, на чистых pointer events.
- **Моушен-система** — FLIP-анимация шкал, одноразовые входы карточек, пружинные тосты; уважает `prefers-reduced-motion`.
- **PWA-безопасные подтверждения** — разрушающие действия защищены двухтаповой взводкой вместо нативных диалогов (установленные PWA могут молча их глушить).
- **Онбординг** — 5 карточек при первом запуске, повторно по `?`; полная блок-схема системы — на вкладке Карта.

## Быстрый старт

1. Открой https://memloop.github.io/ticap/ на телефоне.
2. Установи (меню браузера → «Добавить на главный экран»).
3. Пройди онбординг.
4. Открой первую аллокацию (0,1–0,2 ДЕ на разведку), поработай 30 минут, нажми **+30**.
5. Сезон подключай, когда тик станет привычкой — не раньше.

## Об архитектуре

Vanilla JS, ~1900 строк, один файл. Состояние — один сериализуемый объект (аллокации / сезон / архив сезонов / метки исходящих) в `localStorage` с миграциями схемы при загрузке (уровни, скользящие недели, история пауз — старые данные мигрируют на месте). UI перерисовывается из состояния; лёгкий FLIP-проход анимирует ширины шкал между рендерами и монтирует новые карточки один раз. Локализация — словарь на два языка; справка, включая SVG-схему системы, целиком на обоих и красится переменными темы. Звук синтезируется на лету: пианино — из частичных тонов с темнеющим фильтром, голос чекпоинта — пила через три полосовых формантных фильтра, всё через свёрточный реверб, генерируемый при запуске.

## Процесс

Спроектировано и продуктово управлялось **Memloop**; реализовано в итеративном диалоге с **Claude** (Anthropic). Каждая механика прошла через реальную ежедневную эксплуатацию и внешнее тестирование; крупные были переработаны по этому фидбеку: скользящие недели вместо календарных, правило закрытия квестов («часам должно быть куда накапливаться»), встроенное ретро аллокации в сезоне, четырёхуровневая система треков, протокол паузы с защитой от злоупотребления. Сама система — «Карта» — существовала до приложения; приложение — её инструмент.
