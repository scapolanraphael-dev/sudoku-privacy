# sudoku-privacy

Politique de confidentialité publique de l'application **Sudoku**
(`com.quarktop.games.sudoku`), servie par GitHub Pages.

Une seule page : [`index.html`](index.html), bilingue FR/EN.

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
- le public cible déclaré sur Play inclut une tranche d'âge enfant : la section 10
  devient fausse, et le code doit alors passer `tagForUnderAgeOfConsent: true`.

Penser à mettre à jour la date de dernière mise à jour, présente **dans les deux
langues**.

## Point à vérifier avant la toute première publication

La liste des données de la section 3 décrit ce que collecte un intermédiaire
publicitaire de ce type. Avant de publier, la confronter à la documentation
« Data Safety » d'Appodeal elle-même, qui fait foi — la configuration retenue
(Appodeal seul, `core` + `iab`, sans médiation tierce) est plus étroite que leur
cas générique.
