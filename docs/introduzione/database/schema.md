# Schema

<<<<<<< HEAD:docs/introduzione/database/schema.md
=======

>>>>>>> c382f95de7264b96fd1c025b216424e7c372d4d4:docs/architettura/database/schema.md
## article_parent

| Id  | Descrizione | Tipo | Dimensione |
| --- | ----------- | ---- | ---------- |
| 1   | parent      | int  | 4          |
| 2   | child       | int  | 4          |

## articolo

| Id  | Descrizione        | Tipo      | Dimensione |
| --- | ------------------ | --------- | ---------- |
| 1   | id                 | int       | 4          |
| 2   | title              | nvarchar  | 200        |
| 3   | descrizione        | nvarchar  | 2000       |
| 4   | gruppo             | nvarchar  | 40         |
| 5   | immagine           | nvarchar  | 490        |
| 6   | id_trace           | nvarchar  | 490        |
| 7   | costo              | decimal   | 9          |
| 8   | data_insert        | datetime2 | 6          |
| 9   | data_update        | datetime2 | 6          |
| 10  | attivo             | binary    | 1          |
| 11  | import_trace       | binary    | 1          |
| 12  | need_serial        | binary    | 1          |
| 13  | need_serial_grenke | binary    | 1          |
| 14  | mth_12             | binary    | 1          |
| 15  | mth_24             | binary    | 1          |
| 16  | mth_1              | binary    | 1          |
| 17  | new_year           | binary    | 1          |
| 18  | tipo_articolo      | int       | 4          |
| 19  | cassaincloud_id    | int       | 4          |
| 20  | order_note         | binary    | 1          |
| 21  | article_app_title  | nvarchar  | 2048       |
| 22  | crea_intervento    | binary    | 1          |
| 23  | support_telephone  | binary    | 1          |
| 24  | support_week       | binary    | 1          |

## articolo_cliente_ordine

| Id  | Descrizione | Tipo     | Dimensione |
| --- | ----------- | -------- | ---------- |
| 1   | ordine      | int      | 4          |
| 2   | articolo    | int      | 4          |
| 3   | prg         | int      | 4          |
| 4   | attivazione | date     | 3          |
| 5   | matricola   | nvarchar | 500        |

## articolo_mensile

| Id  | Descrizione | Tipo     | Dimensione |
| --- | ----------- | -------- | ---------- |
| 1   | id          | int      | 4          |
| 2   | mensile     | int      | 4          |
| 3   | articolo    | int      | 4          |
| 4   | price       | decimal  | 9          |
| 5   | matricola   | nvarchar | 490        |
| 6   | t_trace     | int      | 4          |

## articolo_ordine

| Id  | Descrizione      | Tipo    | Dimensione |
| --- | ---------------- | ------- | ---------- |
| 1   | id               | int     | 4          |
| 2   | ordine           | int     | 4          |
| 3   | articolo         | int     | 4          |
| 4   | prezzo           | decimal | 9          |
| 5   | quantita         | int     | 4          |
| 6   | sconto           | decimal | 9          |
| 7   | articolo_rinnovo | int     | 4          |
| 8   | date_esatto      | date    | 3          |
| 9   | item_id_esatto   | int     | 4          |

## articolo_rinnovo

| Id  | Descrizione   | Tipo     | Dimensione |
| --- | ------------- | -------- | ---------- |
| 1   | id            | int      | 4          |
| 2   | rinnovo       | int      | 4          |
| 3   | articolo      | int      | 4          |
| 4   | prezzo        | decimal  | 9          |
| 5   | matricola     | nvarchar | 490        |
| 6   | data_scadenza | date     | 3          |
| 7   | data_rinnovo  | date     | 3          |
| 8   | t_trace       | int      | 4          |
| 9   | sconto        | decimal  | 9          |
| 10  | proponi       | binary   | 1          |

## articolo_rinnovo_storico

| Id  | Descrizione      | Tipo    | Dimensione |
| --- | ---------------- | ------- | ---------- |
| 1   | id               | int     | 4          |
| 2   | rinnovo          | int     | 4          |
| 3   | articolo         | int     | 4          |
| 4   | prezzo           | decimal | 9          |
| 5   | matricola        | varchar | 245        |
| 6   | data_scadenza    | date    | 3          |
| 7   | data_rinnovo     | date    | 3          |
| 8   | t_trace          | int     | 4          |
| 9   | sconto           | decimal | 9          |
| 10  | proponi          | binary  | 1          |
| 11  | data_inserimento | date    | 3          |

## attivazione_articolo_ordine

| Id  | Descrizione     | Tipo | Dimensione |
| --- | --------------- | ---- | ---------- |
| 1   | articolo_ordine | int  | 4          |
| 2   | prg             | int  | 4          |
| 3   | attivazione     | date | 3          |

## cambio_piano

| Id  | Descrizione         | Tipo      | Dimensione |
| --- | ------------------- | --------- | ---------- |
| 1   | id                  | int       | 4          |
| 2   | articolo_precedente | int       | 4          |
| 3   | articolo_successivo | int       | 4          |
| 4   | prezzo_precedente   | decimal   | 9          |
| 5   | prezzo_successivo   | decimal   | 9          |
| 6   | cliente             | int       | 4          |
| 7   | locale              | int       | 4          |
| 8   | data                | datetime2 | 6          |
| 9   | utente              | int       | 4          |

## cliente

| Id  | Descrizione    | Tipo     | Dimensione |
| --- | -------------- | -------- | ---------- |
| 1   | id             | int      | 4          |
| 2   | id_trace       | nvarchar | 20         |
| 3   | nome_locale    | nvarchar | 120        |
| 4   | ragsoc         | nvarchar | 120        |
| 5   | via            | nvarchar | 510        |
| 6   | cap            | nvarchar | 20         |
| 7   | citta          | nvarchar | 200        |
| 8   | provincia      | nvarchar | 100        |
| 9   | piva           | nvarchar | 32         |
| 10  | codfisc        | nvarchar | 32         |
| 11  | tel            | nvarchar | 36         |
| 12  | cell           | nvarchar | 36         |
| 13  | mail           | nvarchar | 510        |
| 14  | contatto       | nvarchar | 80         |
| 15  | notecli        | nvarchar | -1         |
| 16  | notepriv       | nvarchar | 300        |
| 17  | utente_scaduto | int      | 4          |
| 18  | pagamento      | nvarchar | 40         |
| 19  | pec            | nvarchar | 200        |
| 20  | sdi            | nvarchar | 14         |
| 21  | data_insert    | date     | 3          |
| 22  | data_update    | date     | 3          |
| 23  | iban           | nvarchar | 500        |
| 24  | app_pwd        | nvarchar | 100        |
| 25  | iva_esente     | binary   | 1          |

## configurazione_mensile_locale

| Id  | Descrizione              | Tipo    | Dimensione |
| --- | ------------------------ | ------- | ---------- |
| 1   | locale                   | int     | 4          |
| 2   | pagamento                | int     | 4          |
| 3   | note                     | varchar | 1024       |
| 4   | fatturazione_alternativa | int     | 4          |

## configurazione_rinnovo_locale

| Id  | Descrizione              | Tipo    | Dimensione |
| --- | ------------------------ | ------- | ---------- |
| 1   | locale                   | int     | 4          |
| 2   | pagamento                | int     | 4          |
| 3   | note                     | varchar | 1024       |
| 4   | tacito_rinnovo           | binary  | 1          |
| 5   | fatturazione_alternativa | int     | 4          |

## contatto

| Id  | Descrizione      | Tipo      | Dimensione |
| --- | ---------------- | --------- | ---------- |
| 1   | id               | int       | 4          |
| 2   | cliente          | int       | 4          |
| 3   | id_trace         | nvarchar  | 100        |
| 4   | locale           | int       | 4          |
| 5   | prg              | int       | 4          |
| 6   | all_location     | int       | 4          |
| 7   | mail             | nvarchar  | 490        |
| 8   | telephone        | nvarchar  | 490        |
| 9   | reference        | nvarchar  | 490        |
| 10  | date_update      | datetime2 | 6          |
| 11  | active           | int       | 4          |
| 12  | profilo_contatto | int       | 4          |

## costruttore

| Id  | Descrizione | Tipo     | Dimensione |
| --- | ----------- | -------- | ---------- |
| 1   | articolo    | int      | 4          |
| 2   | nome        | nvarchar | 100        |

## disdetta

| Id  | Descrizione        | Tipo      | Dimensione |
| --- | ------------------ | --------- | ---------- |
| 1   | id                 | int       | 4          |
| 2   | articolo           | int       | 4          |
| 3   | prezzo             | decimal   | 9          |
| 4   | matricola          | nvarchar  | 490        |
| 5   | data_scadenza      | date      | 3          |
| 6   | data_cancellazione | datetime2 | 6          |
| 7   | cliente            | int       | 4          |
| 8   | locale             | int       | 4          |
| 9   | motivazione        | int       | 4          |
| 10  | utente             | int       | 4          |
| 11  | note               | nvarchar  | 490        |

## ex_insoluti

| Id  | Descrizione      | Tipo    | Dimensione |
| --- | ---------------- | ------- | ---------- |
| 1   | id_insoluto      | varchar | 50         |
| 2   | id_customer      | bigint  | 8          |
| 3   | date_insoluto    | varchar | 50         |
| 4   | total_insoluto   | real    | 4          |
| 5   | desc_insoluto    | varchar | 50         |
| 6   | pagato           | bigint  | 8          |
| 7   | date_insert      | varchar | 50         |
| 8   | date_last_update | varchar | 50         |

## ex_invoice

| Id  | Descrizione         | Tipo    | Dimensione |
| --- | ------------------- | ------- | ---------- |
| 1   | invoice_id          | varchar | 50         |
| 2   | id_customer         | bigint  | 8          |
| 3   | invoice_nr          | bigint  | 8          |
| 4   | invoice_date_billed | varchar | 50         |
| 5   | total_invoice       | real    | 4          |
| 6   | discount            | varchar | 50         |
| 7   | management_fees     | real    | 4          |
| 8   | payment_id          | bigint  | 8          |
| 9   | is_notacredito      | bigint  | 8          |
| 10  | is_acconto          | bigint  | 8          |

## ex_invoice_item

| Id  | Descrizione | Tipo    | Dimensione |
| --- | ----------- | ------- | ---------- |
| 1   | item_id     | bigint  | 8          |
| 2   | invoice_id  | varchar | 50         |
| 3   | article_id  | varchar | 50         |
| 4   | item_qty    | real    | 4          |
| 5   | item_price  | real    | 4          |
| 6   | is_discount | bigint  | 8          |

## ex_scaduti

| Id  | Descrizione        | Tipo    | Dimensione |
| --- | ------------------ | ------- | ---------- |
| 1   | id_scaduto         | varchar | 50         |
| 2   | id_customer        | bigint  | 8          |
| 3   | invoice_id         | varchar | 50         |
| 4   | payment_id_scaduto | varchar | 50         |
| 5   | date_scaduto       | varchar | 50         |
| 6   | total_scaduto      | real    | 4          |
| 7   | id_login           | varchar | 50         |
| 8   | note               | varchar | 50         |
| 9   | pagato             | bigint  | 8          |
| 10  | date_insert        | varchar | 50         |
| 11  | date_last_update   | varchar | 50         |

## gruppo

| Id  | Descrizione        | Tipo     | Dimensione |
| --- | ------------------ | -------- | ---------- |
| 1   | id                 | int      | 4          |
| 2   | descrizione        | nvarchar | 200        |
| 3   | tipo_gruppo        | int      | 4          |
| 4   | aggiungi_a_rinnovo | binary   | 1          |
| 5   | aggiungi_a_cliente | binary   | 1          |
| 6   | mostra_a_zero      | binary   | 1          |
| 7   | importa_a_zero     | binary   | 1          |
| 8   | not_ratei_risconti | binary   | 1          |
| 9   | id_trace           | nvarchar | 40         |

## gruppo_cassaincloud

| Id  | Descrizione | Tipo     | Dimensione |
| --- | ----------- | -------- | ---------- |
| 1   | id          | int      | 4          |
| 2   | descrizione | nvarchar | 100        |

## locale

| Id  | Descrizione    | Tipo      | Dimensione |
| --- | -------------- | --------- | ---------- |
| 1   | id             | int       | 4          |
| 2   | nome           | nvarchar  | 200        |
| 3   | via            | nvarchar  | 510        |
| 4   | citta          | nvarchar  | 200        |
| 5   | cap            | nvarchar  | 490        |
| 6   | prov           | nvarchar  | 20         |
| 7   | tel            | nvarchar  | 100        |
| 8   | mail           | nvarchar  | 510        |
| 9   | contact        | nvarchar  | 200        |
| 10  | cliente        | int       | 4          |
| 11  | piva           | nvarchar  | 32         |
| 12  | type_sede      | nvarchar  | 2          |
| 13  | prg            | int       | 4          |
| 14  | data_insert    | datetime2 | 6          |
| 15  | data_update    | datetime2 | 6          |
| 16  | profilo_locale | int       | 4          |
| 17  | note           | nvarchar  | 490        |
| 18  | obsoleto       | date      | 3          |
| 19  | iban           | nvarchar  | 100        |

## macro_tipo_articolo

| Id  | Descrizione | Tipo     | Dimensione |
| --- | ----------- | -------- | ---------- |
| 1   | id          | int      | 4          |
| 2   | descrizione | nvarchar | 100        |
| 3   | reparto     | int      | 4          |

## matricola_articolo_ordine

| Id  | Descrizione     | Tipo     | Dimensione |
| --- | --------------- | -------- | ---------- |
| 1   | articolo_ordine | int      | 4          |
| 2   | prg             | int      | 4          |
| 3   | matricola       | nvarchar | 100        |

## mensile

| Id  | Descrizione       | Tipo   | Dimensione |
| --- | ----------------- | ------ | ---------- |
| 1   | id                | int    | 4          |
| 2   | cliente           | int    | 4          |
| 4   | date_billing      | date   | 3          |
| 5   | next_billing      | date   | 3          |
| 6   | locale            | int    | 4          |
| 7   | creation_date     | date   | 3          |
| 8   | tipo_fatturazione | int    | 4          |
| 11  | group_billing     | binary | 1          |

## mesi

| Id  | Descrizione | Tipo    | Dimensione |
| --- | ----------- | ------- | ---------- |
| 1   | id          | int     | 4          |
| 2   | descrizione | varchar | 50         |

## motivazione

| Id  | Descrizione | Tipo     | Dimensione |
| --- | ----------- | -------- | ---------- |
| 1   | id          | int      | 4          |
| 2   | descrizione | nvarchar | 490        |

## numbers

| Id  | Descrizione | Tipo | Dimensione |
| --- | ----------- | ---- | ---------- |
| 1   | number      | int  | 4          |

## ordine

| Id  | Descrizione         | Tipo      | Dimensione |
| --- | ------------------- | --------- | ---------- |
| 1   | id                  | int       | 4          |
| 2   | data                | date      | 3          |
| 3   | cliente_fatt_alt    | int       | 4          |
| 4   | cliente             | int       | 4          |
| 5   | locale              | int       | 4          |
| 6   | utente              | int       | 4          |
| 7   | totale              | decimal   | 9          |
| 8   | date_insert         | datetime2 | 6          |
| 9   | date_lastupdate     | datetime2 | 6          |
| 10  | tipo                | int       | 4          |
| 11  | is_closed           | binary    | 1          |
| 12  | stato               | int       | 4          |
| 13  | data_consegna       | date      | 3          |
| 14  | note_amministrative | nvarchar  | 1000       |
| 15  | pagamento           | int       | 4          |
| 16  | utente_lastupdate   | int       | 4          |
| 17  | tecnico             | int       | 4          |
| 18  | note_pagamento      | nvarchar  | 2048       |
| 19  | data_evasione       | date      | 3          |
| 20  | order_id_esatto     | nvarchar  | 100        |
| 21  | data_fatturazione   | date      | 3          |
| 22  | utente_mail         | int       | 4          |
| 23  | note_tecniche       | nvarchar  | 1000       |
| 24  | has_rid             | binary    | 1          |
| 25  | rid_date            | date      | 3          |
| 26  | down_payment        | decimal   | 9          |
| 27  | down_payment_type   | int       | 4          |
| 28  | rinnovo             | int       | 4          |
| 29  | mensile             | int       | 4          |
| 30  | note_fattura        | nvarchar  | 1000       |
| 31  | tipo_fatturazione   | int       | 4          |
| 32  | grenke              | binary    | 1          |
| 33  | cancellato          | binary    | 1          |
| 34  | down_payment_for    | int       | 4          |
| 35  | invoice_nr          | nvarchar  | 2048       |
| 36  | impegno_nr          | int       | 4          |
| 37  | invoice_id          | nvarchar  | 200        |
| 38  | wait_payment        | binary    | 1          |

## pagamento_mensile

| Id  | Descrizione | Tipo     | Dimensione |
| --- | ----------- | -------- | ---------- |
| 1   | pagamento   | nvarchar | 10         |
| 2   | attivo      | binary   | 1          |

## prezzo

| Id  | Descrizione | Tipo      | Dimensione |
| --- | ----------- | --------- | ---------- |
| 1   | id          | int       | 4          |
| 2   | cod_art     | nvarchar  | 490        |
| 3   | cod_listino | nvarchar  | 100        |
| 4   | prg_listino | int       | 4          |
| 5   | prz_listino | decimal   | 9          |
| 6   | data_insert | datetime2 | 6          |
| 7   | data_update | datetime2 | 6          |
| 8   | articolo    | int       | 4          |

## profilo_contatto

| Id  | Descrizione | Tipo     | Dimensione |
| --- | ----------- | -------- | ---------- |
| 1   | id          | int      | 4          |
| 2   | descrizione | nvarchar | 90         |

## profilo_locale

| Id  | Descrizione | Tipo     | Dimensione |
| --- | ----------- | -------- | ---------- |
| 1   | id          | int      | 4          |
| 2   | descrizione | nvarchar | 100        |

## reparto

| Id  | Descrizione | Tipo     | Dimensione |
| --- | ----------- | -------- | ---------- |
| 1   | id          | int      | 4          |
| 2   | descrizione | nvarchar | 100        |

## rinnovo

| Id  | Descrizione     | Tipo   | Dimensione |
| --- | --------------- | ------ | ---------- |
| 1   | id              | int    | 4          |
| 2   | cliente         | int    | 4          |
| 4   | locale          | int    | 4          |
| 5   | mese            | date   | 3          |
| 6   | ordine_generato | int    | 4          |
| 10  | mail_inviata    | binary | 1          |
| 11  | completato      | binary | 1          |

## stato

| Id  | Descrizione | Tipo     | Dimensione |
| --- | ----------- | -------- | ---------- |
| 1   | id          | int      | 4          |
| 2   | descrizione | nvarchar | 490        |
| 3   | nascondi    | binary   | 1          |

## t_payment_esatto

| Id  | Descrizione   | Tipo     | Dimensione |
| --- | ------------- | -------- | ---------- |
| 1   | cod_pag       | nvarchar | 20         |
| 2   | cod_pag_NEW   | int      | 4          |
| 3   | des_pag       | nvarchar | 100        |
| 4   | val_spese_inc | decimal  | 9          |
| 5   | cod_tipopag   | int      | 4          |
| 6   | des_tipo_pag  | nvarchar | 100        |
| 7   | num_rate      | int      | 4          |
| 8   | ind_data_scad | int      | 4          |
| 9   | num_giorni    | int      | 4          |

## t_trace

| Id  | Descrizione          | Tipo      | Dimensione |
| --- | -------------------- | --------- | ---------- |
| 1   | id                   | int       | 4          |
| 2   | order_id             | int       | 4          |
| 3   | order_type_id        | int       | 4          |
| 4   | customer_for_billing | nvarchar  | 100        |
| 5   | customer_id          | nvarchar  | 100        |
| 6   | prg_location         | int       | 4          |
| 7   | article_id           | nvarchar  | 490        |
| 8   | price                | decimal   | 9          |
| 9   | serial_number        | nvarchar  | 100        |
| 10  | installation_date    | date      | 3          |
| 11  | due_date_maintenance | date      | 3          |
| 12  | deleted              | int       | 4          |
| 13  | date_import_trace    | datetime2 | 6          |
| 14  | date_import_rinnovi  | date      | 3          |
| 15  | date_import_monthly  | datetime2 | 6          |
| 16  | trace_id             | int       | 4          |
| 17  | monthly_id           | int       | 4          |
| 18  | type_billing         | int       | 4          |
| 19  | payment_type         | nvarchar  | 490        |
| 20  | create_operation     | int       | 4          |

## tipo_articolo

| Id  | Descrizione         | Tipo     | Dimensione |
| --- | ------------------- | -------- | ---------- |
| 1   | id                  | int      | 4          |
| 2   | descrizione         | nvarchar | 100        |
| 3   | macro_tipo_articolo | int      | 4          |
| 4   | cassaincloud        | binary   | 1          |

## tipo_fatturazione

| Id  | Descrizione | Tipo     | Dimensione |
| --- | ----------- | -------- | ---------- |
| 1   | id          | int      | 4          |
| 2   | descrizione | nvarchar | 100        |
| 3   | mesi        | int      | 4          |

## tipo_gruppo

| Id  | Descrizione | Tipo     | Dimensione |
| --- | ----------- | -------- | ---------- |
| 1   | id          | int      | 4          |
| 2   | descrizione | nvarchar | 200        |
| 3   | magazzino   | binary   | 1          |
| 4   | ordine      | int      | 4          |

## tipo_ordine

| Id  | Descrizione | Tipo     | Dimensione |
| --- | ----------- | -------- | ---------- |
| 1   | id          | int      | 4          |
| 2   | descrizione | nvarchar | 200        |
| 3   | rinnovo     | binary   | 1          |

## utente

| Id  | Descrizione | Tipo     | Dimensione |
| --- | ----------- | -------- | ---------- |
| 1   | id          | int      | 4          |
| 2   | name        | nvarchar | 40         |
| 3   | password    | nvarchar | 100        |
| 4   | nickname    | nvarchar | 100        |
| 5   | sigillo     | nvarchar | 12         |
| 6   | mail        | nvarchar | 100        |
