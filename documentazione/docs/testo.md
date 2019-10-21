# Scrivere in Markdown

In questa sezione vedremo come scrivere i file in Markdown e la visualizzazione ottunuta con questo.

##Sezioni della pagina
Possiamo creare delle sezioni della pagina usando un semplice comando `#` in vari modi, questo comando crea i titoli e sottotitoli delle sezioni. Al massimo possono essere 6 livelli e si scrivono in questo modo:

	# Titolo 1 	 --> questo indica la sezione pripale e il titolo sarà Titolo1
	## Titolo 2      --> Sotto titolo e seconda sezione

	##### Titolo 5   --> Sotto titolo numero 5 e quinta sezione

In questo modo posso creare sezioni che compariranno anche  nel pannello di destra (se utilizzo readthedoc come tema)

##Creazione di link
Per creare link nella documentazione è necessario utilizzare:

	Consultare [qui](https://informaticabrutta.it/markdown-guida/).

Questo è il risultato---> Consultare qui [qui](https://informaticabrutta.it/markdown-guida/).

Posso anche lasciare l'Url stesso come link usando la seguente notazione:

	<https://informaticabrutta.it/markdown-guida/>

Questo è il risultato---> <https://informaticabrutta.it/markdown-guida/>

## Immagini

Se decido di aggiungere delle immagini nella mia documentazione devo utilizzare una notazione simile a quella del link con l'aggiunta di un punto interrogativo all'inizio

![Myais dashboard](https://myais.it/wp-content/uploads/2019/05/Schermata-2019-05-09-alle-11.15.28-1.png)
Questo è il comando che genera la figura sopra:

	![Myais dashboard](https://myais.it/wp-content/uploads/2019/05/Schermata-2019-05-09-alle-11.15.28-1.png)
	
## Enfasi
Posso scrivere in maniera diversa alcune come in **grassetto** e in *corsivo*
	
	**parole** #grassetto
	*corsivo*  #corsivo
	_enfasi_   #corsivo
	***corsivo e grassetto***  #unione dei due
Per dare enfasi a una citazione posso usare > oppure il Tab:
>Questo è il risultato

##Elenchi

Posso creare elenchi numerati o elenchi puntati. Nel primo caso utilizzo

	1. Primo elemento
	2. Secondo elemento

	9. Nono elemento
		Se uso Tab creo sottoelemento

Nel secondo posso utilizzare indistintamente 3 simboli `-` `*` e `+`

	* Primo
	- Secondo
	+ Terzo

##Riquadri nel testo
Sono molti importanti per scrivere codici o fare esempi, molto utili e semplici da fare basta scrivere quello che si vuole a un Tab di sistanza!
Se voglio mettere in un riquadro e `evidenziare di rosso` invece utilizzo:
```
	`evidenziare di rosso`
```

Se voglio solo mettere in un riquadro una parola, frase o un comando per risaltarla basta utilizzare questo simbolo \`\`\` prima e dopo la parola o la frase scelta.

##Separatore
Posso decidere di mettere un separtore nella pagina come questo.
___

	___ #3 trattini bassi

##Tabelle

Per creare delle tabelle in Markdown bisogna costruirle a suon di `|` e `-`. Quindi è consigliabile andare in rete e trovare un sito che vi setta la tabella che volete voi in base alle righe e colonne, come [questo](https://www.tablesgenerator.com/markdown_tables).
	 
