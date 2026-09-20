# Compiler l'APK Gestion TELEMA — sans installer Android Studio

Ce dossier fait compiler l'application par les serveurs gratuits de GitHub
(GitHub Actions) au lieu de votre ordinateur. Vous n'installez rien de
lourd — seulement, éventuellement, un petit logiciel gratuit pour envoyer
les fichiers.

Cinq étapes, environ 15 minutes au total (dont 5 minutes d'attente pendant
la compilation).

---

## Étape 1 — Créer un compte GitHub (gratuit)

Aller sur https://github.com et créer un compte si vous n'en avez pas déjà un.

## Étape 2 — Créer un nouveau dépôt (repository)

Une fois connecté, cliquer sur le bouton **New** (ou **+** en haut à
droite → **New repository**). Lui donner un nom, par exemple
`telema-android`. Laisser les autres options par défaut, puis
**Create repository**.

## Étape 3 — Envoyer les fichiers de ce dossier

Deux façons de faire, choisissez celle qui vous convient :

**Option A — la plus simple, sans rien installer**
Sur la page du dépôt fraîchement créé, cliquer sur **uploading an existing
file** (ou **Add file → Upload files**). Faire glisser TOUT le contenu de
ce dossier `android-ci` (les fichiers ET les dossiers `.github`, `www`,
`resources`) dans la zone d'envoi. Vérifier que la structure des dossiers
est conservée, puis cliquer **Commit changes**.

**Option B — avec GitHub Desktop (pratique si vous devez le refaire souvent)**
Installer GitHub Desktop (https://desktop.github.com), gratuit. Ajouter ce
dossier comme dépôt local, puis **Publish repository**.

## Étape 4 — Laisser GitHub compiler

Dès que les fichiers sont envoyés, GitHub démarre automatiquement la
compilation. Pour la suivre : onglet **Actions** en haut de la page du
dépôt. Une ligne « Compiler l'APK Gestion TELEMA » apparaît avec un rond
orange (en cours) puis vert (terminé) — cela prend 4 à 6 minutes.

Si rien ne démarre tout seul, ouvrir l'onglet **Actions**, cliquer sur le
workflow dans la liste de gauche, puis le bouton **Run workflow**.

## Étape 5 — Télécharger l'APK

Une fois le rond vert affiché, cliquer sur cette exécution du workflow.
Tout en bas de la page, dans la section **Artifacts**, se trouve
**Gestion-TELEMA-APK** : cliquer pour le télécharger. C'est un fichier zip
contenant `app-debug.apk` — l'extraire.

Transférer ensuite cet APK sur un téléphone Android (câble, Bluetooth,
Google Drive…) et l'ouvrir depuis l'application Fichiers pour l'installer.
Android demandera d'autoriser « l'installation d'applications inconnues »
pour l'application utilisée pour l'ouvrir — c'est normal pour un APK qui
ne vient pas du Play Store.

---

## Que fait exactement le fichier de compilation

Le fichier `.github/workflows/build-apk.yml` demande à GitHub, à chaque
envoi de fichiers :
1. d'installer Node.js, Java et le kit de développement Android ;
2. de générer le projet Android autour du logiciel (`www/index.html`) ;
3. de s'assurer que la permission internet est présente (indispensable à
   la synchronisation avec la base centrale — ne jamais la retirer) ;
4. d'embarquer le moteur de synchronisation dans l'application, pour
   qu'elle démarre et fonctionne aussi sans internet ;
5. de compiler l'APK et de le déposer en téléchargement.

## Mettre à jour le logiciel plus tard

Remplacer `www/index.html` par la nouvelle version, renvoyer les fichiers
(étape 3), et refaire l'étape 5 pour récupérer le nouvel APK.

## Pour une version définitive, signée, à diffuser largement

L'APK produit ici est une version « debug », parfaite pour équiper les
téléphones du diocèse directement. Si vous voulez un jour la déposer sur
le Play Store ou la signer officiellement, cela se fait ensuite avec
Android Studio, sur un poste connecté — la conversation précédente
explique cette étape (dossier `kit/android` déjà fourni).
