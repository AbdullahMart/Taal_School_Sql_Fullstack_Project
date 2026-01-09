# Taal_School_Sql_Fullstack_Project

**Korte beschrijving**
Deze repository bevat een eenvoudige React (Vite) frontend en een Node.js (Express) backend API. De backend maakt verbinding met een MySQL-database en retourneert vragen uit de tabel `app_question_body`. Deze handleiding legt stap voor stap uit hoe studenten met beperkte ervaring met Git en Node het project naar hun lokale machine kunnen downloaden en uitvoeren.

---

## Vereisten ✅
- Git (of download de ZIP vanaf GitHub)
- Node.js **LTS** (18.x of nieuwer) en npm
- MySQL (lokale installatie)
- VS Code of een andere code-editor

---

## 1) Repository downloaden
1. Met Git (aanbevolen):

```bash
git clone https://github.com/AbdullahMart/Taal_School_Project_Fullstack.git
cd Taal_School_Project_Fullstack
```

> Tip: Als je een eigen kopie op GitHub wilt, klik op **Fork** op de GitHub-pagina van het project en clone je fork.

Opmerking: Als je niet bekend bent met Git kun je de repository downloaden via **Code → Download ZIP** op GitHub; pak de ZIP uit en open de map.

---
2. Maak de MySQL-database aan en laad de voorbeeldtabel (voer SQL uit in MySQL CLI of een GUI):

### SQL-bestanden laden met MySQL Workbench of CLI 📥
Volg deze stappen om `app_db-schema.sql` (schema) en vervolgens `app_db-data.sql` (voorbeeldgegevens) te laden. **Voer eerst het schema uit**, daarna het **data**-bestand.

A. Met MySQL Workbench (grafisch):
1. Open MySQL Workbench en maak verbinding met je lokale MySQL-instance.
2. Gebruik **File → Open SQL Script** om `app_db-schema.sql` te openen.
3. Klik op de ⚡ Execute-knop of druk op Ctrl+Shift+Enter om het script uit te voeren. Het schema `app_db` zou zichtbaar moeten worden onder `Schemas`.
4. Open op dezelfde manier `app_db-data.sql` met **File → Open SQL Script** en voer het uit. De gegevens worden ingevoegd in de tabel `app_question_body`.


B. Controle
- In Workbench kun je onder `Schemas → app_db → Tables → app_question_body` de records bekijken.
- Voorbeeld test-query in Workbench:

---Query voor snelle test---

select *
from app_db.app_question_body;

-------------------------------------------

3. Controleer de MySQL-verbinding:
- De connectieconfiguratie in `backend-api/index.js` is een voorbeeld; gebruik je eigen MySQL-gebruiker/wachtwoord. Open `backend-api/index.js` en bewerk het volgende gedeelte:

```js
const db = mysql.createConnection({
  host: 'localhost',
  user: 'root',
  password: '!@#123qwert', // -> verander dit naar je eigen wachtwoord
  database: 'app_db'
});
```

> Tip: Plaats in echte projecten geen echte wachtwoorden in de repo; gebruik een `.env` bestand.


## 3) Backend (API) installatie en starten 🔧

A. Ga naar de `backend-api` map:
- Vanuit de repo-root (kort):

```bash
cd backend-api
```


B. Start de API:

```bash
node index.js
```

> Opmerking: Als je een fout ziet zoals `Error: Cannot find module '...\index.js'`, heb je waarschijnlijk `node index.js` vanuit de verkeerde map uitgevoerd; gebruik `cd backend-api` eerst of voer het uit met het volledige pad.

- Als het succesvol is zie je `🚀 API running: http://localhost:3001` en `✅ MySQL connection successful!`.

- Om te testen of er data van de SQL-server terugkomt:

```web
# open in een webbrowser (Chrome, Edge, etc.)

URL: http://localhost:3001/api/questions
```

---

## 4) Frontend (React + Vite) installatie en starten 🌐
A. Open een nieuwe terminal in VS Code. Sluit de backend-api terminal niet. Ga in de nieuwe terminal naar de frontend-map:

- Vanuit de repo-root (kort):

```bash
cd app_db/App_db
```


B. Installeer afhankelijkheden:

```bash
npm install
```

> Tip: Als je `npm install` in de verkeerde bovenliggende map uitvoert, kunnen de afhankelijkheden in de root of een andere map worden geïnstalleerd; zorg dat je in `app_db/App_db` bent.

C. Start de dev-server:

- Kort:

```bash
npm run dev
```

- Vite dient de app meestal op `http://localhost:5173/` te serveren. Open dit in de browser.
- De frontend zou automatisch data moeten ophalen van de backend API op `http://localhost:3001/api/questions` (CORS is al ingeschakeld).

---

## 4) Veelvoorkomende problemen & oplossingen ⚠️
- "MySQL connection error": draait de MySQL-service? Zijn gebruikersnaam/wachtwoord/host correct? Gebruikt een andere app poort 3306?
- "Port already in use": poorten 3001 of 5173 kunnen al in gebruik zijn. Probeer een andere poort of stop de andere applicatie.
- Ontbrekende pakketten: zorg dat je `npm install` in de juiste map uitvoert.
- Node versie ongelijkheid: gebruik een LTS-versie (18.x/20.x).

Abdullah Mart

Veel succes!
