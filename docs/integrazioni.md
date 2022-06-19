# Integrazioni

T-Order è integrato direttamente con due software: Trace e E.

Trace gestisce le anagrafiche dei clienti e il calendario degli interventi mentre E è un programma di contabilità che si occupa di generare impegni e fatture.

## Trace → T-order

Il passaggio di informazioni da Trace a T-order avviene tramite scrittura da parte di Trace nelle seguenti tabelle del database di T-Order (vecchio nome &rarr; nuovo nome):

- Clienti (t_customer &rarr; cliente)
  - customer_id_trace &rarr; id_trace
  - customer_ragsoc &rarr; ragsoc
  - customer_indirizzo &rarr; via
  - customer_cap &rarr; cap
  - customer_city &rarr; citta
  - customer_prov &rarr; provincia
  - customer_piva &rarr; piva
  - customer_codfisc &rarr; codfisc
- Locali (t_location &rarr; locale)
  - location_loc_desc &rarr; nome
  - location_address &rarr; via
  - location_city &rarr; citta
  - location_provincia &rarr; prov
  - location_telephone &rarr; tel
  - location_telephone1 &rarr; #ELIMINATO
  - location_telephone2 &rarr; #ELIMINATO
  - location_mail &rarr; mail
- Articoli (t_article &rarr; articolo)
  - article_id_trace &rarr; id_trace
  - article_title &rarr; title
  - article_grp &rarr; gruppo
  - cost_price &rarr; costo
  - active &rarr; attivo
  - import_trace &rarr; import_trace
  - data_insert &rarr; data_insert
  - data_update &rarr; data_update
- Gruppi Articoli (t_group &rarr; gruppo)
  - group_loc_desc &rarr; descrizione
  - group_id_trace &rarr; id_trace
  - group_order &rarr; #ELIMINATO
  - group_type_id &rarr; tipo_gruppo
- Prezzi (t_article_price &rarr; prezzo)
  - cod_art &rarr; cod_art
  - cod_listino &rarr; cod_listino
  - prg_listino &rarr; prg_listino
  - prz_listino &rarr; prz_listino
  - data_insert &rarr; data_insert
  - data_update &rarr; data_update
- t_trace:
  - Nuovi articoli cliente

## T-order → Trace

- Trace legge da t_trace se date_import_trace è null & tipo != 5
  - Se deleted = 1: (Disdetta)
    - Effettua disdetta basata su trace_id
  - Se id_trace non è compilato: (Creazione)
    - customer_id
    - prg_location
    - article_id
    - serial_number
    - installation_date
    - due_date_maintenance
  - Se id_trace è compilato: (Modifica)
    - customer_id
    - prg_location
    - article_id
    - serial_number
    - installation_date
    - due_date_maintenance
- Trace legge z_trace_scaduti ??

## E → T-order

- E scrive nelle tabelle:
  - ex_insoluti
  - ex_invoice
  - ex_invoice_item
  - ex_scaduti
  - Metodi di pagamento (t_payment_esatto)
- E effettua modifiche:
  - cambia stato ordine &rarr; impegno (ordine)
  - ordine.order_id_esatto (numero impegno)
  - ordine.is_billed (data_fatturazione)
  - ordine.has_rid (appalto)
  - ordine.rid_date
  - ordine.invoice_nr (numero fattura)
  - ordine.impegno_nr (numero impegno)
  - ordine.invoice_id (id fattura)
  - articolo_ordine.date_esatto (data import e)
  - articolo_ordine.item_id_esatto (id item e)
  - t_order_item_desc.date_import_e (data import e)
  - t_order_item_desc.id_esatto (id e)
  - cliente.id_trace (aggiorna cliente con id_trace)
  - locale.prg (aggiorna locale con prg)

## T-order → E

- E legge da viste:
  - e_order (unione di e_order_customer e e_order_customer_fb)
  - e_order_item
  - e_ratei
  - e_rinnovi
  - e_rinnovi_item
  - e_rinnovi_item_desc

## t_contact

La tabella t_contact è direttamente condivisa fra Trace e T-Order e contiene i contatti dei clienti.

Trace legge e scrive senza nostri id cliente/locale.

## Creazione nuovi clienti/locali:

Procedura di generazione di nuovi clienti/locali a partire da T-Order:

1. e legge vista preventivo con nuovo cliente/locale
2. crea anagrafica cliente
3. crea anagrafica locale
4. aggiorna il nostro database con id cliente (via piva)
5. aggiorna il nostro database con prg locale (locale senza prg con piva)
