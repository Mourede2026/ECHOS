# ECHOS – Zone Sanitaire DAA

Plateforme web de collecte hebdomadaire des « échos » de la zone sanitaire : chaque acteur (RCSE, CAR, RH, RSI, PF ARCH, RSO, PF SRCR, GDR) dépose sa contribution, puis l'administrateur compile et exporte le rapport (Word / texte WhatsApp) pour le staff.

## Contenu du dépôt

| Fichier | Rôle |
|---|---|
| `index.html` | Application complète (page unique, aucun build) |
| `manifest.webmanifest` | Déclaration de l'application installable (nom, couleurs, icônes) |
| `sw.js` | Service worker (installation et secours hors-ligne de l'interface) |
| `icons/` | Icônes de l'application (192, 512, maskable, iOS, favicon) |
| `firestore.rules` | Règles de sécurité Firestore à publier dans la console Firebase |
| `README.md` | Ce guide |

## Mise en ligne sur GitHub Pages

1. Créez un dépôt GitHub (ex. `echos-zs-daa`).
2. Cliquez **Add file → Upload files** et déposez **tous les fichiers et le dossier `icons`** (`index.html`, `manifest.webmanifest`, `sw.js`, `icons/`, `firestore.rules`, `README.md`), puis **Commit changes**.
3. Dans **Settings → Pages**, choisissez **Deploy from a branch**, branche `main`, dossier `/ (root)`, puis **Save**.
4. Après 1 à 2 minutes, le lien `https://<votre-compte>.github.io/echos-zs-daa/` est partagé aux 9 contributeurs.

## Installer l'application sur le téléphone

- **Android (Chrome)** : ouvrez le lien, touchez le bouton **Installer** en haut de la page (ou menu ⋮ → *Installer l'application*).
- **iPhone / iPad (Safari)** : bouton Partager → **Sur l'écran d'accueil**.
- L'installation exige l'adresse HTTPS de GitHub Pages ; elle ne fonctionne pas en ouvrant le fichier directement.
- Hors connexion, l'interface s'ouvre mais l'enregistrement et la lecture des contributions demandent internet.
- Après une mise à jour de `index.html`, changez `echos-v1` en `echos-v2` dans `sw.js` pour forcer le rafraîchissement.

## Firebase (base de données partagée)

1. Console Firebase → **Firestore Database** → onglet **Règles** → collez le contenu de `firestore.rules` → **Publier**.
2. Console Firebase → **Paramètres du projet → Vos applications** : restreignez la clé API aux domaines autorisés (`<votre-compte>.github.io`) via Google Cloud Console → **APIs & Services → Credentials**.

## Utilisation

- **Déposer ma contribution** : choisir l'année/semaine, cliquer son secteur, saisir ou importer (Word, Excel, CSV, TXT), enregistrer.
- **Rapport compilé** : vue consolidée de la semaine, copie du texte pour WhatsApp, export Word (code admin requis).
- **Calendrier (Admin)** : ajout d'une nouvelle année (date de début de la semaine 1 + nombre de semaines).

## Points de sécurité à connaître

- Le code administrateur est écrit en clair dans `index.html` : toute personne qui affiche le code source de la page peut le lire. Il protège contre une erreur de manipulation, pas contre une personne mal intentionnée.
- Les règles Firestore fournies laissent la lecture/écriture ouvertes à qui possède le lien (principe « sans compte »). Ne saisissez aucune donnée nominative de patients.
- Si le dépôt est public, la configuration Firebase et le code admin le sont aussi. Préférez un dépôt privé (GitHub Pages privé nécessite un plan payant) ou changez le code admin régulièrement.
