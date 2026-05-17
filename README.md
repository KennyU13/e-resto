# E-Resto Hotel - Bonita BPM Project

E-Resto Hotel is a Bonita Studio project for managing hotel room reservations, invoicing, payment, room departure, housekeeping, stock verification and daily accounting follow-up.

## Project Scope

The hotel manages three room categories:

| Category | Rooms | Night Price |
| --- | --- | --- |
| Standard | 101 to 106 | 15000 Ar |
| Suite Senior | 201 to 206 | 30000 Ar |
| Suite Prestige | 301 to 306 | 45000 Ar |

A room can be sold only if it is clean and available. Each reservation consumes the following required articles:

| Article | Quantity per night |
| --- | --- |
| gel douche | 1 |
| papier hygienique | 1 |
| pantoufle | 1 |
| brosse a dent | 1 |

## Actors and Test Users

| Actor | Responsibility | Test User |
| --- | --- | --- |
| Client | Starts and completes a reservation | `anthony.nichols` |
| Receptionniste | Reviews invoice and collects payment | `april.sanchez` |
| Femme de menage | Cleans rooms and replaces articles | `thomas.wallis` |
| Comptable | Checks stock, invoices and dashboard | `virginie.jomphe` |

## Business Workflow

1. The client submits a reservation form with category, identity and stay details.
2. The system initializes reference data if needed.
3. The system selects a clean room for the requested category.
4. The system generates the invoice.
5. The receptionist collects the invoice amount.
6. After payment, the room status becomes `occupee`.
7. The client confirms departure.
8. After departure, the room status becomes `sale`.
9. Housekeeping cleans the room and replaces required articles.
10. After cleaning, the room status becomes `propre`.
11. The accountant verifies stock, counts invoices and checks the dashboard.

## Final Process Version

Deploy this process diagram:

```text
app/diagrams/E-Resto-3.4.proc
```

Process name and version:

```text
Hotel 3.4
```

## Business Data Model

The project uses the following main BDM objects:

| Object | Purpose |
| --- | --- |
| `CategorieChambre` | Room category and price |
| `Chambre` | Room number, status and category |
| `Article` | Required room articles and stock |
| `Cliente` | Customer identity and contact data |
| `Reservation` | Reservation details |
| `Facture` | Invoice amount and payment status |
| `ConsommationArticle` | Article consumption tracking |

Reference data is initialized automatically by the process:

- room categories
- rooms
- required articles

## Forms

| Form | Purpose |
| --- | --- |
| `formReservation` | Customer reservation form |
| `formEncaisserMontant` | Payment validation form |
| `formDepart` | Customer departure confirmation |
| `formNettoyer` | Room cleaning confirmation |
| `formVerifierStock` | Stock verification |
| `formTableauBord` | Invoice, room and stock dashboard |

The forms include a simple modern UI style directly inside the Bonita UI Designer pages.

## Local Runtime

Bonita local application URL:

```text
http://localhost:29561/
```

## Deployment Steps

1. Open the project in Bonita Studio.
2. Deploy the BDM if Bonita Studio requests it.
3. Deploy the process `Hotel 3.4`.
4. Start a new case from the Bonita User Application.

## Test Scenario

Use this sequence to validate the process:

1. Log in as `anthony.nichols`.
2. Start process `Hotel 3.4`.
3. Submit a reservation.
4. Log in as `april.sanchez`.
5. Complete `Encaisser montant`.
6. Log in again as `anthony.nichols`.
7. Complete `Depart de l'hotel`.
8. Log in as `thomas.wallis`.
9. Complete `Nettoyer Chambre + remplacer article`.
10. Log in as `virginie.jomphe`.
11. Complete stock verification and check the dashboard.

## Room Status Rules

| Event | Room Status |
| --- | --- |
| Initial reference data | `propre` |
| After payment | `occupee` |
| After customer departure | `sale` |
| After housekeeping | `propre` |

## Notes

- Only clean rooms are available for reservation.
- If no clean room exists in the requested category, no room should be assigned.
- The dashboard displays recent invoices with customer information.
- The stock page groups required articles to avoid duplicate display.
