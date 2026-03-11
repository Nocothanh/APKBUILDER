# APK Builder — GitHub Actions + Expo EAS

Progetto Expo configurato per buildare APK automaticamente tramite GitHub Actions.

---

## 🚀 Setup in 3 passi

### 1. Aggiungi il Secret `EXPO_TOKEN`

1. Vai su **expo.dev** → Account → Access Tokens → crea un token
2. Nel tuo repo GitHub: **Settings → Secrets → Actions → New secret**
   - Nome: `EXPO_TOKEN`
   - Valore: il token copiato da Expo

### 2. Pusha su GitHub

```bash
git init
git add .
git commit -m "init: expo apk builder"
git remote add origin https://github.com/nocothanhs-organization/apkbuilder.git
git push -u origin main
```

Il workflow parte **automaticamente** ad ogni push su `main`.

### 3. Scarica l'APK

- Vai su **Actions** nel tuo repo GitHub
- Clicca sull'ultimo workflow completato ✅
- Sezione **Artifacts** → scarica `app-apk-N`
- Oppure controlla la sezione **Releases** per APK allegati

---

## 📁 Struttura file

```
apkbuilder/
├── .github/
│   └── workflows/
│       └── build-apk.yml    ← il workflow principale
├── assets/
├── App.js
├── app.json                 ← config Expo (slug, projectId)
├── eas.json                 ← profili di build EAS
├── package.json
└── babel.config.js
```

---

## ⚙️ Profili di build

| Profilo      | Output    | Uso                        |
|--------------|-----------|----------------------------|
| `preview`    | `.apk`    | Test interni, sideloading  |
| `production` | `.aab`    | Google Play Store          |
| `development`| `.apk`    | Dev client con hot reload  |

Per triggerare manualmente con un profilo specifico:
**Actions → Build APK → Run workflow → scegli profilo**

---

## 🔑 Variabili d'ambiente

| Secret/Var         | Obbligatorio | Descrizione                     |
|--------------------|--------------|---------------------------------|
| `EXPO_TOKEN`       | ✅ Sì        | Token autenticazione EAS        |
| `GITHUB_TOKEN`     | Auto         | Gestito da GitHub (per Release) |

---

## 📌 Note

- Il **projectId** nel `app.json` è già configurato: `93dacd81-8549-4b68-8542-d631fca981d7`
- Il profilo `preview` genera APK scaricabili direttamente (non richiede firma Play Store)
- L'APK viene anche allegato come **GitHub Release** ad ogni build su `main`
