# Ghazal panel-ops

ابزار رسمی دیپلوی **پنل آموزشی** و **حسابداری** آموزشگاه زبان غزال.

این ریپو یک MCP نیست، یک اپلیکیشن نیست، و کد PHP پنل را هم ندارد. یک اسکریپت پایتون است که فایل‌های ادیت‌شدهٔ ریپوی خصوصی پنل را از طریق **DirectAdmin Evolution File Manager API** روی سرور زنده می‌گذارد.

اگر مدل هوش مصنوعی هستی، بخش [اگر مدل هستی، از اینجا شروع کن](#اگر-مدل-هستی-از-اینجا-شروع-کن) را اول بخوان و از FTP / FileZilla / `scp` / آپلود دستی / n8n / OpenSEO برای پنل استفاده نکن.

ریپو: [github.com/rvincenttt96/ghazal-panel-ops](https://github.com/rvincenttt96/ghazal-panel-ops)

---

## این ریپو چیست

| هست | نیست |
|---|---|
| نقشهٔ دامنه‌ها و مسیر DirectAdmin | کل کد پنل آموزشی |
| آپلود امن با overwrite | FTP / cPanel / Vercel / GitHub Actions |
| بلاک فایل‌های رمز | دیتابیس، مهاجرت SQL، کرون |
| قرارداد اجباری برای مدل‌های دیگر | پلاگین MCP |

خروجی کار مدل باید این باشد:

1. فایل را در **ریپوی خصوصی پنل** ادیت کند.
2. با `deploy.py` همان فایل را روی سرور زنده بگذارد.
3. بگوید کدام فایل روی کدام دامنه آپلود شد.

---

## اگر مدل هستی، از اینجا شروع کن

1. `INSTRUCTIONS.md` را هم بخوان. آن فایل چک‌لیست کوتاه اجباری است؛ این README راهنمای کامل است.
2. کد PHP را **اینجا** عوض نکن. اینجا فقط ابزار آپلود است. ادیت‌ها در ریپوی خصوصی پنل انجام می‌شود.
3. قبل از آپلود واقعی `--dry-run` بزن تا نگاشت مسیر را ببینی.
4. رمز DirectAdmin، دیتابیس، SMS، الوکام، Mattermost را در چت ننویس و چاپ نکن.
5. اگر دیپلوی fail شد، متن خطا را نشان بده و **به FTP سوییچ نکن**.

### متنی که صاحب پنل به مدل می‌دهد

این پاراگراف را کپی کن:

> ریپوی دیپلوی پنل غزال این است: `https://github.com/rvincenttt96/ghazal-panel-ops`
> اول `README.md` و `INSTRUCTIONS.md` را بخوان.
> کد را در ریپوی خصوصی پنل ادیت کن.
> برای گذاشتن روی سرور زنده فقط از `python3 deploy.py` استفاده کن.
> MCP لازم نیست. FTP، FileZilla، scp، n8n و OpenSEO برای پنل ممنوع است.
> Session Plan را به Term Plan تبدیل نکن. لول‌های قدیمی T / B / E / PI / I / UI / ADV را حذف نکن.
> ترم‌پلن Connectivity / Wider World فقط برای لول‌های WT و CB / CE / CPI / CI / CUI / CADV است.
> رمز DirectAdmin را در چت نگذار؛ داخل `config.json` محلی است.

---

## فایل‌های همین ریپو

```
ghazal-panel-ops/
├── README.md              ← همین فایل؛ راهنمای کامل
├── INSTRUCTIONS.md        ← چک‌لیست اجباری مدل
├── AGENTS.md              ← اشاره کوتاه برای ایجنت‌ها
├── GEMINI.md              ← اشاره کوتاه برای Gemini
├── deploy.py              ← آپلودر DirectAdmin (فقط کتابخانه استاندارد پایتون)
├── targets.json           ← دامنه، ریشهٔ سرور، لیست فایل‌های ممنوع
├── config.example.json    ← نمونه؛ رمز خالی
├── config.json            ← محلی؛ گیت نمی‌شود؛ رمز اینجاست
└── .gitignore
```

`deploy.py` به `pip` یا پکیج `requests` نیاز ندارد. پایتون ۳ با `urllib` کافی است.

---

## چهار سایت غزال (فقط دوتا با این ابزار دیپلوی می‌شوند)

| کلید در `targets.json` | دامنه | کد در ریپوی پنل | ریشه روی DirectAdmin | با این ابزار؟ |
|---|---|---|---|---|
| `panel` | `panel.ghazalify.com` | `dashboard/` `includes/` `assets/` و PHP ریشه | `domains/panel.ghazalify.com/public_html` | بله؛ پیش‌فرض |
| `accounting` | `acccounting.ghazalify.com` | `accounting/` | `domains/acccounting.ghazalify.com/public_html` | بله |
| `books` | `books.ghazalify.com` | `bookstore-shop/` | `domains/books.ghazalify.com/public_html` | فقط اگر کاربر صریح بگوید |
| — | `ghazalify.com` | `wordpress/` | وردپرس / LiteSpeed | **نه**؛ این اسکریپت رد می‌کند |

نکتهٔ املا: دامنهٔ حسابداری **سه تا c** دارد: `acccounting`. اشتباه تایپی نیست.

سئوی فنی فقط برای سایت وردپرس `ghazalify.com` است. پنل و حسابداری را سئو نکن، به وردپرس دست نزن مگر کاربر بگوید، و فایل‌های `wordpress/` را با این اسکریپت آپلود نکن.

---

## پیش‌نیاز

روی ماشین مدل / توسعه‌دهنده:

- `python3` (۳.۸ یا جدیدتر)
- دسترسی خواندن به **ریپوی خصوصی پنل** (کلون محلی)
- رمز DirectAdmin داخل `config.json` یا `includes/directadmin-config.php` ریپوی پنل
- شبکه به `https://server16e.irwebspace.com:2223`

روی سرور چیزی نصب نمی‌شود. اسکریپت با کاربر DirectAdmin `ghazali1` لاگین می‌کند و فایل را overwrite می‌کند.

DirectAdmin اینجاست: پنل Evolution، پورت `2223`، نه `:2222` کلاسیک.

---

## دو روش نصب

### روش A — داخل ریپوی خصوصی پنل (ترجیح)

این ابزار را به صورت پوشهٔ `panel-ops/` کنار `dashboard/` و `includes/` بگذار:

```text
panel-repo/
├── dashboard/
├── includes/
├── assets/
├── accounting/
├── bookstore-shop/
└── panel-ops/          ← کلون همین ریپو
    ├── deploy.py
    ├── targets.json
    └── config.json     ← ساختهٔ تو؛ گیت نمی‌شود
```

```bash
cd /path/to/panel-repo
git clone https://github.com/rvincenttt96/ghazal-panel-ops.git panel-ops
cp panel-ops/config.example.json panel-ops/config.json
# فقط password را در config.json پر کن
python3 panel-ops/deploy.py --targets
```

### روش B — کلون جدا با `--root`

اگر این ریپو را جدا کلون کرده‌ای، ریشهٔ ریپوی پنل را بده:

```bash
git clone https://github.com/rvincenttt96/ghazal-panel-ops.git
cd ghazal-panel-ops
cp config.example.json config.json
# password را پر کن

python3 deploy.py --root /path/to/panel-repo --dry-run includes/term-plan.php
python3 deploy.py --root /path/to/panel-repo includes/term-plan.php
```

معادل متغیر محیطی:

```bash
export PANEL_ROOT=/path/to/panel-repo
python3 deploy.py includes/term-plan.php
```

اگر `deploy.py` داخل پوشه‌ای به نام `panel-ops` باشد و والدش `dashboard/` یا `includes/` داشته باشد، `--root` لازم نیست؛ والد همان ریشهٔ پنل فرض می‌شود.

---

## تنظیم رمز

`config.example.json` را کپی کن، نه ادیت مستقیم نمونه:

```json
{
  "url": "https://server16e.irwebspace.com:2223",
  "username": "ghazali1",
  "password": ""
}
```

فقط فیلد `password` را پر کن. این فایل `config.json` می‌شود و در `.gitignore` است.

اولویت خواندن رمز:

1. `config.json` کنار `deploy.py` (یا `panel-ops/config.json`)
2. `includes/directadmin-config.php` داخل ریپوی پنل (اگر آن فایل محلی وجود داشته باشد)

اگر هیچ‌کدام رمز نداشت، اسکریپت خارج می‌شود و می‌گوید `config.example.json` را کپی کن. **رمز را از کاربر در چت Repeat نکن.**

هرگز این‌ها را commit نکن:

- `config.json`
- `includes/directadmin-config.php`
- `includes/rollcall-config.php`
- هر `*-secret.php`
- `accounting/config.php`
- `accounting/identity-config.php`
- `accounting/bookstore-config.php`

---

## مرجع دستورات

همهٔ مسیرهای فایل نسبت به **ریشهٔ ریپوی پنل** هستند، نه نسبت به این ریپو.

```bash
# ببین اسکریپت سه سایت را چطور می‌شناسد
python3 deploy.py --targets

# فقط نگاشت؛ هیچ آپلودی نمی‌شود
python3 deploy.py --dry-run includes/term-plan.php
python3 deploy.py --dry-run accounting/api.php assets/js/term-plan.js

# آپلود واقعی + دانلود برای چک
python3 deploy.py includes/term-plan.php
python3 deploy.py dashboard/teacher/term-plan.php dashboard/teacher/ajax-term-plan.php

# چند فایل با هم
python3 deploy.py \
  includes/term-plan.php \
  includes/term-plan-tracks.php \
  assets/js/term-plan.js \
  assets/css/term-plan.css
```

اگر اسکریپت داخل `panel-ops/` ریپوی پنل است، به‌جای `python3 deploy.py` بنویس `python3 panel-ops/deploy.py`.

خروجی موفق شبیه این است:

```text
Mapped:
  includes/term-plan.php
    → panel.ghazalify.com  domains/panel.ghazalify.com/public_html/includes/term-plan.php
OK   includes/term-plan.php  HTTP 204  remote=12345b  match=True
```

کد آپلود موفق DirectAdmin معمولاً `204` است؛ `200` هم قبول است.

---

## نگاشت مسیر فایل

منطق داخل `deploy.py` → `map_remote()`:

| مسیر محلی در ریپوی پنل | سایت | مسیر روی DirectAdmin |
|---|---|---|
| `includes/term-plan.php` | پنل | `domains/panel.ghazalify.com/public_html/includes/term-plan.php` |
| `dashboard/teacher/term-plan.php` | پنل | `.../public_html/dashboard/teacher/term-plan.php` |
| `dashboard/supervisor/ajax-term-plan.php` | پنل | `.../public_html/dashboard/supervisor/ajax-term-plan.php` |
| `assets/js/term-plan.js` | پنل | `.../public_html/assets/js/term-plan.js` |
| `index.php` | پنل | `.../public_html/index.php` |
| `accounting/index.php` | حسابداری | `domains/acccounting.ghazalify.com/public_html/index.php` |
| `accounting/api.php` | حسابداری | `domains/acccounting.ghazalify.com/public_html/api/api.php` |
| `accounting/login.css` | حسابداری | `.../public_html/login.css` |
| `bookstore-shop/dashboard.php` | کتاب | `domains/books.ghazalify.com/public_html/dashboard.php` |
| `wordpress/ghazal-seo.php` | — | **رد می‌شود** |
| `panel-ops/deploy.py` | — | **رد می‌شود** |

قانون خاص حسابداری: فقط `accounting/api.php` می‌رود زیر پوشهٔ `api/`. بقیهٔ فایل‌های `accounting/foo` می‌شوند `public_html/foo`.

مسیرهای پیش‌فرض پنل (هر چیزی که `accounting/` یا `bookstore-shop/` یا `wordpress/` نباشد) روی `panel.ghazalify.com` می‌روند.

---

## فایل‌هایی که هرگز آپلود نمی‌شوند

اسکریپت اگر یکی از این‌ها را بدهی، با خطا می‌ایستد و آپلود نمی‌کند:

```
includes/directadmin-config.php
includes/rollcall-config.php
includes/liara-ai-config.php
includes/bookstore-config.php
panel-ops/config.json
wordpress/ghazal-seo-secret.php
accounting/bookstore-config.php
accounting/identity-config.php
accounting/config.php
```

همچنین هر فایلی که اسمش به `directadmin-config.php`، `rollcall-config.php`، `liara-ai-config.php`، `seo-secret.php`، `identity-config.php`، `bookstore-config.php` بخورد.

این فایل‌ها معمولاً **فقط روی سرور** هستند و از گیت ساخته نمی‌شوند مگر کاربر صریح بگوید:

- `includes/db.php`
- `includes/auth.php`
- `includes/rollcall-config.php`

---

## اسکریپت روی سرور چه کار می‌کند

وابستگی خارجی ندارد. جریان دقیق:

```
ادیت محلی
  → resolve مسیر نسبت به ROOT
  → بلاک فایل رمز؟
  → map به دامنه + dir DirectAdmin
  → [--dry-run اینجا تمام]
  → POST /api/login   {username, password}
  → GET  loginURL     (نشست Evolution)
  → POST /api/filemanager-actions/upload?dir=...&overwrite=true
  → GET  /api/filemanager/download?path=...
  → مقایسه حجم / چند بایت اول
```

رمز در stdout چاپ نمی‌شود. مدل هم نباید آن را لاگ کند.

بعد از عوض کردن JS/CSS پنل، اگر مرورگر فایل کهنه نشان داد، query cache را روی تگ اسکریپت/لینک بالا ببر (مثلاً `term-plan.js?v=tp3`). خودِ `deploy.py` کش مرورگر را خالی نمی‌کند.

---

## قوانین محصول که مدل نباید بشکند

این‌ها بارها در پنل زنده اشتباه شده‌اند. حتی اگر تسک «یه چیز را ساده کن» باشد، این‌ها را خودسر عوض نکن.

### Session Plan ≠ Term Plan

دو محصول جدا هستند.

| | Session Plan | Term Plan |
|---|---|---|
| چیست | برنامهٔ جلسهٔ آزاد / متن آزاد معلم | تسک‌های ازپیش‌تعریف‌شدهٔ هر جلسهٔ ترم |
| معلم | `dashboard/teacher/session-plan.php` | `dashboard/teacher/term-plan.php` |
| سوپروایزر | `dashboard/supervisor/session-plan.php` | `dashboard/supervisor/term-plan.php` |
| استایل | `assets/css/teacher/session-plan.css` | `assets/css/term-plan.css` |

Session Plan را به Term Plan تبدیل نکن، ادغام نکن، و UI یکی را جای دیگری نگذار مگر کاربر صریح بگوید.

Term Plan: سوپروایزر تسک را با اکسل وارد/ادیت می‌کند و برای هر جلسه ریمارک می‌نویسد. معلم کارت کلاس و درصد سپری‌شده می‌بیند، تسک را تیک (متد اجباری) یا ضربدر (ریمارک اجباری) می‌زند، و اگر تسکی نبود Add Task می‌زند. ریمارک سوپروایزر باید برای معلم روی کارت جلسه دیده شود.

### لول‌های کتاب

لول‌های قدیمی را **حذف نکن**:

`T5…T16` ، `B1…B5` ، `E1…E5` ، `PI1…PI5` ، `I1…I5` ، `UI1…UI5` ، `ADV1…ADV5`

لول‌های جدید (کتاب‌های Wider World و Connectivity) جدا اضافه شده‌اند. شهریه‌شان از لول متناظر قدیمی کپی می‌شود، ولی **ترم‌پلن ورد فقط مال همین لول‌های جدید است**:

| جدید | شهریه از |
|---|---|
| `WT5` … `WT16` | `T5` … `T16` |
| `CB1` … `CB5` | `B1` … `B5` |
| `CE1` … `CE5` | `E1` … `E5` |
| `CPI1` … `CPI5` | `PI1` … `PI5` |
| `CI1` … `CI5` | `I1` … `I5` |
| `CUI1` … `CUI5` | `UI1` … `UI5` |
| `CADV1` … `CADV5` | `ADV1` … `ADV5` |

تشخیص کلاس جدید از عنوان کلاس است (پیشوند `WT` / `CB` / `CE` / `CPI` / `CI` / `CUI` / `CADV`). کلاس `T7` یا `PI2` نباید قالب Connectivity/Wider World بگیرد.

### چیزهای دیگر که دست نزن مگر گفته شود

- دکمهٔ Publish / Vercel برای این پنل PHP روی DirectAdmin معنا ندارد؛ اضافه نکن.
- هویت دانش‌آموز = شماره پرونده. منطق حسابداری / الوکام / ثبت‌نام را بدون درخواست عوض نکن.
- اسم ترم‌ها انگلیسی است (`Fall 1`، `Spring 1 (1405)`، …).
- تاریخ و ساعت پنل به وقت تهران است.

---

## جریان کار پیشنهادی برای یک تسک پنل

1. بفهم کدام فایل‌های ریپوی **خصوصی پنل** باید عوض شوند.
2. ادیت را محلی انجام بده.
3. `--dry-run` برای همان فایل‌ها.
4. اگر نگاشت دامنه غلط بود، با `--root` یا مسیر نسبی درستش کن؛ `targets.json` را حدس نزن و عوض نکن مگر دامنه واقعاً عوض شده باشد.
5. آپلود واقعی همان فایل‌ها.
6. روی `main` ریپوی پنل commit بزن مگر شاخهٔ دیگری خواستند. Pull request نساز مگر بخواهند.
7. در جواب نهایی بنویس: فایل محلی → دامنه → مسیر سرور → HTTP کد.

نمونهٔ گزارش:

```text
آپلود شد:
- includes/term-plan.php → panel.ghazalify.com  public_html/includes/term-plan.php  HTTP 204
- assets/js/term-plan.js → panel.ghazalify.com  public_html/assets/js/term-plan.js  HTTP 204
```

---

## مسیرهای پرتکرار در ریپوی پنل

این‌ها داخل **این** ریپو نیستند؛ داخل ریپوی خصوصی پنل‌اند. برای اینکه مدل بداند کجا را بگردد:

```text
dashboard/student/          داشبورد دانش‌آموز
dashboard/teacher/          معلم (کلاس، حضور، Term Plan، Session Plan، نمره)
dashboard/supervisor/       سوپروایزر (ترم، کلاس‌بندی، دانش‌آموز، Term Plan، رول‌کال)
includes/                   هلپرهای مشترک (term-plan.php، placement، terms، …)
assets/css/  assets/js/     استایل و اسکریپت
accounting/                 کل پنل حسابداری (api.php استثنا در نگاشت)
bookstore-shop/             فروشگاه کتاب
wordpress/                  سایت اصلی؛ با این ابزار آپلود نمی‌شود
```

فایل‌های کلیدی Term Plan:

- `includes/term-plan.php`
- `includes/term-plan-tracks.php`
- `includes/term-plan-tracks-data.php`
- `dashboard/teacher/term-plan.php`
- `dashboard/teacher/term-plan-details.php`
- `dashboard/teacher/ajax-term-plan.php`
- `dashboard/supervisor/term-plan.php`
- `dashboard/supervisor/term-plan-details.php`
- `dashboard/supervisor/ajax-term-plan.php`
- `dashboard/supervisor/term-plan-import.php`
- `assets/js/term-plan.js`
- `assets/css/term-plan.css`

---

## عیب‌یابی

| نشانه | معنی | کار درست |
|---|---|---|
| `No DirectAdmin password found` | `config.json` نیست یا `password` خالی است | کپی از example؛ رمز را در چت نگذار |
| `DirectAdmin login failed HTTP …` | یوزر/رمز/آدرس پنل DA غلط است | `url` باید پورت `2223` باشد؛ رمز را چاپ نکن |
| `Not a file: …` | مسیر نسبی از ریشهٔ پنل نیست | `--root` بده یا از پوشهٔ ریپوی پنل اجرا کن |
| `File is outside the repo` | مسیر مطلق خارج از `ROOT` | همان |
| `Blocked secret file` | فایل رمز است | آپلود نکن |
| `Refusing to map wordpress/…` یا `panel-ops/…` | این ابزار برای آن سایت نیست | اگر واقعاً باید برود، از کاربر مسیر بپرس؛ حدس نزن |
| آپلود `HTTP` غیر از ۱۹۹–۲۰۴ | File Manager رد کرد | متن خطا؛ دوباره با FTP امتحان نکن |
| `match=False` | حجم فایل روی سرور با محلی یکی نیست | دوباره آپلود همان فایل؛ اگر ماند، گزارش بده |
| مرورگر فایل JS کهنه می‌دهد | کش | `?v=` روی لینک اسکریپت |

`--dry-run` هیچ لاگینی نمی‌زند؛ برای تست نگاشت بدون رمز هم کار می‌کند.

---

## امنیت

- `config.json` را commit نکن. در این ریپو `.gitignore` دارد.
- توکن گیت‌هاب، رمز DA، رمز دیتابیس، توکن SMS / الوکام / Mattermost را در Issue و چت مدل نگذار.
- این ریپو پابلیک است؛ هیچ رمز واقعی داخلش نباشد.
- اسکریپت رمز را `print` نمی‌کند؛ مدل هم نباید محتوای `config.json` را در پاسخ بیاورد.
- کاربر DirectAdmin `ghazali1` است؛ با کاربر دیگری آپلود نکن مگر گفته شود.

اگر توکن یا رمزی در چت لو رفت، همان‌جا بگو revoke شود. توکن را در ریپو ذخیره نکن.

---

## بعد از ادیت این ابزار (خود همین ریپو)

اگر `deploy.py` یا `targets.json` را عوض کردی:

1. روی `main` همین ریپوی پابلیک commit/push کن.
2. کپی داخل ریپوی خصوصی پنل (`panel-ops/`) را هم هم‌خوان نگه دار.

تغییر دامنه یا ریشهٔ سرور فقط با به‌روز کردن `targets.json`؛ مسیر را سخت‌کد داخل مدل ننویس.

---

## English — what another model must do

This repository is the **only** allowed live-deploy tool for Ghazal’s PHP panels. It talks to DirectAdmin Evolution (`server16e.irwebspace.com:2223`, user `ghazali1`). It is **not an MCP**.

1. Edit files in the **private panel repo**, not in this repo.
2. Copy `config.example.json` → `config.json` and put the DirectAdmin password there. Never paste the password into chat.
3. Dry-run, then upload:

```bash
python3 deploy.py --root /path/to/panel-repo --dry-run PATH [PATH...]
python3 deploy.py --root /path/to/panel-repo PATH [PATH...]
```

4. Do not use FTP, FileZilla, scp, n8n MCP, or OpenSEO MCP.
5. Do not merge Session Plan into Term Plan.
6. Do not delete legacy levels T / B / E / PI / I / UI / ADV.
7. Connectivity / Wider World term plans apply only to WT / CB / CE / CPI / CI / CUI / CADV class titles.
8. Accounting host is spelled `acccounting.ghazalify.com` (three c’s). `accounting/api.php` maps to `public_html/api/api.php`.
9. Refuse `wordpress/` and secret `*-config.php` / `*-secret.php` uploads.
10. After a live upload, report local path → host → remote path → HTTP status. If deploy fails, show the error and stop; do not “try FTP instead”.
