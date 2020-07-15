Introduzione
==================

GisHosting è basato sul webclient Lizmap.

DA COMPLETARE ROBERTO



Componenti principali:
* qgis server
* Lizmap Web Client (nel seguito LWC)
* nextcloud per la sincronizzazione file tra client e server


Nuovo utente 
===============================




Aggiunta opzione geoDB
===============================



Creazione repository
===============================
Modifica 






Creazione cartella media su storage box
============================================
1. Con connessione ssh (es.mobaxterm)

.. code-block:: bash

   cd /mnt/dav/media_utenti_gishosting_upgrades
   mkdir nomeutente_nomerepository

2. vado su https://robot.your-server.de/storage con utente e password che trovo su drive
   
   Step 1 Sub-account → Create
   
   .. image:: img/robot1.png
   
   Step 2 – scelgo la cartella e check su samba, webdav e external reachability e se mi ricordo metto un commento
   
   .. image:: img/robot2.png
   
   
3. Salvo user e password su file *utenti_server_gishosting_e_storage.ods* che trovo nella cartella coordinamento/prodotti del NAS Gter 
   
4. Vado su nextcloud di quell’utente e rinomino la cartella media (**sarebbe meglio farlo con il client nextcloud su proprio PC e non da interfaccia web**) 
   
   
5. Bisogna creare la cartella media sul server e impostare il mount con CIFS/SAMBA

.. code-block:: bash

mkdir /home/gter/nextcloud-data/**nomeutente**/files/**nomerepository**/media

oppure 

mkdir /home/gter/nextcloud-data/**nomeutente**/files/media

qualora non ci sia il repository per quell'utente

.. code-block:: bash

nano /etc/fstab


.. code-block:: bash

//indirizzo_smb /mountpoint cifs soft,uid=33,gid=33,dir_mode=0755,username=us,password=pwd 0 0

ad esempio se l'utente **u221008-sub3** fosse quello corrispondente alla cartella astergenova_STRADE:

.. code-block:: bash

//**u221008-sub3**.your-storagebox.de/**u221008-sub3** /home/gter/nextcloud-data/**astergenova**/files/**STRADE**/media cifs soft,uid=33,gid=33,dir_mode=0755,username=u221008-sub3,password=XXXXXXXXXXX 0 0


6. Montare la cartella 
   sudo mount -a
   
   
7. E fare un sync dei dati su nextcloud 
   cd /var/www/html/nextcloud/  
   sudo -u www-data php console.php files:scan --path="username/files/" 



NB Qualora venga cambiato il nome di un repository è necessario rifare i passi 1-4 da capo (con nuovo utente e nuova pwd) e sostituire utente, password e nomerepository nel file /etc/fstab




Progetti particolari
===============================

Form creazione utenti ASTER 
-----------------------------------

DA COMPLETARE ROBERTO





GisHosting è basato sul webclient Lizmap. 
Lizmap consente di dare accesso ai repository o alle singole mapppe a specifici gruppi. 

Questa guida è pensata per gli utenti che acquistino il piano geoDB che include di default 


* un utente amministratore (con un suo gruppo)
* 3 gruppi utenti
* 3 repository utente 

A titolo di esempio supponendo che **user** sia l'utente amministratore ci saranno di default 4 gruppi:

* *user_group* (gruppo admin)
* *user1_group* 
* *user2_group* 
* *user3_group* 


E' sempre possibile (ma con un costo aggiuntivo rispetto al contratto base) richiedere l'aggiunta di repository. Per ogni repository viene creato un gruppo associato.


Di default ogni repository creato corrisponde a un gruppo come mostrato nella seguente figura

.. image:: img/repo_default.png



GisHosting è un server cloud condiviso, per cui occorre sottolineare che esistono due diverse figure:

* *utente amministratore*: è l'utente creato al momento della creazione del proprio spazio su GisHosting, di cui abbiamo già discusso. Ha accesso completo ai repository lizmap così come alla cartella di Nextcloud contenente i progetti QGIS da pubblicare 
* *amministratore di sistema*: che è invece rappresentato da chi gestisce il server GisHosting, ossia da personale di Gter 



Il solo **amministratore di sistema**, sulla base delle specifiche richieste dell'**utente amministratore**, può modificare i permessi per ogni repository secondo le seguenti regole:

* Vedere progetti nel repository
* Visualizza il link del WMS dei progetti
* Usa lo strumento edizione
* Consenti l'esportazione dei layer
* Mostrare sempre i dati completi, anche se filtrati da login


.. image:: img/3repo.PNG


L' **utente amministratore** attraverso il plugin lizmap ha inoltre la possibilità di filtrare singoli progetti per ogni gruppo di utente agendo direttamente sul progetto QGIS.

.. image:: img/lizmap_gruppi.PNG



Gestione utenti (e gruppi)
===========================================

Con queste funzionalità si può creare un numero illimitato di utenti (purchè il nome non sia già stato assegnato) da associare a specifici gruppi. **Non si possono invece creare nuovi gruppi.
Questa funzionalità come detto nelle precedenti sezioni è consentita al solo amministratore di sistema.** 


Accesso alla dashboard utente
------------------------------------------
Dalla pagina principale di GisHosting https://gishosting.gter.it/home/ con il tasto in alto a destra si accede alla dashboard del proprio utente (solo per il piano geoDB)

.. image:: img/user_dashboard0.PNG

Da questa schermata cliccando sul tasto "Check your data" è possibile inserire i seguenti dati:

* utente amministratore
* password utente amministratore
* il nome del proprio DB


.. image:: img/user_dashboard0.PNG




Dashboard utente
------------------------------------------

Si possono così visualizzare le dimensioni del proprio geoDB PostgreSQL/PostGIS:

.. image:: img/dim_db.PNG



E l'elenco degli utenti associati al proprio **utente amministratore**, oltre che, se necessario aggiungere nuovi utenti.

.. image:: img/dati_utente.PNG


Per aggiungere nuovi utenti bisogna completare un form in cui è necessario specificare almeno un gruppo di appartenenza:

.. image:: img/form.PNG


Per ogni utente creato si possono modificare i gruppi di appartenenza.

.. image:: img/edit_utente.png



Si ricorda che il gruppo *nomeutente_group* è il gruppo amministratore per cui occorre fare attenzione nell'assegnazione dei permessi.




Note finali
**************************************************************

Si ricorda infine che dal progetto QGIS, tramite il plugin lizmap, è possibile filtrare la visualizzazione di un layer sulla base del nome utente.

In tal caso si rimanda a:

* guida di lizmap: https://docs.lizmap.com/current/it/publish/advanced_lizmap_config.html#filtered-layers-filtering-data-in-function-of-users
* video-tutorial: https://vimeo.com/83966790









GisHosting è il server su cloud basato sui software free ed open source *qgis-Server* e *Lizmap* ed è realizzato da `Gter srl`_  




.. _Gter srl: https://www.gter.it
