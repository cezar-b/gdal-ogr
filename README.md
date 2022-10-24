# gdal-ogr

## ogr2ogr

- Pentru a vedea ce formate sunt acceptate de OGR, se introduce comanda:  
`ogr2ogr --formats`

### Conversii de formate

- **Din Shapefile în GeoPackage**  
`ogr2ogr -f GPKG nume.gpkg nume.shp`

- **Din Shapefile în GeoJSON**  
`ogr2ogr -f GeoJSON nume.geojson nume.shp`

- **Pentru a converti în masă fișiere de un singur format într-un GeoPackage nou**  
`ogr2ogr -f GPKG nume.gpkg /calea/către/dosar`


- Pentru a scrie și alte elemente în același vector, se folosește în plus comanda `-append`.

- Pentru a crea un nou strat alături de unele deja existente (de exemplu, într-un GeoPackage), se folosește comanda `-update`

- Pentru a suprascrise un strat deja existent: `-overwrite`.

- Pentru a introduce într-un GeoPackage doar anumite elemente vectoriale, se poate realiza o interogare prin dialect SQLite, folosind comanda `-sql` și `-nln` pentru un nou nume; pentru a defini dialectul de SQL folosit, înainte de -sql: `-dialect sqlite`; util inclusiv dacă generăm un nou GeoPackage cu ajutorul terminalului, dacă stratul final e invalid; exemplu: `ogr2ogr -update -f GPKG test.gpkg judete_1930.shp -nln nume_nou -sql "SELECT * FROM rohgis_judete_1930 WHERE Nume LIKE 'B%'"`

### Subseturi

- **Subset bazat pe interogare**  
`ogr2ogr -where 'denumire LIKE "R%"' subset_nume.shp nume.shp`

### Reproiectări

- Pentru a folosi o anumită proiecție, se folosește comanda:
`-t_srs`, urmată de un cod EPSG, ESRI sau o definiție +proj, înainte de o eventuală interogare SQL.

## ogrinfo

Prezintă un sumar al informațiilor referitoare la un strat (nume, număr de entități, sistem de coordonate, numele și tipul cîmpurilor).

`ogrinfo -so <path/to/file.gpkg> <layer_name>`

`-so` (summary only) = sinteză a informațiilor  
`-al` (list all features) = pentru afișarea tuturor entităților din strat  

## gdalinfo

Prezintă un sumar al informațiilor referitoare la un raster (nume, tip, rezoluție, număr de benzi, sistem de coordonate etc).  

`gdalinfo raster.tif`

## gdalwarp

Utilitar de proiectare, reproiectare, georeferențiere și mozaicare a datelor raster.   
Sintaxa minimală pentru proiectare (reproiectare) este:

`gdalwarp intrare.tif rezultat.tif -t_srs EPSG:3844`

## gdaldem

Utilitar de analiză pentru modele numerice de teren. Conține mai multe moduri ce corespund cu unii indicatori morfometrici.
Sintaxa de bază este următoarea:  

`gdaldem <mod> intrare.tif rezultat.tif`

Unde `<mod>` poate fi:  
- `hillshade` – generează un model de umbrire pentru un raster cu informație altitudinală;  
- `slope` – generează un model de pante pentru un raster cu informație altitudinală;  
- `aspect` – generează un model de expunere a versanților pentru un raster cu informație altitudinală;  
- `color-relief` – generează un model hipsometric pentru un raster cu informație altitudinală;  
- `TRI` – generează un model ce cuprinde indicele de rugozitate al terenului pentru un raster cu informație altitudinală;  
- `TPI` – generează un model ce cuprinde indicele poziției topografice pentru un raster cu informație altitudinală;  
- `roughness` – generează un model de rugozitate pentru un raster cu informație altitudinală.




