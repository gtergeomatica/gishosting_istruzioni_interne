I file javascript di Lizmap
============================

E' possibile estendere le funzionalità di Lizmap attraverso la creazione di appositi file javascript. Questi file sono disponibili su una repository github dedicata a questo link: https://github.com/3liz/lizmap-javascript-scripts . Altri si possono trovare nella cartella *lizmap-web-client/lizmap/install/qgis/media/js/* (basta rimuovere l'estensione .example per utilizzarli). La maggior parte di quelli che utilizziamo noi si trovano nella cartella della repository di Concert-Eaux.

Questi file javascript vanno messi nella cartella della repository a questo percorso **repository/media/js/nome_progetto/** (ad esempio nel caso di Novara sarebbe **progetti_privati/media/js/nuovo_cs_novara/**). In questo modo caricando la pagina web del progetto nominato *nuovo_cs_novara* tutti i file javascript dentro la cartella corrispondente saranno eseguiti.

La documentazione di Lizmap sui file javascript aggiuntivi si trova qui https://docs.lizmap.com/current/it/publish/advanced_lizmap_config.html#adding-your-own-javascript


GoogleStreetView.js
++++++++++++++++++++++++
Aggiunge un pulsante alla toolbar di Lizmap che consente di aprire una finestra (tipo mini-dock) e visualizzare Google Street View cliccando su un punto della mappa. Richiede una API key Google che deve essere inserita nel file javascript e in particolare come contenuto (stringa) della variabile **gkey** (riga 4 del codice).

.. image:: img/streetview.png

Le API Key Google di Gter si gestiscono da questo sito https://console.cloud.google.com/home/dashboard?project=gishosting utilizzando l'account gmail di Gter rischio.idrogeologico@gmail.com (vedi file drive per la pwd) o il proprio account gmail personale se abilitato a vedere anche i progetti dell'account di Gter.
TUTTE le API Key create per GisHosting devono essere create all'interno del progetto **GisHosting OK** verificare quindi sempre che sia selezionato questo progetto come da immagine sotto

.. image:: img/progetto_api_google.PNG

E' fondamentale creare tutte le API all'interno del progetto **GisHosting OK** perchè al momento è l'unico collegato a un account di fatturazione. Nello specifico è collegato all'account **GisHosting Billing** (CC BPM di Gter). Se infatti non c'è un account di fatturazione collegato al progetto Google la visualizzazione di Google Stret View viene corrota (es. visualizzazione tipo in negativo).

Per vedere l'elenco delle API del progetto **GisHosting OK** bisogna andare in --> vedi immagine sotto

.. image:: img/elenco_api.png

Attualmente utilizziamo per Concerteaux e Novara l' API nominata **gishosting street view cloud** mentre per Piacenza ne utilizziamo una ad hoc nominata **cs piacenza street view**. Qualora si voglia ggiungere questo javascript a un qualsiasi progetto che risiede sul server GisHosting si deve utilizzare la prima chiave, se invece si vuole utilizzare per un progetto che risiede su altro server, come nel caso di Piacenza, bisogna crearne una ad hoc ma sempre nel progetto Google **GisHosting OK**.

.. _Gter srl: https://www.gter.it