# Cordinator Component

## API
- `/source`: Lista fonti disponibili. Le fonti sono delle classi python scritte in dei file appositi, in `data-module/src/sources`
e sono caricate in fase di lancio. Possono essere attivate con un'altra API, passando il nome di una delle fonti restituite da `/source`.
Ritorna un JSON contenente un array di fonti (vuoto se nessuna disponibile):
`
	source = nomi fonti disponibili
`

- `source/activate`: Attiva una delle fonti disponibili. L'attivazione comporta l'inizio del download da quella fonte, cioe' l'esecuzione
del suo metodo `download`, che legge i dati da una sorgente e li salva sul database di storage.
Il metodo e' disponibile in due varianti, GET e POST.
**GET**: `source/activate/<source name>`: il nome della fonte da attivare e' passato tramite l'URL.
**POST**: `/source/activate` si aspetta come dati passati un **JSON** con un parametro `source` di tipo `string`:
	Esempio input:
	`{ "source": "KrakenRawSource" }`
Ritorna un JSON di risposta che conferma l'operazione avvenuta, oppure da' un messaggio di errore.
`
	ok = messaggio di operazione riuscita
	error = eventuale messaggio di errore (parametri non corretti / fonte richiesta non esistente)
`

- `/source/active`: Lista delle fonti attivate in precedenza con la API `source/activate`, corredate da ultimo istante di aggiornamento,
cioe' il datetime del piu' recente dato scaricato dalla fonte.ù
Ritorna un JSON con un array di fonti:
`
	sources = array di fonti
		<nome fonte>
		<ultimo datetime aggiornato>
`

- `/ticker`: Elenco di tutti i ticker disponibili dalle fonti. Non necessariamente i ticker qua elencati sono in scaricamento; sono soltanto
elencati tutti gli asset disponibili dalle fonti. Per esaminare i ticker attivi, cioe' che stanno venendo scaricati, vedere la API `/ticker/acticve`
Ritorna un JSON contenente un array di ticker.
`
	ticker = array di ticker
`

- `/ticker/active`: Lista di tutti i ticker **attualmente in scaricamento** dalle varie fonti. Una volta che una fonte e' stata attivata e scarica dati,
registra i vari nomi dei ticker che sta scaricando, aggiornati con l'ultimo istante di scaricamento.
Ritorna un JSON contenente un array di ticker con il loro datetime.
`
	ticker = array di ticker + time
		<nome ticker>
		<ultimo datetime aggiornato>
`

- `/candle/create`: Comando di creazione candele OHLCV.

- `/holes`: Comando di scansione buchi nel database.
	
