Introduzione
==================

GisHosting è il server su cloud basato sui software free ed open source *qgis-Server* e *Lizmap* ed è realizzato da `Gter srl`_  


Le componenti principali sono:
* qgis server
* Lizmap Web Client (nel seguito LWC)
* nextcloud per la sincronizzazione file tra client e server



DA COMPLETARE ROBERTO





Nuovo utente 
===============================


DA COMPLETARE ROBERTO


Aggiunta opzione geoDB
===============================


DA COMPLETARE ROBERTO


Creazione di un repository o modifica del nome all'interno della cartella utente 
===================================================================================

Sono sostanzialmente necessari 3 step:

1. creare cartella per repository o rinominarla **avendo cura che la struttura del repository interna sia completa (es. cartella media) e eventuali cartelle dati** 

2. da amministazione LWC modificare il percorso al repository

.. image:: img/lwc_mod_repo.png

3. verificare presenza storagebox (LINK INDICE SEGUENTE TODO) e nel caso seguire passi da 1 a 4 e sostituire utente, password e nomerepository nel file /etc/fstab (step 5). 





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

.. code-block:: bash

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

.. code-block:: bash   

   sudo mount -a
   
   
7. E fare un sync dei dati su nextcloud

.. code-block:: bash

   cd /var/www/html/nextcloud/  
   sudo -u www-data php console.php files:scan --path="username/files/" 



NB Qualora venga cambiato il nome di un repository è necessario rifare i passi 1-4 da capo (con nuovo utente e nuova pwd) e sostituire utente, password e nomerepository nel file /etc/fstab




Progetti particolari
===============================

Form creazione utenti ASTER 
-----------------------------------

DA COMPLETARE ROBERTA




Note finali
**************************************************************


* guida di lizmap: https://docs.lizmap.com/current/it/





.. _Gter srl: https://www.gter.it
