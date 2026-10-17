# Ghazal panel-ops

ابزار دیپلوی پنل آموزشی و حسابداری غزال از طریق DirectAdmin. MCP نیست.

به مدل (جمنای ۴، GPT، کلود، …) بگو:

> اول `INSTRUCTIONS.md` را بخوان. برای ادیت پنل فقط از `python3 deploy.py` استفاده کن.

## نصب کنار پنل

این ریپو را داخل ریپوی خصوصی پنل به نام `panel-ops/` بگذار، یا جدا کلون کن و `--root` بده.

```bash
cp config.example.json config.json
# رمز DirectAdmin فقط داخل config.json
python3 deploy.py --dry-run includes/term-plan.php
python3 deploy.py includes/term-plan.php
```

اگر اسکریپت داخل `panel-ops/` ریپوی پنل است:

```bash
python3 panel-ops/deploy.py includes/term-plan.php
```

اگر این ریپو جداست:

```bash
python3 deploy.py --root /path/to/panel-repo includes/term-plan.php
```

`config.json` را commit نکن. رمز را در چت مدل نگذار.

نقشهٔ دامنه‌ها در `targets.json` است. جزئیات اجباری برای مدل: `INSTRUCTIONS.md`.
