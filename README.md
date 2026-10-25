# Octet CRM

CRM open source, gratuit et installable (PWA) pour boutique de vente d'ordinateurs et de matériel informatique.

![Tableau de bord](docs/screenshot-desktop.png)

## Fonctionnalités

- **Tableau de bord** : ventes du mois et objectif, alertes de stock bas, réparations en cours, derniers clients.
- **Clients** : fiche détaillée avec ordinateurs (numéros de série), devis, factures et réparations.
- **Stock** : marque, modèle, CPU, RAM, stockage, GPU, neuf ou reconditionné, prix, quantité. Alerte sous 3 unités, filtres par catégorie et par état.
- **Ventes** : devis, passage en facture, statuts En attente / Payé / Annulé. Le stock baisse quand une facture est payée.
- **SAV** : suivi des machines déposées (Diagnostiqué, En cours, Prêt, Récupéré).
- **Recherche globale** : client, numéro de série, produit ou statut de réparation.
- **Langue et devise** : français ou anglais, devise MAD, FCFA (XOF), EUR ou USD (réglages via l'icône en haut à droite). Le changement de devise modifie l'affichage, sans conversion des montants.
- **Interface** : thème clair et sombre, barre de navigation basse sur mobile, installable, utilisable hors-ligne.

| Mobile |
|---|
| ![Mobile](docs/screenshot-mobile.png) |

## Utiliser en local

Aucune installation : ouvre `index.html` dans un navigateur.
Pour tester le mode PWA (service worker), lance un petit serveur :

```bash
python3 -m http.server 8000
# puis ouvre http://localhost:8000
```

## Déployer en ligne

### GitHub Pages (inclus)

1. Pousse ce dossier sur un dépôt GitHub public.
2. Dans **Settings → Pages**, choisis **Source : GitHub Actions**.
3. Chaque `push` sur `main` redéploie le site via `.github/workflows/pages.yml`.

Le site sera disponible sur `https://TON-COMPTE.github.io/NOM-DU-DEPOT/`.

### Cloudflare Pages ou Netlify

Connecte le dépôt, laisse la commande de build vide et indique `.` comme dossier de publication.

## Connexion, langue et devise

- Au premier lancement, l'application demande de créer un compte (utilisateur et mot de passe de 8 caractères minimum). Ensuite, elle affiche l'écran de connexion. Ce compte est stocké dans le navigateur de l'appareil : c'est une barrière d'accès simple, pas une sécurité de niveau serveur.
- Le bouton Paramètres (en haut) permet de choisir le français ou l'anglais, et la devise (MAD, FCFA, EUR, USD).

## Utilisateurs, récupération, logo et export Excel

- Le premier compte créé est administrateur. Il peut ajouter d'autres utilisateurs (Paramètres → Utilisateurs) et réinitialiser leur mot de passe.
- Un code de récupération est remis à la création de chaque compte. Écran de connexion → « Mot de passe oublié ? » permet de choisir un nouveau mot de passe avec ce code. Le Gmail de récupération est enregistré avec le compte, mais l'application n'envoie pas d'e-mails (il faudrait un serveur).
- Paramètres → Boutique et logo : nom et logo affichés sur l'accueil et l'écran de connexion.
- Le bouton « Exporter la semaine (Excel) » (accueil et Ventes) génère un fichier .xlsx des factures de la semaine en cours (module SheetJS chargé depuis cdnjs, connexion internet requise la première fois).

## Factures, garantie et catégories

- Ventes → « Voir et imprimer » ouvre la facture (ou le devis) avec le logo et le nom de la boutique, la durée de garantie de chaque article et sa date de fin, puis « Imprimer » (la mise en page d'impression n'affiche que la facture).
- La garantie se règle par produit (champ « Garantie (mois) » à la création, 12 mois par défaut ; 6 mois par défaut pour les produits reconditionnés déjà en stock).
- Dans la facture, les boutons WhatsApp et E-mail ouvrent un message prérempli (résumé de la facture) pour le client. Pour joindre le PDF : Imprimer → Enregistrer en PDF, puis ajoute le fichier au message. L'indicatif du pays se règle dans Paramètres → Boutique et logo (225 par défaut pour la Côte d'Ivoire, dont les numéros à 10 chiffres gardent leur 0 initial : +225 07 XX XX XX XX).
- Stocks : chaque produit a une référence et une image (à la création, ou via « Modifier la fiche », qui permet aussi de régler la garantie). La recherche du catalogue trouve aussi par référence.
- Paramètres → Boutique et logo : téléphone, e-mail et localisation de la boutique, affichés sous le logo sur la facture.
- Stocks → « Ajouter une catégorie » et « Supprimer une catégorie » (une catégorie utilisée par des produits ne peut pas être supprimée).
- SAV → « Déposer une machine » comporte une date de dépôt.

## Données

Les données d'exemple sont enregistrées dans le `localStorage` du navigateur : elles restent sur l'appareil et ne sont pas partagées entre postes. **N'enregistre pas de vraies données clients dans un dépôt public.** Pour un usage multi-postes, il faudra brancher une base en ligne avec authentification (Supabase ou Firebase, par exemple).

## Mettre à jour l'application

Modifie `index.html`, puis change la valeur de `VERSION` dans `sw.js` (par exemple `octet-v2`) pour que les appareils déjà installés récupèrent la nouvelle version.

## Pistes d'évolution

- Base de données partagée et connexion des utilisateurs
- Export des factures en PDF
- Modification et suppression des enregistrements
- Relances clients et rappels de garantie

## Contribuer

Les contributions sont les bienvenues : ouvre une *issue* pour proposer une idée ou signaler un bug, ou une *pull request* pour proposer une modification.

## Licence

[MIT](LICENSE)
