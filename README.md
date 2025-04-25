# Jupyter Uptime & Root Access Setup

Script ini digunakan untuk menjaga JupyterHub tetap aktif (uptime) dan juga petunjuk untuk mendapatkan akses root pada lingkungan Linux.

---

## 🚀 Jupyter Uptime Script (Python)

Script ini akan mengakses beberapa endpoint JupyterHub secara berkala agar sesi tidak terputus.

### Persyaratan

- Python 3.x
- Modul `requests` (`pip install requests`)

### Cara Penggunaan

1. **Salin kode berikut dan simpan sebagai `uptime.py`:**

```python
import requests
import time

# Define your session details (Replace these with actual values)
SESSION_ID = "isi cookienya disini"
XSRF_TOKEN = "isi cookienya disini"
JUPYTERHUB_USER = "isi cokienya disini"

# Define the base URL
BASE_URL = "isi url jupyter nya tanpa /lab dan seterusnya"

# Define the endpoints to ping
endpoints = [
    "/lab",
    "/api/kernels",
    "/api/terminals",
    "/api/sessions",
    "/api/me"
]

# Headers for authentication
headers = {
    "accept": "*/*",
    "authorization": "token your_jupyter_token",  # Replace with your actual token
    "content-type": "application/json",
    "user-agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/133.0.0.0 Safari/537.36",
    "x-xsrftoken": XSRF_TOKEN,
}

# Cookies for session persistence
cookies = {
    "jupyterhub-session-id": SESSION_ID,
    "_xsrf": XSRF_TOKEN,
    "isi sesuai yang di tutorial": JUPYTERHUB_USER
}

# Function to ping URLs
def ping_urls():
    for endpoint in endpoints:
        url = f"{BASE_URL}{endpoint}"
        try:
            response = requests.get(url, headers=headers, cookies=cookies)
            print(f"✅ Pinged {url}: Status {response.status_code}")
        except requests.RequestException as e:
            print(f"❌ Failed to ping {url}: {e}")

# Run the ping every 8 seconds
while True:
    ping_urls()
    time.sleep(8)
```

2. **Jalankan script:**

```bash
python3 uptime.py
```

---

## ⚙️ Cara Mendapatkan Akses Root

Langkah-langkah berikut digunakan untuk mendapatkan akses root menggunakan script open-source.

### Langkah-Langkah:

1. **Clone repositori root:**

```bash
git clone https://github.com/foxytouxxx/freeroot.git
```

2. **Masuk ke direktori:**

```bash
cd freeroot
```

3. **Jalankan script:**

```bash
./root.sh
```
**atau**
```bash
bash root.sh
```


4. **Install dependensi:**

```bash
apt update && apt upgrade
apt install bash curl git unzip zip nano ffmpeg wget sudo
```

---

## 📌 Catatan

- Jangan bagikan token, cookie, atau informasi sensitif Anda ke publik.
- Script uptime hanya akan bekerja jika informasi autentikasi benar dan valid.
- Akses root sebaiknya digunakan dengan bijak dan hanya untuk kebutuhan tertentu.

---

## Lisensi

Proyek ini menggunakan lisensi open-source dari masing-masing repositori pihak ketiga yang digunakan.
