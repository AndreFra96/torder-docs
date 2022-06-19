# Esempi richieste

Di seguito alcuni esempi riguardanti gli endpoint principali delle API e del loro utilizzo.

## Login

### Username/Password

Effettua il login con username e passord

```
curl "http://localhost:3000/api/login" \
-X POST \
-H "Content-Type: application/json" \
-d '{"username":"{username}","password":"{password}"}'
```

## Ordine

### Ottieni tutti

Ottieni tutti gli ordini, questo endpoint va preferibilmente evitato poichè molto lento.

```
curl "http://localhost:3000/api/ordine" \
-X GET \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {token}" \
```

### Ottieni in base all'id

Ottieni uno specifico ordine in base al suo id

```
curl "http://localhost:3000/api/ordine/{id}" \
-X GET \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {token}" \
```

### Ottieni pagina

Ottieni una pagina di ordini

```
curl "http://localhost:3000/api/ordine/pagina/{numero_pagina}" \
-X GET \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {token}" \
```

### Ottieni con Join

Ottieni uno specifico ordine e il cliente associato in base all'id dell'ordine

```
curl "http://localhost:3000/api/ordine/{id}" \
-X GET \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {token}" \
-d '{"options":{"include":"cliente_cliente"}}'
```

### Matricole e Date di attivazione

E' disponibile uno specifico endpoint per ottenere lo stato di inserimento di matricole e date di attivazione e uno per cancellare contemporaneamente tutte quelle legate ad uno specifico ordine

#### Ottieni

```
curl "http://localhost:3000/api/ordine/{id}/serialActivation" \
-X GET \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {token}" \
```

#### Cancella

```
curl "http://localhost:3000/api/ordine/{id}/serialActivation" \
-X DELETE \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {token}" \
```

### Stato selezionabile

E' disponibile uno specifico endpoint per sapere quali sono i possibili stati di destinazione dell'ordine.

```
curl "http://localhost:3000/api/ordine/{id}/availableStatus" \
-X GET \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {token}" \
```

### Modifica stato

E' disponibile uno specifico endpoint per modificare lo stato di un ordine, utilizzando questo endpoint vengono effettuati i controlli e le azioni necessarie prima della modifica dello stato.

```
curl "http://localhost:3000/api/ordine/{id}/stato/{stato}" \
-X PUT \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {token}" \
```

## Rinnovi Annuali

### Effettua rinnovo

Avvia la conferma di un rinnovo

```
curl "http://localhost:3000/api/rinnovo/{id}/rinnova" \
-X PUT \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {token}" \
```

### Totale per profilo

Un'informazione utile, disponibile direttamente tramite uno specifico endpoint è il totale dei rinnovi di un certo mese e anno raggruppati per profilo locale

Richiesta:

```
curl "http://localhost:3000/api/rinnovo/totaleProfili/{mese}/{anno}" \
-X GET \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {token}" \
```

Risposta:

```
[
    {
        "descrizione":"descrizione_gruppo",
        "totale":totale
    },
    ...
]
```
