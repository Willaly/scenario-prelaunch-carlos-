# Comment mettre votre landing en ligne — Guide pas à pas

Ce dossier contient :

- `index.html` — Votre **landing page** de pré-lancement, version **éditoriale** (style Scenario Redesign : serif Fraunces, palette crème/terracotta/noir, italiques expressifs). C'est le fichier qui sera servi par défaut sur Vercel/Netlify.
- `demo.html` — Le **mockup interactif** de l'application (les 7 écrans cliquables, style Airbnb). Reste accessible via la nav "Démo" et via la section "Aperçu" de la landing.
- `index-airbnb-style.html.backup` — L'ancienne version de la landing (style Airbnb). Conservée pour comparaison. À supprimer une fois la version éditoriale validée définitivement.

**Note sur la cohérence visuelle** : la landing est éditoriale, l'app derrière est Airbnb-like. C'est volontaire et c'est ce que font les meilleures marketplaces (Airbnb, Aimé Leon Dore, Aesop) : la home crée la marque, l'app convertit. Si le décrochage vous gêne à l'usage, on pourra refaire le mockup d'app dans l'esprit éditorial — c'est plusieurs heures de travail supplémentaire à prévoir.

À la fin de ce guide, vous aurez :

1. ✅ Une vraie URL publique (du genre `scenario-prelaunch.vercel.app`) à partager
2. ✅ Des formulaires d'inscription qui vous envoient les leads par email
3. ✅ Un site rapide, sécurisé (HTTPS), sans serveur à gérer
4. ✅ Tout ça gratuitement

Comptez **30 à 45 minutes** la première fois. Vous n'avez besoin d'aucune compétence technique.

---

## Étape 1 — Activer la réception des formulaires (5 min)

Les deux formulaires (Particuliers + Artistes) sont déjà branchés sur **Formsubmit**, un service gratuit qui transfère les soumissions directement par email. **Aucun compte à créer**. Les soumissions arrivent dans la boîte `aly.william@gmail.com`.

### Une seule action de votre côté : activer chaque formulaire

Le premier envoi de chaque formulaire déclenche un email de confirmation envoyé par Formsubmit à `aly.william@gmail.com`. Vous devez cliquer le lien d'activation pour valider l'endpoint. C'est une protection anti-spam standard. Après cette confirmation unique, toutes les vraies soumissions arrivent normalement.

**À faire immédiatement après le déploiement** :

1. Ouvrir l'URL publique de votre site (du type `scenario-prelaunch.netlify.app`)
2. **Soumettre le formulaire Particuliers** une fois (utilisez vos vraies infos, c'est juste pour activer)
3. **Soumettre le formulaire Artistes** une fois aussi
4. Aller sur la boîte `aly.william@gmail.com`
5. Vous trouverez **deux emails** de `noreply@formsubmit.co` intitulés "Confirm Subscription"
6. Cliquer le lien de confirmation dans chaque email
7. C'est terminé. Toutes les soumissions futures arriveront directement dans votre boîte.

### Ce que vous recevrez à chaque soumission

Un email formaté en tableau avec :
- Le type d'inscrit (particulier / artiste)
- Tous les champs remplis
- L'horodatage de la soumission

Le visiteur, lui, recevra un **email automatique de remerciement** (différencié selon qu'il est particulier ou artiste). Vous pouvez modifier le texte de cette réponse automatique dans le code : cherchez `_autoresponse` dans `index.html` et adaptez.

### Conseils

- **Surveillez bien votre boîte les premiers jours**. Les emails Formsubmit peuvent parfois atterrir en spam au début — marquez-les comme "Non spam" pour entraîner Gmail à les laisser passer.
- **Pour exporter vos leads en lot** : Formsubmit ne propose pas de dashboard par défaut. Filtrez vos emails Gmail avec `from:noreply@formsubmit.co` puis utilisez un outil comme [emailmeform](https://www.emailmeform.com/) ou un script Apps Script Gmail pour les compiler en Google Sheet.
- **Si vous voulez plus de fonctionnalités** (dashboard, export CSV, webhooks, intégration Slack/Notion) → migrez à terme vers Formspree ([formspree.io](https://formspree.io)), Tally ([tally.so](https://tally.so)) ou Web3Forms ([web3forms.com](https://web3forms.com)). Tous ont des plans gratuits généreux.
- **Changer l'email destinataire** plus tard : ouvrir `index.html`, faire Cmd+F sur `aly.william@gmail.com`, remplacer par votre nouvelle adresse aux **deux** endroits (un par formulaire). Re-soumettre une fois pour reconfirmer.

---

## Étape 2 — Déployer sur Vercel (10 min)

Vercel est un hébergeur gratuit, ultra-rapide, qui sert vos fichiers HTML partout dans le monde.

### Création du compte

1. Aller sur [vercel.com](https://vercel.com)
2. Cliquer **"Sign Up"**
3. Créer un compte avec votre email (le plan **Hobby** est gratuit, suffisant pour vous)

### Déployer le dossier

Vercel propose plusieurs méthodes de déploiement. La plus simple pour vous :

#### Option A — Import par drag & drop (RECOMMANDÉE)

1. Une fois connectée, aller sur [vercel.com/new](https://vercel.com/new)
2. Cliquer sur l'onglet **"Templates"** puis remonter en haut et trouver le bouton **"Browse Templates"** ou cliquer **"Other"** → **"Static Site"**
3. **Si Vercel ne propose pas le drag & drop directement** (la fonctionnalité a évolué), passer à l'Option B ci-dessous

#### Option B — Via Netlify Drop (alternative plus simple)

Honnêtement, Netlify a un drag & drop plus simple que Vercel pour un premier site statique. Recommandé pour démarrer :

1. Aller sur [app.netlify.com/drop](https://app.netlify.com/drop)
2. Glisser-déposer **tout le dossier `deploy-vercel`** dans la zone indiquée
3. Netlify déploie en 30 secondes et vous donne une URL du type `https://abc123.netlify.app`
4. Créer un compte Netlify pour pouvoir gérer le site (renommer, ajouter votre domaine plus tard)

#### Option C — Via GitHub (workflow pro, recommandé à terme)

Voir la **section "Workflow GitHub"** plus bas pour un guide complet.

### Renommer votre site

Une fois déployé, dans le dashboard Vercel ou Netlify, vous pouvez personnaliser l'URL publique :

- Vercel : Settings → Domains → renommer le sous-domaine
- Netlify : Site settings → Change site name

Choisir un nom temporaire facile, par exemple `scenario-prelaunch` → l'URL devient `scenario-prelaunch.netlify.app` ou `scenario-prelaunch.vercel.app`.

---

## Étape 3 — Tester que tout marche (5 min)

1. Ouvrir l'URL publique dans votre navigateur
2. Vérifier que la page s'affiche correctement
3. Cliquer sur **"Voir la démo"** — le mockup doit s'ouvrir
4. Remplir le formulaire **"Particuliers"** avec un faux nom et **votre vrai email**
5. Cliquer "Envoyer"
6. Vérifier que vous recevez l'email dans les minutes qui suivent

⚠ La première soumission de chaque formulaire Formspree demande une **confirmation par email** (anti-spam). Suivez le lien dans l'email reçu.

7. Refaire la même chose avec le formulaire **"Artistes"**

---

## Étape 4 — Personnalisations à faire avant de communiquer

Avant de partager l'URL largement, prendre 30 minutes pour :

### Le nom de marque

Une fois le nom validé avec votre associée, faire un **find & replace** dans `index.html` ET `demo.html` :

- Remplacer `Scenario` (avec majuscule) → votre nom
- Remplacer `scenario` (minuscule, dans `scenario.fr`, `contact@scenario.fr`) → votre nom en minuscule

(Dans VS Code : Cmd+Shift+H ou Ctrl+Shift+H)

Re-déployer après modification (re-drag & drop sur Netlify ou push GitHub).

### Le titre du navigateur

Dans `index.html` ligne 5 (`<title>...</title>`), adapter le titre.

### L'email de contact

Dans le footer d'`index.html`, remplacer `contact@scenario.fr` par votre vraie adresse de contact (peut être votre email pro le temps que vous ayez un nom de domaine).

### Les statistiques du Trust Strip

Dans la section "trust" d'`index.html`, les chiffres `220 000 mariages/an` (Insee, vrai) et `100 % conforme GUSO` sont OK. Mais **`3 200 artistes pré-inscrits`** est faux — vous en avez 0 au lancement. Le remplacer par quelque chose d'honnête, par exemple :

- `+ 50` si vous avez quelques artistes en pré-inscrit
- Ou supprimer cette stat et passer à 3 colonnes au lieu de 4

L'éthique paie en early-stage : un faux "3 200 artistes" qui se découvre, et la confiance s'effondre.

### Le footer (mentions légales)

Avant la mise en ligne large, prévoir :

- Une page Mentions Légales (templates gratuits sur [legalplace.fr](https://www.legalplace.fr) ou [captaincontrat.com](https://www.captaincontrat.com))
- Une politique de confidentialité (templates RGPD chez [cnil.fr](https://www.cnil.fr) ou [tomtisme.fr](https://tomtisme.fr/generateur-rgpd) gratuit)
- Adapter le `SIRET` du footer une fois votre société créée

---

## Étape 5 — Brancher votre nom de domaine (le jour où il est validé)

Quand vous aurez tranché sur le nom avec votre associée :

1. Acheter le domaine sur [Gandi](https://www.gandi.net) ou [OVH](https://www.ovhcloud.com) (~12 €/an pour un `.fr`)
2. Dans Netlify ou Vercel : Settings → Domains → Add Custom Domain
3. Suivre les instructions (ils vous donnent 2 enregistrements DNS à coller chez Gandi/OVH)
4. Le HTTPS est configuré automatiquement en quelques minutes

---

## Maintenance et mesure

### Voir les statistiques de visite

Plan gratuit Vercel ou Netlify intègre des stats basiques. Pour quelque chose de plus complet et RGPD-friendly :

- **Plausible** ([plausible.io](https://plausible.io)) — 9 €/mois, pas de cookies, conforme RGPD nativement
- **Matomo Cloud** ([matomo.org](https://matomo.org)) — alternative française

Ajouter le snippet de tracking dans le `<head>` d'`index.html`, redéployer.

### Modifier la page

À chaque modification d'un fichier, redéployer en re-glissant le dossier sur Netlify Drop (ou en push si vous êtes en mode GitHub).

### Surveiller les leads

Connectez-vous régulièrement à votre dashboard Formspree pour voir les soumissions. Vous pouvez aussi exporter en CSV pour les importer dans un Notion, Airtable ou Google Sheets.

---

## Récapitulatif des coûts

- **Hébergement (Netlify ou Vercel)** : 0 € / mois (plan gratuit suffit)
- **Formspree** : 0 € / mois (jusqu'à 50 leads / mois)
- **Nom de domaine** : ~12 € / an
- **Plausible Analytics** (optionnel) : 9 € / mois

**Total : 12 € pour la première année**, voire 0 € si vous gardez l'URL Netlify/Vercel par défaut.

---

## Configurer le contact WhatsApp

La landing inclut désormais un **bouton flottant WhatsApp** (en bas à droite, apparaît après scroll) et un **lien WhatsApp dans le footer**. Les deux pointent vers `REMPLACER_PAR_VOTRE_NUMERO` qu'il faut remplacer par votre vrai numéro.

### Format du numéro

Le numéro doit être au **format international, sans le `+`, sans espaces, sans tirets**.

| Votre numéro affiché | Format à utiliser |
|---|---|
| 06 12 34 56 78 (France) | `33612345678` |
| 07 89 12 34 56 (France) | `33789123456` |
| +44 7700 900 123 (UK) | `447700900123` |

### Brancher le numéro

Ouvrir `index.html`, faire **Cmd+F (Mac) / Ctrl+F (Windows)** et chercher :

```
REMPLACER_PAR_VOTRE_NUMERO
```

Il apparaît **2 fois** (une fois pour le bouton flottant, une fois pour le lien footer). Remplacer les deux occurrences par votre numéro (par exemple `33612345678`).

Tester en cliquant sur le bouton : WhatsApp doit s'ouvrir (web ou app) avec une conversation pré-remplie vers votre numéro et le message "Bonjour, je viens du site Scenario. J'aimerais en savoir plus."

### Personnaliser le message pré-rempli

Le message pré-rempli est encodé dans l'URL après `?text=`. Pour le modifier :

1. Chercher dans le code les deux occurrences de `?text=Bonjour%2C%20je%20viens%20...`
2. Écrire votre nouveau message en clair (par exemple "Bonjour Scenario, j'ai une question.")
3. Le passer dans un encodeur d'URL : [urlencoder.org](https://www.urlencoder.org), copier le résultat et le coller à la place de l'ancien texte.

### ⚠ Recommandé : utiliser WhatsApp Business

Si le numéro que vous renseignez est votre numéro personnel, vous allez recevoir potentiellement beaucoup de messages mélangés avec vos conversations privées. Solution : créer un compte **WhatsApp Business** (gratuit, application séparée à télécharger).

Avantages de WhatsApp Business :
- Profil pro distinct du perso (logo, description, site web, horaires d'ouverture)
- **Réponses automatiques** : message d'accueil pour les nouveaux contacts, message d'absence en dehors des heures d'ouverture
- **Labels** pour organiser les conversations (Particulier intéressé, Artiste, Suivi, etc.)
- Catalogue produit/service intégré
- Statistiques basiques (messages envoyés/reçus/lus)

Vous pouvez utiliser WhatsApp Business sur **un numéro dédié** (carte SIM Orange/Free à ~5 €/mois, ou numéro virtuel via OnOff, Sonetel, etc.) pour bien séparer.

### Changer la couleur du bouton WhatsApp

Le bouton est par défaut en **vert WhatsApp officiel** (`#25D366`) pour la reconnaissance immédiate des utilisateurs. Si vous préférez le passer en noir cohérent avec la palette éditoriale :

Dans `index.html`, chercher la section `.wa-float` et remplacer :
```css
background: #25D366;
```
par :
```css
background: #0F0F0F;
```

Et dans `:hover` :
```css
background: #1FB855;
```
par :
```css
background: #D44523;
```

Mon conseil de consultant : gardez le vert. La perte d'élégance est minime, le gain en reconnaissance immédiate est réel. C'est exactement ce que font les sites pros (Airbnb, Booking, etc. utilisent le vert officiel).

---

## Workflow GitHub (recommandé à terme)

### Pourquoi passer par GitHub ?

Avec Netlify Drop, à chaque modification du moindre fichier, vous devez re-glisser tout le dossier sur le site. Vite fastidieux.

Avec GitHub, votre code vit dans un **dépôt** (un dossier versionné en ligne). Vercel ou Netlify "regarde" ce dépôt en permanence et **redéploie automatiquement** dès qu'une modification est publiée. Vous gagnez aussi :

- **Un historique de toutes les versions** (vous pouvez revenir en arrière facilement).
- **La possibilité de collaborer** avec votre associée sur le même code, sans s'écraser mutuellement.
- **Un workflow standard** que toute agence ou freelance saura reprendre quand vous passerez à la phase de développement de la vraie plateforme.

Comptez **45 min à 1 heure** la première fois. Une seule fois — après, ce sont des modifs au fil de l'eau.

---

### Étape 1 — Créer un compte GitHub (5 min)

1. Aller sur [github.com](https://github.com) → **"Sign up"**
2. Utiliser votre email pro (`sheila@blaedagency.com`)
3. Choisir un nom d'utilisateur court et propre (par exemple `sheila-blaed` ou `blaedagency`). C'est public, choisissez bien.
4. Le plan **Free** est suffisant — il permet des dépôts publics ET privés en illimité.
5. Confirmer l'email.

---

### Étape 2 — Installer GitHub Desktop (5 min)

GitHub Desktop est une application qui rend Git utilisable sans ligne de commande. Pour un profil non-tech, c'est l'outil le plus accessible.

1. Aller sur [desktop.github.com](https://desktop.github.com) et télécharger l'app (gratuit, Mac ou Windows).
2. Installer puis lancer l'application.
3. Se connecter avec le compte GitHub créé à l'étape précédente.

Alternative pour les courageuses : si vous préférez la ligne de commande, voir le bas de cette section.

---

### Étape 3 — Créer un dépôt et y mettre les fichiers (10 min)

#### Dans GitHub Desktop

1. **File → New Repository**
2. Remplir :
   - **Name** : `scenario-prelaunch` (ou un autre nom court, sans espaces)
   - **Description** : "Landing de pré-lancement Scenario"
   - **Local path** : choisir où le dépôt sera stocké sur votre Mac (par exemple `~/Documents/Code/`)
   - **Initialize this repository with a README** : coché
   - **Git ignore** : laisser "None"
   - **License** : laisser "None"
3. Cliquer **"Create Repository"**
4. GitHub Desktop crée un nouveau dossier vide `scenario-prelaunch/` sur votre Mac.

#### Copier les fichiers de la landing dedans

1. Ouvrir le Finder, naviguer vers le dossier `scenario-prelaunch/` créé.
2. Copier dedans **tous les fichiers** du dossier `deploy-vercel/` que je vous ai préparé :
   - `index.html`
   - `demo.html`
   - `README - Comment mettre en ligne.md`
   - `index-airbnb-style.html.backup` (optionnel — vous pouvez ne pas le copier si vous êtes convaincue par la nouvelle version)
3. Retourner dans GitHub Desktop. Vous devriez voir les fichiers apparaître dans la colonne de gauche, marqués comme "nouveaux".

#### Publier sur GitHub (premier push)

1. En bas à gauche, dans le champ **"Summary"**, écrire un message court décrivant cet ajout. Par exemple : `Initial commit – landing et démo Scenario`.
2. Cliquer **"Commit to main"**.
3. En haut, cliquer **"Publish repository"**.
4. Une fenêtre s'ouvre :
   - Laisser le nom tel quel.
   - **Cocher "Keep this code private"** (vivement recommandé tant que c'est en pré-lancement — vous le rendrez public plus tard si vous voulez).
   - Cliquer **"Publish Repository"**.
5. Vos fichiers sont maintenant sur github.com, dans votre compte, dans un dépôt privé.

---

### Étape 4 — Connecter Vercel (ou Netlify) au dépôt GitHub (10 min)

#### Avec Vercel (recommandé pour le workflow GitHub)

1. Aller sur [vercel.com](https://vercel.com) et créer un compte **avec "Continue with GitHub"** (le plus simple — ça branche tout de suite les deux services).
2. Vercel demande l'autorisation d'accéder à vos repos GitHub. **Accorder l'accès au repo `scenario-prelaunch` uniquement** (vous pouvez choisir "Only select repositories" pour ne pas tout donner).
3. Une fois connectée, cliquer **"Add New… → Project"**.
4. Dans la liste de vos repos, sélectionner `scenario-prelaunch` → **"Import"**.
5. Vercel détecte automatiquement que c'est un site statique. Laisser tous les paramètres par défaut.
6. Cliquer **"Deploy"**.
7. En ~30 secondes, votre site est en ligne. Vercel vous donne une URL du type `scenario-prelaunch-xyz.vercel.app`.

#### Avec Netlify (alternative équivalente)

1. Sur [app.netlify.com](https://app.netlify.com), choisir **"Add new site → Import from Git"**.
2. Connecter votre compte GitHub.
3. Choisir le repo `scenario-prelaunch`.
4. Laisser les paramètres par défaut → **"Deploy site"**.

---

### Étape 5 — Le workflow au quotidien

Voilà la magie : à partir de maintenant, **toute modification que vous faites suit ce cycle** :

1. **Modifier un fichier** dans votre dossier `scenario-prelaunch/` (par exemple corriger une faute dans `index.html`).
2. **Ouvrir GitHub Desktop** : la modif apparaît automatiquement.
3. Écrire un petit message dans **"Summary"** (par exemple `Correction faute dans le hero`).
4. Cliquer **"Commit to main"**.
5. Cliquer **"Push origin"** (en haut).
6. **Vercel ou Netlify redéploie tout seul** dans la minute qui suit. Vous recevez même un email de notification.

Aucun re-upload manuel. Aucune intervention sur l'hébergeur.

---

### Conseils pratiques

- **Faire des commits fréquents** avec des messages clairs. Plus tard, vous pourrez voir d'un coup d'œil ce que vous avez changé et quand.
- **Mode "branches"** : pour les modifications plus risquées (refonte complète d'une section par exemple), GitHub Desktop permet de créer une "branche" — une version parallèle de votre site, que vous fusionnez à la version principale une fois testée. Pas indispensable au début.
- **Sécurité** : ne mettez **JAMAIS** de mots de passe, clés API ou tokens dans des fichiers que vous commitez. Si ça vous arrive, dites-le moi immédiatement — il y a des étapes spécifiques pour les retirer proprement.
- **Collaboration avec votre associée** : invitez-la sur le repo GitHub (**Settings → Collaborators**). Elle installe GitHub Desktop, clone le repo (File → Clone Repository), et vous pouvez travailler à deux dessus.

---

### Pour les courageuses : la ligne de commande

Si vous préférez la CLI au lieu de GitHub Desktop, le workflow équivalent dans un terminal est :

```bash
# Une seule fois, dans le dossier scenario-prelaunch/
git init
git remote add origin https://github.com/votre-pseudo/scenario-prelaunch.git
git add .
git commit -m "Initial commit"
git push -u origin main

# Pour chaque modification ensuite :
git add .
git commit -m "Description courte"
git push
```

Mais honnêtement, GitHub Desktop fait exactement la même chose en cliquant et c'est plus serein quand on débute.

---

## En cas de blocage

Si vous coincez sur une étape, écrivez-moi ce qui bloque exactement (copie d'écran si possible) — la majorité des soucis sont triviaux à débloquer.
