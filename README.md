# E-Resto - Processus hotel Bonita

Projet Bonita Studio de gestion de reservation de chambres pour un hotel.

## Objectif

Le processus permet de gerer une reservation de chambre, la generation de facture, l'encaissement, le depart du client, le nettoyage de la chambre et le suivi comptable.

L'hotel possede trois categories de chambres :

- Standard : chambres 101 a 106, prix nuit 15000 Ar
- Suite Senior : chambres 201 a 206, prix nuit 30000 Ar
- Suite Prestige : chambres 301 a 306, prix nuit 45000 Ar

Pour vendre une chambre, elle doit etre propre et les articles obligatoires doivent etre disponibles :

- gel douche
- papier hygienique
- pantoufle
- brosse a dent

## Acteurs

- Client : effectue la reservation
- Receptionniste : encaisse le montant de la facture
- Femme de menage : nettoie la chambre et remplace les articles
- Comptable : verifie les stocks, compte les factures et consulte le tableau de bord

Utilisateurs de test configures :

- Client : `anthony.nichols`
- Receptionniste : `april.sanchez`
- Femme de menage : `thomas.wallis`
- Comptable : `virginie.jomphe`

## Flux principal

1. Le client remplit le formulaire de reservation.
2. Le systeme verifie la disponibilite d'une chambre propre dans la categorie demandee.
3. Si une chambre propre existe, le systeme genere la facture.
4. Le receptionniste encaisse le montant.
5. Apres encaissement, la chambre devient `occupee`.
6. Le client confirme son depart.
7. Apres le depart, la chambre devient `sale`.
8. La femme de menage nettoie la chambre et remplace les articles.
9. Apres nettoyage, la chambre redevient `propre`.
10. Le comptable verifie les articles en stock et consulte le tableau de bord.

## Diagramme a deployer

Le diagramme final a deployer est :

```text
app/diagrams/E-Resto-3.4.proc
```

Les anciennes versions ne sont pas necessaires pour le deploiement final.

## BDM

Le modele de donnees metier contient notamment :

- `CategorieChambre`
- `Chambre`
- `Article`
- `Cliente`
- `Reservation`
- `Facture`
- `ConsommationArticle`

Les donnees de reference sont initialisees automatiquement par le processus :

- categories
- chambres
- articles

## Pages principales

- `formReservation`
- `formEncaisserMontant`
- `formDepart`
- `formNettoyer`
- `formVerifierStock`
- `formTableauBord`

Les pages ont une interface simple avec un style moderne integre.

## Deploiement

Dans Bonita Studio :

1. Deployer le BDM si Bonita le demande.
2. Deployer le processus `Hotel 3.4`.
3. Lancer un nouveau cas avec l'utilisateur `anthony.nichols`.
4. Continuer le test avec les utilisateurs selon les acteurs.

## Test rapide

Sequence de test conseillee :

1. `anthony.nichols` lance `Hotel 3.4` et reserve une chambre.
2. `april.sanchez` voit la tache `Encaisser montant`.
3. Apres encaissement, `anthony.nichols` voit la tache `Depart de l'hotel`.
4. Apres le depart, `thomas.wallis` voit la tache `Nettoyer Chambre + remplacer article`.
5. Apres nettoyage, `virginie.jomphe` verifie le stock et consulte le tableau de bord.

## Notes

- Les chambres disponibles doivent avoir le statut `propre`.
- Une chambre devient `occupee` apres paiement.
- Une chambre devient `sale` apres le depart du client.
- Une chambre redevient `propre` apres nettoyage.
- Le tableau de bord affiche les factures recentes avec les informations du client.
