# Ciclo dell'ordine

Ogni ordine segue un ciclo specifico che parte dallo stato di preventivo e termina nello stato evaso.

Questo ciclo deve avvenire in parallelo alle operazioni fisiche e burocratiche necessarie per completare la consegna dell'ordine.

## Fasi

Il ciclo dell'ordine comprende 5 fasi:

1. Preventivo
   <br> E' lo stato iniziale di ogni ordine e rappresenta il momento dell'offerta al cliente, permette l'inserimento di molte informazioni mantenendone la maggior parte non obbligatorie. In questo modo è possibile creare un preventivo iniziale con le informazioni in possesso per poi integrarle in seguito.
2. Ordine
   <br> E' il primo stato successivo alla conferma del preventivo, il passaggio a questo stato rappresenta il raggiunto accordo con il cliente sull'ordine e permette di procedere ai passaggi successivi.
   <br> Per effettuare il passaggio ad ordine è necessario inserire buona parte delle informazioni che erano facoltative in fase di preventivo.
   <br> Gli ordini in questo stato vengono letti dal programma di contabilità che genera l'impegno e modifica lo stato impostandolo ad impegno.
3. Impegno
   <br> Quando un ordine giunge in questo stato significa che è stato generato correttamente l'impegno in contabilità e, dopo i necessari controlli, è possibile passare allo stato lavorazione
4. Lavorazione
   <br> Lo stato in lavorazione indica che è in corso la fase di preparazione del materiale e di consegna al cliente.
5. Evaso
   <br> E' lo stato finale di un ordine, quando un ordine giunge in questo stato significa che il ciclo è completato e gli articoli inseriti possono essere sincronizzati con trace e letti dal programma di contabilità per procedere alla generazione della fattura.

## Passaggi di stato

Quando un ordine viene creato si trova in fase di preventivo, nel passaggio agli stati successivi vengono effettuate diverse operazioni che è possibile suddividere in 2 categorie: controlli e azioni.

I controlli e le azioni vengono effettuati prima del passaggio di stato tramite un middleware inserito nell'endpoint di modifica stato di un ordine.

Per ogni ordine viene controllato che lo stato di destinazione non sia uguale allo stato attuale e che sia compatibile con lo stato dell'ordine attuale.

<u>Calcolo stati disponibili:</u>

```
switch (ordine.stato) {
  case 1:
    if (ordine.deleted)
      stati_disponibili = [
        { status_id: 0, status_loc_desc: "CANCELLATO", active: true },
        { status_id: 1, status_loc_desc: "ARCHIVIATO", active: false },
        { status_id: 2, status_loc_desc: "PREVENTIVO", active: false },
      ];
    else
      stati_disponibili = [
        { status_id: 0, status_loc_desc: "CANCELLATO", active: false },
        { status_id: 1, status_loc_desc: "ARCHIVIATO", active: true },
        { status_id: 2, status_loc_desc: "PREVENTIVO", active: false },
      ];
    break;
  case 2:
    stati_disponibili = [
      { status_id: 0, status_loc_desc: "CANCELLATO", active: false },
      { status_id: 1, status_loc_desc: "ARCHIVIATO", active: false },
      { status_id: 2, status_loc_desc: "PREVENTIVO", active: true },
      { status_id: 3, status_loc_desc: "ORDINE", active: false },
    ];
    break;
  case 3:
    stati_disponibili = [
      { status_id: 3, status_loc_desc: "ORDINE", active: true },
    ];
    break;
  case 5:
    if (ordine.data_fatturazione == null)
      stati_disponibili = [
        { status_id: 5, status_loc_desc: "IMPEGNO", active: true },
        { status_id: 6, status_loc_desc: "LAVORAZIONE", active: false },
        { status_id: 0, status_loc_desc: "CANCELLATO", active: false },
      ];
    else
      stati_disponibili = [
        { status_id: 5, status_loc_desc: "IMPEGNO", active: true },
        { status_id: 6, status_loc_desc: "LAVORAZIONE", active: false },
      ];
    break;
  case 6:
    if (ordine.data_fatturazione == null)
      stati_disponibili = [
        { status_id: 6, status_loc_desc: "LAVORAZIONE", active: true },
        { status_id: 7, status_loc_desc: "EVASO", active: false },
        { status_id: 0, status_loc_desc: "CANCELLATO", active: false },
      ];
    else
      stati_disponibili = [
        { status_id: 6, status_loc_desc: "LAVORAZIONE", active: true },
        { status_id: 7, status_loc_desc: "EVASO", active: false },
      ];
    break;
  case 7:
    if (ordine.data_fatturazione == null)
      stati_disponibili = [
        { status_id: 7, status_loc_desc: "EVASO", active: true },
        { status_id: 0, status_loc_desc: "CANCELLATO", active: false },
      ];
    else
      stati_disponibili = [
        { status_id: 7, status_loc_desc: "EVASO", active: true },
      ];
    break;
  default:
    stati_disponibili = [];
}
```

<u> Controlli specifici per stato: </u>

I controlli e le azioni effettuati in seguito dipendono dallo stato di destinazione dell'ordine, se i controlli o le azioni sollevano un errore il passaggio di stato non viene eseguito

- &rarr; Preventivo (2)
  - Azioni:
    - Aggiorno la data dell'ordine impostando la data attuale
- &rarr; Ordine (3)
  - Controlli:
    - Campi obbligatori locale (loc_desc,via,citta,prov,profilo_locale)
    - Campi obbligatori cliente (ragosc,via,cap,citta,provincia,piva)
    - IBAN obbligatorio se pagamento con sdd
    - Note tecniche obbligatorie in base agli articoli inseriti (se c'è almeno un articolo con order_note = 1 note_tecniche è obbligatorio)
  - Azioni:
    - Aggiorno la data dell'ordine impostando la data attuale
    - Generazione ordine di acconto (se down_payment > 0)
    - Invio mail creazione ordine
- &rarr; Lavorazione (6)
  - Controlli:
    - ordine non in attesa di pagamento (wait_payment)
- &rarr; Evaso (7)
  - Controlli:
    - ordine non in attesa di pagamento (wait_payment)
    - sono state inserite le matricole e attivazioni necessarie
    - prg locale obbligatorio
    - id_trace cliente obbligatorio
  - Azioni:
    - Aggiorno la data_evasione dell'ordine con la data attuale
    - Eseguo import ordine in trace (compresi articoli cliente)
