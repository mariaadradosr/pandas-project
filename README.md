# SHARK ATTACKS

Este proyecto consiste en la limpieza, análisis y extracción de conclusiones sobre los datos de ataques de tiburones que registra 'Shark Attack Institute' en todo el mundo desde hace años. 
http://www.sharkattackfile.net/index.htm

## Etapas

### Análisis exploratorio del dataset

- Dataset de 24 columnas y 5.992 filas.
- El 16% de valores nulos. El 52% de los nulos se concentran en dos columnas (`Unmamed: 22` y `Unmamed: 23`).
- La mayoría de colunas tiene una cantidad de valores únicos muy alto.
- No hay filas duplicadas.

### Limpieza y reorganización de datos: 

- Cambio del nombre de algunas columnas 
- Homogeneización de valores de columnas: 
    - `Country`: 
        - Para esta variable primero estudio en cuántos países se concentra más del 90% de los ataques (5.442). El resultado es 40
        - 'USA', 'AUSTRALIA', 'SOUTH AFRICA', 'PAPUA NEW GUINEA', 'NEW ZEALAND', 'BRAZIL', 'BAHAMAS', 'MEXICO', 'ITALY', 'FIJI', 'PHILIPPINES', 'REUNION', 'NEW CALEDONIA', 'MOZAMBIQUE', 'CUBA', 'SPAIN', 'INDIA', 'EGYPT', 'CROATIA', 'PANAMA', 'JAPAN', 'IRAN', 'SOLOMON ISLANDS', 'GREECE', 'HONG KONG', 'JAMAICA', 'FRENCH POLYNESIA', 'INDONESIA', 'ENGLAND', 'PACIFIC OCEAN', 'ATLANTIC OCEAN', 'BERMUDA', 'TONGA', 'VANUATU', 'VIETNAM', 'FRANCE', 'MARSHALL ISLANDS', 'SRI LANKA', 'TURKEY', 'IRAQ'
        - Defino la función países que persigue estudiar los literales de la columna Country y si encuentra parecido con algún país de la lista devolverme el nuevo literal.
        - Consigo transformar el literal de 60 casos más, por tanto mi escenario de estudio pasa de tener 5.442 valores (90.8% sobre el total) a 5.502 (91.8% sobre el total)
    - `Activity`:
        - Parto de las 5.502 filas filtradas en el paso anterior. Si miramos la columna Activity vemos que hay 480 nulos y los restantes 5.021 están poblados por 1.332 valores distintos.
        - Con el objetivo de reducir el número de actividades aplico una lógica similar a la de la columan Country y consigo quedarme con 4.682 filas de las 5.502 (480 tenían un nulo en Activity y el resto no he conseguido enmarcarlas en ninguna actividad genéricas) reduciendo a 27 valores únicos los 1.332 iniciales. 
    - `Year`: 
        - En el caso de los años voy a descartar todos los valores que no sigan un patrón de cuatro números y que el primer número no sea un 1 o un 2.
        - De las 4.682 filas anteriores me deshago de 73 filas cuyo año no sigue el patrón marcado. 
    - Extracción de los meses de la columna `Case Number`:
        - Creo una nueva columna 'Month__c' en la que mediante una función lambda extraigo el mes del campo Case Number que se compone de año, mes y día 
- Creo el dataset final (`shark`) dejando la columnas que necesito para el análisis y añadiendo una 'freq' que igualo a 1 para hacer conteos. Ajusto los types de los campos Year y Month.

## Análisis:
Para el análisis se estudia la evolución anual de los ataques desde que se tienen registro y después enfoco el análisis en los lugares que concentran la mayoría de ataquews (Estados Unidos y Australia)