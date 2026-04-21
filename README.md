# CloudPy — Python Hosting Site

> Made by **fade** — Discord: `.yurix_`

---

## 🚀 GitHub Pages Setup (3 Steps)

### Step 1 — Create GitHub Repo
1. Go to **github.com** → New repository  
2. Name it: `cloudpy`  
3. Set to **Public**  
4. Upload all 3 files: `index.html`, `dashboard.html`, `admin.html`

### Step 2 — Enable GitHub Pages
1. Go to repo **Settings → Pages**
2. Under **Source**, select `main` branch → `/ (root)`
3. Click **Save**
4. Live at: `https://YOUR_USERNAME.github.io/cloudpy/`

---

## 🔵 Discord Login Setup (2 Minutes, Free)

1. Go to **https://discord.com/developers/applications**
2. Click **New Application** → name it `CloudPy`
3. Go to **OAuth2** → **Redirects** → **Add Redirect**
4. Paste your full URL: `https://YOUR_USERNAME.github.io/cloudpy/index.html`
5. Save, then copy your **Client ID**
6. Open `index.html`, find this line:
   ```js
   const DISCORD_CLIENT_ID = 'YOUR_CLIENT_ID_HERE';
   ```
7. Replace with your actual Client ID → re-upload to GitHub

Done! Real Discord login, no backend needed.

---

## 🔐 Owner Panel
- URL: `https://YOUR_SITE/admin.html`
- Default password: **`cloudpy_owner`**
- Change it in `admin.html` → `const OWNER_PASSWORD = 'cloudpy_owner';`

---

*CloudPy © 2025 — Made by fade | Discord: .yurix_*
