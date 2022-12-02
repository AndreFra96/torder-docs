# Mail

T-Order permette di inviare mail di notifica agli utenti e mail di comunicazione ai clienti, i due tipi di mail vengono mandate da due indirizzi diversi.

## Mail interne

Le mail interne, ovvero le notifiche destinate agli utenti dell'applicazione, vengono inviate dall'indirizzo `noreply@rcamilano.it` e la selezione dei destinatari avviene in tre modi:

1. Tramite i metadati degli utenti personalizzabili nel pannello di controllo di Auth0
2. Tramite ricerca dell'indizzo mail dell'utente o tecnico assegnato nel caso di notifiche su ordini
3. Tramite estrazione dell'utente che ha effettuato una particolare richiesta al backend

### Passaggi di stato

#### &rarr; ordine

Mail di notifica inviata automaticamente nel momento in cui un documento viene trasformato nello stato ordine.

##### Destinatari

1. Tutti gli utenti che hanno `ordine_da_preventivo`
2. Sia il tecnico che l'utente assegnati all'ordine
3. -

#### &rarr; evaso

Mail di notifica inviata automaticamente nel momento in cui un documento viene trasformato nello stato evaso

##### Destinatari

1. Tutti gli utenti che hanno `ordine_evaso`
2. -
3. -

### Errore conferma cliente

Mail di notifica inviata automaticamente nel momento in cui un cliente tenta di confermare un preventivo ma non è possibile trasformarlo in ordine perchè alcuni campi sono mancanti.

#### Destinatari

1. Tutti gli utenti che hanno `errore_conferma_cliente`
2. L'utente assegnato all'ordine
3. -

### Generazione ordine da rinnovo

Mail di notifica inviata automaticamente nel momento in cui viene generato un ordine tramite conferma di un rinnovo annuale

#### Destinatari

1. Tutti gli utenti che hanno `ordine_da_rinnovo`
2. -
3. -

### Modifica tecnico assegnato

Mail di notifica inviata automaticamente nel momento in cui viene modificato il tecnico assegnato ad un documento che si trova in uno stato diverso da `Preventivo``

#### Destinatari

1. -
2. Nuovo tecnico assegnato all'ordine
3. -

### Posticipo rinnovo

Mail di notifica inviata automaticamente nel momento in cui viene eseguito il posticipo di un rinnovo annuale

1. Tutti gli utenti che hanno `posticipo_rinnovo`
2. -
3. Utente che ha effettuato la richiesta del posticipo

## Mail esterne

Le mail esterne sono tutte quelle inviate ai clienti dell'azienda, queste mail vengono inviate utilizzando l'indirizzo `commerciale@rcamilano.it`.

### Preventivo

La mail preventivo è un tipo di mail destinata ai clienti alla quale viene aggiunto un QR code e viene allegato automaticamente il PDF relativo al documento inviato.
