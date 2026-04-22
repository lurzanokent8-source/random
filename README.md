# CloudPy — Real Python Hosting Platform
> Made by **fade** — Discord: `.yurix_`

---

## 🗂 Project Structure

```
cloudpy/
├── backend/          ← Node.js server (deploy to Railway/Render/VPS)
│   ├── server.js     ← Main server: API + WebSocket + Python process runner
│   ├── package.json
│   └── .env.example  ← Copy to .env and fill in
│
└── frontend/         ← Static HTML (deploy to GitHub Pages)
    ├── index.html    ← Landing page + login
    ├── dashboard.html ← User dashboard + real terminal
    ├── callback.html  ← Discord OAuth callback
    └── admin.html    ← Owner panel
```

---

## 🚀 Step 1 — Deploy Backend (Railway — Free Tier)

1. Go to **https://railway.app** → New Project → Deploy from GitHub repo
2. Push your `backend/` folder to a GitHub repo
3. Railway auto-detects Node.js
4. Add environment variables in Railway dashboard (see below)
5. Copy your Railway URL: `https://cloudpy-xyz.railway.app`

**Environment Variables to set in Railway:**

| Variable | Value |
|----------|-------|
| `PORT` | `3000` |
| `JWT_SECRET` | any 64-char random string |
| `DISCORD_CLIENT_ID` | from Discord Developer Portal |
| `DISCORD_CLIENT_SECRET` | from Discord Developer Portal |
| `DISCORD_REDIRECT_URI` | `https://YOUR_USERNAME.github.io/cloudpy/callback.html` |
| `OWNER_DISCORD_ID` | your personal Discord user ID |
| `OWNER_SECRET_KEY` | any secret string (for admin panel) |
| `PYTHON_BIN` | `python3` |

---

## 🌐 Step 2 — Deploy Frontend (GitHub Pages)

1. Upload all 4 files from `frontend/` to a GitHub repo
2. **Settings → Pages → Deploy from main branch**
3. Live at: `https://YOUR_USERNAME.github.io/cloudpy/`

---

## 🔵 Step 3 — Discord App Setup

1. Go to **https://discord.com/developers/applications**
2. New Application → `CloudPy`
3. **OAuth2 → Redirects → Add:**
   - `https://YOUR_USERNAME.github.io/cloudpy/callback.html`
4. Copy **Client ID** and **Client Secret**
5. Set these as Railway env vars (above)
6. In `index.html`, set:
   ```js
   const DISCORD_CLIENT_ID = 'YOUR_CLIENT_ID_HERE';
   ```

---

## ⚙️ Step 4 — Connect Frontend to Backend

On the login page, paste your Railway URL in the **Backend URL** field and click **Save & Test**.

---

## 🧾 Invoices

- Users see their invoices in **Dashboard → Invoices tab**
- Each invoice has a **Download PDF** button (generated server-side)
- Owner can issue invoices from **Admin Panel → Issue Invoice**
- Pro user invoices auto-generate on the 1st of each month via cron

---

## 🔐 Admin Panel

- URL: `https://YOUR_SITE/admin.html`
- Enter your Railway backend URL + `OWNER_SECRET_KEY`
- Features: user management, ban/unban, plan upgrades, kill sessions, invoice management, broadcast announcements

---

## 🐍 How Python Execution Works

1. User uploads `.py` file via dashboard
2. File saved to server at `data/scripts/{user_id}/{filename}.py`
3. Click **▶ START** → server calls `spawn('python3', ['-u', scriptPath])`
4. `stdout` and `stderr` stream line-by-line → stored in SQLite + sent over WebSocket
5. Browser receives logs instantly via WebSocket connection
6. Session keeps running until user clicks **■ STOP** or server restarts
7. Pro users: if script crashes → auto-restart after 5 seconds

---

*CloudPy © 2025 — Real Python Hosting | Made by fade | Discord: .yurix_*
