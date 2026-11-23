# VELO SPEED — application Android pour l'AVDL A13

Application **exclusivement Android**, **entièrement en français** (Android 6 à 15, Bluetooth Low Energy).
Coque Kotlin native + interface web locale (WebView) : compteur GPS, trajets, météo, maintenance, et onglet « Mon vélo » (Bluetooth).

## Installer depuis le téléphone, sans PC
1. Crée un compte GitHub gratuit, puis un dépôt **privé** (ex. `velo-speed`).
2. Dans le dépôt : « Add file » → « Upload files » → envoie **tout le contenu** de ce dossier (ou `projet.zip` + `.github/workflows/build.yml`).
3. Onglet **Actions** → « Construire l'APK VELO SPEED » → **Run workflow** (≈ 5 min).
4. Onglet **Releases** → télécharge `VELO-SPEED.apk` → ouvre-le → autorise « sources inconnues » pour ton navigateur.
5. Au premier lancement, accepte les autorisations « Appareils à proximité » et « Localisation ».

## Ce qui est confirmé / non confirmé
| Fonction | État |
|---|---|
| Vitesse par GPS, distance, trajets, GPX/CSV, météo, maintenance, plein écran | Testée (interface, simulateur) — **à valider sur ton téléphone** |
| Scan, connexion, liste des services BLE, lecture, notifications | Code complet, **jamais exécuté sur un vrai A13** |
| Batterie standard BLE (0x180F) | Fonctionne seulement si le vélo l'expose |
| **Vitesse réelle du vélo par Bluetooth** | **NON CONFIRMÉ** : protocole A13 non public. Utiliser l'assistant (onglet Mon vélo → Labo) |
| **Modification des limites de vitesse (niveaux 1–5)** | **NON CONFIRMÉ** : verrouillée tant qu'un profil « confirmé » n'est pas importé |

Rien n'est inventé : aucun identifiant Bluetooth du A13 n'est codé en dur.

Détail de la compatibilité Bluetooth : `docs/COMPATIBILITE_BLE.md` · étude sur la limitation de vitesse : `docs/ETUDE_LIMITATION.md` · analyse des captures : `docs/ANALYSE_CAPTURES.md` · test sur Nothing Phone (1) : `docs/TEST_NOTHING_PHONE.md` · version iPhone (plus tard) : `docs/PLAN_IOS.md`.

## Obtenir la vitesse réelle et les limites
1. Onglet **Mon vélo → Labo** : « Rapport de diagnostic » → partage-le (il liste les services et valeurs du vélo).
2. Assistant : roule en GPS, enregistre, il cherche le champ qui suit ta vitesse GPS.
3. Pour les limites : capture HCI de l'appli officielle YouFs (voir `docs/PROFIL.md`), puis import d'un profil.

## Sécurité et réglementation
Au-delà de **25 km/h** d'assistance, un vélo n'est plus un VAE légal (cyclomoteur : immatriculation, assurance, casque). Usage **uniquement sur terrain privé fermé**. Chaque écriture exige une confirmation explicite, un **mode lecture seule est actif par défaut** (aucune écriture), et une sauvegarde des valeurs avant modification existe (« Restaurer la sauvegarde »), et chaque écriture est relue pour vérification. Tu restes responsable de l'usage.

## État de vérification (2.1.0)
Kotlin **relu, jamais compilé** ; APK **jamais construit ici** ; tests = simulateur JS uniquement. Détails : `docs/AUDIT.md`.

## Compilation
JDK 17, Gradle 8.7, AGP 8.5.2, Kotlin 1.9.24, compileSdk/targetSdk 34, minSdk 23, `applicationId fr.velospeed.a13`. Clé de signature fixe (`app/velo-debug.jks`) : les mises à jour s'installent par-dessus. Clé de test : à remplacer pour toute diffusion publique.
