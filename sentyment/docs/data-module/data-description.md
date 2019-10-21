# Data Module

I dati grezzi vengono scaricati da sorgenti diverse ed eterogenee; il componente si occupa di filtrare i dati e organizzarli in modo standard in uno storage su filesystem e, successivamente, su database.

Le sorgenti di dati possono essere dei file locali oppure delle API di servizi web da cui scaricare. Raw Data distingue i vari casi e scarica / salva i dati nello storage indifferentemente. È possibile attivare / disattivare i download dalle sorgenti e aggiungere nuove fonti di dati (riferimenti oppure dati stessi, per esempio in formato testuale) e raw_data periodicamente scarica in modo automatico dalle sorgenti attivate.

Data manager preleva i dati salvati da raw data e li pulisce e filtra, scrivendoli poi su database remoto, seguendo lo schema dei dati definito. Implementa anche un livello di astrazione rispetto al database vero e proprio: la tecnologia sottostante può cambiare a seconda delle esigenze, e data manager gestisce le varie situazioni in modo indipendente fornendo un’interfaccia per l’accesso in scrittura / lettura. 
Se data manager riscontra dati mancanti o incompleti chiede a raw data di riscaricarli.
Ogni altro modulo che vuole accedere ai dati si rivolge a data manager, il quale preleva i dati dal database e mantiene anche una copia cache locale aggiornata.


