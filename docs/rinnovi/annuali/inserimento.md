# Inserimento nuovi articoli

All'interno di un rinnovo già esistente è possibile inserire dei nuovi articoli annuali/biennali/31-12.

Questa funzionalità risponde alla specifica necessità di inserire dei nuovi articoli all'interno di rinnovi già presenti senza passare per la procedura classica di [generazione rinnovo](../generazione), al fine di fatturare il nuovo prodotto insieme agli altri articoli presenti all'interno del rinnovo nel momento in cui viene confermato.

Un articolo inserito in questo modo viene ritenuto temporaneo fino alla prima conferma del rinnovo con conseguente fatturazione, fino a quel momento l'articolo inserito non viene importato nella scheda cliente di trace e può essere disdetto in maniera diretta senza indicare una motivazione.

(Note tecniche) Gli articoli inseriti in questo modo sono riconoscibili poichè hanno il campo trace_id = NULL

Per la logica di rinnovo di questi articoli vedi [rinnovo con percorso alternativo](../rinnovo/#percorso-alternativo).
