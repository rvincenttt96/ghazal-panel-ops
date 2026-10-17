# وقتی پنل غزال را ادیت می‌کنی، از این ابزار استفاده کن

راهنمای کامل (نصب، نگاشت مسیر، قوانین محصول، عیب‌یابی): [`README.md`](README.md). این فایل چک‌لیست کوتاه اجباری است.

ادیت پنل آموزشی یا حسابداری **MCP نمی‌خواهد**. ابزار اجباری همین پوشه است.

## قانون اصلی

1. کد را در **همین ریپو** عوض کن.
2. برای رفتن روی سرور زنده **فقط** این را اجرا کن:

```bash
python3 panel-ops/deploy.py dashboard/teacher/term-plan.php includes/term-plan.php
```

اگر این ابزار را جدا از ریپوی پنل کلون کرده‌ای:

```bash
python3 deploy.py --root /path/to/panel-repo includes/term-plan.php
```

3. از FTP، FileZilla، `scp`، آپلود دستی، n8n MCP، OpenSEO MCP، و حدس زدن مسیر سرور استفاده نکن.
4. رمز DirectAdmin، دیتابیس، SMS، الوکام را در چت ننویس و در گیت commit نکن.

---

## دو پنل

| پنل | دامنه | کد در ریپو | ریشه روی DirectAdmin |
|---|---|---|---|
| آموزشی | panel.ghazalify.com | `dashboard/` `includes/` `assets/` و PHP ریشه | `domains/panel.ghazalify.com/public_html/` |
| حسابداری | acccounting.ghazalify.com | `accounting/` | `domains/acccounting.ghazalify.com/public_html/` |

حسابداری سه c دارد: `acccounting`.

`accounting/api.php` روی سرور می‌شود `public_html/api/api.php`. بقیهٔ فایل‌های `accounting/` همان نام نسبی را زیر `public_html/` می‌گیرند.

فروشگاه کتاب `bookstore-shop/` → `books.ghazalify.com` است، پنل نیست؛ مگر کاربر صریح بگوید.

سایت `ghazalify.com` وردپرس است. سئو فقط همان‌جا. پنل و حسابداری را سئو نکن.

---

## جریان کار

```
ادیت محلی در ریپو
    → python3 panel-ops/deploy.py <فایل‌ها>
    → اسکریپت به DirectAdmin لاگین می‌کند و با overwrite آپلود می‌کند
    → دانلود همان فایل و چک محتوا
```

قبل از آپلود واقعی ببین فایل کجا می‌رود:

```bash
python3 panel-ops/deploy.py --dry-run includes/term-plan.php accounting/api.php
```

لیست هدف‌ها:

```bash
python3 panel-ops/deploy.py --targets
```

رمز از یکی از این‌ها خوانده می‌شود (اولین موجود):

- `panel-ops/config.json` (کپی از `config.example.json`، گیت نمی‌شود)
- `includes/directadmin-config.php` (گیت نمی‌شود)

اگر هیچ‌کدام نبود، بگو کاربر `panel-ops/config.example.json` را کپی کند و رمز بگذارد. رمز را از او در چت تکرار نکن.

---

## چه چیزی را دست نزن

- Session Plan معلم/سوپروایزر را به Term Plan تبدیل نکن مگر صریح بگویند.
- لول‌های قدیمی T / B / E / PI / I / UI / ADV را حذف نکن.
- ترم‌پلن Connectivity / Wider World فقط برای لول‌های جدید WT و CB / CE / CPI / CI / CUI / CADV است.
- `includes/db.php`، `includes/auth.php`، `includes/rollcall-config.php` معمولاً فقط روی سرور هستند؛ از گیت نساز و آپلود نکن مگر کاربر بگوید.
- این‌ها را هرگز آپلود نکن: `directadmin-config.php`، `rollcall-config.php`، `*-secret.php`، `panel-ops/config.json`.

---

## بعد از ادیت

- روی `main` commit بزن مگر شاخهٔ دیگری خواستند.
- Pull request نساز مگر بخواهند.
- بگو کدام فایل‌ها روی کدام دامنه آپلود شد.

اگر دیپلوی fail شد، متن خطا را نشان بده و دوباره با FTP امتحان نکن.
