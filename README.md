# غيمة (Ghayma)

تطبيق GNOME بسيط لتحميل المقاطع والصوتيات، مبني على
[yt-dlp](https://github.com/yt-dlp/yt-dlp) وFFmpeg بواجهة GTK4 + libadwaita.

> **الحالة:** الإصدار v0.1 (هيكل أولي قيد التطوير). لم يُنشر بعد،
> وواجهة التطبيق (`app.py`) لم تُجرَّب على GNOME حقيقي، فالتشغيل الأول هو الاختبار.

- برنامج حر برخصة `GPL-3.0-or-later` (انظر ملف `COPYING`)
- بدون حسابات وبدون تتبّع
- التوزيع المخطط: Flatpak على Flathub

---

## المتطلبات

- Python 3.10 أو أحدث
- GTK 4 وlibadwaita وPyGObject
- FFmpeg (لدمج الفيديو والصوت وتحويل MP3)
- yt-dlp وyt-dlp-ejs (يُثبَّتان عبر pip داخل البيئة الافتراضية)

## 1) تثبيت متطلبات النظام

**Debian / Ubuntu:**

```bash
sudo apt install python3-gi gir1.2-gtk-4.0 gir1.2-adw-1 python3-venv ffmpeg
```

**Fedora:**

```bash
sudo dnf install python3-gobject gtk4 libadwaita ffmpeg-free
```

> ملاحظة: `ffmpeg-free` في فيدورا لا يتضمن مرمّز MP3 (libmp3lame)،
> فإذا فشل تحويل الصوت إلى MP3 ثبّت `ffmpeg` الكامل من مستودع
> [RPM Fusion](https://rpmfusion.org/).

**Arch:**

```bash
sudo pacman -S python-gobject gtk4 libadwaita ffmpeg
```

## 2) تنزيل المشروع وتجهيز البيئة

```bash
unzip ghayma-v0.1-skeleton.zip
cd ghayma
python3 -m venv --system-site-packages .venv
source .venv/bin/activate
pip install yt-dlp yt-dlp-ejs
```

الخيار `--system-site-packages` ضروري، لأن PyGObject يأتي من حزم النظام
وليس من pip، وبدونه لن تجده البيئة الافتراضية.

## 3) التشغيل

```bash
source .venv/bin/activate        # إن لم تكن البيئة مفعّلة
PYTHONPATH=src python3 -m ghayma
```

في كل مرة تفتح فيها طرفية جديدة نفّذ `source .venv/bin/activate` أولًا.

### ملاحظة عن يوتيوب

يحتاج yt-dlp إلى بيئة JavaScript (يُوصى بـ [Deno](https://deno.com/)) لفك
بعض روابط يوتيوب، والحزمة `yt-dlp-ejs` هي الجزء المرافق لذلك. إذا ظهر خطأ
أو غابت بعض الجودات على يوتيوب فثبّت Deno وتأكد أنه في `PATH`.

## الاختبارات

اختبارات المحرّك فقط (لا تحتاج GTK):

```bash
source .venv/bin/activate
pip install pytest
python3 -m pytest tests
```

## حل المشاكل الشائعة

| المشكلة | الحل |
|---|---|
| `ModuleNotFoundError: No module named 'gi'` | أنشئ البيئة بالخيار `--system-site-packages`، وتأكد من تثبيت `python3-gi` (أو المقابل في توزيعتك) |
| `ValueError: Namespace Adw not available` | ثبّت `gir1.2-adw-1` (Debian) أو `libadwaita` (Fedora/Arch) |
| `No module named ghayma` | شغّل الأمر من مجلد `ghayma` الجذر وأبقِ `PYTHONPATH=src` |
| فشل التحويل إلى MP3 | تأكد من وجود `ffmpeg` بمرمّز MP3 (انظر ملاحظة فيدورا أعلاه) |
| فشل التحميل من يوتيوب | حدّث yt-dlp: `pip install -U yt-dlp yt-dlp-ejs` وثبّت Deno |

## إخلاء مسؤولية قانوني

أنت المسؤول عن احترام شروط خدمة المواقع التي تحمّل منها وقوانين حقوق النشر
المعمول بها. لا يدعم هذا المشروع انتهاك الحقوق.

---

# Ghayma (English)

A simple GNOME app for downloading videos and audio, powered by yt-dlp and
FFmpeg. GTK4 + libadwaita, Wayland-first. Free software (`GPL-3.0-or-later`),
no accounts, no telemetry. **Status:** v0.1 skeleton, not released.

## Quick start

```bash
# 1. System packages (Debian/Ubuntu shown; see the Arabic section for Fedora/Arch)
sudo apt install python3-gi gir1.2-gtk-4.0 gir1.2-adw-1 python3-venv ffmpeg

# 2. Project setup
unzip ghayma-v0.1-skeleton.zip
cd ghayma
python3 -m venv --system-site-packages .venv   # keeps system PyGObject visible
source .venv/bin/activate
pip install yt-dlp yt-dlp-ejs

# 3. Run
PYTHONPATH=src python3 -m ghayma
```

Notes:

- On Fedora, `ffmpeg-free` lacks the MP3 encoder; use full `ffmpeg` from RPM Fusion for MP3 output.
- YouTube extraction needs a JavaScript runtime (Deno recommended) alongside `yt-dlp-ejs`.
- Tests (engine only, no GTK): `pip install pytest && python3 -m pytest tests`

## Legal notice

You are responsible for respecting the terms of service of the websites you
download from and applicable copyright law. This project does not endorse
infringement.
