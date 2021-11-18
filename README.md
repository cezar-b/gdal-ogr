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
