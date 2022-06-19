# Logiche di business

Oltre agli endpoint che forniscono le funzionalità CRUD sono presenti altri endpoint per le logiche di business più complesse, tendenzialmente annidata all'interno degli endpoint della tabella che li riguarda maggiormente.

## Articolo

Logiche di business articolo:

### Articoli figli

`GET articolo/{id}/childrens`

Restituisce ricorsivamente gli articoli figli di uno specifico articolo, utilizzando i dati contenuti nella tabella article_parent.

## Articolo Mensile

Logiche di business articolo mensile:

### Disdetta mensile

`PUT articoloMensile/{id}/disdetta`

Effettua la disdetta di un articolo di un mensile comunicando la disdetta a trace nel caso in cui l'articolo non sia un nuovo articolo e cancellando il mensile se non sono presenti altri articoli nello stesso mensile

### Cambio Piano Mensile

`PUT articoloMensile/{id}/cambioPiano`

Esegue il cambio piano dell'articolo mensile con un altro articolo

### Opzioni Cambio Piano Mensile

`GET articoloMensile/{id}/opzioniCambioPiano`

Restituisce gli articoli con i quasi è possibile effettuare il cambio piano

## Articolo Ordine

Logiche di business articolo ordine:

### Cancella articoli ordine

`DELETE articoloOrdine/ordine/{id}`

Cancella tutti gli articoli allegati ad un ordine

## Articolo Rinnovo

Logiche di business articolo rinnovo:

### Disdetta rinnovo

`PUT articoloRinnovo/{id}/disdetta`

Effettua la disdetta di un articolo di un rinnovo comunicando la disdetta a trace nel caso in cui l'articolo non sia un nuovo articolo e impostando il rinnovo a completato se non sono presenti altri articoli nello stesso rinnovo

### Cambio Piano Rinnovo

`PUT articoloRinnovo/{id}/cambioPiano`

Esegue il cambio piano dell'articolo rinnovo con un altro articolo

### Opzioni Cambio Piano Rinnovo

`GET articoloRinnovo/{id}/opzioniCambioPiano`

Restituisce gli articoli con i quasi è possibile effettuare il cambio piano

## Mensile:

Logiche di business mensile:

### Genera Fatture

`PUT mensile/generaFatture`

Esegue la generazione delle fatture per tutti i mensili del mese attuale.

### Totale Profili Mensile

`GET mensile/totaleProfili/{mese}/{anno}`

Restituisce il totale dei rinnovi mensili di un certo mese e anno raggruppati per profilo locale

## Ordine

Logiche di business ordine:

### Ottieni stati disponibili

`GET ordine/{id}/availableStatus`

Restituisce i possibili stati con i quali è possibile modificare lo stato dell'ordine

### Modifica stato

`PUT ordine/{id}/stato/{stato}`

Effettua la modifica dello stato di un ordine con prima tutti i controlli e le azioni necessarie.

Ottieni ulteriori informazioni sui [passaggi di stato](/ordini/ciclo_ordine/#passaggi-di-stato) nella sezione dedicata

### Ottieni matricole e attivazioni

`GET ordine/{id}/serialActivation`

Restituisce lo stato di inserimento delle matricole e date di attivazioni all'interno dell'ordine.

Questo endpoint mette in relazione gli articoli dell'ordine con le matricole e le date di attivazione che sono state inserite.

Il risultato ottenuto è una rappresentazione dello stato attuale di inserimento delle matricole e date di attivazione dove è possibile sapere quali articoli hanno bisogno di matricola / attivazione, per quali sono già state inserite e quali sono i valori che sono eventualmente stati inseriti.

### Cancella matricole e attivazioni

`DELETE ordine/{id}/serialActivation`

Permette di cancellare tutte le matricole e le date di attivazione che sono state inserite per un ordine.

Questo endpoint è necessario in caso di modifica degli articoli di un ordine.

## Rinnovo

Logiche di business rinnovo:

### Rinnova

`PUT rinnovo/{id}/rinnova`

Effettua la conferma di un rinnovo

### Totale Profili Rinnovo

`GET rinnovo/totaleProfili/{mese}/{anno}`

Restituisce il totale dei rinnovi di un certo mese e anno raggruppati per profilo locale

## T Payment Esatto

Logiche di business t_payment_esatto (metodi di pagamento):

### Pagamento Canoni

`GET tPaymentEsatto/canoni`

Ottieni tutti i metodi di pagamento di tipo canone

## T Trace

Logiche di business t_trace:

### Contratto locale

`GET tTrace/contratto/{cliente}/{locale}`

Restituisce il contratto di un cliente relativo ad uno specifico locale

### Contratto generale

`GET tTrace/contratto/{cliente}`

Restituisce il contratto di un cliente relativo a tutti i locali
