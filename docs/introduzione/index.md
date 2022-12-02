# Introduzione

T-Order è un software di difficile definizione, è stato sviluppato con [metodologia agile](https://it.wikipedia.org/wiki/Metodologia_agile) e per questo motivo fornisce una serie di funzionalità che sono state aggiunte in maniera incrementale complicando la categorizzazione.

Per questo piuttosto che definire che <u>cos'è</u> T-Order questa introduzione ha lo scopo di definire <u>cosa fa</u> T-Order ripercorrendo parte della sua storia e i vari sviluppi:

## 1. Preventivatore

T-Order è nato come <b>preventivatore</b>, le prime funzionalità introdotte erano finalizzate alla creazione di preventivi da inviare ai clienti.

In particolare sono state introdotte le seguenti funzioni:

- Salvataggio dell'anagrafica cliente e locali
- Salvataggio degli articoli con classificazione in gruppi e tipi
- Generazione dei preventivi
- Visualizzazione del preventivo in formato PDF
- Comunicazione con il cliente tramite Mail

## 2. Stati dell'ordine

Quasi subito è stato chiaro che T-Order poteva essere molto utile anche per gestire le fasi successive al preventivo ed è stato quindi introdotto il concetto di <b>stato</b> di un ordine.

Ogni ordine a questo punto può essere paragonato ad un percorso compiuto contemporaneamente da cliente e azienda:

1. <b>Preventivo</b>  
   la prima fase del percorso è quella del preventivo, in questa fase al cliente viene fatta una proposta che può decidere di accettare o meno
2. <b>Ordine</b>  
   Se la proposta viene accettata viene modificato lo stato del preventivo in ordine, in questa fase l'amministrazione dell'azienda genera l'<i>impegno</i> nel software di contabilità da inviare al cliente
3. <b>Impegno</b>  
   Dopo aver generato l'impegno lo stato dell'ordine viene modificato in impegno, in questa fase l'ordine è pronto per passare al reparto tecnico che si occuperà dell'effettiva preparazione del materiale per la consegna
4. <b>Lavorazione</b>  
   Dopo aver preparato tutto l'occorrente l'ordine passa allo stato lavorazione, questa fase corrisponde con l'effettiva consegna dei prodotti acquistati al cliente
5. <b>Evaso</b>  
   Quando l'ordine è stato completato e i prodotti sono stati consegnati al cliente l'ordine passa allo stato evaso, in questa fase l'amministrazione dell'azienda genera la <i>fattura</i> nel software di contabilità da inviare ai clienti

## 3. Rinnovi

Con il passare del tempo l'azienda si è mossa nella stessa direzione del mercato che spingeva sempre meno verso la vendita di prodotti e sempre più verso la vendita di servizi che, a differenza dei prodotti hardware, necessitano di pagamenti periodici.

Basandosi su questa necessità sono state aggiunte le funzionalità necessarie per generare delle scadenze periodiche utilizzando le informazioni presenti negli ordini evasi, gli ordini evasi vengono quindi letti periodicamente e per ogni articolo di tipo periodico all'interno di questi ordini viene generata la prima scadenza in una sezione apposita.

La logica dei rinnovi è suddivisa in due categorie principali, in base al tipo di articoli che possono essere inseriti all'interno.

- <b>Rinnovi Annuali/Biennali/31-12</b>  
   All'interno di questi rinnovi vengono importati tutti gli articoli di tipo annuale/biennale/31-12, questi rinnovi vengono rinnovati singolarmente
- <b>Rinnovi Mensili/Trimestrali/Semestrali</b>  
   All'interno di questi rinnovi vengono importati tutti gli articoli di tipo mensile, questi rinnovi vengono confermati contemporaneamente ogni mese

## 4. Integrazioni

Oltre a T-Order ci sono altri 2 software che vengono utilizzati all'interno dell'azienda, uno è [Trace](https://rcatrace.newchurchill.eu/login.jsp) che è un software utilizzato principalmente per l'organizzazione dei ticket, la gestione degli interventi e la consultazione delle anagrafiche clienti; l'altro è Cube, un software di contabilità che viene utilizzato per gestire tutta la parte contabile dell'azienda.

### Problema

Il passaggio di dati fra i 3 software, fino a questo punto, era manuale:

- Gli articoli venivano sincronizzati manualmente
- La scheda dei clienti/locali in Trace doveva essere modificata manualmente inserendo/rimuovendo prodotti e/o servizi in base agli ordini e alle disdette effettuate
- In Cube doveva essere generato manualmente l'impegno basandosi sull'ordine e poi scrivere nell'ordine relativo su T-Order il numero dell'impegno
- In Cube doveva essere generata manualmente la fattura basandosi sull'ordine e poi scrivere nell'ordine relativo su T-Order il numero della fattura e la data di fatturazione

### Soluzione

Con questo ulteriore passaggio sono stati automatizzati i passaggi di dati fra i 3 software, ora infatti:

- Gli articoli presenti in Cube vengono sincronizzati automaticamente con quelli presenti su T-Order.
- I clienti e locali nuovi creati in T-Order vengono sincronizzati automaticamente con Trace e Cube
- I prodotti e servizi del cliente presenti nella scheda cliente di Trace vengono aggiornati automaticamente in base ai nuovi ordini e le disdette effettuate in T-Order
- Ogni volta che un rinnovo viene confermato, nella scheda cliente di trace vengono aggiornati: la scadenza, la matricola e il prezzo
- Gli impegni vengono generati automaticamente in Cube in base agli ordini e automaticamente viene riportato nell'ordine il numero di impegno
- Le fatture vengono generate automaticamente in Cube in base agli ordini che vengono evasi e automaticamente viene riportato nell'ordine il numero della fattura e la data di fatturazione
- Tutti i dati sulle fatture e i pagamenti generati dal software di contabilità vengono resi disponibili a T-Order per qualsiasi utilizzo

## 5. Passaggi successivi

Successivamente sono state introdotte altre funzionalità e altre ancora sono già in programma, le ultime funzionalità aggiunte sono:

- Gestione pagamenti scaduti
- Statistiche tecniche e amministrative
