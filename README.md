# ⛳ Tarifs Golf · Laurentides 2026

Comparateur de droits de jeu (18 trous) pour les clubs de golf des Laurentides.
Choisis une **date** et une **heure de départ** : l'app affiche, pour chaque club,
le bon tarif du jour (semaine / vendredi / fin de semaine + fériés) et la bonne
saison (haute, basse…), avec ou sans voiturette.

**[➡️ Ouvrir l'application](https://justsimpleweb1.github.io/golf-tarifs-laurentides/)**
*(le lien deviendra actif une fois GitHub Pages publié — voir plus bas)*

---

## Ce que fait l'app

- **Comparateur** — tableau triable de ~31 parcours sur 26 clubs, filtrable par
  région, voiturette, heure de départ et **format de parcours (18 ou 9 trous)**.
  Le meilleur tarif marcheur est mis en avant. Un badge indique le format réel de
  chaque parcours (18, 9, 13, 9×2, 27). En mode 9 trous, les clubs qui n'offrent
  pas de 9 trous sont grisés.
- **Club de golf** — choisis un club et vois toute son information au même endroit :
  saisons (haute/basse), politique et prix de la voiturette, statut des taxes, bouton vers
  la page de réservation/tarifs du club et téléphone (à gauche), plus la **grille tarifaire
  complète** 18 et 9 trous (à droite sur desktop, en dessous sur mobile).
- **Statistiques** — moyennes, min/max et classement des tarifs pour la date choisie.
- **Carte** — tous les clubs sur une carte interactive (Leaflet + OpenStreetMap) ; clique
  un marqueur pour le tarif et le lien de réservation.

Les prix sont saisis manuellement à partir des sites officiels des clubs.
Chaque tarif porte une mention de vérification (✓ vérifié · ~ dynamique · n.d.).

## Comment ça marche techniquement

C'est un **site statique** : l'interface et la logique sont dans [`index.html`](index.html),
et **toutes les données des golfs sont dans [`golfs.json`](golfs.json)**. Aucun serveur
applicatif, aucune base de données, aucune dépendance à installer. L'app charge `golfs.json`
au démarrage (via `fetch`). Cette séparation prépare un éventuel CMS futur : il suffira
qu'il produise ce même `golfs.json`.

Structure de `golfs.json` :
- `clubs` — liste des parcours. Chaque club : `n` (nom), `t` (ville), `tax`, grilles
  `sem`/`ven`/`fds` (slots `{s,l,w,c,wc}`), `seasons`/`lo` (saisons), `cartIncl`, `badges`, `note`.
- `club_meta` — par nom de club : `tel`, `url` (réservation), `lat`, `lng` (carte).
- `club9` — par nom de club : `holes` (format), `g9` (grille 9 trous). Pas de `g9` = pas de 9 trous.

Côté code : `TAXF` = facteur de taxes (TPS+TVQ) ; la saison et le jour-type se déduisent de
la date ; la carte utilise [Leaflet](https://leafletjs.com/) via CDN (pas de clé API).

## Mettre à jour les prix / ajouter un terrain

1. Ouvre **`golfs.json`** (et non `index.html`).
2. Pour un prix : trouve le club dans `clubs`, modifie `w` (marcheur) / `c` (supplément voiturette).
3. Pour un lien, un téléphone ou une position carte : modifie son entrée dans `club_meta`.
4. Pour ajouter un terrain : ajoute une entrée dans `clubs` (+ `club_meta` et `club9` au besoin).
5. Sauvegarde, puis `git commit` + `git push` — GitHub Pages se met à jour seul.

> Remarque : comme les données sont dans un fichier séparé, l'app doit être servie par un
> serveur (GitHub Pages le fait ; en local utilise `python3 -m http.server`). Double-cliquer
> `index.html` ne suffit plus.

## Lancer en local

L'app charge `golfs.json`, il faut donc un petit serveur (le double-clic ne marche plus) :

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
├── index.html        # l'application (HTML + CSS + JS) — charge golfs.json
├── golfs.json        # TOUTES les données des golfs (à éditer pour mettre à jour)
├── README.md         # ce fichier
└── archive/          # anciennes données de référence (non utilisées par l'app)
    └── golfs-data.json
```

---

Construit pour Simon · Just Simple Web.
