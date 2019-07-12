# lidar_tile_maker_manuale
Manuale del Plugin qgis Lida Tile Maker per la creazione automatica delle tile derivanti da un volo lidar

Note per la Traduzione (Windows)
---------------------------------
Installare sphinx da cmd *pip install -U sphinx*
Installare sphinx-intl da cmd *pip install sphinx-intl*

Per tradurre un progetto Readthedocs bisogna seguire i seguenti passaggi:

* Dalla cartella della repository github lanciare tramite cmd *sphinx-build -b gettext . _build/gettext* il comando crea una cartella _build/gettext_ con all'interno i file .pot
* Sempre dalla cartella della repository github lanciare tramite cmd *sphinx-intl update -p _build/gettext -l it -l de -l es* questo comando creerà una cartella _locales_ con dentro una cartella per ogni lingua che si è scelta, dentro alle singole cartelle delle lingue si trovano i file .po
* Aprire ogni file .po con un editor di testo e tradurre seguendo la sintassi

  es.<br>
  msgid ""<br>
  "Read the Docs hosts documentation for the open source community."<br>
  "It supports :ref:`Sphinx <sphinx>` docs written with reStructuredTe<br>
  msgstr ""<br>
  "Read the Docs pubblica la documentazione per la comunità open source "<br>
  "Supporta documenti :ref:`Sphinx <sphinx>` scritti con reStructuredText."<br>

* Committare il tutto su github nella repository del manuale
* Da Readthedocs creare un nuovo progetto (uno per ogni lingua) importando la repository github del manuale (si deve fare con la modalità manuale dando come url il link alla repository github del manuale)
* Dalla proprietà Admin del nuovo progetto Readthedocs impostare come lingua del progetto quella della traduzione (es. italiano)
* Da Readthedocs fare il build
* Da Readthedocs andare nel progetto in lingua originale e dalle proprietà Admin--Translation, impostare il progetto tradotto come traduzione 

In questo modo comparirà nella versione in lingua originale del documento on line la possibilità di andare alla traduzione

Qualora venissero fatte modifiche e/o aggiunte al testo in lingua originale (file .rst), è ovviamente possibile fare un update dei file della traduzione (.pot e .po):

* Dalla cartella della repository github lanciare tramite cmd <br>
  *sphinx-build -b gettext . _build/gettext* <br>
  Con questo comando vengono aggiornati i file .pot
* Dalla cartella della repository github lanciare tramite cmd <br>
  *sphinx-intl update -p _build/gettext -l it -l de -l es* <br>
  Con questo comando vengono aggiornati i file .po, ovviamente le parti già tradotte e che non sono state modificate nella lingua originale vengono mantenute. Eventuali nuove righe di testo e parti modificate vengono invece aggiornate e si deve quindi procedere ad aggiungere la traduzione o modificare quella esistente.
* Committare le modifiche su github

NB. Se successivamente si volessero aggiungere nuove traduzioni bisogna rifare tutto il procedimento saltando però il primo step.

**Link utili**

http://www.sphinx-doc.org/en/master/usage/installation.html

https://docs.readthedocs.io/en/stable/localization.html

https://docs.readthedocs.io/en/stable/guides/manage-translations.html

http://www.sphinx-doc.org/en/stable/intl.html#intl

https://github.com/BurntSushi/nfldb/wiki/Python-&-pip-Windows-installation
