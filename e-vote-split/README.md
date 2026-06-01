# E Vote — Halqa 4 Roundu  (backend + frontend)

```
/backend     Node + Express API. Also serves the frontend. Reads DB creds from env vars.
/frontend    The website (index.html, vote-hero.svg). Served by the backend.
```
The backend serves the frontend, so this runs as ONE Railway service (one URL = site + API).

────────────────────────────────────────────────────────
DEPLOY ON RAILWAY  (one service + one MySQL database)
────────────────────────────────────────────────────────
1. Push this repo to GitHub (keep the /backend and /frontend folders).
2. Railway → New Project → Deploy from GitHub repo → select the repo.
3. Add the database:  New → Database → Add MySQL.
4. Open the app service → Settings → set:
     Root Directory : (leave EMPTY)
     Build Command  : cd backend && npm install
     Start Command  : cd backend && npm start
5. Open the app service → Variables → add (use the REAL values from your
   MySQL service's Variables tab — see below). Do NOT use ${{...}} unless the
   database service is named exactly "MySQL".

     DB_HOST       = (MySQL service -> MYSQLHOST)
     DB_PORT       = (MySQL service -> MYSQLPORT)
     DB_USER       = (MySQL service -> MYSQLUSER, usually root)
     DB_PASSWORD   = (MySQL service -> MYSQLPASSWORD, copy the RAW value)
     DB_NAME       = (MySQL service -> MYSQLDATABASE, usually railway)
     JWT_SECRET    = 333994101f5848713ee1a07593eaef44f09096f0ae0d29c7406fe7625c6f09dacdb6c8309bf93d157dc1afcd2ea301d1
     ADMIN_USERNAME= admin
     ADMIN_PASSWORD= Skadmin@1122
     NODE_ENV      = production
   (Do NOT set PORT — Railway provides it.)

6. After it deploys green, app service → Settings → Networking → Generate Domain.

Where to find DB values: click the MySQL service → Variables tab → reveal/copy
MYSQLHOST, MYSQLPORT, MYSQLUSER, MYSQLPASSWORD, MYSQLDATABASE. Copy MYSQLPASSWORD
directly (not from a URL — URL passwords can be %-encoded and won't match).

Tables + the 12 candidates and 5 union councils are created automatically on first
start. Admin login: admin / Skadmin@1122.

────────────────────────────────────────────────────────
RUN LOCALLY
────────────────────────────────────────────────────────
1. Install Node.js and MySQL (e.g. XAMPP). Create an empty database, e.g. halqa4_roundu.
2. cd backend
3. copy .env.example to .env  and fill DB_HOST/DB_PORT/DB_USER/DB_PASSWORD/DB_NAME
4. npm install
5. npm start
6. open http://localhost:3001
