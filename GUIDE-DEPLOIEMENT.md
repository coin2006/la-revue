# 🗞️ La Revue — Guide de déploiement
### Mettre ton app en ligne en 20 minutes, gratuitement

---

## Ce dont tu as besoin
- Un ordinateur (Mac, Windows ou Linux)
- Une adresse email
- Les fichiers de l'app (téléchargés depuis Claude)

---

## ÉTAPE 1 — Prépare tes fichiers (2 min)

Dézippe le dossier téléchargé. Tu dois avoir cette structure :

```
la-revue-pwa/
├── index.html
├── manifest.json
├── sw.js
└── icons/
    ├── icon-192.png
    └── icon-512.png
```

---

## ÉTAPE 2 — Crée un compte GitHub (5 min)

GitHub, c'est l'endroit où ton code sera stocké. C'est gratuit.

1. Va sur **https://github.com**
2. Clique sur **Sign up**
3. Choisis un nom d'utilisateur, une adresse email, un mot de passe
4. Vérifie ton email (ils envoient un code)
5. Sur la page d'accueil GitHub, clique sur **"New repository"** (bouton vert)
6. Remplis :
   - **Repository name** : `la-revue`
   - **Visibility** : ✅ Public
   - ✅ Coche **"Add a README file"**
7. Clique sur **"Create repository"**

---

## ÉTAPE 3 — Upload tes fichiers sur GitHub (5 min)

1. Sur la page de ton repository, clique sur **"Add file" → "Upload files"**
2. Glisse-dépose **tous tes fichiers** dans la zone (index.html, manifest.json, sw.js)
3. Pour le dossier `icons/` : clique sur **"choose your files"** et sélectionne les deux icônes
4. En bas, dans "Commit changes", laisse le message par défaut
5. Clique sur **"Commit changes"**

> ⚠️ Si GitHub ne permet pas d'uploader le dossier icons directement, upload d'abord les fichiers racine, puis fais un deuxième upload en naviguant dans le dossier icons.

---

## ÉTAPE 4 — Déploie sur Vercel (5 min)

Vercel va publier ton app sur Internet, gratuitement et instantanément.

1. Va sur **https://vercel.com**
2. Clique sur **"Sign Up"**
3. Choisis **"Continue with GitHub"** — connecte ton compte GitHub
4. Une fois connecté, clique sur **"Add New… → Project"**
5. Tu vois la liste de tes repositories GitHub → clique sur **"Import"** à côté de `la-revue`
6. Laisse tous les paramètres par défaut
7. Clique sur **"Deploy"**
8. Attends ~30 secondes ⏳
9. ✅ Vercel te donne une URL du type : `https://la-revue-xxx.vercel.app`

**Ton app est en ligne !**

---

## ÉTAPE 5 — Ajoute ta clé API Anthropic (3 min)

Pour que Claude génère les articles, il faut une clé API.

### Obtenir la clé (gratuit pour commencer)
1. Va sur **https://console.anthropic.com**
2. Crée un compte si ce n'est pas fait
3. Clique sur **"API Keys" → "Create Key"**
4. Copie la clé (elle commence par `sk-ant-...`)

> 💡 Anthropic offre des crédits gratuits au départ. Chaque génération de revue coûte environ 0,02€.

### Ajouter la clé à ton app
Dans ton fichier `index.html`, cherche cette ligne :

```javascript
headers: { 'Content-Type': 'application/json' },
```

Et remplace-la par :

```javascript
headers: {
  'Content-Type': 'application/json',
  'x-api-key': 'sk-ant-TA_CLÉ_ICI',
  'anthropic-version': '2023-06-01',
  'anthropic-dangerous-direct-browser-iab': 'true',
},
```

Puis re-upload le fichier `index.html` modifié sur GitHub (même procédure qu'à l'étape 3). Vercel se met à jour automatiquement en 30 secondes.

---

## ÉTAPE 6 — Installe l'app sur ton téléphone (2 min)

### Sur iPhone (Safari)
1. Ouvre ton URL Vercel dans **Safari** (pas Chrome)
2. Appuie sur le bouton **Partager** (carré avec flèche vers le haut)
3. Fais défiler et appuie sur **"Sur l'écran d'accueil"**
4. Appuie sur **"Ajouter"**
5. ✅ L'icône "La Revue" apparaît sur ton écran d'accueil

### Sur Android (Chrome)
1. Ouvre ton URL Vercel dans **Chrome**
2. Une bannière "Installer l'app" apparaît automatiquement en bas → appuie dessus
3. Ou : appuie sur les **⋮ trois points** en haut à droite → **"Ajouter à l'écran d'accueil"**
4. ✅ L'icône apparaît sur ton écran d'accueil

---

## ÉTAPE 7 — Active les notifications (1 min)

1. Ouvre l'app installée
2. Une bannière verte apparaît en haut : **"Activer les notifications"**
3. Appuie sur **Activer** et accepte la demande du navigateur
4. Dans l'app, active le toggle **"Notification quotidienne"**
5. Règle l'heure souhaitée (ex. 08h00)
6. ✅ Tu recevras une notification chaque matin à cette heure

> ⚠️ Note : les notifications push web fonctionnent mieux sur Android. Sur iPhone, elles nécessitent iOS 16.4+ et que l'app soit installée sur l'écran d'accueil.

---

## ✅ Récapitulatif

| Étape | Quoi | Temps |
|-------|------|-------|
| 1 | Préparer les fichiers | 2 min |
| 2 | Créer compte GitHub + repository | 5 min |
| 3 | Uploader les fichiers | 5 min |
| 4 | Déployer sur Vercel | 5 min |
| 5 | Ajouter la clé API Anthropic | 3 min |
| 6 | Installer sur téléphone | 2 min |
| 7 | Activer les notifications | 1 min |
| **Total** | | **~23 min** |

---

## En cas de problème

**L'app ne charge pas ?**
→ Vérifie que tous les fichiers sont bien uploadés sur GitHub (index.html, manifest.json, sw.js, icons/)

**Erreur "API 401" ?**
→ Ta clé API est incorrecte ou mal collée. Vérifie qu'elle commence par `sk-ant-`

**Erreur "API 403" ?**
→ Ajoute bien le header `anthropic-dangerous-direct-browser-iab: true`

**Les notifications ne marchent pas sur iPhone ?**
→ Assure-toi d'utiliser Safari et que l'app est installée sur l'écran d'accueil (pas juste ouverte dans le navigateur)

**Vercel ne se met pas à jour après modification ?**
→ Attends 1 minute, puis force le rechargement (Ctrl+Shift+R)

---

*La Revue · Guide v1.0*
