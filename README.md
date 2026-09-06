# DashboardTeepee

Pages HTML statiques affichées dans **TeePee**, l'intranet Omexom. Chaque page est
autonome (HTML + CSS + polices, aucune dépendance, aucun build) et est intégrée dans
TeePee via son URL de publication GitHub Pages.

## Pages

| Fichier | Rôle | URL publiée |
|---|---|---|
| `index.html` | Accueil TeePee — Omexom Vincennes Nagi | https://omxbv.github.io/DashboardTeepee/ |
| `en.html` | Home TeePee — Omexom International | https://omxbv.github.io/DashboardTeepee/en.html |
| `offre.html` | Offre & Projet · Omexom Teepee | https://omxbv.github.io/DashboardTeepee/offre.html |
| `rh.html` | Ressources humaines · Omexom Teepee | https://omxbv.github.io/DashboardTeepee/rh.html |

## Publication

Le site est servi par GitHub Pages depuis la branche `main`, à la racine du dépôt.
Tout commit poussé sur `main` est mis en ligne automatiquement en une à deux minutes.

**Ces URL sont utilisées en production dans TeePee.** Renommer un fichier, renommer le
dépôt ou changer la branche de publication casse l'affichage côté intranet.

## Modifier une page

Aucun outillage nécessaire : les fichiers s'ouvrent directement dans un navigateur.

```bash
git clone https://github.com/OMXBV/DashboardTeepee.git
cd DashboardTeepee
# ouvrir index.html dans un navigateur, éditer, vérifier
git commit -am "..." && git push
```

Les styles sont en `<style>` dans chaque page, les couleurs passent par des variables CSS
déclarées sur `:root` en haut de fichier.

## Confidentialité

Ces pages affichent des données d'exploitation Omexom : chantiers en cours et leurs
puissances, responsables affectés, volumétrie du plan d'action et des non-conformités,
et des liens profonds vers l'application interne `safeplace.teepee.fr`.

Le dépôt étant public, **ces informations sont lisibles par toute personne connaissant
l'URL**. Les quatre pages portent un `noindex, nofollow, noarchive` et un `robots.txt`
interdit l'exploration : les moteurs de recherche sont écartés, mais ce n'est pas un
contrôle d'accès.

Avant d'ajouter une donnée à ces pages, se demander si elle peut être lue par quelqu'un
d'extérieur au groupe.

## Polices

Les fichiers `vinci_sans_*.woff2` sont la police d'entreprise **Vinci Sans**, propriété du
groupe VINCI. Elles sont présentes uniquement pour le rendu des pages ci-dessus.

Elles ne sont couvertes par aucune licence de réutilisation : elles ne peuvent être ni
extraites, ni redistribuées, ni employées dans un autre projet, interne ou externe.

Elles sont sous-ensemblées au latin étendu (729 glyphes, kerning et `ss02` conservés) et
livrées en WOFF2 — 396 Ko au lieu de 1,3 Mo en TTF. `index.html` les embarque en base64
pour rester autonome ; `en.html`, `offre.html` et `rh.html` les chargent en externe.

Pour régénérer après une mise à jour de la police :

```bash
pip install fonttools brotli
pyftsubset vinci_sans_regular.ttf --output-file=vinci_sans_regular.woff2 \
  --flavor=woff2 --layout-features='*' --name-IDs='*' \
  --unicodes=U+0020-024F,U+0259,U+02B0-02FF,U+0300-036F,U+1E00-1EFF,U+2000-206F,\
U+2070-209F,U+20A0-20CF,U+2100-214F,U+2190-21FF,U+2200-22FF,U+2C60-2C7F,U+A720-A7FF
```

## Conditions

Contenu, marques et identité visuelle Omexom / VINCI Energies — tous droits réservés.
Dépôt public pour les seuls besoins de la publication GitHub Pages ci-dessus.
