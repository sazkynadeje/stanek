# ⚽ Fotbal Stánek — Objednávkový systém

Jednoduchý objednávkový systém pro fotbalový stánek s real-time synchronizací přes Firebase.

## Stránky

| Stránka | Soubor | Použití |
|---|---|---|
| 🛒 **Stánek** | `stanek.html` | Obsluha přijímá objednávky |
| 🔥 **Kuchyň** | `kuchyn.html` | Kuchař vidí objednávky live |
| 👤 **Zákazník** | `zakaznik.html` | Zákazník sleduje stav |

---

## Nastavení Firebase (nutné před spuštěním)

### 1. Vytvoř Firebase projekt

1. Jdi na [console.firebase.google.com](https://console.firebase.google.com)
2. Klikni **"Add project"**
3. Pojmenuj projekt (např. `fotbal-stanek`)
4. Google Analytics — můžeš přeskočit
5. Klikni **"Create project"**

### 2. Aktivuj Realtime Database

1. V levém menu vyber **"Realtime Database"**
2. Klikni **"Create Database"**
3. Vyber region: **Europe (Belgium)**
4. Pravidla: zvol **"Start in test mode"** (na akce stačí)
5. Klikni **"Enable"**

### 3. Získej Firebase config

1. V levém menu klikni na **ozubené kolečko ⚙️ → Project settings**
2. Přejdi dolů na **"Your apps"**
3. Klikni na ikonku **`</>`** (Web)
4. Zaregistruj app (název např. `stanek-web`)
5. Zkopíruj objekt `firebaseConfig`

### 4. Vyplň konfiguraci

Otevři soubor `firebase-config.js` a vyplň hodnoty:

```js
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "fotbal-stanek.firebaseapp.com",
  databaseURL: "https://fotbal-stanek-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "fotbal-stanek",
  storageBucket: "fotbal-stanek.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};
```

---

## Nasazení na GitHub Pages

### 1. Vytvoř GitHub repozitář

1. Jdi na [github.com/new](https://github.com/new)
2. Název např. `fotbal-stanek`
3. Nastav jako **Public**
4. Klikni **"Create repository"**

### 2. Nahraj soubory

Buď přes web (drag & drop na stránce repozitáře), nebo přes terminál:

```bash
git init
git add .
git commit -m "Fotbal stanek v1"
git branch -M main
git remote add origin https://github.com/TVUJ-USERNAME/fotbal-stanek.git
git push -u origin main
```

### 3. Zapni GitHub Pages

1. V repozitáři jdi na **Settings → Pages**
2. Source: **"Deploy from a branch"**
3. Branch: **main**, složka: **/ (root)**
4. Klikni **Save**
5. Za chvíli (1–2 min) bude web dostupný na:
   `https://TVUJ-USERNAME.github.io/fotbal-stanek/`

---

## Použití na akci

| Zařízení | URL |
|---|---|
| Tablet obsluhy | `.../stanek.html` |
| Tablet v kuchyni | `.../kuchyn.html` |
| Telefon zákazníka | `.../zakaznik.html` |

Všechna zařízení musí mít připojení k internetu (stačí mobilní data nebo Wi-Fi).

---

## Firebase pravidla (doporučení pro produkci)

Po akci nebo pokud chceš větší bezpečnost, v Firebase Console → Realtime Database → Rules nastav:

```json
{
  "rules": {
    "objednavky": {
      ".read": true,
      ".write": true
    }
  }
}
```

Pro plnou bezpečnost je potřeba přidat autentizaci — pro občasnou akci test mode postačí.

---

## Reset objednávek po akci

V Firebase Console → Realtime Database → Data → klikni na `objednavky` → Delete.
