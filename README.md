طريقة التنزيل والتشغيل حاليًا :
1-تثبيت المتطلبات:
Debian:
sudo apt install python3-gi gir1.2-gtk-4.0 gir1.2-adw-1 python3-venv ffmpeg
Fedora:
sudo dnf install python3-gobject gtk4 libadwaita ffmpeg-free
Arch:
sudo pacman -S python-gobject gtk4 libadwaita ffmpeg
الثبيت:
unzip ghayma-v0.1-skeleton.zip
cd ghayma
python3 -m venv --system-site-packages .venv
source .venv/bin/activate
pip install yt-dlp yt-dlp-ejs
التشغيل:
PYTHONPATH=src python3 -m ghayma
