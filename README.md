# ⛳ Tarifs Golf · Laurentides 2026

Comparateur de droits de jeu (18 trous) pour les clubs de golf des Laurentides.
Choisis une **date** et une **heure de départ** : l'app affiche, pour chaque club,
le bon tarif du jour (semaine / vendredi / fin de semaine + fériés) et la bonne
saison (haute, basse…), avec ou sans voiturette.

**[➡️ Ouvrir l'application](https://justsimpleweb1.github.io/golf-tarifs-laurentides/)**
*(le lien deviendra actif une fois GitHub Pages publié — voir plus bas)*

---

## Ce que fait l'app

- **Comparateur** — tableau triable de ~30 parcours sur 25 clubs, filtrable par
  région, voiturette, heure de départ. Le meilleur tarif marcheur est mis en avant.
- **Fiches par club** — la grille tarifaire complète de chaque club (toutes les
  plages horaires, semaine et fin de semaine, par saison).
- **Statistiques** — moyennes, min/max et classement des tarifs pour la date choisie.

Les prix sont saisis manuellement à partir des sites officiels des clubs.
Chaque tarif porte une mention de vérification (✓ vérifié · ~ dynamique · n.d.).

## Comment ça marche techniquement

C'est un **site statique d'un seul fichier** : tout (design, données, logique) est
dans [`index.html`](index.html). Aucun serveur, aucune base de données, aucune
dépendance à installer. Il suffit d'ouvrir le fichier dans un navigateur.

- Les données des clubs vivent dans la constante `CLUBS` (dans la balise `<script>`).
- `TAXF` = facteur de taxes (TPS+TVQ) appliqué aux clubs dont les prix sont hors taxes.
- La saison et le jour-type sont déduits automatiquement de la date choisie.

## Mettre à jour les prix

1. Ouvre `index.html` dans un éditeur.
2. Trouve le club dans la liste `CLUBS` (cherche son nom).
3. Modifie les valeurs `w` (prix marcheur) et `c` (supplément voiturette/pers.).
4. Sauvegarde, puis `git commit` + `git push` — GitHub Pages se met à jour seul.

## Lancer en local

Double-clique simplement sur `index.html`, ou :

```bash
# avec Python (déjà installé sur macOS)
python3 -m http.server 8000
# puis ouvre http://localhost:8000
```

## Publier / mettre à jour en ligne (GitHub Pages)

Une fois le dépôt poussé sur GitHub, active **Settings → Pages → Branch: main**.
Le site est servi à `https://<utilisateur>.github.io/<nom-du-repo>/`.
Chaque `git push` sur `main` met le site à jour automatiquement.

## Structure du projet

```
.
├── index.html        # l'application complète (HTML + CSS + JS + données)
├── README.md         # ce fichier
└── archive/          # anciennes données de référence (non utilisées par l'app)
    └── golfs-data.json
```

---

Construit pour Simon · Just Simple Web.
