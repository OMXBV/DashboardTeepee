# Règles de travail sur ce dépôt

Pages HTML statiques affichées dans TeePee, l'intranet Omexom. Le `README.md` décrit
le dépôt et la publication, ce fichier décrit la façon de travailler dessus.

## Les liens TeePee passent par LIENS.md

`LIENS.md` est la **source de vérité** de tous les liens vers `safeplace.teepee.fr`.

- Un lien ajouté ou remplacé se reporte dans `LIENS.md` **dans le même commit** que la
  page modifiée. Pas de mise à jour différée.
- Un remplacement se note aussi dans la section « Historique des remplacements », avec
  l'ancien et le nouvel identifiant. Ces identifiants changent sans prévenir côté
  TeePee et cassent les pages en silence : l'historique sert à reconnaître le motif.
- Quand un lien manque, il se note dans « Liens manquants » plutôt que d'être deviné.
  **Ne jamais fabriquer une URL TeePee par déduction.** Un lien mort en production est
  pire qu'une carte absente.
- Avant de retirer une carte, vérifier dans `LIENS.md` si son lien sert ailleurs.

## La V2 se développe sur `claude/v2`

- `main` est publié automatiquement par GitHub Pages et **affiché en production dans
  l'intranet**. Tout commit sur `main` est en ligne en une à deux minutes.
- Le travail de V2 reste sur `claude/v2`. Rien ne part sur `main` sans un feu vert
  explicite de Bastou, demandé en une ligne.
- Exception : un lien mort en production se corrige tout de suite, et on le dit.

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
    def handle_endtag(self,t):
        if not self.stack or self.stack[-1]!=t: print('MISMATCH',t,self.stack[-4:]); sys.exit(1)
        self.stack.pop()
p=P(); p.feed(open('offre.html',encoding='utf-8').read()); print('non fermees:',p.stack)
"
grep -n '—\|–' *.html
```

Voir le rendu réel plutôt que le supposer :

```bash
/opt/pw-browsers/chromium-1194/chrome-linux/chrome --headless --no-sandbox --disable-gpu \
  --hide-scrollbars --window-size=1440,900 --screenshot=/tmp/page.png \
  --virtual-time-budget=3000 file://$PWD/offre.html
```

`index.html` porte un `</div>` en trop, antérieur à ces règles : le contrôle de balises
échoue dessus tant qu'il n'est pas nettoyé.

## Cohérence entre les pages

Les pages FR partagent la même direction artistique. Un composant modifié doit l'être
partout où il apparaît, sinon les pages divergent. Aujourd'hui le même CSS est recopié
dans chaque fichier, et les cartes projet sont dupliquées entre `index.html` et
`offre.html` : toute modification de l'un demande la même dans l'autre.
