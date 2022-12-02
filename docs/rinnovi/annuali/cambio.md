# Cambio piano

E' possibile effettuare un cambio piano (modifica dell'articolo) con tutti gli articoli appartenenti allo stesso gruppo e con lo stesso tipo di scadenza (annuale,biennale,31/12).

(Note tecniche) E' disponibile uno specifico endpoint che per ogni articolo_rinnovo restituisce i possibili articoli sostituitivi.

Per gli articoli inseriti tramite [inserimento nuovi articoli](../inserimento) la procedura di cambio piano non è disponibile, poichè il cambio piano in quel caso avviene tramite cancellazione diretta dell'articolo e inserimento di un nuovo articolo.

## Controlli iniziali

Nel momento in cui viene avviata la procedura di cambio piano vengono effettuati alcuni controlli sull'articolo del rinnovo:

1. l'articolo rinnovo non deve essere stato inserito tramite [inserimento nuovi articoli](../inserimento)
2. l'articolo selezionato per il cambio deve rientrare nelle opzioni di cambio piano dell'articolo rinnovo
3. l'articolo selezionato per il cambio deve esistere in trace
   1. (Note tecniche) l'articolo deve avere trace_id

## Cambio

Il cambio piano consiste in:

1. Modifica prezzo, articolo e matricola dell'articolo nel rinnovo con quelli del nuovo articolo
2. Invio della modifica dell'articolo, del prezzo e della matricola a trace

## Cambio con anticipo scadenza

La procedura di cambio piano prevede la possibilità di anticipare la scadenza dell'articolo alla data attuale, in questo caso oltre ad effettuare il cambio di piano dell'articolo verrà anche modificata la scadenza del singolo articolo impostandola ad oggi.

Nello specifico il cambio piano con anticipo della scadenza consiste in:

1. Modifica prezzo, articolo, matricola e scadenza (oggi) dell'articolo nel rinnovo con quelli del nuovo articolo
2. Controllo se esiste già un rinnovo dello stesso locale nel mese attuale
3. Se non esiste creazione di un nuovo rinnovo nel mese attuale
4. Inserimento dell'articolo all'interno del rinnovo nel mese attuale
5. Invio della modifica dell'articolo, del prezzo, della matricola e della scadenza a trace
6. Se non sono presenti altri articoli all'interno del rinnovo imposto il rinnovo a completato
