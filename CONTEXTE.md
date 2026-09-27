# Qui voit quoi

Ce que l'export des menus TeePee apprend sur le public réel de ces pages, et ce que
ça implique pour les concevoir.

**L'export lui-même n'est pas versionné ici.** C'est une matrice des droits de 33 rôles
sur 473 entrées de menu : le dépôt est public, cette matrice n'a rien à y faire. Seules
les conclusions sont consignées ci-dessous. Fichier source : `Menu_dataExport_1.xlsx`,
à redemander à Bastou quand il faut le reconsulter.

## Les quatre pages sont des pages d'accueil par entité

Dans TeePee, chacune de ces pages est une entrée « Home page » du menu **Aide**, servie
à un ensemble de rôles précis :

| Page | Entrée TeePee | Public |
|---|---|---|
| `index.html` | ORES · Home page | 8 rôles ORES : études, chantier, QHSE, ingénierie, performance PV, supervision, sous-traitance |
| `en.html` | OSI · Home page | 8 rôles OSI : direction projet, HSE site, ingénierie, supervision, sous-traitance |
| `offre.html` | CRM · Home page | 5 rôles ORES : chef d'entreprise, chef de projet, responsable d'activité, responsable projet |
| `rh.html` | RH · Home page | 4 rôles CRE : directeur, gestionnaire RH, responsable RH |

Un rôle n'est pas une personne : un rôle peut couvrir une ou trente personnes. Mais
l'ordre de grandeur est là, et il change la façon de concevoir.

**Ce ne sont pas des pages grand public.** Chacune sert une poignée de profils qui se
ressemblent. Inutile de tout mettre partout : il vaut mieux coller au métier du public
de chaque page.

## La règle qui en découle

Une carte ne se met sur une page que si le public de **cette** page peut l'ouvrir. Une
carte qu'on ne peut pas ouvrir est pire qu'une carte absente : elle fait douter du
reste de la page.

État au moment de l'analyse :

- **`offre.html`** : les neuf cartes sont ouvrables par les cinq rôles du public. Rien
  à corriger.
- **`index.html`** : quatorze cartes sur seize sont ouvrables par au moins six rôles
  sur huit. Deux exceptions, ouvrables par le seul Administrateur :
  - le menu métier **MPA** (5 rôles sur 33, et aucun dans le public de l'accueil)
  - le menu métier **Administration** (1 rôle sur 33)

  Ces deux cartes occupent un quart de la rangée « Menus métier » pour rien.

## Contacts : la question est tranchée

Le formulaire **Contact** existe, mais dans le menu **CRM · Annuaire**, accessible à
**1 rôle sur 33**. Le remettre sur `offre.html` donnerait une carte que quatre des cinq
lecteurs de la page ne peuvent pas ouvrir. **On ne le remet pas.**

Le même menu contient aussi un *Kanban Opportunité* et un *CRM · Compte rendu de
visite*, tous deux à 1 rôle sur 33. Même conclusion.

## Ce que TeePee affiche déjà lui-même

Les listes TeePee portent leur propre compteur, à jour. Au moment de la capture :
accueil sécurité chantier 566, quart d'heure sécurité 289, non-conformités 77.

La page d'accueil annonce « 80 fiches » pour les non-conformités : c'était vrai un
jour, TeePee en compte 77. C'est la démonstration du problème, et la raison de la règle
« pas de chiffre figé » dans `CLAUDE.md`.

## Le rendu réel dans TeePee

La page est affichée dans une iframe, à droite du rail de navigation TeePee, sur une
largeur d'environ **1830 px** sur un écran de 1920. C'est nettement plus large que les
1440 px auxquels on teste d'habitude : les grilles à cinq colonnes respirent, et il
reste de la place.

L'iframe a son propre ascenseur, en plus de celui de TeePee. Sur l'accueil, la rangée
**Menus métier** tombe sous la ligne de flottaison : ce qui y est placé est vu par
ceux qui font l'effort de descendre.

## Les noms officiels diffèrent des nôtres

Nos libellés sont volontairement plus courts que ceux de TeePee. L'écart est assumé,
mais il faut le connaître pour ne pas égarer les gens :

| Notre libellé | Nom TeePee |
|---|---|
| En cours de suivi | Offres · Opportunités en cours de suivi |
| Toutes les opportunités | Offres · Toutes les opportunités |
| Actions commerciales | Offre · Action commerciale |
| Panel clients | Panel clients |
| Enquêtes de satisfaction | MPA 35.1 Enquête de satisfaction client |
| Non-conformités | SM 04.1 · Fiche de traitement d'une non-conformité / Réclamation client |
| Quart d'heures QSE | SM 01.4 · Quart d'heure sécurité / environnement |
| Quart d'heure QSE (Power BI) | SM · Synthèse des quarts d'heures |
| Suivi fiche de contrôle | IN · Suivi des fiches de contrôle qualité |
| Suivi chantier | IN / SM · Suivi chantier |

## Pistes ouvertes par l'export

- **Un tableau de bord qu'on n'affiche pas** : `HA · Panel d'entreprise`, ouvert à 31
  rôles sur 33, le plus largement accessible de tous. Il n'est sur aucune page.
- **`rh.html` est une page recrutement**, bâtie sur le menu `02E2474B`. Le menu
  `RH · Ressources humaines` contient quatre entrées bien plus largement ouvertes :
  demande d'ouverture de poste (17 rôles), parcours d'intégration (22), fiche
  d'évaluation Omexom RE (24), grille d'évaluation de formation (23). Le public de
  `rh.html` étant le service RH, le recrutement se défend, mais ces quatre entrées
  manquent si la page doit servir au-delà.
- Le menu **CRE** et le menu **Suivi ST** existent et ne sont liés nulle part.
