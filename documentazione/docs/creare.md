#Creare, prime modifiche e creazione del sito

Vediamo come creare una documentazione di default e fare le prime modifiche.

##Creazione del progetto
Per prima cosa vediamo come si crea un progetto:

Utilizzo il comando

        $ mkdocs new nome_progetto

In questo modo ho creato un nuovo progetto, nella directory corrente è stato creato un folder con il nome del progetto. Questa cartella contiene un file di configurazione di tipo YAML, nominato `mkdocs.yml` e una cartella in cui è contenuta un file di tipo Markdown, in questo caso contiene un unico file `index.md` in cui è contenuto il file sorgente della tua documentazione.
Possiamo gia visualizzare questo abbozzo di documentazione. Per farlo devo utilizzare il seguente comando assicurandomi di essere nella directory in cui c'è il file di configurazione `mkdocs.yml` e faccio partire il server con

        $ mkdocs serve

Ora posso andare all'indirizzo ip locale porta 8000 --> `http://127.0.0.1:8000/` nel mio browser e vedere la pagina di default.
Posso modificare la documentazione e vedrò le modifiche in diretta sul browser

##Modifiche di configurazione della documentazione

Ora possiamo modificare il file di configurazione `mkdics.yml` e possiamo settare il titolo, le pagine e il tema

        site_name: name          #modifico il nome del sito
        nav:                    #creo pagine e le collego al file Markdown
            - Home: index.md
            - About: about.md
            - Other: other.md

        theme: readthedocs       #posso modificare il tema e scelgo Readthedocs

Naturalmente quando creo le pagine con il collegamento al nostro file, quest'ultimo deve esistere.

##Costruzione del sito

Passiamo a costruire il sito della nostra documentazione, per farlo utilizzo il comando `mkdocs build`:
        $ mkdocs build

Questo comando crea una cartella chiamata `site` dentro la quale c'è un file chiamato `index.html`
