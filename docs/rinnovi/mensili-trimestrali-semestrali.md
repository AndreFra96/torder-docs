# Mensili/Trimestrali/Semestrali

I rinnovi mensili sono organizzati in due tabelle: mensile e articolo_mensile.

Ad ogni articolo_mensile corrisponde uno ed un solo mensile, ad ogni mensile corrisponono uno o più articolo_mensile.

N.B. A differenza dei rinnovi Annuali/Biennali/31-12 i rinnovi di questo tipo vengono eliminati una volta completati, per questo motivo non devono esistere mensili senza articoli_mensili collegati.

## Import da trace

I rinnovi vengono generati tramite import dalla tabella t_trace.

La data di scadenza per ogni nuovo rinnovo è il primo giorno del mese successivo all'importazione.

Creazione record mensili:

1.  Query di estrazione

        SELECT t_trace.id as id_trace,articolo.id as articolo,t_trace.price
        as prezzo, t_trace.serial_number as matricola,cus1.id as cliente,
        cus2.id as cliente_fatt_alt, locale.id as locale,t_trace.type_billing
        as tipo_fatturazione
        FROM t_trace
        JOIN articolo ON articolo.id_trace = t_trace.article_id
        JOIN cliente as cus1 ON cus1.id_trace = t_trace.customer_id
        LEFT JOIN cliente as cus2
        ON cus2.id_trace = t_trace.customer_for_billing
        JOIN locale
        ON locale.piva = cus1.piva AND locale.prg = t_trace.prg_location
        WHERE
        articolo.mth_1 = 1 AND deleted <> 1 AND date_import_monthly IS NULL

2.  raggruppamento per cliente,locale, e tipo_fatturazione.
3.  Importazione

## Metodo di pagamento

Gli unici metodi di pagamento concessi sono quelli restituiti nella sezione canoni dei metodi di pagamento

## Configurazione mensile locale

Tutti i mensili di un certo locale condividono alcune informazioni: pagamento, fatturazione alternativa e note.

Questi dati vengono salvati all'interno della tabella configurazione_mensile_locale che prevede un record per ogni locale per il quale sono stati inseriti almeno uno dei campi scritti sopra.

## Fatturazione per cliente

I rinnovi di uno stesso cliente ma con locali diversi, appartenenti allo stesso mese e anno di scadenza possono essere raggruppati in un solo ordine selezionando per i rinnovi desiderati il campo fatturazione per cliente.

Vedi sotto come avviene il rinnovo.

## Rinnovo

Il rinnovo avviene contemporaneamente per tutti i rinnovi di un certo mese e anno.

1.  Controllo iban:

        if group_billing = 1 then
          if cliente.iban != null && cliente.iban != "" then
              return true
          else
              return false
        else
          if fatt_alternativa != null then
            if cliente_fatt_alt.iban != null && cliente_fatt_alt.iban != "" then
                return true
            else
                return false
          else
            if locale.iban != null && locale.iban != "" then
                return true
            else
                if cliente.iban != null && cliente.iban != "" then
                    return true
                else
                    return false

2.  Controllo metodo di pagamento
3.  Se tutti i mensili del mese attuale passano i controlli:

    1.  Import trace (per ogni mensile):
        <br>Il rinnovo viene comunicato a trace tramite la tabella t_trace:

        - Se l'articolo_mensile ha il campo <b>trace_id a NULL</b>:
          <br>
          Significa che è stato inserito manualmente dopo l'ultimo rinnovo - Viene passato il nuovo articolo a trace tramite un <b>insert</b> nella tabella t_trace con i seguenti campi:

                {
                    order_type_id: 15,
                    customer_for_billing,
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

          - Viene <u>aggiornato l'articolo mensile</u> con l'id della t_trace del record appena inserito

        - Se l'articolo_rinnovo ha il campo <b>trace_id diverso da NULL</b>:
          <br>
          Significa che è stato importato dalla t_trace, in questo caso viene effettuato un <b>update</b> sul record della t_trace con trace_id corrispondente:

                {
                  price,
                  serial_number,
                  due_date_maintenance,
                  date_import_trace: null, (per import in trace)
                  date_import_monthly: now(), (non deve essere reimportato)
                  create_operation: (in base all'articolo)
                }

    2.  Generazione ordine di rinnovo

        - Suddivisione fatturazione per cliente
          - i mensili con group_billing = 1 vengono divisi da quelli con group_billing = 0 e raggruppati per id cliente
        - Generazione ordini fatturazione per cliente

          - ?? Sincronizzazione configurazioni locali ??
          - Generazione ordine: <br>per ogni gruppo di mensili viene generato un ordine <u>utilizzando la configurazione del locale del rinnovo mensile con id più basso</u>, con i seguenti campi:

                {
                  data: now(),
                  cliente_fatt_alt,
                  cliente,
                  utente, (chi ha effettuato la richiesta)
                  totale,
                  date_insert,
                  tipo: 15, (rinnovo),
                  is_closed: 1,
                  stato: 7, (evaso)
                  pagamento,
                  data_evasione: now(),
                  mensile,
                  tipo_fatturazione
                }

          - Generazione articoli ordine: <br> gli articoli mensili di tutti gli articoli del gruppo vengono a loro volta <u>raggruppati per id articolo e prezzo</u>, aumentando la quantità di conseguenza, dopo di che vengono generati gli articoli ordine e associati all'ordine generato in precedenza con i seguenti campi:

                {
                  ordine,
                  articolo,
                  prezzo,
                  quantita,
                  sconto
                }

          - descrizione_articolo_ordine:
            - ...
            - ...

        - Generazione ordini per fatturazione classica

          - Generazione ordine: <br>per ogni mensile viene generato un ordine con i seguenti campi:

                {
                  data: now(),
                  cliente_fatt_alt,
                  cliente,
                  locale,
                  utente, (chi ha effettuato la richiesta)
                  totale,
                  date_insert,
                  tipo: 15, (rinnovo)
                  is_closed: 1,
                  stato: 7, (evaso)
                  pagamento,
                  data_evasione: now(),
                  mensile,
                  tipo_fatturazione
                }

          - Generazione articoli ordine: <br> gli articoli del mensile vengono <u>raggruppati per id articolo e prezzo</u>, aumentando la quantità di conseguenza e dopo di che associati all'ordine generato in precedenza con i seguenti campi:

                {
                  ordine,
                  articolo,
                  prezzo,
                  quantita,
                  sconto
                }

          - descrizione_articolo_ordine:
            - ...
            - ...

    3.  Aggiornamento mensili (per ogni mensile)

        - Calcolo la nuova data di scadenza del mensile come next_billing + tipo_fatturazione.mesi

                data.setMonth(data.getMonth() + tipo_fatturazione.mesi);

        - Controllo se esiste già un mensile per questo tipo di fatturazione, locale, mese e anno:
          - Se esiste sposto gli articoli nel mensile esistente e cancello il mensile vuoto
          - Altrimenti modifico la data di scadenza del mensile con la data calcolata

## Cambio piano

E' possibile effettuare un cambio piano (modifica dell'articolo) con tutti gli articoli appartenenti allo stesso gruppo e con mth_1 = 1;

E' disponibile uno specifico endpoint che per ogni articolo_mensile restituisce i possibili articoli sostituitivi.

Per gli articoli inseriti successivamente e quindi non ancora importati in trace la procedura di cambio piano non è disponibile, poichè il cambio piano in quel caso avviene tramite cancellazione diretta dell'articolo e inserimento id un nuovo articolo.

Controlli iniziali:

1. l'articolo mensile deve avere trace_id (non deve essere un nuovo articolo)
2. l'articolo selezionato per il cambio deve rientrare nelle opzioni di cambio piano dell'articolo mensile
3. l'articolo selezionato per il cambio deve avere id_trace compilato

Procedura cambio piano:

1. Modifico articolo, prezzo e matricola dell'articolo mensile
2. Invio la modifica dell'articolo, del prezzo e della matricola a trace

## Disdetta

E' possibile eliminare un articolo da un mensile effettuando la disdetta.

La disdetta dell'articolo di un mensile consiste in:

- scrittura disdetta nella t_deleted:

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

- invio disdetta a trace (se trace_id != null)

        {
          "deleted": 1,
          "date_import_trace": null
        }

- eliminazione dell'articolo mensile
- eliminazione del mensile (se non ci sono altri articoli)
