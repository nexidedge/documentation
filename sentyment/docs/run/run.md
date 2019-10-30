## Requisiti
### Sottomoduli
Partendo dal modulo sentyment-root, che contiene soltanto dei file di configurazione, alcuni script e il launcher, e' necessario
scaricare i sotto-moduli **sentyment-data-module** e **sentyment-coordinator** tramite `git`.<br>
Dare i seguenti comandi dalla linea di comando, **nella directory di sentyment-root**:

- sentyment-data-module:

		git remote add data-module https://github.com/nexidedge/sentyment-data-module
		git subtree add --prefix=sentyment-data-module data-module master --squash

- sentyment-coordinator:

		git remote add coord-module https://github.com/nexidedge/sentyment-coordinator
		git subtree add --prefix=sentyment-coord-module coord-module master --squash


	A questo punto dovrebbero essere disponibili le sotto-directory **sentyment-data-module** e **sentyment-coordinator**

### Configurazioni
Al fine di raggruppare tutti i file di configurazione in un unica directory, sono usato dei link simbolici.<br>
Sistemare i link simbolici eseguendo lo script apposito (**dalla directory di sentyment-root**):

	./script/conf_link.sh

### Database
Sentyment si appoggia su **mysql**, ha un database "remoto" e uno "locale" di storage, entrambi gestiti con mysql.<br>

- Installare mysql-server:

		apt install default-mysql-server libmariadbclient-dev


- Creare due database, nomi di default: **storage** e **nexid** (configurabile in *data_module_conf.py*).<br>
  Entrare nell'interfaccia di mysql con:

		mysql

	(fornire utente e password)<br><br>

- Creare i database:

		create database storage; create database nexid;


- Modificare la stringa di connessione al database in **config/data_module_conf.py**, inserendo URL, utente e password dei database mysql appena creati:

		# mysql db: "mysql://<user>:<password>@<server IP>:<server PORT>/<database name>"
		storage_path = "mysql://root:root@127.0.0.1:3306/storage"
		db_path = "mysql://root:root@127.0.0.1:3306/nexid"


	Ora sentyment dovrebbe essere in grado di connettersi.

- Creare le tabelle necessarie a partire dagli oggetti python / sqlalchemy, utilizzando lo script apposito.<br>
  Dalla directory di sentyment-root, dare il seguente comando:

		./script/create_tables.py



### Package python
Sono necessare alcune librerie di python3 su cui il sistema appoggia, da scaricare con `pip`:

- Installare pip, se non gia' presente:

		apt install pip3

- Installare i moduli python con pip:

		pip3 install sqlalchemy mysql-client flask-marshmallow termcolor krakenex



# RUN
Assumendo di aver seguito tutti i punti precedenti, di aver quindi fatto il setup del database fornendo stringhe di connessione con 
nomi utente e password, aver creato database e tabelle, possedere tutti i sotto moduli di sentyment e installato tutte le librerie mancanti di
python, ora e' sufficiente eseguire lo script del launcher che attivera' tutti i moduli del sistema (comandi sempre **dalla directory di sentyment.root**):

	./sentyment_run.py


Attivare anche il job di `cron` per il timer che esegue la creazione giornaliera delle candele:

	./script/daily_candles_cron.sh

Attivare infine una fonte, dato che nessuna fonte e' attiva di default in fase di inizializzazione. Consultare le API di coordinator per dettagli.
Esempio:

	curl --header "Content-Type: application/json" --request GET http://localhost:8080/source/activate/KrakenRawSource


### Aggiunte
- E' possibile definire nuove fonti di dati scrivendo una nuova classe python in `sentyment-data-module/src/sources`,
  le quali devono implementare una classe specifica (dettagli nella sezione `data module`).
