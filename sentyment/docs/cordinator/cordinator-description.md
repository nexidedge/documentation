# Cordinator

Si interfaccia con il front-end tramite delle API che permettono di attivare e interrogare i vari componenti e gestisce la coordinazione dei messaggi fra i moduli del sistema.

Quando un componente intende dialogare con un altro (per esempio, nuove AI vengono generate e testate, quindi possono passare alla fase successiva di simulazione) si rivolge al coordinatore secondo un protocollo definito, inviandogli un messaggio con destinatario il modulo che deve ricevere; il coordinatore quindi inoltra il messaggio secondo un pattern publish-subscribe.

Il coordinator riceve anche messaggi dalle applicazioni front-end e interroga i moduli interessati. Nel caso della dashboard, esiste una API che permette a questa di chiedere i dati degli andamenti: il coordinatore allora interroga il database e restituisce tali dati.
