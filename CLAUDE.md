# Règles de travail sur ce dépôt

Pages HTML statiques affichées dans TeePee, l'intranet Omexom. Le `README.md` décrit
le dépôt et la publication, ce fichier décrit la façon de travailler dessus.

Rangement : les pages HTML, `omexom.css` et `robots.txt` restent à la racine, car leurs
URL sont celles de la production. La doc est dans `docs/`, les polices dans `polices/`
(les sources TTF dans `polices/source/`), les images dans `img/`.

## Les liens TeePee passent par docs/LIENS.md

`docs/LIENS.md` est la **source de vérité** de tous les liens vers `safeplace.teepee.fr`.

- Un lien ajouté ou remplacé se reporte dans `docs/LIENS.md` **dans le même commit** que la
  page modifiée. Pas de mise à jour différée.
- Un remplacement se note aussi dans la section « Historique des remplacements », avec
  l'ancien et le nouvel identifiant. Ces identifiants changent sans prévenir côté
  TeePee et cassent les pages en silence : l'historique sert à reconnaître le motif.
- Quand un lien manque, il se note dans « Liens manquants » plutôt que d'être deviné.
  **Ne jamais fabriquer une URL TeePee par déduction.** Un lien mort en production est
  pire qu'une carte absente.
- Avant de retirer une carte, vérifier dans `docs/LIENS.md` si son lien sert ailleurs.

## `main` est la production

- `main` est publié automatiquement par GitHub Pages et **affiché en production dans
  l'intranet**. Tout commit sur `main` est en ligne en une à deux minutes.
- Le travail se fait sur une branche à part. Rien ne part sur `main` sans un feu vert
  explicite de Bastou, demandé en une ligne. La V2 a été mise en ligne le 2026-09-28
  et sa branche `claude/v2` n'a plus lieu d'être.
- Exception : un lien mort en production se corrige tout de suite, et on le dit.

## Une carte doit être ouvrable par le public de sa page

`docs/CONTEXTE.md` dit qui voit chaque page et ce que ce public a le droit d'ouvrir dans
TeePee. Chaque page sert une poignée de rôles, pas tout le monde : une carte que son
lecteur ne peut pas ouvrir est pire qu'une carte absente, elle fait douter du reste.

Avant d'ajouter ou de déplacer une carte, vérifier là-bas. L'export des droits n'est
pas dans le dépôt, il est à redemander à Bastou.

## Écriture

- **Pas de tirets cadratins ni demi-cadratins** (`—`, `–`), nulle part : pages, doc,
  messages de commit. Utiliser le point médian `·`, une virgule, ou reformuler.
- Les pages et la doc sont en français, accents compris. Les messages de commit sont
  en français sans accents.
- Pas de chiffre figé dans une page. « 407 actions », « 9 chantiers actifs » : ces
  compteurs écrits en dur deviennent faux et abîment la confiance dans le reste de la
  page. Préférer un libellé qualitatif.

## Contraintes techniques

- Aucun build, aucune dépendance : chaque page s'ouvre directement dans un navigateur.
- Les liens vers TeePee portent `target="_parent"`, les pages étant affichées dans une
  iframe de l'intranet.
- Le dépôt est **public**. Avant d'ajouter une donnée d'exploitation, se demander si
  elle peut être lue par quelqu'un d'extérieur au groupe.
- Les polices Vinci Sans sont propriété VINCI, présentes pour le seul rendu de ces
  pages. Ne pas les réutiliser ailleurs.

## Vérifier avant de livrer

Contrôler l'équilibre des balises et l'absence de tirets cadratins :

```bash
python3 -c "
import html.parser,sys
class P(html.parser.HTMLParser):
    def __init__(self):
        super().__init__(); self.stack=[]; self.void={'meta','link','br','img','hr','input','source'}
    def handle_starttag(self,t,a):
        if t not in self.void: self.stack.append(t)
    def handle_startendtag(self,t,a): pass   # les balises SVG auto-fermantes
    def handle_endtag(self,t):
        if not self.stack or self.stack[-1]!=t: print('MISMATCH',t,self.stack[-4:]); sys.exit(1)
        self.stack.pop()
for f in sys.argv[1:]:
    p=P(); p.feed(open(f,encoding='utf-8').read()); print(f,'non fermees:',p.stack)
" *.html
grep -n '—\|–' *.html
```

Voir le rendu réel plutôt que le supposer :

```bash
/opt/pw-browsers/chromium-1194/chrome-linux/chrome --headless --no-sandbox --disable-gpu \
  --hide-scrollbars --window-size=1440,900 --screenshot=/tmp/page.png \
  --virtual-time-budget=3000 file://$PWD/offre.html
```

## Le style vit dans omexom.css

`omexom.css` porte les polices, les jetons de couleur et tous les composants partagés
par au moins deux pages. Toutes les pages le chargent. **Un composant se modifie là,
une seule fois**, et le changement vaut pour tout le monde.

Ce qui reste dans la balise `<style>` de chaque page : le nombre de colonnes de ses
grilles et ses points de rupture, qui lui sont propres. Rien d'autre n'a vocation à y
rester. Si une règle ajoutée dans une page se met à servir ailleurs, elle remonte dans
la feuille commune.

Les cartes projet restent dupliquées entre `index.html` et `offre.html` cote HTML :
modifier l'une demande encore la même dans l'autre.

Après une modification de `omexom.css`, vérifier toutes les pages, pas seulement celle
sur laquelle on travaillait.

## Les pictogrammes sont maison

Pas d'emoji dans les pages. Les pictogrammes sont des SVG en traits, dessinés à la
main, posés en ligne dans le HTML : 24 par 24, `fill="none"`, `stroke="currentColor"`,
épaisseur 1.8, bouts et jointures ronds. Ils prennent la couleur de leur support, fixée
par la classe de la carte dans `omexom.css`.

En ligne et non dans un fichier séparé, parce qu'un sprite SVG externe appelé par
`<use>` est bloqué par le navigateur en `file://` : la page ne s'ouvrirait plus
directement. Le coût est quelques centaines d'octets par pictogramme.
