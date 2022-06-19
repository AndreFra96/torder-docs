# CRUD

Le API offrono uno specifico endpoint per l'interazione con ogni tabella del database.

## Interazioni base

Per ogni tabella del database è possibile:

- Creare un nuovo record (CREATE)
- Ottenere un record esistente (READ)
- Modificare un record esistente (UPDATE)
- Eliminare un record esistente (DELETE)

Ognuno di queste operazioni è disponibile in un endpoint denominato come la tabella in questione mappato allo specifico metodo HTTP:

| CRUD   | HTTP   | ENDPOINT            | DESCRIZIONE                          |
| ------ | ------ | ------------------- | ------------------------------------ |
| CREATE | POST   | api/nomeTabella     | aggiungi un record                   |
| READ   | GET    | api/nomeTabella/:id | ottieni un record in base al suo id  |
| UPDATE | PUT    | api/nomeTabella/:id | modifica un record in base al suo id |
| DELETE | DELETE | api/nomeTabella/:id | elimina un record in base al suo id  |

!!! tip "Chiavi composte"

    Per le tabelle la quale chiave primaria è composta da più campi gli endpoint riferiti ad uno specifico record vengono composti in questo modo: api/nomeTabella/:campo1/:campo2/...

## Interazioni aggiuntive

Ogni tabella fornisce altri tre endpoint:

| CRUD | HTTP | ENDPOINT                       | DESCRIZIONE                                 |
| ---- | ---- | ------------------------------ | ------------------------------------------- |
| READ | GET  | api/nomeTabella                | ottieni tutti i record di una tabella       |
| READ | GET  | api/nomeTabella/count          | ottieni il totale dei record di una tabella |
| READ | GET  | api/nomeTabella/pagina/:pagina | ottieni i record impaginati 10 alla volta   |
