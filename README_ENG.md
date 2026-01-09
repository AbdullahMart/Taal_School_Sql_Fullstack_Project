# Taal_School_Sql_Fullstack_Project

**Short Description**
This repository contains a simple React (Vite) frontend and a Node.js (Express) backend API. The backend connects to a MySQL database and returns questions from the `app_question_body` table. This guide explains step-by-step how students with limited Git and Node experience can download and run the project on their local machines.

---

## Requirements ✅
- Git (or download the ZIP from GitHub)
- Node.js **LTS** (18.x or newer) and npm
- MySQL (local installation)
- VS Code or another code editor

---

## 1) Clone / Download the repository
1. Using Git (recommended):

```bash
git clone https://github.com/AbdullahMart/Taal_School_Project_Fullstack.git
cd Taal_School_Project_Fullstack
```

> Tip: If you want to have your own copy on GitHub, click **Fork** on the project's GitHub page and clone your fork.

Note: If you are not familiar with Git you can download the repository via **Code → Download ZIP** on GitHub; extract the ZIP and open the folder.

---
2. Create the MySQL database and load the example table (run SQL in MySQL CLI or a GUI):

### Loading SQL files with MySQL Workbench or CLI 📥
Follow these steps to load `app_db-schema.sql` (schema) and then `app_db-data.sql` (sample data). **Run the schema first**, then the **data** file.

A. Using MySQL Workbench (graphical):
1. Open MySQL Workbench and connect to your local MySQL instance.
2. Use **File → Open SQL Script** to open `app_db-schema.sql`.
3. Click the ⚡ Execute button or press Ctrl+Shift+Enter to run the script. The `app_db` schema should appear under `Schemas`.
4. Likewise, open `app_db-data.sql` with **File → Open SQL Script** and execute it. The data will be inserted into the `app_question_body` table.


B. Verify
- In Workbench, check `Schemas → app_db → Tables → app_question_body` to see the records.
- Example test query in Workbench:

---Query for quick test---

select *
from app_db.app_question_body;

-------------------------------------------

3. Check MySQL connection settings:
- The connection config in `backend-api/index.js` is an example; use your MySQL user/password. Open `backend-api/index.js` and edit the following section:

```js
const db = mysql.createConnection({
  host: 'localhost',
  user: 'root',
  password: '!@#123qwert', // -> change this to your own password
  database: 'app_db'
});
```

> Tip: For security, do not commit real passwords to the repo in real projects; use a `.env` file.


## 3) Backend (API) setup and run 🔧

A. Go to the `backend-api` directory:
- From repo root (short):

```bash
cd backend-api
```


B. Start the API:

```bash
node index.js
```

> Note: If you see an error like `Error: Cannot find module '...\index.js'`, you probably ran `node index.js` from the wrong directory; either `cd backend-api` first or run with the full path.

- If successful: you should see `🚀 API running: http://localhost:3001` and `✅ MySQL connection successful!`.

- To test if data is returned from the SQL server:

```web
# open in a web browser (Chrome, Edge, etc.)

URL: http://localhost:3001/api/questions
```

---

## 4) Frontend (React + Vite) setup and run 🌐
A. Open a new terminal in VS Code. Do not close the backend-api terminal. In the new terminal, go to the frontend folder:

- From repo root (short):

```bash
cd app_db/App_db
```


B. Install dependencies:

```bash
npm install
```

> Tip: If you run `npm install` in the wrong parent folder the dependencies may be installed in the root or another folder; make sure you are in `app_db/App_db`.

C. Start the development server:

- Shortcut:

```bash
npm run dev
```

- Vite will usually serve the app at `http://localhost:5173/`. Open it in a browser.
- The frontend should automatically fetch data from the backend API at `http://localhost:3001/api/questions` (CORS is already enabled).

---


## 4) Common Problems & Solutions ⚠️
- "MySQL connection error": Is the MySQL service running? Are username/password/host correct? Is port 3306 used by another application?
- "Port already in use": Ports 3001 or 5173 may be used by other apps. Try a different port or stop the other application.
- Missing packages: make sure you run `npm install` in the correct directory.
- Node version mismatch: use an LTS release (18.x/20.x).

Abdullah Mart

Best of luck!
