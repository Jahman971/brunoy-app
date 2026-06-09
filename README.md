# ES Brunoy HB — Prépa 2026
## Déploiement Vercel + Supabase

---

### 1. Supabase — Créer les tables

Dans **Supabase > SQL Editor**, exécute ce script :

```sql
-- Table joueurs
create table if not exists joueurs (
  code text primary key,
  data jsonb not null default '{}',
  updated_at timestamptz default now()
);

-- Table meta (annonces, config)
create table if not exists meta (
  key text primary key,
  value jsonb,
  updated_at timestamptz default now()
);

-- Row Level Security (désactive pour commencer, active en prod)
alter table joueurs disable row level security;
alter table meta disable row level security;
```

---

### 2. index.html — Renseigner les clés Supabase

Dans `index.html`, remplace lignes 25-26 :

```javascript
const SUPABASE_URL  = 'https://XXXX.supabase.co';
const SUPABASE_KEY  = 'eyJXXXX...'; // Clé anon publique
```

Trouve ces valeurs dans **Supabase > Project Settings > API**.

---

### 3. Mot de passe Coach

Par défaut : **BRUNOY**

Pour changer, va dans Supabase > Table Editor > `meta` et ajoute :
```json
key: "coach_pwd"
value: "TONMOTDEPASSE"
```

---

### 4. Déployer sur Vercel

```bash
# Option A — CLI
npm i -g vercel
cd brunoy-app
vercel

# Option B — GitHub
# Push ce dossier sur GitHub > connecte dans vercel.com
```

---

### 5. Ajouter à l'écran d'accueil

**iOS (Safari) :** Partager → "Sur l'écran d'accueil"
**Android (Chrome) :** Menu ⋮ → "Ajouter à l'écran d'accueil"

---

### 6. Workflow Coach

1. Connecte-toi avec le mot de passe Coach
2. Onglet **Joueurs** → ajoute chaque joueur (prénom, poste, code auto ou perso)
3. Distribue les codes aux joueurs (WhatsApp, SMS...)
4. Le joueur ouvre l'app, entre son code, complète son profil VMA + jours

---

### Structure des fichiers

```
brunoy-app/
├── index.html      ← App complète (1 fichier)
├── manifest.json   ← PWA (installation écran d'accueil)
├── vercel.json     ← Config Vercel
└── README.md       ← Ce fichier
```
