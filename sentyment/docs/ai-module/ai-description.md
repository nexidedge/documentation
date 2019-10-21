# AI Module

Intelligenza artificiale che genera a sua volta delle AI, le quali effettuano predizioni sul mercato.
AI evolutiva legge dal database e crea diverse intelligenze predittive; queste sono monitorate da un’ulteriore AI, AI di controllo, che effettua dei test sulle intelligenze generate utilizzando una test suite. AI di controllo produce quindi uno score per ciascuna AI generata ed esclude quelle che falliscono, mentre le migliori saranno usate dal trading module per le predizioni.

Un componente di reportistica può essere interrogato per produrre report riguardanti le varie AI generate; report AI riceve in input una particolare AI e legge tutte le informazioni disponibili riguardanti le sue prestazioni, le predizioni effettuate e i vari score associati, insieme ad altre informazioni presenti sul database.
