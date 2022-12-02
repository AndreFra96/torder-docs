# File Manager

Il backend offre le funzionalità da file manager per due scopi principali:

- Allegati ordini
- File temporanei

La dimensione massima ammessa per i file caricati è di 50 Mb.

!!! note

    Il backend utilizza il middleware fornito dal pacchetto [express-fileupload](https://www.npmjs.com/package/express-fileupload) per gestire l'upload dei file

## Allegati ordini

Ogni ordine ammette un numero indefinito di file allegati, sono disponibili 4 endpoint per la gestione dei file allegati ad un ordine:

### Allega File

`POST file/ordine/{id}`

Questo endpoint permette di caricare un file come allegato di un ordine.

### Lista Allegati

`GET file/ordine/{id}`

Ottieni la lista dei nomi dei file allegati all'ordine

### Ottieni Allegato

`GET file/ordine/{id}/{file}`

Scarica un file allegato all'ordine in base al suo nome

### Cancella Allegato

`DELETE file/ordine/{id}/{file}`

Cancella un file allegato all'ordine

## File Temporanei

La sezione file temporanei permette di caricare dei file organizzandoli in cartelle.

Lo scopo principale di queste api è quello di preparare una serie di file per poi procedere ad allegarli ad una mail.

### Carica file

`POST file/temp/{id}`

Questo endpoint permette di caricare un file all'interno della cartella temporanea id.

Se la cartella non esiste viene creata automaticamenteo.

La dimensione massima ammessa per i file allegati è di 50 Mb.

### Lista file in cartella

`GET file/temp/{id}`

Ottieni la lista dei nomi dei file presenti nella cartella temporanea

### Cancella cartella

`DELETE file/temp/{id}`

Cancella tutto il contenuto di una cartella temporanea

### Ottieni un file

`GET file/temp/{id}/{file}`

Ottieni uno specifico file da una cartella temporanea

### Cancella un file

`DELETE file/temp/{id}/{file}`

Cancella un file da una cartella temporanea
