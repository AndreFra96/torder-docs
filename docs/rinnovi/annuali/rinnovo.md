# Rinnovo

Ogni rinnovo può essere confermato (rinnovato), la conferma di un rinnovo consiste in:

## 1. Controllo iniziale

Prima di effettuare il rinnovo viene controllato che:

- Il rinnovo non sia completato
- Il rinnovo abbia un cliente valido
- Il rinnovo abbia un locale valido
- Il rinnovo abbia un metodo di pagamento valido

Se almeno una di queste condizioni non è verificata viene restituito un messaggio di errore e il rinnovo non viene confermato.

## 2. Salvataggio storico

Viene salvata una copia di ogni articolo del rinnovo all'interno di una specifica tabella dedicata allo storico, per future estrazioni di dati e statistiche

## 3. Invio a trace

In questa fase i dati del rinnovo vengono sincronizzati con trace, in particolare avviene:

- Modifica delle date di scadenza degli articoli nella scheda cliente di trace
- Importazione degli articoli che erano stati inseriti tramite [inserimento nuovi articoli](../inserimento)
- Invio delle modifiche di prezzo o matricola degli articoli del rinnovo
- Creazione dell'intervento per gli articoli configurati con 'crea intervento'

### Note tecniche

`Calcolo della nuova data di scadenza`

: La nuova data di scadenza viene calcolata per ogni articolo basandosi sulla scadenza attuale e il tipo di articolo, se l'articolo è annuale o al 31/12 viene aggiunto un anno alla data di scadenza se invece è biennale vengono aggiunti due anni

Dopo la prima fase comune di calcolo della nuova scadenza l'import in trace prende due percorsi diversi, quello classico se l'articolo è stato importato tramite [generazione rinnovo](../generazione) e uno alternativo se è stato inserito tramite [inserimento nuovi articoli](../inserimento):

#### Percorso classico

Il percorso classico prevede che l'articolo sia già presente in trace e consiste quindi in una modifica del record relativo a quell'articolo nella tabella di scambio.

Ogni articolo di un rinnovo conserva l'id del record della tabella di scambio dalla quale proviene, viene quindi effettuata una query di update nella tabella di scambio per il record corrispondente con i seguenti parametri:

```
{
    price, (prezzo aggiornato)
    serial_number, (matricola aggiornata)
    due_date_maintenance, (scadenza calcolata)
    date_import_trace: null, (impostato a null per forzare trace a leggere nuovamente il record)
    date_import_rinnovi: null (impostato a null per importare il prossimo rinnovo)
    create_operation (generazione dell'intervento, in base all'articolo)
}
```

#### Percorso alternativo

Il percorso alternativo prevede che l'articolo sia stato inserito direttamente all'interno del rinnovo e che quindi ancora non esista un record ad esso collegato nella tabella di scambio, è necessario quindi effettuare una query di insert nella tabella di scambio con i seguenti parametri:

```
{
  order_type_id: 15, (il tipo 15 è riconosciuto da trace come rinnovo)
  customer_for_billing, (cliente per la fatturazione alternativa)
  customer_id, (cliente)
  prg_location, (locale)
  article_id, (articolo)
  price, (prezzo)
  serial_number, (matricola)
  installation_date: now(), (data di installazione impostata al momento attuale)
  due_date_maintenance, (scadenza calcolata)
  type_billing, (tipo di fatturazione)
  payment_type, (metodo di pagamento)
  create_operation (generazione dell'intervento, in base all'articolo)
}
```

## 4. Generazione ordine e fattura

In seguito alla conferma di un rinnovo viene generato un ordine in stato evaso, da questo ordine viene generata la fattura nel software di contabilità.

### Generazione ordine da rinnovo

La conversione di un rinnovo in ordine avviene in questo modo:

- Viene generato un ordine di tipo rinnovo, in stato evaso con lo stesso cliente e lo stesso locale del rinnovo
- Se presente viene impostato il cliente per la fatturazione alternativa basandosi sui dati contenuti nella [configurazione rinnovo locale](../configurazione)
- Vengono inserite nel campo note amministrative le note contenute nella [configurazione rinnovo locale](../configurazione)
- Viene impostato il metodo di pagamento dell'ordine basandosi sul metodo di pagamento impostato nella [configurazione rinnovo locale](../configurazione)
- Vengono generati gli articoli dell'ordine raggruppando gli articoli del rinnovo per articolo, prezzo e sconto (lo sconto viene convertito da cifra a percentuale)

### Generazione fattura

Dal momento in cui l'ordine viene creato viene reso disponibile al software di contabilità per la generazione della fattura, una volta generata la fattura viene scritto il numero di fattura all'interno dell'ordine.

### Note tecniche

## 5. Chiusura rinnovo

A questo punto il rinnovo viene chiuso e non è più visibile.

### Note tecniche

La chiusura del rinnovo consiste nell'eliminazione di tutti gli articolo_rinnovo e nell'impostazione del campo completato del rinnovo a 1

## 6. Import nuove scadenze

A questo punto viene generato il nuovo rinnovo con le scadenze aggiornate.

### Note tecniche

La generazione del nuovo rinnovo avviene tramite la classica procedura di [generazione rinnovo](../generazione) poichè in fase di [invio a trace](#3-invio-a-trace) è stato impostato a null il campo 'date_import_rinnovi' viene letto come un qualsiasi nuovo rinnovo
