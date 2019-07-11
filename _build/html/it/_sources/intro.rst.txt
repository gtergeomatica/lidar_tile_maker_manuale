Introduction
==================

Credits
------------------------------------------

.. image:: img/Gter.png
https://www.gter.it/


The **Lidar Tile Maker** Plugin for QGIS and this related manual have been developed by Gter srl Innovazione in Geomatica GNSS e GIS.



Both the plugin and the manual are licensed under a Creative Commons Attribution 4.0 International License https://creativecommons.org/licenses/by/4.0/




Purpose
------------------------------------------

The Lidar Tile Maker Plugin has been developed in order to make easier the use of the CHM from Lidar Plugin. The latter has been developed by Gter srl and funded by the 'Programma di sviluppo rurale per il Veneto 2014-2020' - Regione del Veneto - Direzione AdG FEASR e Foreste. It allows to compute the Canopy Height Model (CHM) starting from Lidar data, in particular Digital Surface Model (DSM)  and Digital Terrain Model (DTM).

The use of CHM from LIDAR plugin is based on a Tile Vector Layer which is automatically uploaded to the working Qgis project when the plugin icon is pressed. By default the tile vector layer, named **tile_dsm_dtm.gpkg**, contains data of Regione Veneto (Italy) which has founded its development. Obviously the **tile_dsm_dtm** layer can be modified by user including its own data.

The **Lidar Tile Maker** Plugin allows users to create their own Tile Vector Layer with all the characteristics requested by the CHM from LIDAR Plugin. For instance, the plugin creates a **tile_dsm_dtm.gpkg** with all the necessary information stored in the attribute table. The table fields are automatically created and named so as to be used by the CHM from LIDAR Plugin.

The final output is a file GeoPackage (**tile_dsm_dtm.gpkg**).


Glossary
------------------------------------------

* CHM: Canopy Height Model
* DSM: Digital Surface Model
* DTM: Digital Terrain Model
* GIS: Geographic Information System
* LIDAR: Laser Imaging Detection and Ranging









.. _Gter srl: https://www.gter.it
