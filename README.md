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

* Fare il build della traduzione, dalla cartella del nuovo progetto/repository readthedocs lanciare tramite cmd *sphinx-build -b html -D language=it . _build/html/it*
* Da Readthedocs importare la repository con la traduzione come nuovo progetto
* Dalla proprietà Admin di Readthedocs impostare come lingua quella della traduzione (es. italiano)
* Da Readthedocs fare il build
* Da Readthedocs andare nel progetto in lingua originale e dalle proprietà Admin- Translation, impostare il progetto tradotto come traduzione 
* Da Readthedocs fare il build

In questo modo comparirà nella versione in lingua originale del documento on line la possibilità di andare alla traduzione

**Link utili**

http://www.sphinx-doc.org/en/master/usage/installation.html

https://docs.readthedocs.io/en/stable/localization.html

https://docs.readthedocs.io/en/stable/guides/manage-translations.html

http://www.sphinx-doc.org/en/stable/intl.html#intl

https://github.com/BurntSushi/nfldb/wiki/Python-&-pip-Windows-installation
