The Lidar Tile Maker Plugin
==================================
The **Lidar Tile Maker** Plugin creates the tile vector layer, named *tile_dsm_dtm*, to be used as input for the CHM from LIDAR Plugin. As already mentioned in the introduction of the manual, the CHM from LIDAR plugin automatically uploads and uses the *tile_dsm_dtm* vector layer, which contains data of Regione Veneto, but it can be replaced with the one created by the **Lidar Tile Maker** Plugin.
It creates a GeoPackage file, automatically named *tile_dsm_dtm.gpkg*, which contains the polygons of tiles computed from the extensions of the DTM/DSM file given by users as input. Also the related attribute table is automatically created with all the required fields and filled with all the necessary information taken from input parameters provided by users or from the data themselves.

**NB. In order to use the tile_dsm_dtm.gpkg file as input for the CHM from LIDAR plugin, DO NOT rename the file and the Qgis layer and DO NOT delete or rename any field of the related attribute table.**

The DTM and DSM data deriving from a LIDAR flight campaign are divided into tiles. The **Lidar Tile Maker** Plugin computes the extention of each DTM tile and of its related DSM tile given as input. If the two tiles, DTM and related DSM, have the same extention, the plugin creates the tile polygon. The final output is a vector layer containing all the polygons corresponding to the extension of each tile DTM/DSM given as input. The plugin creates the corresponding tile polygon only if both DTM and DSM exist and if they have the same extention. Otherwise the tool returns a warning message.

The plugin works for a single LIDAR flight campaign. In case of several campaigns, the plugin has to be run for each campaign and it will create the corrisponding tile vector file. Then the tile vector layers have to be merged in order to obtain a single *tile_dsm_dtm.gpkg* file with all the tile polygons of each campaign to be used as input of the CHM from LIDAR plugin.

The main and mandatory input of the **Lidar Tile Maker** Plugin are:

* the folder containing all the DSM file of the desired campaign
* the folder containing all the DTM file of the desired campaign
* the Coordinates Reference System (CRS) of the DTM/DSM file
* an output path folder where the plugin will save the final tile_dsm_dtm.gpkg file

NB. If a tile_dsm_dtm.gpkg file already exists in the provided output folder, it will be automatically overwritten.

Graphical User Interface
--------------------------------------------
All the required input parameters can be provided by users through the graphical user interface (GUI) of the **Lidar Tile Maker** Plugin that is shown pressing its icon in the toolbar.

.. image:: img/gui.png

* **1 - Select an AOI:** da qui è possibile selezionare il layer vettoriale contenente le geometrie dell'are di interesse per la quale si desidera calcolare il CHM. Il menù a tendina elenca tutti i layer vettoriali caricati all'interno del progetto corrente, è quindi necessario che il vettoriale contenete l'AOI sia stato già caricato nel progetto Qgis.
* **2 - Using selected features:** qualora il layer dell'AOI selezionato avesse geometrie selezionate la check box si attiva. Checkandola verranno quindi utilizzate le sole geometrie selezionate e quindi verranno selezionate tutte le tile (dal layer tile_dsm_dtm) che intersecano le sole geometrie selezionate nel layer di AOI selezionato al punto 1. Se la check box non viene spuntata verrà utilizzato per l'intersezione l'intero layer. Nel caso in cui nel layer di AOI selezionato non siano presenti geometrie selezionate la check box sarà disattivata.
* **3 - Select di autority:** tra le varie informazioni immagazzinate nella tabella del layer delle tile (tile_dsm_dtm) è presente anche l'Ente che ha gestito la campagna di volo. Il menù a tendina elenca tutti gli enti indicati all'interno della tabella, è possibile quindi selezionare l'ente desiderato e di conseguenza visualizzare nel menù a tendina, di cui al punto 4, le sole campagne di volo gestite dall'ente selezionato. NB: in questo momento questa funzione non è ancora attiva, verrà integrata nel codice nei giorni seguenti al corso.
* **4 - Select a campaign:** sulla base dell'ente selezionato al punto 3, il menù a tendina elencherà tutte le campagne di volo gestite dall'ente. Sarà quindi possibile selezionare la campagna desiderata per la quale calcolare il CHM. NB: al momento il menù a tendina elenca tutte le campagne presenti nella tabella degli attributi associata al layer delle tile  (tile_dsm_dtm) senza il filtro sulla base dell'ente. Questa funzione sarà implementata nei prossimi giorni come già detto al punto 3.
* **5 - Clip file name:** selezionando un'are di interesse è necessario indicare un nome per il raster che conterrà il CHM ritagliato sul confine dell'area AOI selezionata. E' necessario indicare solo il nome senza l'estensione del file che verrà aggiunta automaticamente sulla base del formato di output scelto dall'utente. Qualora l'utente non indicasse il nome per il clip, il plugin restituirà un warning in cui si avvisa l'utente che verrà dato al file un nome di default (es. clip.*). **NB: non inserire nel nome del file spazi o caratteri speciali.**
* **6 - Choose resolution (m):** da qui è possibile selezionare la risoluzione, espressa in metri, con cui verrà ricampionato il file del clip. I CHM delle singole tile vengono infatti calcolati con la risoluzione originaria del DSM e DTM, mentre per quanto riguarda il clip è possibile appunto definire una risoluzione diversa da quella originaria. Il valore è espresso in metri. Qualora si volesse utilizzare un sistema di riferimento non proiettato (es. WGS84 con unità in gradi), la risoluzione deve essere comunque espressa in metri, sarà il plugin a convertire il valore fornito nell'unità di misura corrispondente al sistema di riferimento scelto. Qualora l'utente non specifichi un valore lasciando la box al valore di default (0.00), verrà utilizzata la risoluzione originaraia del DSM e del DTM per calcolare il clip. La box per la scelta della risoluzione si attiverà solo nel caso in cui venga selezionata la sola AOI, senza quindi selezionare una campagna specifica. Infatti qualora venga selezionata anche una campagna di volo la box sarà disattivata e il clip verrà restituito con la stessa risoluzione del CHM, ovvero quella originaria. NB: qualora l'utente definisse un valore di risoluzione inferiore a quello del dato di origine, il plugin restituirà un warning.
* **7 - Output CHM folder:** premendo sul bottone (...) si aprirà una finestra di dialogo tipo esplora risorse da cui sarà possibile navigare all'interno della propria macchina e selezionare la cartella dentro cui si desiderano salvare tutti gli output del processo (CHM delle singole tile e clip). Una volta selezionata la cartella il percorso a questa comparirà nella stringa di testo accanto al bottone. NB: qualora l'utente non selezionasse una cartella di output il plugin restituirà un messaggio di errore, il processo verrà bloccato e l'utente avrà la possibilità di selezionare la cartella e successivamente rilanciare il calcolo.
* **8 - scelta del formato:** dal menù a tendina è possibile selezionare il formato di output con cui si vogliono salvare i risultati del processo, sia i CHM delle singole tile che il clip file. Di default il formato selezionato è il GeoTIFF.
* **9 - scelta del sistema di riferimento:** clickando sul bottone si aprirà la finestra di dialogo standard di Qgis per la scelta del sistema di riferimento. Di default il plugin utilizza il sistema di riferimento originario del DSM e DTM. Qualora invece l'utente selezionasse un sistema di riferimento diverso, gli output del processamento saranno riproiettati nel sistema di riferimento richiesto.
* **10 - remove values < 0:** la casella di controllo permette appunto di gestire l'eliminazione di eventuali valori negativi dal CHM. Se la casella è spuntata i valori negativi presenti nei CHM calcolati verranno posti uguali a 0. Di default la casella è già spuntata ma è sufficiente rimuovere la spunta per ottenere i CHM risultanti con il valore minimo effettivo quindi eventualmente comprensivo anche di valori negativi.
* **11- remove values > xx:** in questo caso inserendo un valore numerico intero nella box verranno eliminati dai CHM finali i valori maggiori del valore di soglia indicato. Come nel caso della soglia per i valori negativi, anche in questo caso tutti i pixel con valore maggiore di quello indicato verranno posti uguali al valore stesso. Di default il valore è 0, qualora l'utente non specifichi un valore di soglia diverso da quello di default, verrà restituito il CHM con i valori effettivi.
* **12 - Log:** in questa area compariranno durante il processo messaggi informativi sullo stato di avanzamento del processo. Qui appariranno anche eventuali messaggi di warning e di errore. Nel caso di warning si tratta solo di avvisi per l'utente che però non bloccano il processo, in caso di errori o problematiche di vario tipo verrà restituito un messaggio e l'utente potrà modificare l'impostazione dei parametri di input e successivamente rilanciare il processamento. Al termine del processo, qualora andato a buon fine, comparirà un messaggio contenente un riassunto di tutti i parametri di input indicati per il calcolo seguito dalla scritta 'Processo terminato'.
* **13 - Clear Log:** si tratta di un bottone che pulisce l'area di testo eliminando i messaggi relativi a un processamento precedente.
* **14 - OK:** è il pulsante che l'ancia l'intero processamento. Una volta definiti tutti i parametri in input l'utente clickando sul pulsante Ok darà avvio al processo vero e proprio. Come già anticipato al punto 12, in caso di messaggi di errore che richiedano da parte dell'utente un'ulteriore interazione con l'interfaccia grafica, sarà possibile andare a modificare i parametri necessari e successivamente clickare nuovamente il tasto ok per rilanciare il processamento.
* **15 - Close:** l'interfaccia grafica del plugin resta aperta e attiva finchè l'utente non la chiuderà clickando sul tasto Close. In questo modo si chiuderà l'interfaccia grafica e tutti i vari parametri di input verranno ripristinati ai loro valori di default.

Prove di elaborazione
--------------------------------------------

In occasione del corso è stato preparato un dataset ridotto che verrà utilizzato per mostrare il funzionamento del plugin ed esemplificare le diverse casistiche che si possono presentare. Nella cartella **dataset_corso_06_19_venezia** sono contenuti:

* file tile_regione_cortina.gpkg: estrazione del file *tile_dsm_dtm* per il comune di Cortina d'Ampezzo
* file c0605011_categforestali.shp: estrazione della Carta Forestale Regionale per il comune di Cortina d'Ampezzo
* cartella dati_lidar: contiene le sottocartelle relative ad alcune campagne di volo effettuate sul territorio del comune di Cortina d'Ampezzo, in particolare per il corso sono state selezionate solo alcune campagne e un numero limitato di tile per ridurre i tempi di computazione in aula

Operazioni preliminari
"""""""""""""""""""""""""""""""""""""""""""""""""""
* Avviare Qgis
* Installazione del Plugin CHM from LIDAR (si veda sopra)
* Avviare il Plugin clickando sull'icona che sarà comparsa nella toolbar a installazione avvenuta. Come già descritto, all'avvio del plugin viene automaticamente caricato nel progetto Qgis il file *tile_dsm_dtm* contenente le tile delle diverse campagne di volo effettuato sul territorio regionale. **NB: per il corso verrà utilizzato il file tile_regione_cortina.gpkg, quindi rimuovere dal progetto il layer tile_dsm_dtm**

.. image:: img/rimuovere_layer.png

* Caricare il layer **tile_regione_cortina.gpkg**. Di default al caricamento del layer questo viene nominato *tile_regione_cortina tile_dsm_dtm* rinominare il layer in **tile_dsm_dtm**

.. image:: img/rinomina_layer.png

Una volta rinominato il layer, aprire la tabella degli attributi e con l'utilizzo del calcolatore di campi sostituire il contenuto della colonna **P_BASE** con il percorso assoluto alla cartella dati_lidar salvata sul PC

.. image:: img/tabella_path.png

.. image:: img/path_base.png

**ATTENZIONE alla sintassi!** E' molto importante che il percorso sia scritto correttamente, infatti il contenuto della colonna P_BASE unito alle altre colonne (P_CAMPAGNA, P_DTM e P_DSM) compongono il percorso ai file DSM e DTM che il plugin utilizza per il calcolo del CHM.

**NB:** queste operazioni preliminari sono richieste solo per il corso, in seguito sarà possibile utilizzare direttamente il file tile_dsm_dtm che viene caricato all'avvio del plugin e che contiene già i percorsi alle cartelle di Regione Veneto.

Scelta della sola Campagna di Volo
""""""""""""""""""""""""""""""""""""""""
Scegliendo la sola campagna di volo, viene calcolato il CHM per ogni tile appartenente alla campagna selezionata.

.. image:: img/solo_campagna_bis.png

* Selezionare la campagna **CAMPAGNA_TEST\\Contratto_140** dal menù a tendina *Select a campaign*
* Scegliere una cartella in cui salvare gli output del processo

Nel caso della sola campagna di volo sono abilitate le funzioni che consentono:

* la scelta del formato file, 
* la scelta del sistema di riferimento,
* la rimozione dei valori negativi
* la rimozione dei valori sopra una certa soglia

Restano invece disabilitate le funzioni relative al clip e alla scelta della risoluzione con cui crearlo. Infatti non scegliendo un'area di interesse non verrà prodotto alcun ritaglio.

Clickando su OK si avvia il processo di calcolo

.. image:: img/processo_camapagna_terminato.png

I CHM calcolati vengono automaticamente caricati nel progetto Qgis insieme al file vettoriale che contiene le tile per cui è stato calcolato il CHM. Aprendo la tabella di questo layer vettoriale, si nota che all'interno della colonna **P_CHM** è stato automaticamente inserito il percorso alla cartella in cui sono stati salvati i CHM, nella cartella **N_CHM** il nome dei file con relativa estensione del formato e nella colonna **EPSG_CHM** il codice EPSG del sistema di riferimento scelto.

.. image:: img/tabella_campagna.png

Scelta di un'Area di interesse e della Campagna di Volo
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
Caricare nel progetto Qgis il file vettoriale della Carta Forestale. Si selezioni una geometria che rappresenterà l'area di interesse per la quale verrà calcolato il CHM. **NB:** utilizzando un dataset limitato e non avendo quindi a disposizione tutti i file DSM e DTM del territorio di Cortina utilizzeremo un'AOI che sappiamo intersecare la campagna **CAMPAGNA_TEST\\Contratto_140**

.. image:: img/aoi_campagna.png

In questo caso verranno calcolati i CHM per tutte le tile che intersecano l'area di interesse selezionata.

.. image:: img/aoi_campagna_gui_bis.png

* Selezionare il layer che contiene l'area di interesse **c0605011_categforestali** dal menù a tendina *Select an AOI*
* Checkare la casella *Using selected features*
* Selezionare la campagna **CAMPAGNA_TEST\\Contratto_140** dal menù a tendina *Select a campaign*
* Scegliere un nome per il file clip (senza estensione)
* Scegliere una cartella in cui salvare gli output del processo

Nel caso della scelta di un'AOI e della campagna di volo sono abilitate le funzioni che consentono:

* la scelta del formato file, 
* la scelta del sistema di riferimento,
* la rimozione dei valori negativi
* la rimozione dei valori sopra una certa soglia

Resta invece disabilitate le funzione per la scelta della risoluzione con cui creare il file clip, in questo caso infatti il clip verrà creato con la risoluzione originaria della campagna.

Clickando su OK si avvia il processo di calcolo

.. image:: img/aoi_campagna_end.png

I CHM calcolati e il file clip vengono automaticamente caricati nel progetto Qgis insieme al file vettoriale che contiene le tile per cui è stato calcolato il CHM. Anche in questo caso aprendo la tabella di questo layer vettoriale, si nota che all'interno della colonna **P_CHM** è stato automaticamente inserito il percorso alla cartella in cui sono stati salvati i CHM, nella cartella **N_CHM** il nome dei file con relativa estensione del formato e nella colonna **EPSG_CHM** il codice EPSG del sistema di riferimento scelto.

Scelta della sola Area di interesse
""""""""""""""""""""""""""""""""""""
Si tratta del caso in cui l'utente voglia calcolare il CHM per una particolare area di interesse senza però conoscere la campagna o le campagne di volo che la intersecano. In questo caso si potranno verificare tre casistiche che il plugin gestirà in modo diverso:

* 1 - l'AOI interseca una sola campagna di volo: verranno calcolati i CHM di tutte le tile che intersecano l'AOI e verrà generato il clip. In questo caso verrà utilizzata la risoluzione e il sistema di riferimento originari dei dati qualora l'utente non ne abbia settati di diversi. 
* 2 - l'AOI interseca più campagne di volo non sovrapposte: verranno calcolati i CHM di tutte le tile che intersecano l'AOI e verrà generato il clip. In questo caso però verranno fatte in fase di calcolo due controlli, uno sul sistema di riferimento e uno sulla risoluzione. Qualora le campagne abbiano sistema di riferimento diverso il processo si bloccherà restituendo un messaggio di warning e verrà richiesto all'utente di selezionare un sistema di riferimento a meno che non sia stato già selezionato in fase di settaggio dei parametri in input. Qualora invece le campagne di volo abbiano risoluzione diversa e non sia stata definita una risoluzione in input, verrà presa di default quella maggiore.
* 3 - l'AOI interseca più campagne di volo sovrapposte: il processo si blocca e verrà restituito un messaggio con elencate alcune informazioni relative alle diverse campagne di volo (ente, nome della campagna, anno e risoluzione) e verrà richiesto all'utente di selezionare la campagna per la quale si vuole calcolare il CHM.

**CASO 1**

Si utilizzi la stessa area di interesse del caso precedente che sappiamo intersecare la sola campagna di volo  **CAMPAGNA_TEST\\Contratto_140**.

.. image:: img/solo_aoi_gui.png

* Selezionare il layer che contiene l'area di interesse **c0605011_categforestali** dal menù a tendina *Select an AOI*
* Checkare la casella *Using selected features*
* Scegliere un nome per il file clip (senza estensione)
* Scegliere una cartella in cui salvare gli output del processo

Nel caso della scelta della sola AOI sono abilitate le funzioni che consentono:

* la scelta della risoluzione
* la scelta del formato file, 
* la scelta del sistema di riferimento,
* la rimozione dei valori negativi
* la rimozione dei valori sopra una certa soglia

**NB:** per quanto riguarda la risoluzione se l'utente non definisce un valore nell'apposita box verrà utilizzata la risoluzione originaria dei dati (DSM e DTM)

Clickando su OK si avvia il processo di calcolo

.. image:: img/solo_aoi_end.png

**CASO 2**

Selezioniamo un'area di interesse che sappiamo intersecare le tile di due campagne differenti che non si sovrappongono. L'area selezionata infatti si sovrappone alle due campagne di volo create ad hoc per il corso, ovvero la **CAMPAGNA_TEST\\Contratto_140** e la **CAMPAGNA_TEST_ADIACENZA\Contratto_XXX**.

.. image:: img/solo_aoi_caso2_gui.png

* Selezionare il layer che contiene l'area di interesse **c0605011_categforestali** dal menù a tendina *Select an AOI*
* Checkare la casella *Using selected features*
* Scegliere un nome per il file clip (senza estensione)
* Scegliere una cartella in cui salvare gli output del processo

Nel caso della scelta della sola AOI sono abilitate le funzioni che consentono:

* la scelta della risoluzione
* la scelta del formato file, 
* la scelta del sistema di riferimento,
* la rimozione dei valori negativi
* la rimozione dei valori sopra una certa soglia

**NB:** per quanto riguarda la risoluzione se l'utente non definisce un valore nell'apposita box verrà utilizzata la risoluzione originaria dei dati (DSM e DTM). In questo specifico caso però, è possibile che le risoluzioni siano diverse dal momento che le campagne di volo che vengono intersecate sono più di una. Se così fosse il plugin utilizzerà di default la risoluzione minore. Qualora invece l'utente avesse definito una risoluzione come parametro in input verrà ovviamente utilizzata quella definita.

Clickando su OK si avvia il processo di calcolo

.. image:: img/solo_aoi_caso2_end.png

Si provi a modificare la risoluzione nella tabella del layer *tile_dsm_dtm* per almeno una delle tile che vengono intersecate dall'AOI selezionata inserendo un valore maggiore di quello presente in tabella (es. 3). Una volta salvata la modifica alla tabella, si rilanci il processo premendo OK. In questo caso il file di clip verrà creato con una risoluzione pari al valore massimo trovato in tabella per le tile selezionate.

.. image:: img/solo_aoi_caso2_maxres.png

In questo caso il plugin fa anche un controllo sul sistema di riferimento delle diverse campagne che vengono selezionate. Nel caso in cui il sistema di riferimento sia diverso, il processo si blocca e il plugin restituisce un messaggio di warning in cui vengono elencati i sistemi di riferimento trovati e si richiede all'utente di indicare un sistema di riferimento clickando sul tasto CRS. NB: questo particolare caso non è riproducibile in occasione del corso in quanto i dati messi a nostra disposizione hanno tutti lo stesso sistema di riferimento.

.. image:: img/solo_aoi_caso2_rs.png

**CASO 3**

In questo caso utilizziamo come area di interesse il poligono all'interno del file AOI.shp presente all'interno della cartella **dataset_corso_06_19_venezia**. Si cariche lo shapefile AOI.shp all'interno del progetto Qgis. Si noti che il layer contiene una sola geometria quindi non sarà necessario selezionarla per utilizzarla come area di interesse all'interno del plugin. 

L'area di interesse in questo caso si interseca con la campagna **CAMPAGNA_TEST_SOVRAPPOSIZIONE\Contratto_YYY** creata ad hoc per il corso e a altre campagne che in questo caso però si sovrappongono fra loro.

.. image:: img/solo_aoi_caso3_gui.png

* Selezionare il layer che contiene l'area di interesse **AOI** dal menù a tendina *Select an AOI*
* La casella *Using selected features* rimarrà disabilitata
* Scegliere un nome per il file clip (senza estensione)
* Scegliere una cartella in cui salvare gli output del processo

Nel caso della scelta della sola AOI sono abilitate le funzioni che consentono:

* la scelta della risoluzione
* la scelta del formato file, 
* la scelta del sistema di riferimento,
* la rimozione dei valori negativi
* la rimozione dei valori sopra una certa soglia

Clickando su OK si avvia il processo di calcolo

.. image:: img/solo_aoi_caso3_war.png

Il plugin blocca il processso e restituisce un messaggio di warning in cui vengono elencate le campagne di volo selezionate. Per ogni campagna viene indicato l'ente, il nome della campagna, l'anno e la risoluzione. Viene quindi richiesto all'utente di selezionare la campagna di volo sulla quale si desidera calcolare il CHM.

* Selezionare la campagna **CAMPAGNA_TEST_SOVRAPPOSIZIONE\Contratto_YYY** dal menù a tendina *Select a campaign*

Clickando nuovamente su OK si avvia il processo di calcolo

.. image:: img/solo_aoi_caso3_end.png

In questo caso se l'utente non ha fornito in input un valore di risoluzione verrà utilizzata per generare il clip quella della campagna che è stata selezionata, altrimenti verrà utilizzato il valore fornito.
