# Portail FSRDC

**Point d'entrée unifié de toutes les applications internes du Fonds Social de la République Démocratique du Congo.**

Le portail centralise l'accès aux outils de la Direction du Numérique : email, gestion des visites, suivi des marchés publics, gestion des congés, ordres de mission, banque d'images, générateur de signature, et plateforme DIA.

> Déployé en production sur **[portail.fondsocialrdc.org](https://portail.fondsocialrdc.org)**.

---

## Aperçu fonctionnel

Le portail est un **tableau de bord** qui présente toutes les applications FSRDC sous forme de cartes interactives. Authentification centralisée (Supabase), recherche d'application, audit log au clic.

### Applications accessibles depuis le portail

| App | Description | URL |
|---|---|---|
| **Messagerie** | Email FSRDC | webmail.fondsocial.cd |
| **Gestion des Visites** | RDV & accueil visiteurs | visites.fondsocialrdc.org |
| **Suivi des Marchés (PPM)** | PADCV-PTA & PAGDC-PTA | ppm.fondsocialrdc.org |
| **Gestion des Congés** | Demandes RH & validation | conges.fondsocialrdc.org |
| **Missions Flow** | Ordres de mission & rapports | missions.fondsocialrdc.org |
| **Photos-Mission** | Banque institutionnelle d'images | photos.fondsocialrdc.org |
| **Signature Email** | Générateur de signature officielle | portail.fondsocialrdc.org/signature/ |
| **DIA PADCV-PTA** | Plateforme agricole | diapadcv-pta.online |
| **Administration Système** | Supabase, Cloudflare | (liens externes) |

---

## Stack technique

| Couche | Technologie |
|---|---|
| **Frontend** | HTML/CSS/JavaScript vanilla (sans framework) |
| **Hébergement** | Cloudflare Workers (assets statiques) |
| **Domaine** | portail.fondsocialrdc.org |
| **Authentification** | Supabase Auth (session partagée avec les autres apps) |
| **Sous-app intégrée** | Générateur de signature email (`/signature/`) |

---

## Structure du dépôt

```
portail-fsrdc-html/
├── index.html                       # Portail principal (cartes + auth + audit log)
├── signature/
│   └── index.html                   # Générateur de signature email
├── logo-fsrdc.jpg                   # Logo FSRDC (JPG)
├── logo-fsrdc.png                   # Logo FSRDC (PNG)
├── logo-fsrdc-officiel.jpg          # Variante officielle du logo
├── wrangler.jsonc                   # Configuration Cloudflare Worker
├── .gitignore
└── README.md
```

---

## Fonctionnalités du portail

- **Authentification Supabase** centralisée
- **Cartes d'applications** générées dynamiquement à partir d'un tableau `APPS` dans `index.html`
- **Recherche d'application** (filtre temps réel par nom, description, lien)
- **Audit log** : chaque clic sur une carte est tracé (utilisateur, app, horodatage)
- **Signature email** intégrée comme sous-application avec bouton "Retour au portail"
- **Design institutionnel** : palette FSRDC (bleu marine, or, drapeau RDC)
- **Signature auteur** dans le footer

---

## Déploiement

### Cloudflare Workers

```bash
# Première fois : installer Wrangler globalement
npm install -g wrangler

# Déployer (depuis la racine du repo)
wrangler deploy
```

La configuration `wrangler.jsonc` pointe sur le dossier racine comme dossier d'assets.

### Domaine personnalisé

Le domaine `portail.fondsocialrdc.org` est configuré via Cloudflare Dashboard :
Workers & Pages → portail-fsrdc → Settings → Domains & Routes → Add Custom Domain.

---

## Conventions

- **Design** : institutionnel premium (bleu marine FSRDC + or, typographie Fraunces)
- **Pas de caractères typographiques** (tirets cadratin, guillemets français) — utiliser des tirets simples et des guillemets droits
- **Aucune URL `.workers.dev`** dans le code — toutes les apps pointent vers `fondsocialrdc.org`

---

## Auteur

**Armel Manzambi**
Chargé du Numérique - Direction du Numérique, FSRDC
[armel.manzambi@fondsocial.cd](mailto:armel.manzambi@fondsocial.cd)

---

## License

Code propriétaire du Fonds Social de la République Démocratique du Congo (FSRDC).
Tous droits réservés.
