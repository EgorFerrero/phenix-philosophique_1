# Phénix Philosophique

Site pour découvrir et progresser en philosophie : forum, glossaire des philosophes, œuvres par thématiques, question du jour et progression jusqu'au niveau 100.

Le site tient dans un seul fichier `index.html`. Il fonctionne en deux modes :

- **Mode démo** (par défaut) : connexion simulée par pseudonyme, données gardées dans le navigateur. Utile pour tester et montrer le site.
- **Mode réel** : connexion Google et forum partagé entre tous les visiteurs, grâce à Firebase (gratuit à cette échelle).

---

## 1. Mettre le site en ligne sur GitHub Pages (10 min)

1. Sur GitHub, créer un dépôt public nommé `phenix-philosophique`.
2. Bouton **Add file → Upload files** : déposer `index.html`, `firestore.rules` et `README.md`, puis **Commit changes**.
3. **Settings → Pages** : Source = *Deploy from a branch*, Branch = `main`, dossier `/ (root)`, **Save**.
4. Après 1 à 2 minutes, le site est en ligne à l'adresse :
   `https://ferreroegor2-ops.github.io/phenix-philosophique/`

À ce stade, le site marche en **mode démo**.

## 2. Activer la vraie connexion Google (15 min)

GitHub Pages n'héberge que des pages statiques : il ne peut ni gérer des comptes, ni stocker des messages. Firebase (Google) joue ce rôle.

1. Aller sur https://console.firebase.google.com → **Ajouter un projet** (Google Analytics : facultatif).
2. **Authentication → Commencer → Sign-in method → Google → Activer** (renseigner l'e-mail d'assistance).
3. **Authentication → Paramètres → Domaines autorisés → Ajouter un domaine** : `ferreroegor2-ops.github.io`
4. **Firestore Database → Créer une base de données** → mode production → région `eur3 (europe-west)`.
5. **Firestore → Règles** : coller le contenu de `firestore.rules` → **Publier**.
6. **Paramètres du projet (roue dentée) → Vos applications → icône Web `</>`** → enregistrer l'appli. Firebase affiche un objet `firebaseConfig`.
7. Dans `index.html`, remplacer le bloc `FIREBASE_CONFIG` (en haut du `<script>`) par vos valeurs `apiKey`, `authDomain`, `projectId`, `appId`.
8. Re-déposer `index.html` sur GitHub. Le bandeau « Mode démonstration » disparaît : la connexion Google est active.

> La clé `apiKey` de Firebase n'est pas un secret : elle peut être publique. La sécurité repose sur les **règles Firestore** et les **domaines autorisés**.

## 3. Personnaliser le contenu

Tout le contenu est en haut du script de `index.html` :

- `PHILOS` : les philosophes du glossaire
- `OEUVRES` : les œuvres (thème, niveau, résumé)
- `QUIZ` : les questions du jour (une par jour, en rotation)
- `xpFor()` : la courbe d'expérience (niveau 100 ≈ 14 800 XP)

## Limites connues

- L'XP est calculée dans le navigateur : un utilisateur technique pourrait tricher. Pour un vrai contrôle, il faudrait des Cloud Functions Firebase.
- Pas encore d'outil de modération du forum (suppression par l'administrateur).
- Avant d'ouvrir largement au public : ajouter des mentions légales complètes (RGPD).
