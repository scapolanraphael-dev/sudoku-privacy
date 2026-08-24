# sudoku-privacy

Politique de confidentialité publique de l'application **Sudoku**
(`com.quarktop.games.sudoku`), servie par GitHub Pages.

**Deux pages statiques**, une par langue, sans une ligne de JavaScript :

| Fichier | URL | Langue |
|---|---|---|
| [`index.html`](index.html) | `…/sudoku-privacy/` | Français |
| [`en/index.html`](en/index.html) | `…/sudoku-privacy/en/` | English |
| [`style.css`](style.css) | — | feuille de style partagée |

Chaque page porte un lien vers l'autre en haut, et les deux se déclarent
mutuellement via `<link rel="alternate" hreflang>`.

**Pourquoi deux pages et pas une bascule JavaScript** : la première version
utilisait un sélecteur de langue en JS. Il suffit que les scripts ne tournent pas
— capture statique, navigateur restrictif, extension de blocage, impression
papier, lecteur d'écran mal luné — pour qu'une des deux langues devienne
inatteignable. Sur un document qui a une valeur juridique et que Google peut
examiner, c'est un risque gratuit. Deux URL réelles reliées par un `<a href>` ne
peuvent pas tomber en panne. **Ne pas réintroduire de JavaScript ici.**

**Toute modification doit être portée dans les deux pages.** Elles comptent 12
rubriques identiques ; une divergence entre les deux versions n'est pas une
coquille, ce sont deux engagements différents pris envers deux publics.

## ⚠️ Cette URL ne doit jamais casser

L'URL de référence est **<https://scapolanraphael-dev.github.io/sudoku-privacy/>**
(pas de domaine personnalisé — voir « Migrer vers un domaine » plus bas).

Elle est référencée à trois endroits, et une URL morte casse chacun d'eux :

1. **Play Console** → fiche du magasin, champ « Politique de confidentialité ».
   Une URL inaccessible au moment de la revue = fiche rejetée. Y mettre l'URL
   racine (française) : elle porte le lien vers l'anglais.
2. **Le formulaire de consentement Google UMP / Appodeal**, affiché au premier
   lancement en EEE/RU. Le message de consentement ne peut pas être certifié sans
   politique accessible — donc plus de publicité personnalisée en Europe.
3. Le lien « Politique de confidentialité » de l'écran Réglages de l'app, si/quand
   il est ajouté.

Conséquences pratiques :

- **ne jamais renommer ni supprimer ce dépôt** — le nom du dépôt est dans l'URL ;
- ne jamais désactiver GitHub Pages dans les réglages du dépôt ;
- garder le dépôt **public** ;
- **ne rien mettre dans `CNAME` qui ne soit pas un domaine réel et possédé.**
  Déjà arrivé une fois : le fichier a contenu `quarktop.games.support`, la partie
  gauche d'une adresse e-mail. Pages l'a lu comme un domaine personnalisé et a
  redirigé l'URL ci-dessus vers un hôte inexistant — la politique n'était plus
  servie nulle part, sans le moindre message d'erreur côté GitHub.

## Publier / mettre à jour

Le dépôt est servi tel quel : pousser sur `main` suffit, Pages redéploie en une
minute environ.

```bash
git add -A && git commit -m "docs: mise à jour de la politique de confidentialité" && git push
```

Activation initiale : *Settings → Pages → Source: Deploy from a branch → `main` / `root`*.

## Migrer vers un domaine personnalisé (plus tard, si l'envie vient)

Rien ne presse : Google ne fait aucune différence entre un `github.io` et un
domaine propre, du moment que la page est publique, stable et en HTTPS. Mais la
migration est prévue pour, et elle ne casse pas les liens déjà déposés :
poser le domaine dans `CNAME` + les enregistrements DNS chez le registrar suffit,
et GitHub redirige l'ancienne URL vers la nouvelle.

Trois choses à ne pas oublier ce jour-là :

1. **Ne pas le faire pendant une revue Play en cours.** GitHub ne provisionne le
   certificat HTTPS qu'après la propagation DNS — de quelques minutes à quelques
   heures. Pendant cette fenêtre l'URL en `https://` peut échouer, et Play comme
   UMP exigent HTTPS. Attendre « Enforce HTTPS » dans *Settings → Pages* avant de
   considérer la migration comme faite.
2. **Corriger les URL codées en dur.** Les balises `<link rel="alternate"
   hreflang>` de [`index.html`](index.html) et [`en/index.html`](en/index.html)
   citent explicitement `scapolanraphael-dev.github.io`. La redirection les
   laisserait fonctionnelles mais fausses — trois occurrences par page.
3. **Mettre à jour les trois inscriptions** listées plus haut (Play Console,
   message de consentement, lien dans les Réglages de l'app). La redirection les
   sauve, mais faire dépendre un document légal d'une redirection est une dette.

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
