# Anthosphere Projects Network — TZ v8

**Repository:** `TonyParf/anthosphere-network`
**Domain:** network.anthosphere.com
**Version:** v8
**Updated:** April 2026 (active development)
**Stack:** PHP 8.x + MySQL 8, no framework, PDO, sessions
**Hosting:** DirectAdmin (manual file upload, no git/CI)

---

## Authorship & License

**Author / Architect:** Tony Parf (Anton Parf)
**AI co-author:** Claude (Anthropic)
**First public commit:** April 2026
**License:** [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)

You are free to share and adapt this work, including for commercial purposes,
**provided you give appropriate credit** to Tony Parf and the Anthosphere
project, link to this repository, and indicate if changes were made.

**Filiation:** This document is the engineering specification of a system
implementing the **Grand Axiom** and the **17 Foundations** as formulated in
*Architect of Reality* (Tony Parf, 2025).

- Book repository: [`TonyParf/architect-of-reality`](https://github.com/TonyParf/architect-of-reality)
- Theoretical layer: Grand Axiom + 17 Foundations + 5 Domains
- Engineering layer (this document): scoring, moderation, AI-consensus, claim contract, point ledger

The axiom is not decorative. It is mathematically expressed in the points
formula (`× LIS × FAS`) and structurally embedded in the database schema
(`project_foundations`, domain scores, alignment scales).

---

## Філософія і місія

### Grand Axiom

> Life is the irreducible value of any sustainable system.

Будь-який проект, дія, рішення в мережі оцінюється за тим, наскільки воно служить життю — людському, біологічному, культурному, екологічному. Це не моральна декорація, а математично виражений principal в формулі балів.

### Призначення мережі

Anthosphere Projects Network — це **децентралізована мережа life-aligned проєктів**, де:

- Автори подають проєкти що працюють на користь життя
- Будівники беруть задачі з цих проєктів і отримують бали
- Усе оцінюється спільно: AI (Claude та інші) + спільнота (модератори)
- Бали відображають реальний вплив, а не самопіар
- Найкращі проєкти підіймаються нагору органічно — за фактичну корисність

### Не є

- Не Upwork (бали ≠ гроші, не біржа фрілансу)
- Не Reddit (модерація змістовна, не голосування)
- Не Open Source Catalog (це активна мережа дій, а не каталог)
- Не Crowdfunding (хоча `/post-submit/{id}` пропонує помічники для збору)

---

## 17 Foundations

Усі проєкти оцінюються по 17 фундаментах (плюс 5 доменах для зведення):

**Domains (5):** Ecology, Energy, Psychology, Peace, Tech

**Foundations (17):**
1. Biological diversity
2. Ecosystem health
3. Climate stability
4. Human dignity
5. Bodily integrity
6. Material sufficiency
7. Knowledge access
8. Civic participation
9. Cultural continuity
10. Emotional wellbeing
11. Conflict resolution
12. AI alignment with life
13. Cultural diversity
14. Education
15. Children's rights
16. Future generations
17. Memory + intergenerational wisdom

Claude під час аудиту проставляє score 0-100 по кожному з 5 доменів і виявляє "weak foundations" — те, чого проєкту бракує.

---

## Roles

| Role | Опис |
|------|------|
| `member` | Базовий — автор проєктів і будівник задач |
| `community_mod` | Модератор-волонтер, апрувить проєкти/задачі |
| `senior_mod` | Призначений Anthropic-довірою, розглядає flagged |
| `admin` | Анти-бан, full access (поки тільки для DEV — Тоні) |

`mod_level`: для community_mod = 1-5 за accuracy. Senior має level=10.

`mod_points_total` — поточні бали за модерацію. Community_mod з низьким accuracy втрачає роль.

`flag_credits` — звичайний юзер може флагати проєкти, обмежено кредитами на місяць.

---

## Архітектура файлів

```
/public_html/
  ├── config/
  │   ├── app.php              ← константи, helpers, calculatePoints
  │   ├── design.php           ← CSS змінні
  │   └── credentials.php      ← (не в репо!) DB + API keys
  ├── includes/
  │   ├── head.php             ← <head> + GA4
  │   ├── nav.php              ← навігація
  │   ├── footer.php           ← Grand Axiom
  │   ├── debug.php            ← DEV панель внизу
  │   ├── auth.php             ← сесії, ролі, CSRF
  │   ├── db.php               ← PDO + helpers (db_row, db_all, ...)
  │   ├── ai/
  │   │   ├── AIProvider.php   ← інтерфейс
  │   │   ├── AIConsensus.php  ← Singleton, стратегії
  │   │   ├── ClaudeProvider.php  ← активний
  │   │   ├── GPTProvider.php  ← заглушка
  │   │   └── GeminiProvider.php  ← заглушка
  │   └── memory/
  │       └── NetworkMemory.php  ← клієнт до Python (Крок E)
  ├── pages/                   ← сторінки сайту
  ├── api/                     ← endpoints (POST only)
  ├── logs/                    ← error.log + audit.log
  ├── index.php                ← роутер
  └── .htaccess
```

> `config/credentials.php` зберігається лише на сервері і не публікується в
> цьому репозиторії. Структура файлу описана у документації для розробника
> окремо.

---

## Маршрути (детально в ROUTES.md)

**Публічні:** `/`, `/projects`, `/projects/{id}`, `/tasks`, `/tasks/{id}/take`, `/tasks/{id}/result`, `/leaderboard`, `/commons`, `/login`, `/register`

**З авторизацією:** `/profile`, `/profile/{id}`, `/profile/prefs`, `/submit`, `/onboarding`, `/post-submit/{id}`, `/projects/{id}/edit`, `/logout`

**Admin (`/admin`):** `index` (dashboard), `gen` (DEV генератор), `projects` (черга проектів), `eval` (черга submissions), `tasks` (черга AI-задач), `flagged` (Senior), `moderators`, `memory`, `ai-settings`

**API (POST only):** `/api/audit`, `/api/projects/submit`, `/api/tasks/take`, `/api/tasks/claim`, `/api/tasks/generate`, `/api/evaluate`, `/api/moderation/{approve|sandbox|reject|flag|pass|fail}`, `/api/auth/{login|register}`, `/api/onboarding/save`, `/api/memory/{save|search}`, `/api/spam-report`

---

## База даних

**17 таблиць** (всі InnoDB, utf8mb4_unicode_ci):

### Користувачі
- `members` — основна таблиця: name, email, password_hash, bio, avatar_url, points_total, points_this_month, role, mod_level, mod_points_total, flag_credits, status, created_at
- `member_skills` — skill_tag, source ('user'|'auto'), level
- `member_preferences` — dynamic_score, archetype, schedule, regions[], focus[], notifications, vis з онбордингу
- `member_login_attempts` — rate limiting

### Проєкти
- `projects` — id, author_id, title, tagline, description, type, stage, status, audit_score, audit_json, lis_scale, lis_multiplier, fas_multiplier, video_url, links_json, open_source, sandbox_note, sandbox_count, flagged_by, flagged_reason, moderation_note, points_*, domain_eco/energy/psych/peace/tech, created_at
- `project_foundations` — many-to-many для 17 фундаментів

### Задачі та виконання
- `tasks` — id, project_id, title, description, instructions (JSON), type, result_type, **capacity** (`single`|`parallel`), status (open/taken/completed/pending_moderation), points_reward, fas_multiplier, ai_generated
- `task_skills` — skill_tag для задачі (привʼязка до member_skills)
- `task_submissions` — id, task_id, member_id, result_link/text/number, comment (≥80 chars), tool_used, **was_claimed**, status (pending_review/ai_evaluated/passed/failed), ai_score, ai_verdict, ai_improvement_note, points_awarded, attempt, parent_submission_id (resubmit chain)
- **`task_claims`** — soft-контракт: id, task_id, member_id, claimed_at, expires_at, released_at, status (active/submitted/expired/released)

### Бали і нагороди
- `points_log` — кожне нарахування: base_reward, ai_score_pct, lis_multiplier, fas_multiplier, points_total, created_at

### AI і memory
- `ai_settings` — provider, enabled, strategy, weight, model_name
- `ai_audit_log` — кожен виклик AI з токенами і tier

### Модерація
- `moderation_actions` — історія дій
- `flag_reports` — для не-модераторів

### VIEW (для статистики)
- `v_open_tasks` — швидкий каталог
- `v_leaderboard` — топ будівників
- `v_project_stats` — для admin

---

## Формула балів

```
Points = base × (ai_score / 100) × LIS × FAS
```

### Пороги AI-score

| AI Score | Множник | Поведінка |
|----------|---------|-----------|
| 0-49% | × 0 | Submission failed, 0 балів |
| 50-79% | × 0.5 | Половина балів |
| 80-100% | × 1.0 | Повні бали |

### LIS — Life Impact Scale (масштаб впливу)

| Scale | Multiplier | Опис |
|-------|------------|------|
| `local` | × 1.0 | Локальна спільнота, окремі люди |
| `regional` | × 1.6 | Регіон, кілька міст |
| `global` | × 2.0 | Системний/планетарний вплив |

LIS встановлюється Claude під час аудиту, переглядається модератором.

### FAS — Foundations Alignment Scale

| FAS | Опис |
|-----|------|
| × 0.8 | Слабка узгодженість з фундаментами |
| × 1.0 | Базова |
| × 1.3 | Сильна — кілька доменів |
| × 1.5 | Виключна — вирівняна по 17 фундаментах |

---

## Ключові потоки

### 1. Submit Project

```
/submit (3 кроки)
  Step 1: Form (title, tagline, desc≥100, type, stage, video, links)
  Step 2: Claude audit — отримуємо score, foundations, LIS suggestion,
          hidden_strength, critical_gap, рекомендації
  Step 2 (продовження): "Add this fix" додає текст у description
       → score "застарів" → блокує перехід далі
       → ОБОВ'ЯЗКОВО: Re-run Audit для оновлення
  Step 3: Confirm & Publish (preview + кнопка submit)
  ↓
projects.status = submitted
  ↓
/admin/projects → Approve → published
```

### 2. Generate Tasks (для published проєкту)

```
/admin/projects → "Auto-generate tasks" checkbox при approve
  ↓
api/tasks/generate → Claude generateTasks (5-7 задач)
  ↓
tasks.status = pending_moderation
  ↓
/admin/tasks → Approve → tasks.status = open
  ↓
Видно в /tasks каталозі
```

### 3. Claim → Take → Submit

```
/tasks → /tasks/{id}/take
  ↓
(опційно) Claim 72h
  - max 10 active claims на юзера одночасно
  - кілька юзерів можуть клеймити паралельно (soft contract)
  - інші бачать "Claimed by @X · 48h left"
  - lazy cleanup протермінованих при кожному звертанні
  ↓
Submit: result + comment≥80 chars + tool_used (опційно)
  ↓
task_submissions.status = pending_review
  was_claimed = 1 якщо був active claim
  ↓
Якщо це перший submission → tasks.status = open → taken
```

### 4. Evaluate → Pass / Fail

```
/admin/eval → "Send to Claude" → /api/evaluate
  ↓
ai_score, ai_verdict, ai_improvement_note → ai_evaluated
  ↓
/admin/eval → "Confirm Passed" → /api/moderation/pass
  - submission.status = passed
  - points_awarded = base × (ai_score/100) × LIS × FAS
  - INSERT в points_log
  - members.points_total += points_awarded
  - members.points_this_month += points_awarded
  - INSERT IGNORE в member_skills (auto) для skill_tags задачі
  - Single: tasks.status = completed
  - Parallel: tasks.status залишається taken (приймає ще)
  - +3 mod_points модератору
  ↓
АБО
  ↓
/admin/eval → "Reject as Failed" → /api/moderation/fail
  - submission.status = failed, points = 0
  - Single: якщо нема інших активних submissions → tasks.status = open (resubmit)
  - Parallel: нічого не міняємо
  - +3 mod_points модератору
  - Builder може зробити resubmit (новий attempt, parent_submission_id)
```

### 5. Resubmit

Якщо submission був failed — builder повертається на `/tasks/{id}/take`, бачить banner "Attempt N", форма preпопульована попереднім результатом, нова submission має `parent_submission_id` старої. Цикл нескінченний.

---

## Рішення архітектури сесії

### Soft-контракт claim (Варіант 4)

**Відхилено:** жорсткий лок (перший submit закриває для всіх) — гальмує мережу, перший "тяп-ляп" блокує кращих.

**Прийнято:** claim як соціальний контракт.
- Claim 72 години, max 10 active на юзера
- Інші БАЧАТЬ хто клеймив, але ТЕХНІЧНО можуть здавати
- `was_claimed=1` дає пріоритет у модератора
- Параллельні задачі: claim теж є, тільки як індикатор "in progress"

### Автор може здавати свої задачі

**Прибрано** заборону "автор не може брати свої задачі":
- Claude оцінює об'єктивно
- Модератор все одно перевіряє
- Автор знає проєкт найкраще
- Маніпуляція лідербордом неможлива (бали обмежені на проєкт, не зведено по власних)

### Модератор НЕ може модерувати свій проєкт

Залишається — реальний конфлікт інтересів. У `/admin/projects`, `/admin/eval`, `/admin/tasks` запит має `WHERE p.author_id != $me_id`. Admin (Тоні) бачить все для DEV.

### Re-audit обов'язковий після AI fixes

В `pages/submit.php`: коли юзер натискає "Add this fix", JS блокує "Continue to Publish" і показує "Re-audit required". `goStep3()` і `submitProject()` мають guard. Можливість обходу через DevTools нейтралізована подвійною перевіркою (UI + JS на submit).

---

## AI Architecture

### Провайдери

```php
interface AIProvider {
    public function audit(array $project): array;
    public function generateTasks(array $project, ?int $count): array;
    public function evaluate(array $task, array $submission): array;
}
```

**Активний:** ClaudeProvider (claude-sonnet-4-6)
**Заглушки:** GPTProvider, GeminiProvider (будуть в Кроці C продовження)

### Consensus

`AIConsensus` — Singleton що читає `ai_settings`. Стратегії:
- `single` — один провайдер
- `average` — середнє score (для audit/evaluate)
- `weighted` — з вагами по провайдеру
- `majority` — більшість

Для генерації задач — завжди один провайдер (немає сенсу мерджити списки).

### Claude API параметри

| Метод | max_tokens | Чому |
|-------|------------|------|
| `audit` | 4000 | 17 фундаментів × оцінки + рекомендації |
| `generateTasks` | 6000 | 5-7 задач × інструкції українською (~3× токенів) |
| `evaluate` | 1500 | verdict + improvement_note |

Curl timeout: 120с. PHP `max_execution_time` має бути ≥180с (DirectAdmin → PHP Settings).

При `stop_reason=max_tokens` — кидаємо зрозумілу помилку, не пробуємо парсити обірваний JSON.

---

## Дизайн

- Палітра: gold accent `#e6db88` (--teal), dark bg, мінімалізм
- Шрифти: **Oxanium** (heading), **IBM Plex Mono** (mono/labels), **Crimson Pro** (body italics)
- Цільовий екран: MacBook Air 13"
- Без зайвих градієнтів, статусні кольори: teal/gold/violet/red/green
- Усі сторінки використовують CSS змінні з `config/design.php`

---

## Безпека

- CSRF токен на кожну форму, перевіряється в API через `hash_equals`
- Сесійні куки httpOnly, secure
- Rate limiting в `member_login_attempts`
- Захист від конфлікту інтересів: `if (!isAdmin() && project.author_id == me_id) → 403`
- SQL injection: всі запити параметризовані PDO
- XSS: helper `e()` всюди в шаблонах

---

## Що готово (Квітень 2026)

```
✅ Auth: register / login / logout / onboarding
✅ Projects: submit (з re-audit guard), каталог, view, edit
✅ Tasks: генерація (admin/gen), каталог, take, claim/release, result, resubmit
✅ Profile: реальний з БД, Impact Spectrum, Skills, 4 tabs
✅ Admin: dashboard, gen, projects queue, eval queue
✅ API: audit, projects/submit, tasks/take/claim/generate, evaluate,
       moderation/{approve,sandbox,reject,flag,pass,fail}
✅ Database: 17 tables + task_claims + was_claimed
✅ Cycle замкнено: submit→approve→generate→take→evaluate→pass→points
```

---

## Що залишилося

```
⬜ admin/tasks — черга AI-задач (pending_moderation → open)
⬜ admin/flagged — для Senior
⬜ admin/moderators / ai-settings / memory UI
⬜ /commons — каталог інструментів
⬜ /leaderboard з реальними даними з v_leaderboard
⬜ /post-submit/{id} з реальними даними
⬜ /profile/prefs
⬜ tasks/view (окрема сторінка)
⬜ Memory layer (Python + NetworkMemory.php)
⬜ Cron health_check.php
⬜ GPTProvider / GeminiProvider
```

---

## Тестування

DEV режим: `APP_ENV='dev'`. Тестовий юзер — Anton Parf (admin), 2 проєкти, 7 задач.

Для нормального тестування flow потрібен другий юзер (не admin) — щоб бачити різницю в обмеженнях. Зараз обхід через `isAdmin()` дозволяє все.

---

## Відомі проблеми

1. **Lazy cleanup претендує на ~10мс** на кожен запит до `/tasks/{id}/take`. Якщо база виросте — переходимо на cron.
2. **PHP `max_execution_time`** на DirectAdmin може бути 30-60с (за замовчуванням). Claude API тайм-аутить за 120с — треба підняти PHP timeout до 180с через DirectAdmin → PHP Settings, не через `php_value` в .htaccess (FastCGI ігнорує).
3. **Українські промпти** жеруть в 2-3 рази більше токенів — закладено в MAX_TOKENS.
4. **Browser HSTS cache** після оновлення Let's Encrypt — у Chrome треба очищати в `chrome://net-internals/#hsts`.

---

## Контакти

- **Архітектор:** Tony Parf (анти-бан admin)
- **AI помічник:** Claude (Anthropic)
- **Канонічний домен:** network.anthosphere.com
- **Документація:** `/docs/` на сервері + `ROUTES.md` + `TZ_v8.md`
- **Канал помилок:** `/logs/error.log`

---

## Citation

Якщо ви посилаєтесь на цю архітектуру в академічній, технічній або публічній
роботі — будь ласка, цитуйте так:

> Parf, T. (2026). *Anthosphere Projects Network — Technical Specification v8*.
> Repository: TonyParf/anthosphere-network. Filiation: Architect of Reality
> (Parf, 2025). License: CC BY 4.0.

---

*This document is the engineering ground of an axiom-aligned network. The
formula and the schema are reproducible. The axiom is the part that makes
them coherent.*
