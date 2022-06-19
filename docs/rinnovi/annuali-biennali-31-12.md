# Annuali/Biennali/31-12

I rinnovi Annuali/Biennali sono organizzati in due tabelle: rinnovo e articolo_rinnovo.

Ad ogni articolo_rinnovo corrisponde uno ed un solo rinnovo, ad ogni rinnovo (se non è completato) corrisponono uno o più articolo_rinnovo.

Gli articoli all'interno dei rinnovi di questo tipo sono gli articoli con mth_12, mth_24 o new_year = 1

## Import da t_trace

I rinnovi vengono generati tramite import dalla tabella t_trace:

Creazione record rinnovi

1.  Query di estrazione

        SELECT t_trace.id as t_trace_id,cus1.id as cliente,cus2.id as
        cliente_fatt_alt, locale.id as locale, articolo.id as articolo,
        price,serial_number,installation_date, due_date_maintenance,
        payment_type
        FROM [T-ORDER].[db_ordini].t_trace
        JOIN [T-ORDER].[db_ordini].cliente AS cus1
        ON cus1.id_trace = t_trace.customer_id
        JOIN [T-ORDER].[db_ordini].locale
        ON locale.piva = cus1.piva AND locale.prg = t_trace.prg_location
        JOIN [T-ORDER].[db_ordini].articolo
        ON articolo.id_trace = t_trace.article_id
        LEFT JOIN [T-ORDER].[db_ordini].cliente AS cus2
        ON cus2.id_trace = t_trace.customer_for_billing
        WHERE (date_import_rinnovi IS NULL)
        AND due_date_maintenance IS NOT NULL
        AND trace_id IS NOT NULL
        AND (deleted IS NULL OR deleted = 0);

2.  Raggruppamento per (mese,anno,locale)
3.  Inserimento

## Configurazione rinnovo locale

Tutti i rinnovi di un certo locale condividono alcune informazioni: pagamento, fatturazione alternativa, note e tacito rinnovo.

Questi dati vengono salvati all'interno della tabella configurazione_rinnovo_locale che prevede un record per ogni locale per il quale sono stati inseriti almeno uno dei campi scritti sopra.

## Disdetta

E' possibile eliminare un articolo da un rinnovo effettuando la disdetta.

La disdetta dell'articolo di un rinnovo consiste in:

1.  scrittura disdetta della t_deleted

        {
          articolo,
          prezzo,
          matricola,
          data_scadenza,
          data_cancellazione: now(),
          cliente,
          locale,
          motivazione,
          utente: utente_richiesta,
          note
        }

2.  invio disdetta a trace (se trace_id != null)

        {
          "deleted": 1,
          "date_import_trace": null
        }

3.  eliminazione articolo_rinnovo
4.  impostazione rinnovo a completato (se non ci sono altri articoli)

## Inserimento nuovi articoli

All'interno di un rinnovo è possibile inserire gli articoli che hanno mth \_12, mth_24 o new_year = 1.

Per la logica di rinnovo di questi articoli vedi rinnovo con <u>trace_id a null</u>.

## Cambio piano

E' possibile effettuare un cambio piano (modifica dell'articolo) con tutti gli articoli appartenenti allo stesso gruppo e con lo stesso tipo di scadenza.

E' disponibile uno specifico endpoint che per ogni articolo_rinnovo restituisce i possibili articoli sostituitivi.

Per gli articoli inseriti successivamente e quindi non ancora importati in trace la procedura di cambio piano non è disponibile, poichè il cambio piano in quel caso avviene tramite cancellazione diretta dell'articolo e inserimento id un nuovo articolo.

La procedura del cambio piano, dopo i controlli iniziali, varia in base al campo anticipo scadenza:

Infatti se il campo anticipo scadenza è true significa che oltre a effettuare il cambio dell'articolo è necessario portare ad oggi la scadenza dell'articolo.

Controlli iniziali:

1. l'articolo rinnovo deve avere trace_id (non deve essere un nuovo articolo)
2. l'articolo selezionato per il cambio deve rientrare nelle opzioni di cambio piano dell'articolo rinnovo
3. l'articolo selezionato per il cambio deve avere id_trace compilato

Procedura cambio piano (anticipa = true):

1. Modifico articolo, prezzo, matricola e scadenza (oggi) dell'articolo rinnovo
2. Controllo se esiste già un rinnovo dello stesso locale nel mese attuale
3. Se non esiste creo un nuovo rinnovo nel mese attuale
4. Inserisco l'articolo all'interno del rinnovo nel mese attuale
5. Invio la modifica dell'articolo, del prezzo, della matricola e della scadenza a trace
6. Se non sono presenti altri articoli_rinnovo imposto il rinnovo a completato

Procedura cambio piano (anticipa = false):

1. Modifico articolo, prezzo e matricola dell'articolo rinnovo
2. Invio la modifica dell'articolo, del prezzo e della matricola a trace

## Metodi di pagamento

Il metodo di pagamento, salvato nella configurazione_rinnovo_locale, per questo tipo di rinnovo può essere uno qualsiasi di quelli disponibili

## Rinnovo

Tutti gli articoli di un rinnovo vengono rinnovati insieme ma è comunque necessario analizzare ogni articolo_rinnovo poichè possono presentarsi diverse casistiche:

1.  Salvataggio storico: <br>Ogni riga della articolo_rinnovo del rinnovo viene copiata nella articolo_rinnovo_storico.
2.  Import trace: <br>Il rinnovo viene comunicato a trace tramite la tabella t_trace:

    - Se l'articolo_rinnovo ha il campo <b>trace_id a NULL</b>:
      <br> Significa che è stato inserito manualmente dopo l'ultimo rinnovo, in questo caso viene passato il nuovo articolo a trace tramite un insert nella tabella t_trace con i seguenti campi:

            {
              order_type_id:15,
              customer_for_billing,
              customer_id,
              prg_location,
              article_id,
              price,
              serial_number,
              installation_date: now(),
              due_date_maintenance,
              type_billing,
              payment_type,
              create_operation (in base all'articolo)
            }

    - Se l'articolo_rinnovo ha il campo <b>trace_id diverso da NULL</b>:
      <br> Significa che è stato importato dalla t_trace, in questo caso viene effettuato un update sul record della t_trace con trace_id corrispondente:

            {
                price,
                serial_number,
                due_date_maintenance,
                date_import_trace: null, (per import in trace)
                date_import_rinnovi: null (per importare prossimo rinnovo)
                create_operation (in base all'articolo)
            }

3.  Generazione ordine di rinnovo: <br>

    - Per ogni rinnovo viene generato un ordine:

            {
              data:now(),
              cliente_fatt_alt,
              cliente,
              locale,
              utente,
              date_insert,
              tipo: 15, (rinnovo)
              is_closed: 1,
              stato: 7, (evaso)
              pagamento,
              data_evasione: now(),
              rinnovo,
              tipo_fatturazione
            }

    - Gli articoli del rinnovo vengono raggruppati per id_articolo, sconto e prezzo, aumentando di conseguenza la quantità e poi inseriti nella articolo_ordine associati all'ordine appena creato:

            {
              ordine,
              articolo,
              prezzo,
              quantita,
              sconto
            }

4.  Eliminazione articoli rinnovo
5.  Impostazione rinnovo a completato

## Proposta

Tutti gli articoli di un rinnovo con il campo proponi = 1 fanno parte della proposta di rinnovo

In base a questo campo viene popolato il pdf di proposta di rinnovo.
