# Annuali/Biennali/31-12

## Introduzione

I rinnovi sono lo strumento di T-Order per gestire i pagamenti ricorrenti, i rinnovi di questo tipo devono essere utilizzati per gestire i pagamenti ricorrenti su base annua, biennale o con scadenza al 31/12.

Un singolo rinnovo contiene tutti i prodotti in abbonamento di uno specifico locale in scadenza nello stesso mese e anno, è possibile che per un singolo locale siano presenti più rinnovi attivi solo se le scadenze sono in mesi diversi, mentre è possibile che nello stesso mese e anno siano presenti più rinnovi dello stesso cliente ma di locali diversi.

## Introduzione tecnica

I rinnovi Annuali/Biennali sono organizzati in due tabelle: rinnovo e articolo_rinnovo.

Gli articoli all'interno dei rinnovi di questo tipo sono gli articoli con mth_12, mth_24 o new_year = 1.

## Metodi di pagamento

Il metodo di pagamento, salvato nella configurazione_rinnovo_locale, per questo tipo di rinnovo può essere uno qualsiasi di quelli disponibili

## Proposta

Tutti gli articoli di un rinnovo con il campo proponi = 1 fanno parte della proposta di rinnovo

In base a questo campo viene popolato il pdf di proposta di rinnovo.

### Funzionalità

[Generazione Rinnovo](generazione){.md-button .md-button--primary}

[Configurazione Rinnovo Locale](configurazione){.md-button .md-button--primary}

[Disdetta](disdetta){.md-button .md-button--primary}

[Inserimento nuovi articoli](inserimento){.md-button .md-button--primary}

[Cambio Piano](cambio){.md-button .md-button--primary}

[Rinnovo](rinnovo){.md-button .md-button--primary}
