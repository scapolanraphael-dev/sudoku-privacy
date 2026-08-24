# sudoku-privacy

Politique de confidentialité publique de l'application **Sudoku**
(`com.quarktop.games.sudoku`), servie par GitHub Pages.

Une seule page : [`index.html`](index.html), **bilingue FR/EN**, sélecteur de
langue en haut de page.

La langue est aussi adressable par fragment d'URL — pratique quand l'URL doit
être transmise à quelqu'un qui ne lit pas le français :

- `…/sudoku-privacy/` → français par défaut, anglais si la langue du navigateur
  n'est pas le français
- `…/sudoku-privacy/#en` → anglais
- `…/sudoku-privacy/#fr` → français

Sans JavaScript, les deux versions s'affichent l'une après l'autre plutôt qu'une
seule : une politique de confidentialité doit rester lisible même dégradée.

**Toute modification doit être portée dans les deux langues.** Les deux sections
comptent 12 rubriques identiques ; une divergence entre les deux versions est un
risque juridique, pas une coquille.

## ⚠️ Cette URL ne doit jamais casser

Elle est référencée à trois endroits, et une URL morte casse chacun d'eux :

1. **Play Console** → fiche du magasin, champ « Politique de confidentialité ».
   Une URL inaccessible au moment de la revue = fiche rejetée.
2. **Le formulaire de consentement Google UMP / Appodeal**, affiché au premier
   lancement en EEE/RU. Le message de consentement ne peut pas être certifié sans
   politique accessible — donc plus de publicité personnalisée en Europe.
3. Le lien « Politique de confidentialité » de l'écran Réglages de l'app, si/quand
   il est ajouté.

Conséquences pratiques :

- **ne jamais renommer ni supprimer ce dépôt** — le nom du dépôt est dans l'URL ;
- ne jamais désactiver GitHub Pages dans les réglages du dépôt ;
- garder le dépôt **public**.

## Publier / mettre à jour

Le dépôt est servi tel quel : pousser sur `main` suffit, Pages redéploie en une
minute environ.

```bash
git add -A && git commit -m "docs: mise à jour de la politique de confidentialité" && git push
```

Activation initiale : *Settings → Pages → Source: Deploy from a branch → `main` / `root`*.

## À mettre à jour quand l'app change

La politique doit rester **cohérente avec le formulaire Sécurité des données de
Play** : une fiche qui contredit le formulaire est une infraction, et l'inverse
aussi. Toute divergence est à corriger des deux côtés en même temps.

Repasser sur cette page si :

- une dépendance qui collecte des données est ajoutée ou retirée
  (analytics, crash reporting, backend, achats intégrés…) ;
- le prestataire publicitaire change, ou une médiation tierce est ajoutée
  (voir P3.5 de `docs/roadmap.md` dans le dépôt du jeu) ;
- le libellé du chemin `Réglages → Confidentialité → Préférences publicitaires`
  change dans l'app — il est cité tel quel en section 4 ;
- le public cible déclaré sur Play inclut une tranche d'âge enfant. Ce n'est pas une
  question de classement de contenu (le jeu sortira « Tout public ») mais de régime
  publicitaire : déclarer une audience enfant fait basculer sous **Families Policy**,
  où la publicité personnalisée et l'identifiant publicitaire sont interdits pour les
  moins de 13 ans, et où le kit publicitaire doit être certifié Families — ce
  qu'Appodeal n'est pas. La section 10 deviendrait fausse, le code devrait passer
  `tagForUnderAgeOfConsent: true`, et le chiffrage revenu de la roadmap tomberait.
  **La déclaration « grand public » est le choix retenu.**

Penser à mettre à jour la date de dernière mise à jour, présente **dans les deux
langues**.

## Formulaire « Sécurité des données » de Play : quoi cocher

Vérifié le 2026-08-24 contre la page officielle d'Appodeal
(<https://docs.appodeal.com/android/data-protection/app-privacy-details>) et
recoupé avec la déclaration Google du SDK Mobile Ads
(<https://developers.google.com/admob/android/privacy/play-data-disclosure>).

| Type de donnée | À cocher ? | Pourquoi |
|---|---|---|
| Identifiants d'appareil (AAID) | **Oui** — collecté + partagé | Le SDK tire `com.google.android.gms.permission.AD_ID`, confirmé dans le manifeste fusionné de la build release |
| Interactions dans l'app | **Oui** — collecté + partagé | Affichages, clics, vidéos rewarded |
| Diagnostics | **Oui** — collecté | Erreurs du kit publicitaire |
| Autres performances de l'app | **Oui** — collecté | Signaux techniques appareil |
| **Localisation** (approx. ou précise) | **Non** | Appodeal ne la collecte que si l'app détient une autorisation de localisation. L'app n'en déclare aucune — vérifié dans le manifeste fusionné : seules `VIBRATE`, `POST_NOTIFICATIONS`, `RECEIVE_BOOT_COMPLETED`, plus `INTERNET` / `ACCESS_NETWORK_STATE` / `ACCESS_WIFI_STATE` / `AD_ID` ajoutées par le SDK. La localisation grossière déduite de l'IP ne relève pas de cette catégorie chez Google (l'IP est traitée à part) |
| **Identifiants utilisateur** | **Non** | Uniquement si `Appodeal.setUserId()` est appelé. Absent du code |
| **Historique d'achat** | **Non** | Uniquement si l'app transmet des achats au SDK. Pas d'achats intégrés |

À revérifier si l'une de ces trois dernières lignes change (ajout d'achats
intégrés, d'un identifiant joueur, ou d'une fonctionnalité géolocalisée).

⚠️ La page d'Appodeal précise qu'elle **ne couvre que son propre SDK** : chaque
réseau publicitaire activé dans le tableau de bord Appodeal a sa propre
déclaration. À reprendre le jour où des réseaux sont activés côté dashboard.

Deux réponses du formulaire restent à confirmer auprès d'Appodeal, non
documentées sur leur page : le chiffrement en transit, et le mécanisme de
demande de suppression. (Google déclare TLS pour son propre SDK ; ne pas le
supposer pour Appodeal sans vérification.)
