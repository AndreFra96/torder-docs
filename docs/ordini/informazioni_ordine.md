# Informazioni ordine

Ad ogni ordine sono associate diverse informazioni, alcune salvate nella tabella ordine e altre salvate in tabelle secondarie.

## Cliente

Ogni ordine deve essere associato ad un cliente, l'associazione con il cliente avviene tramite scrittura dell'id del cliente nel campo cliente della tabella ordine.

I clienti vengono sincronizzati bilateralmente con trace.

Il passaggio da trace a t-order avviene tramite scrittura nella tabella clienti, nel momento dell'inserimento trace compila il campo id_trace con un identificativo univoco relativo al cliente.

Il passaggio da t-order a trace avviene quando l'ordine si trova in fase ORDINE, prima di generare l'impegno infatti trace controlla se il cliente ha il campo trace_id a null e nel caso inserisce il cliente nel suo database e aggiorna il campo trace_id della tabella cliente con il nuovo id.

(Vedi documentazione sincronizzazioni per ulteriori informazioni)

## Locale

Ogni ordine può essere associato ad uno specifico locale di un cliente, l'associazione con il locale avviene tramite scrittura dell'id del locale nel campo locale della tabella ordine.

La sincronizzazione con trace avviene nello stesso modo in cui avviene la sincronizzazione dei clienti.

(Vedi documentazione sincronizzazioni per ulteriori informazioni)

## Articoli Ordine

Ad ogni ordine sono associati una serie di articoli, salvati nella tabella articolo_ordine.

Ogni articolo_ordine possiede una serie di informazioni:

- ordine &rarr; campo di associazione con l'ordine, contiene l'id dell'ordine di appartenenza
- articolo &rarr; campo di associazione con l'articolo, contiene l'id dell'articolo
- quantità
- prezzo &rarr; il prezzo di partenza può essere modificato rispetto al prezzo di base dell'articolo
- sconto &rarr; sconto sull'articolo

<u>Ordini con canoni</u>

Se il campo has_rid della tabella ordine è true significa che l'ordine in questione è un ordine con canone e gli unici articoli che possono essere associati sono gli articoli appartenenti ad un gruppo con mth_12 = 1 (mensili).

Questi ordini una volta evasi permetteranno di generare dei rinnovi mensili.

<u>Sconto sul Totale</u>

Oltre agli sconti effettuati sul singolo articolo è possibile effettuare uno sconto generale su tutto il carrello, questa informazione viene memorizzata tramite il campo totale della tabella ordine.

<u>Matricole e Date di attivazione</u>

Per ogni articolo ordine:

- l'inserimento della matricola è obbligatorio se l'articolo corrispondente all'articolo ordine ha need_serial = 1 oppure se ha need_serial_grenke = 1 e l'ordine ha grenke = 1

  ```
  need_serial == 1 || (need_serial_grenke == 1 && grenke == 1);
  ```

- l'inserimento della data di attivazione è obbligatorio se l'articolo corrispondente è un articolo di tipo rinnovo (mth_1 = 1 o mth_12 = 1 o mth_24 = 1 o new_year = 1)

  ```
  mth_1 == 1 || mth_12 == 1 || mth_24 == 1 || new_year == 1;
  ```

  Le matricole vengono salvate nella tabella matricola_articolo_ordine e le date di attivazione nella tabella attivazione_articolo_ordine.

Dato che la tabella articoli cliente prevede un campo quantità mentre la matricola o data di attivazione è da assegnare al singolo articolo le tabelle attivazione_articolo_ordine e matricola_articolo_ordine hanno un campo prg (intero progressivo), utilizzato per riferirsi ad uno spefico oggetto anche quando la quantità è maggiore di 1.

## Fatturazione

All'interno dell'ordine è necessario inserire una serie di informazioni che saranno utilizzate per la generazione della fattura:

- Tipo di fatturazione:

  Per ogni ordine è necessario definire un tipo per la fatturazione, i tipi disponibili cambiano in funzione del campo has_rid (ordine con canoni) dell'ordine - se has_rid = 1: - Fatturazione Mensile - Fatturazione Trimestrale - Fatturazione Semestrale - se has_rid = 0: - Singola Fatturazione

- Fatturazione alternativa:

  Per ogni ordine è possibile definire un secondo cliente al quale intestare la fattura, l'impostazione di un cliente per la fatturazione alternativa avviene tramite scrittura nel campo cliente_fatt_alt dell'id del cliente alternativo.

- Grenke:

  Indica un ordine di tipo grenke, questo campo viene impostato a 1 automaticamente quando viene selezionato il cliente grenke.

  Se questo campo è a 1 gli articoli inseriti nell'ordine con need_serial_grenke = 1 avranno bisogno della matricola

## Acconto

Quando un ordine si trova in stato preventivo è possibile associare un acconto, l'inserimento di un acconto comporta la creazione di un secondo ordine di acconto nel momento di passaggio dallo stato preventivo allo stato ORDINE.

L'inserimento dell'acconto avviene tramite scrittura dei campi down_payment (totale acconto) e down_payment_type (metodo di pagamento).

La creazione dell'acconto avviene quando down_payment è > 0, in tal caso se down_payment_type non corrisponde ad un metodo di pagamento viene sollevato un errore.

<u>L'ordine di acconto viene generato automaticamente nello stato evaso.</u>

## Pagamento

E' necessario associare ad ogni ordine un metodo di pagamento.

L'associazione avviene tramite scrittura nel campo pagamento della tabella ordine dell'id del metodo di pagamento.

<u>Attesa di pagamento</u>
<br>E' possibile bloccare il passaggio di stato di un ordine in attesa del pagamento impostando il campo wait_payment dell'ordine a 1.

## Informazioni tecniche

E' possibile inserire delle informazioni del reparto tecnico all'interno dell'ordine:

- tecnico &rarr; l'assegnazione di un ordine ad un tecnico prevede l'invio di una mail al tecnico interessato
- data_consegna
- note_tecniche

## Articoli cliente

All'interno di un ordine è possibile inserire degli articoli che sono già in possesso del cliente per poter sincronizzare l'informazione con trace.
Questi articoli vengono trattati in maniera diversa rispetto agli articolo_ordine e vengono salvati in una tabella dedicata (articolo_cliente_ordine).

E' possibile inserire in questa tabella tutti gli articoli appartenenti ad un gruppo con aggiungi_a_cliente = true.

## Allegati

E' possibile allegare ad un ordine diversi file, i file devono essere caricati tramite lo specifico enpoint.

## PDF

E' disponibile uno specifico endpoint che resitituisce un file PDF con una rappresentazione dell'ordine.
