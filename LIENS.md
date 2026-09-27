# Liens TeePee

Ce fichier est la **source de vérité** des liens vers `safeplace.teepee.fr` utilisés
dans les pages du dépôt. Toute page publiée doit pointer vers une URL présente ici.

Quand un lien est ajouté ou remplacé, on met ce fichier à jour **dans le même commit**
que la page concernée. Un lien qui ne figure pas ici n'a rien à faire dans une page.

## Comment lire une URL TeePee

```
https://safeplace.teepee.fr/#/category/32DB80F2/50F618EA/dataList/CRMOpportunite/default_CRMOpportunite
                              |        |        |        |        |                |
                              |        |        |        |        |                filtre ou vue
                              |        |        |        |        formulaire
                              |        |        |        type d'affichage
                              |        |        sous-catégorie
                              |        catégorie racine (le menu)
                              type de route
```

Quatre routes existent :

- `#/category/<menu>` : un menu complet
- `#/category/<menu>/<sous-cat>/dataList/<formulaire>/<vue>` : une liste
- `#/viewData/<menu>/<sous-cat>/<formulaire>/<vue>/<GUID>?context=<GUID>` : une fiche
- `#/viewData/<menu>/<sous-cat>/<formulaire>/<vue>` : une saisie vierge. C'est
  l'absence du GUID de fiche qui la distingue, et le `?context=` est facultatif
- `#/homepage/view/<id>` : un rapport Power BI
- `#/home/view/<id>` : une page d'accueil TeePee, celle qui porte l'iframe

## Ce que l'URL ne porte pas

Relevé dans TeePee le 2026-09-27, sur la liste Actions commerciales.

**La recherche, le tri et le filtrage ne passent pas dans l'URL.** Ils restent dans
l'état de l'application. Impossible donc de fabriquer un lien vers une liste
pré-filtrée en bricolant l'adresse.

Le seul filtrage partageable est le **dernier segment**, qui est le nom d'une vue
définie dans TeePee : `default_CRMOpportunite` contre `CRMOpportuniteEnCours`. Pour
obtenir un lien filtré, il faut donc créer la vue côté TeePee puis pointer sur son
nom. C'est du paramétrage TeePee, pas du HTML.

**Le raccourci de saisie fonctionne.** Vérifié le 2026-09-27 : ouvrir la route sans
`?context=` ouvre bien une saisie vierge, TeePee génère le contexte lui-même. Un lien
de création directe est donc constructible pour n'importe quel formulaire, en reprenant
l'URL de sa liste et en remplaçant `category` par `viewData` et `dataList/` par rien :

```
liste    #/category/32DB80F2/36086F3F/dataList/CRMActionCommerciale/default_CRMActionCommerciale
saisie   #/viewData/32DB80F2/36086F3F/CRMActionCommerciale/CRMActionCommerciale
```

Attention : le dernier segment de la saisie est le nom de la **vue du formulaire**, qui
n'est pas toujours celui du filtre de la liste. À vérifier formulaire par formulaire.

**Le compteur du formulaire avance à chaque ouverture de saisie, même annulée.** Sur
Actions commerciales, deux ouvertures annulées ont consommé les numéros 318 et 319
alors que le maximum en base était 311. Un raccourci de saisie posé sur une page
d'accueil creusera donc un trou dans la numérotation à chaque clic curieux.

**Les identifiants de catégorie ne sont pas stables.** Une réorganisation côté TeePee
les change sans prévenir et sans redirection : les liens cassent en silence. D'ou ce
fichier, et l'historique en bas.

## Menus racines

| Libellé | Identifiants | Pages | URL |
|---|---|---|---|
| Système de management | `92F82BEE` | index | https://safeplace.teepee.fr/#/category/92F82BEE |
| Installation | `0CBC7D3A` | index | https://safeplace.teepee.fr/#/category/0CBC7D3A |
| Moyen matériel | `9A294B91` | index | https://safeplace.teepee.fr/#/category/9A294B91 |
| Management des projets & affaires / Management de projet et des affaires | `32DB80F2` | index, offre | https://safeplace.teepee.fr/#/category/32DB80F2 |
| Achats | `67103350` | index | https://safeplace.teepee.fr/#/category/67103350 |
| Ressources humaines | `D92BB7C3` | index, rh | https://safeplace.teepee.fr/#/category/D92BB7C3 |
| Construction & performance | `1EEE8D15` | index | https://safeplace.teepee.fr/#/category/1EEE8D15 |
| Ressources humaines / Recrutement | `02E2474B` | rh | https://safeplace.teepee.fr/#/category/02E2474B |
| Material & Equipment | `C602A3FD` | en | https://safeplace.teepee.fr/#/category/C602A3FD |
| Management System | `18F7F9BA` | en | https://safeplace.teepee.fr/#/category/18F7F9BA |
| Installation | `5C12180C` | en | https://safeplace.teepee.fr/#/category/5C12180C |

## Tableaux de bord Power BI

| Libellé | Identifiants | Pages | URL |
|---|---|---|---|
| Suivi fiche de contrôle | `7FFDF492` | index, offre | https://safeplace.teepee.fr/#/homepage/view/7FFDF492 |
| Tableau de bord qualité | `F4D24233` | index, offre | https://safeplace.teepee.fr/#/homepage/view/F4D24233 |
| Quart d'heure QSE | `403B7A7F` | index, offre | https://safeplace.teepee.fr/#/homepage/view/403B7A7F |
| Suivi chantier | `D877A9DE` | index, offre | https://safeplace.teepee.fr/#/homepage/view/D877A9DE |
| CRM | `D35E43C6` | offre | https://safeplace.teepee.fr/#/homepage/view/D35E43C6 |

## Projets France

| Libellé | Identifiants | Pages | URL |
|---|---|---|---|
| Bienvenue sur Teepee / Projets en cours / Tous les projets | `F427C2AF` / `D956BEFD` | index, offre | https://safeplace.teepee.fr/#/category/F427C2AF/D956BEFD/dataList/Projets/default_Projets |
| Lorris 2 | `F427C2AF` / `D956BEFD` | index, offre | https://safeplace.teepee.fr/#/viewData/F427C2AF/D956BEFD/Projets/FRWEBV2/77FA5821-4992-46BE-B434-941BC3A1F169?context=6BB2C517-0812-42A4-A32C-24ED6C10D686 |
| Sennely | `F427C2AF` / `D956BEFD` | index, offre | https://safeplace.teepee.fr/#/viewData/F427C2AF/D956BEFD/Projets/FRWEBV2/151959C9-2C1D-4B22-8E7C-0AAF0E75C6A9?context=1F101FEF-C862-4D06-BC59-24A685C88007 |
| Chauvigny | `F427C2AF` / `D956BEFD` | index, offre | https://safeplace.teepee.fr/#/viewData/F427C2AF/D956BEFD/Projets/FRWEBV2/2450A316-F4B0-467D-BDD9-3A660E517E23?context=36965137-E5A8-4E70-94ED-A31591FF59A5 |
| Geloux 2 | `F427C2AF` / `D956BEFD` | index, offre | https://safeplace.teepee.fr/#/viewData/F427C2AF/D956BEFD/Projets/FRWEBV2/8AB86A1F-FF0F-4AFB-B8C0-0EECD079676D?context=15C74294-C011-4AD2-8EB1-BABC94A3A114 |
| Beauchêne | `F427C2AF` / `D956BEFD` | index, offre | https://safeplace.teepee.fr/#/viewData/F427C2AF/D956BEFD/Projets/FRWEBV2/909B5DEA-0E07-4CEE-A2E0-70B4C4C075C3?context=4484E9AF-26D7-4C6E-951F-1E2A72ABA3E2 |
| Barlieu | `F427C2AF` / `D956BEFD` | index, offre | https://safeplace.teepee.fr/#/viewData/F427C2AF/D956BEFD/Projets/FRWEBV2/9FE56ECE-FEF0-4CE8-855C-5D540AE5E813?context=F5BE3E28-B535-4802-A409-64E264C15064 |
| Monts | `F427C2AF` / `D956BEFD` | index, offre | https://safeplace.teepee.fr/#/viewData/F427C2AF/D956BEFD/Projets/FRWEBV2/B089CAB9-1BF4-4FFA-BCA1-B93E3921789B?context=8D988B0E-139F-4FE5-AA13-C33B41AF41DD |

## Projets International

| Libellé | Identifiants | Pages | URL |
|---|---|---|---|
| Welcome to Teepee | `DDCDAF73` / `7ADDAB11` | en | https://safeplace.teepee.fr/#/category/DDCDAF73/7ADDAB11/dataList/Projets/default_Projets |
| ThreeCastle | `DDCDAF73` / `7ADDAB11` | en | https://safeplace.teepee.fr/#/viewData/DDCDAF73/7ADDAB11/Projets/ENProjetWeb/98EE3433-FBE0-44E2-B1CA-39A70FC34B79?context=01362DEE-5A00-441E-BDAD-BD89B3240270 |
| Ballinknockane | `DDCDAF73` / `7ADDAB11` | en | https://safeplace.teepee.fr/#/viewData/DDCDAF73/7ADDAB11/Projets/ENProjetWeb/00F71013-6615-4195-A339-B004991B3CB7?context=02A1C672-861B-4AAF-AF4D-0689795567F8 |
| Garr | `DDCDAF73` / `7ADDAB11` | en | https://safeplace.teepee.fr/#/viewData/DDCDAF73/7ADDAB11/Projets/ENProjetWeb/4F9DBAFD-E998-4801-8C86-EC361E5F5006?context=B4362240-6E2C-4E98-A4BB-D8EFBB324C88 |
| Johnstown North | `DDCDAF73` / `7ADDAB11` | en | https://safeplace.teepee.fr/#/viewData/DDCDAF73/7ADDAB11/Projets/ENProjetWeb/F1713C99-2928-4BAB-8E2A-9EC6BFD70761?context=B953F48E-55F8-4F2C-AB26-0DF7CC2EFA09 |

## MPA · CRM

| Libellé | Identifiants | Pages | URL |
|---|---|---|---|
| Toutes les opportunités | `32DB80F2` / `50F618EA` | offre | https://safeplace.teepee.fr/#/category/32DB80F2/50F618EA/dataList/CRMOpportunite/default_CRMOpportunite |
| En cours de suivi | `32DB80F2` / `2A96401C` | offre | https://safeplace.teepee.fr/#/category/32DB80F2/2A96401C/dataList/CRMOpportunite/CRMOpportuniteEnCours |
| Panel clients | `32DB80F2` / `65B438CC` | offre | https://safeplace.teepee.fr/#/category/32DB80F2/65B438CC/dataList/TEEPEE_Entreprise/default_TEEPEE_Entreprise_CRM |
| Actions commerciales | `32DB80F2` / `36086F3F` | offre | https://safeplace.teepee.fr/#/category/32DB80F2/36086F3F/dataList/CRMActionCommerciale/default_CRMActionCommerciale |
| Enquêtes de satisfaction | `32DB80F2` / `8D8DC69D` | offre | https://safeplace.teepee.fr/#/category/32DB80F2/8D8DC69D/dataList/EnqueTeDeSatisfactionClient/default_EnqueTeDeSatisfactionClient |

## RH · Recrutement

| Libellé | Identifiants | Pages | URL |
|---|---|---|---|
| Ouvertures de poste | `02E2474B` / `8663F6A6` | rh | https://safeplace.teepee.fr/#/category/02E2474B/8663F6A6/dataList/OuvertureDePoste/default_OuvertureDePoste |
| Entretiens candidats | `02E2474B` / `E4FDB727` | rh | https://safeplace.teepee.fr/#/category/02E2474B/E4FDB727/dataList/RHEntretientCandidat/default_RHEntretienCandidat |
| Renseignements d'embauche | `02E2474B` / `0A9A7C08` | rh | https://safeplace.teepee.fr/#/category/02E2474B/0A9A7C08/dataList/RHDemandeDeRenseignementsDEmbauche/default_RHAutorisationDEmbauche |
| Autorisations d'embauche | `02E2474B` / `EBEF9E36` | rh | https://safeplace.teepee.fr/#/category/02E2474B/EBEF9E36/dataList/RHAutorisationDEmbauche/default_RHAutorisationDEmbauche |
| Entreprises Omexom | `02E2474B` / `092F1C43` | rh | https://safeplace.teepee.fr/#/category/02E2474B/092F1C43/dataList/EntrepriseOmexomRE/ToutesLesEntreprisesCREAdmin |

## QSE et Installation

| Libellé | Identifiants | Pages | URL |
|---|---|---|---|
| Plan d'action | `0CBC7D3A` / `1A268114` | index | https://safeplace.teepee.fr/#/category/0CBC7D3A/1A268114/dataList/PlanDActions/PlanDActionsGeNeRal |
| Non-conformités | `92F82BEE` / `E279156E` | index | https://safeplace.teepee.fr/#/category/92F82BEE/E279156E/dataList/FicheDeNonConformite/default_FicheDeNonConformite |
| Quart d'heures QSE | `92F82BEE` / `4231E439` | index | https://safeplace.teepee.fr/#/category/92F82BEE/4231E439/dataList/14DHeureQHSE/default_14DHeureQHSE |

## International · listes

| Libellé | Identifiants | Pages | URL |
|---|---|---|---|
| Pick Up Permit | `C602A3FD` / `969BDBDF` | en | https://safeplace.teepee.fr/#/category/C602A3FD/969BDBDF/dataList/TESTGARRPICKUPPERMIT/default_TESTGARRPICKUPPERMIT |
| Delivery | `C602A3FD` / `72956F51` | en | https://safeplace.teepee.fr/#/category/C602A3FD/72956F51/dataList/TESTGARRLIVRAISONS/default_TESTGARRLIVRAISONS |
| HSE Observations | `18F7F9BA` / `CC910484` | en | https://safeplace.teepee.fr/#/category/18F7F9BA/CC910484/dataList/SMObservationsHSE/default_SMObservationsHSE |
| Minor Injury Report | `18F7F9BA` / `3D8F08DD` | en | https://safeplace.teepee.fr/#/category/18F7F9BA/3D8F08DD/dataList/AccidentBeNin/default_AccidentBeNin |

## Transverse

| Libellé | Identifiants | Pages | URL |
|---|---|---|---|
| Mon profil | `E6FE12CE` / `ED68D778` | index, rh | https://safeplace.teepee.fr/#/category/E6FE12CE/ED68D778/dataList/USER/FiltreLUtilisateurNeVoitQueSesTickets |
| Support | `DC3605A6` / `AE9641CE` | index, rh | https://safeplace.teepee.fr/#/category/DC3605A6/AE9641CE/dataList/TicketsSupport/FiltreLUtilisateurVoirQueSesTickets |
| Administration / Annuaire | `FA584D40` / `DED3EB21` | index, rh | https://safeplace.teepee.fr/#/category/FA584D40/DED3EB21/dataList/USER/default_USER |

## Saisies directes

Les liens de création, fabriqués selon la route ci-dessus. Vérifier chaque nouveau lien
en l'ouvrant une fois avant de le poser sur une page.

| Formulaire | Menu | URL |
|---|---|---|
| IN PV de livraison | Projets `F427C2AF` / `D956BEFD` | https://safeplace.teepee.fr/#/viewData/F427C2AF/D956BEFD/INPVDeLivraison/FRINPVDeLivraison |

## Historique des remplacements

| Date | Ce qui a changé | Avant | Après |
|---|---|---|---|
| 2026-09-21 | Menu MPA réorganisé, tous les liens CRM cassés | `0E3BFD62` | `32DB80F2` |

Détail du remplacement du 2026-09-21 :

| Libellé | Ancien | Nouveau |
|---|---|---|
| Menu MPA | `0E3BFD62` | `32DB80F2` |
| Toutes les opportunités | `B83A513C` | `50F618EA` |
| En cours de suivi | `E6B257D2` | `2A96401C` |
| Actions commerciales | `9ED75B57` | `36086F3F` |
| Clients / Panel clients | `DD0397AD` + filtre `Client` | `65B438CC` + filtre `default_TEEPEE_Entreprise_CRM` |
| Enquêtes de satisfaction | n'existait pas | `8D8DC69D` |
| Contacts | `46A65DBC` (`TEEPEE_Contact`) | **aucun équivalent fourni, carte retirée** |

## Liens manquants

Avant d'ajouter une carte, vérifier dans `CONTEXTE.md` que le public de la page
concernée a le droit d'ouvrir la liste visée.

Ce qu'il reste à obtenir, et pourquoi :

| Ce qu'il faut | Pour quoi faire | État |
|---|---|---|
| ~~Contacts CRM~~ | ~~carte Contacts sur la page Offre~~ | **abandonné**, voir `CONTEXTE.md` |
| URL du bouton **Saisir**, deux échantillons du même formulaire | raccourcis de création directe sur les cartes | à tester, voir plus bas |
| Rapport Power BI RH | section tableaux de bord de la page RH | aucun identifiant connu |
| Listes RH hors recrutement | menu `D92BB7C3`, aujourd'hui seul le menu racine est lié. L'export nomme les quatre entrées : demande d'ouverture de poste, parcours d'intégration, fiche d'évaluation Omexom RE, grille d'évaluation de formation | à fournir |
| Tableau de bord `HA · Panel d'entreprise` | le rapport le plus largement accessible de tous, 31 rôles sur 33, affiché sur aucune page | à fournir |

### Sur les liens de saisie

Le bouton **Saisir** de TeePee est un bouton JavaScript : le clic droit ne propose
aucun lien à copier. Pour en récupérer un, ouvrir une saisie vierge, copier l'URL de
la barre d'adresse, quitter sans enregistrer, **et recommencer une seconde fois sur le
même formulaire**.

Si les deux URL sont identiques, c'est une route générique et le raccourci est
utilisable. Si elles diffèrent, TeePee crée un brouillon au clic et l'URL désigne ce
brouillon précis : un raccourci figé renverrait alors tout le monde sur la même fiche,
et l'idée est à abandonner.
