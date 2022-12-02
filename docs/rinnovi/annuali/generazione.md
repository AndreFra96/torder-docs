# Generazione rinnovo

I rinnovi <u>non</u> possono essere generati da zero, la classica procedura che porta alla generazione di un rinnovo è la seguente:

1.  Viene generato un documento con all'interno almeno un articolo con canone annuale/biennale/31-12
1.  Il documento subisce i vari passaggi di stato che lo portano fino allo stato evaso
1.  I dati del documento evaso vengono importati in trace e nei rinnovi, in particolare:

    1.  (Note tecniche) I dati del documento evaso vengono inseriti nella tabella di scambio con trace
    2.  (Note tecniche) Periodicamente viene letta la tabella di scambio con trace controllando se sono presenti articoli con canone annuale/biennale/31-12 che sono stati importati in trace ma non sono ancora stati importati nei rinnovi
    3.  (Note tecniche) Per ogni articolo, se è già presente un rinnovo per lo stesso locale con la stessa scadenza, viene inserito all'interno del rinnovo, se invece non è presente ancora un rinnovo per il locale nella scadenza desiderata viene generato un nuovo rinnovo e associato l'articolo al rinnovo
    4.  (Note tecniche) Per ogni articolo viene scritta nella tabella di scambio la data di import all'interno dei rinnovi
