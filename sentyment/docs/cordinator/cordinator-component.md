# Cordinator Component

## API
- `/source`: Lista fonti disponibili. Le fonti sono delle classi python scritte in dei file appositi, in *data-module/src/sources*
e sono caricate in fase di lancio. Possono essere attivate con un'altra API, passando il nome di una delle fonti restituite da `/source`.<br><br>
**Risultato**: Ritorna un JSON contenente un array di fonti (vuoto se nessuna disponibile):<br>


		source = nomi fonti disponibili (str)


- `/source/activate`: Attiva una delle fonti disponibili. L'attivazione comporta l'inizio del download da quella fonte, cioe' l'esecuzione
del suo metodo *download*, che legge i dati da una sorgente e li salva sul database di storage.
Il metodo e' disponibile in due varianti, GET e POST.
	- **GET**: `/source/activate/<source name>`: <br>il nome della fonte da attivare e' passato tramite l'URL.
	- **POST**: `/source/activate`<br>**Input**: si aspetta come dati passati un **JSON** con un parametro `source` di tipo `string`.<br>
	**Esempio**:<br>
	

			{ "source": "KrakenRawSource" }

		<br>

	**Risultato**: Ritorna un JSON di risposta che conferma l'operazione avvenuta, oppure da' un messaggio di errore.

			ok = messaggio di operazione riuscita (str)
			error = eventuale messaggio di errore (parametri non corretti / fonte richiesta non esistente) (str)
		

- `/source/active`: Lista delle fonti attivate in precedenza con la API `/source/activate`, corredate da ultimo istante di aggiornamento,
cioe' il datetime del piu' recente dato scaricato dalla fonte.<br><br>
**Risultato**: Ritorna un JSON con un array di fonti:


		sources = array di fonti
			< nome fonte > (str)
			< ultimo datetime aggiornato > (str che rappresenta datetime)


- `/ticker`: Elenco di tutti i ticker disponibili dalle fonti. Non necessariamente i ticker qua elencati sono in scaricamento; sono soltanto
elencati tutti gli asset disponibili dalle fonti. Per esaminare i ticker attivi, cioe' che stanno venendo scaricati, vedere la API `/ticker/acticve`
<br><br>**Risultato**: Ritorna un JSON contenente un array di ticker.


		ticker = array di ticker


- `/ticker/active`: Lista di tutti i ticker **attualmente in scaricamento** dalle varie fonti. Una volta che una fonte e' stata attivata e scarica dati,
registra i vari nomi dei ticker che sta scaricando, aggiornati con l'ultimo istante di scaricamento.<br><br>
**Risultato**: Ritorna un JSON contenente un array di ticker con il loro datetime.


		ticker = array di ticker + time
			< nome ticker > (str)
			< ultimo datetime aggiornato > (str che rappresenta datetime)


- `/candle/create`: Comando di creazione candele OHLCV. Accetta diversi parametri, tra cui i ticker da analizzare, l'istante da cui iniziare
   la creazione di candele e la lunghezza delle stesse. Legge da database storage e crea candele di lunghezza scelta, a partire da una data scelta.
   E' inoltre possibile decidere se creare a partire dai dati RAW di trading, oppure se creare altre candele OHLCV partendo da dati gia' sotto
   forma di candele.<br>
   Il risultato del comando e' la scrittura nel database di storage delle candele specificate, partendo dal timestamp di inizio e scorrendo via via
   fino alla fine dei dati piu' recenti disponibili. (E' gia' attivato un processo automatico di creazione candele giornaliere).<br><br>
   **Input**:


		start_timestamp = tempo da cui iniziare a creare candele (timestamp di un dato in database)
		tickers = array di ticker (str) su cui creare le candele, in sequenza
		candle_len = dimensione candele ("D" / "H")
		source = sorgente da cui creare ("RAW" / "OHLCV")
		
	<br>
	*start_timestamp* puo' essere in formato stringa "DD-MM-YYYY HH:MM" oppure un intero in formato unix timestamp.<br>
	*tickers* puo' essere una lista vuota, e la creazione di candele e' effettuata su TUTTI i ticker disponibili.<br>
	*candle_len* ha attualmente solo due valori accettati: "D" (candele giornaliere) e "H" (candele orarie).<br>
	*source* indica se creare a partire da dati RAW o se partire da candele gia' esistenti (OHLCV).<br>
	<br>
	**Esempio**:

		{"start_timestamp": "2011-09-16 06:00", "tickers": ["EURUSD"], "candle_len": "D", "source": "RAW"}

		{"start_timestamp": 1572430313, "tickers": [], "candle_len": "H", "source": "OHLCV"}
  

- `/holes`: Comando di scansione buchi nel database. Attiva la scansione del database di storage, ticker per ticker a partire dai dati di
  trading RAW, e analizza le differenze di timestamp fra un dato e il successivo, scrivendo nel log se trova eventuali buchi. Da implementare.
	
