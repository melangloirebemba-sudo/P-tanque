# Cochonnet d'Or

Jeu de pétanque - **by L'insomniaque**.
Application Android construite avec **Capacitor**, et APK fabriqué automatiquement par **GitHub Actions**.

## Contenu du dossier

| Élément | Rôle |
|---|---|
| `www/index.html` | Le jeu complet (s'ouvre aussi dans un navigateur pour tester) |
| `www/fonts/` | Les polices du jeu, intégrées pour fonctionner hors ligne |
| `www/icon.png` | Icône pour la version web |
| `resources/` | Icône et écran de démarrage de l'application (images sources) |
| `capacitor.config.json` | Nom de l'appli, identifiant, réglages de l'écran de démarrage |
| `package.json` | Les outils Capacitor utilisés |
| `.github/workflows/build-apk.yml` | La recette qui construit l'APK sur GitHub |

## Obtenir l'APK en 4 étapes

1. **Créez un dépôt** sur github.com, par exemple `cochonnet-dor`.
2. **Envoyez tout le contenu de ce dossier** dans le dépôt, sur la branche `main`.
   Sur le site GitHub : *Add file → Upload files*, puis glissez les fichiers.
   ⚠️ Vérifiez que le fichier `.github/workflows/build-apk.yml` est bien arrivé. Certains ordinateurs cachent
   les dossiers qui commencent par un point. S'il manque, créez-le avec *Add file → Create new file*
   en tapant le chemin `.github/workflows/build-apk.yml` et en collant son contenu.
3. **Onglet « Actions »** : la construction démarre toute seule (environ 5 à 10 minutes).
   Vous pouvez aussi la lancer à la main avec *Construire l'APK → Run workflow*.
4. **Téléchargez l'APK** : ouvrez la construction terminée (coche verte), en bas de la page,
   section *Artifacts*, téléchargez `cochonnet-dor-apk`. C'est un zip qui contient `app-debug.apk`.
   Copiez-le sur le téléphone et ouvrez-le pour l'installer (autorisez l'installation
   depuis des sources inconnues si Android le demande).

## Mettre le jeu à jour

Remplacez `www/index.html` par la nouvelle version et envoyez-la sur GitHub :
un nouvel APK est construit automatiquement. Pour changer l'icône ou l'écran de démarrage,
remplacez les images du dossier `resources/` (mêmes noms, mêmes tailles).

## Tester sans téléphone

Ouvrez simplement `www/index.html` dans un navigateur (Chrome, Edge, Safari…).

## Construire sur son ordinateur (facultatif)

Il faut Node.js 22, Java 21 et le SDK Android (Android Studio) :

```bash
npm install
npx cap add android
npx capacitor-assets generate --android
npx cap sync android
cd android && ./gradlew assembleDebug
```

L'APK se trouve ensuite dans `android/app/build/outputs/apk/debug/`.

## Bon à savoir

- L'APK produit est une version **de test** (« debug ») : parfaite pour l'installer soi-même et la partager.
  Pour publier sur le **Play Store**, il faut une version **signée** avec une clé personnelle :
  cela s'ajoute au workflow avec des secrets GitHub, le moment venu.
- Identifiant de l'application : `com.linsomniaque.cochonnetdor`. Ne le changez plus une fois l'appli publiée.
- Le bouton retour du téléphone met le jeu en pause, revient à l'écran précédent, ou quitte depuis l'accueil.
- Polices : Lilita One et Nunito, sous licence SIL Open Font License (voir `www/fonts/`).
