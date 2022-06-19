# Query

Alle richieste di tipo GET è possibile allegare una query in formato JSON che verrà utilizzata per modificare il risultato della richiesta

## Come inviarla

E' possibile passare la query all'interno della richiesta direttamente come oggetto JSON all'interno del corpo oppure serializzata e passata come query parameter.

!!! danger "Break the Rules"

    Secondo le [specifiche HTTP](https://www.rfc-editor.org/rfc/rfc2616) ogni richiesta può contenere un corpo, a prescindere dal suo metodo.

    Nonostante questo la [sezione 4.3](https://www.rfc-editor.org/rfc/rfc2616#section-4.3) specifica che il corpo di una richiesta di tipo GET non dovrebbe modificare il risultato della richiesta stessa, <u> questa regola viene appositamente infranta in T-Order </u> nel momento in cui la query viene passata tramite corpo della richiesta.

## Sintassi

La query più semplice possibile è la seguente:

```json
{
  "options": {}
}
```

All'interno di options è possibile inserire tutte le opzioni:

### Includere (Join)

Alcuni dei campi del database di t-order sono riferimenti a specifici record in altre tabelle, è possibile inserire nella risposta anche il record riferito.

Per effettuare una Join è necessario inserire l'opzione `include`:

```json
{
  "options": {
    "include": []
  }
}
```

#### Stringa di relazione

All'interno di include a questo punto è necessario inserire una stringa corrispondente alla relazione.

La stringa in questione viene composta in maniera diversa in base al tipo di relazione fra le due tabelle:

##### Relazione 1:1

In una relazione "uno a uno", un record in una tabella è associato a un unico record in un'altra tabella.

Il database di T-Order presenta questa relazione solo per le tabelle configurazione_rinnovo_locale e configurazione_mensile_locale, tabelle contenenti le configurazioni (pagamento, fatturazione alternativa, ...) comuni per ogni rinnovo o mensile di un locale.

Per ogni locale esiste un'unica configurazione_rinnovo_locale ed ogni configurazione rinnovo locale è legata ad un unico locale, vale lo stesso per la configurazione_mensile_locale.

Un locale può non avere nessuna configurazione_mensile_locale o configurazione_rinnovo_locale ma non può esistere configurazione senza il locale collegato.

Per ottenere questo tipo di relazione in un database relazionale è necessario inserire una chiave esterna in una delle due tabelle, in particolare la soluzione adottata è stata quella di inserire nella configurazione_mensile_locale e nella configurazione_rinnovo_locale un campo locale contenente l'id del locale e utilizzarlo come chiave primaria per la tabella. In questo modo è possibile inserire solo un record per locale nella configurazione_mensile_locale e uno nella configurazione_rinnovo_locale.

Per eseguire join da endpoint `GET api/locale` devo comporre la stringa in questo modo:

- `"locale_configurazione_mensile_locale"` &rarr; per collegare la configurazione mensile
- `"locale_configurazione_rinnovo_locale"` &rarr; per collegare la configurazione rinnovo

Per eseguire join da endpoint `GET api/configurazione_mensile_locale` o da `GET api/configurazione_mensile_locale` devo utilizzare la stringa `"locale_locale"`

Per effettuare una join a partire dalla tabella contenente la chiave esterna, la stringa si compone in questo modo:

`"[chiave]_[nome_altra_tabella]"`

Per effettuare una join a partire dalla tabella senza la chiave esterna, la stringa si compone in questo modo:

per comporre la stringa è sufficente tradurre il pensiero `tramite il campo abc collego la tabella def` nella stringa `abc_def`

!!! example "Esempio"

    La tabella configurazione_mensile_locale ha un campo locale che che contiene l'id di uno specifico record nella tabella locale, la query che dovrò passare all'endpoint `GET api/configurazione_mensile_locale/:id` è la seguente:

    ``` json
    {
        "options":{
            "include":["locale_locale"]
        }
    }
    ```

    Risponde alla frase: "tramite il campo locale includo la tabella locale"

hasOne

belongsTo

##### Relazione 1:N

belongsTo

!!! example "Esempio"

    La tabella cliente ha un campo locale che che contiene l'id di uno specifico record nella tabella locale, la query che dovrò passare all'endpoint `GET api/cliente/:id` è la seguente:

    ``` json
    {
        "options":{
            "include":["locale_locale"]
        }
    }
    ```

    Risponde alla frase: "tramite il campo locale includo la tabella locale"

    La richiesta restituirà un oggetto di questo tipo:

    ``` json
    {
        "id": "id_cliente"
        "nome": "nome_cliente",
        "ragsoc": "ragione_sociale",
        ... ,
        "locale": "id_locale",
        "locale_locale":{
            "id_locale",
            ...
        }
    }
    ```

    Se per qualsiasi motivo non è possibile collegare il cliente al locale il campo `locale_locale` sarà <b>null</b>

##### Relazione N:M

#### Nested Join

Per effettuare join innestate è necessario utilizzare un'altra strategia per include.

In questo caso infatti la query dovrà essere composta in questo modo:

```json
{
    "options":{
        "include":{
            "model": "nome_tabella",
            "as": stringa di relazione,
            "include": {
                "model": "nome_seconda_tabella",
                "as": stringa di relazione
            }
        }
    }
}
```

!!! example "Esempio"

    La tabella cliente ha un campo locale che che contiene l'id di uno specifico record nella tabella locale e il locale ha un campo profilo_locale che contiene l'id di uno specifico record nella tabella profilo_locale, la query che dovrò passare all'endpoint `GET api/cliente/:id` è la seguente:

    ``` json
    {
        "options":{
            "include":{
                "model": "locale",
                "as": "locale_locale",
                "include": {
                    "model": "profilo_locale",
                    "as": "profilo_locale_profilo_locale"
                }
            }
        }
    }
    ```

    La richiesta restituirà un oggetto di questo tipo:

    ``` json
        {
            "id": "id_cliente"
            "nome": "nome_cliente",
            "ragsoc": "ragione_sociale",
            ... ,
            "locale": "id_locale",
            "locale_locale":{
                "id_locale",
                ... ,
                "profilo_locale": "id_profilo_locale",
                "profilo_locale_profilo_locale":{
                    "id":"id_profilo_locale",
                    "descrizione":"descrizione_profilo_locale"
                }
            }
        }
    ```

### Filtrare (Where)

Per filtrare i risultati all'interno di una query è possibile utilizzare l'opzione where:

```json
{
  "options": {
    "where": {}
  }
}
```

!!! example "Filtro per uguaglianza"

    Voglio ottenere tutti i locali che hanno profilo_locale = 4, la query che dovrò passare all'endpoint `GET api/locale` è la seguente:

    ```json
    {
        "options":{
            "where":{
                "profilo_locale": 4
            }
        }
    }
    ```

#### Operazioni disponibili

Oltre a filtrare per uguaglianza è possibile inserire all'interno dell'opzione where una serie di specifiche stringhe che vengono poi mappate in operazioni sequelize, le operazioni disponibili sono:

```json
"where": {
    "and": [{ "a": 5 }, { "b": 6 }],      // (a = 5) AND (b = 6)
    "or": [{ "a": 5 }, { "b": 6 }],       // (a = 5) OR (b = 6)
    "attributo": {
        // Base
        "eq": 3,                          // = 3
        "ne": 20,                         // != 20
        "is": null,                       // IS NULL
        "not": true,                      // IS NOT TRUE
        "or": [5, 6],                     // (attributo = 5) OR (attributo = 6)

        // Specificare colonna
        "col": 'user.organization_id',    // = "user"."organization_id"

        // Comparazione numerica
        "gt": 6,                          // > 6
        "gte": 6,                         // >= 6
        "lt": 10,                         // < 10
        "lte": 10,                        // <= 10
        "between": [6, 10],               // BETWEEN 6 AND 10
        "notBetween": [11, 15],           // NOT BETWEEN 11 AND 15

        // Altri operatori

        "all": ...,                       // > ALL (...)

        "in": [1, 2],                     // IN [1, 2
        "notIn": [1, 2],                  // NOT IN [1, 2

        "like": "%hat",                   // LIKE '%hat'
        "notLike": "%hat",                // NOT LIKE '%hat'
        "startsWith": "hat",              // LIKE 'hat%'
        "endsWith": "hat",                // LIKE '%hat'
        "substring": "hat",               // LIKE '%hat%'
    }
}
```

!!! tip "Nested where"

    Per filtrare una query basandosi su un campo annidato è possibile utilizzare la seguente sintassi: `$nested.column$`

    ```json
      "where": {
        "$instruments.size$": { "ne" : "small" }
      },
    ```

### Ordinare (Order by)

l'opzione order permette di ordinare i risultati di una query, la sintassi da utilizzare è la seguente

```json
"order": ["nome_colonna",ASC | DESC]
```

è possibile anche ordinare per più di una colonna con la seguente sintassi:

```json
"order":[
            ["colonna1",ASC | DESC],
            ["colonna2",ASC | DESC]
        ]
```

### Raggruppare (Group by)

l'opzione group permette di raggruppare i risultati di una query, la sintassi da utilizzare è la seguente

```json
"group": ["nome_colonna"]
```

è possibile anche raggruppare per più di una colonna con la seguente sintassi:

```json
"group":["colonna1","colonna2"]
```
