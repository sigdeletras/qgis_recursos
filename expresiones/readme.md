# Expresiones

## Ayuda

- https://docs.qgis.org/2.18/en/docs/user_manual/working_with_vector/expression.html 
- HfcQGIS: Help funzioni calcolatore di campi di QGIS http://hfcqgis.opendatasicilia.it/it/latest/ 

## Operadores matemáticos
```
125862 +586215
5805 * 4.5
25897/489
1528^3 
sqrt(458 )
```

## Funciones con cadenas
```
length('Curso Avanzado de QGIS’)
upper('Curso Avanzado de QGIS’)
regexp_replace('Curso Avanzado de SIG','SIG','QGIS')
substr('Curso Avanzado de GIS',7,9)
replace('Curso Avanzado de GIS',' ', '&')
strpos('Curso Avanzado de QGIS','QGIS')
```

Selecciona los municipios cuya población haya crecido en 2018
```
"pop18" > "pop17"
```

¿Hay algún municipio cuya población sea igual en los años?
```
"pop18" = "pop17"
```

Busca el topónimo “caseta la mechuga” en la capa “nombres_geográficos”. Usa el operador LIKE
```
"etiqueta"  LIKE 'caseta la mechuga'
```

Realiza la misma búsqueda con el operador ILIKE ¿El resultado es el mismo?
```
"etiqueta"  ILIKE 'Caseta la Mechuga'
```

Busca todos los nombres que empiezan con Barranco
```
"etiqueta" like 'Barranco%'
```

Busca los nombres que terminen con ‘Alto’
```
"etiqueta"  LIKE '%Alto'
```

Busca los nombres que empiecen por Barranco y que terminen por Fuente
```
"etiqueta"  LIKE 'Barranco%' and   "etiqueta"  LIKE '%Fuente' 
```

Busca los nombres que empicen por Cerro o por Corona
```
"etiqueta"  LIKE 'Cerro%'  or  "etiqueta"  LIKE 'Corona%'
```

Busca los nombres que contenganpor Fuente pero no sean de tipo Rural
```
"etiqueta"  LIKE '%Fuente%'  and not "ruralurban"   LIKE  'R' 
```

## Funciones de geometría

Selecciona los municipios con una superfie (m²) inferior o igual a la media.
```
$area <= mean($area)
```

Genera las columnas virtuales xcent e ycent  de tipo numérico decimal que tenga el centroide ($centroid) de cada municipio.
```
x(centroid($geometry))
y(centroid($geometry))
```

Crea los campos  virtuales latitud y longitud con las coordenadas geográficas de cada uno de los puntos. Recuerda que van a ser valores numéricos con decimales.
```
x(transform( $geometry, 'EPSG:25830', 'EPSG:4258' ))
y(transform( $geometry, 'EPSG:25830', 'EPSG:4258' ))
```

Etiquetado GMS
```
'lon :' || floor($x)
|| '° ' || 
floor( ($x - floor($x))*60) 
||''' '|| 
format_number( 
to_real((($x - floor($x))*60) -floor((($x - floor($x))*60 )))*60 ,2)||'" E'
|| '_' || 
'lat :' || floor($y)
|| '° ' || 
floor( ($y - floor($y))*60) 
||''' '|| 
format_number( 
to_real((($y - floor($y))*60) -floor((($y - floor($y))*60 )))*60 ,2) ||'" N'
```

## Operador de concatenación

• Nombre del municipio, la provincia entre paréntesis y la densidad de población preceda del texto “Densidad: “ en indicando que el datos está en km². Usa el operador concatenación (||)  para añadir campos y texto. Los textos auxiliares se añaden entre comillas simples.
 ```
 "d_muni_ine"  || ' (' ||  "provincia" || ') Densidad: ' ||  "pop18"   || ' km2'
 ```

## Condional

Municipios han tenido un crecimiento positivo de  la población y cuáles no.
```
CASE 
  WHEN  "pop18" > "pop17" THEN 'Positivo'
  ELSE 'Negativo'
END
```
## Funciones de agregación (sum, group_by)
Calcula la superficie en km²  de la provincia (sum)
```
sum($area*0.000001)
```
Calcula la densidad de población en km²  de la provincia.
```
mean(pop18/($area*0.000001))
```

Selecciona el municipio con el área menor por zonas POTA
```
$area =  minimum( $area, group_by:= "zonapota")
```

Campo  virtual del porcentaje de superficie del municipio respecto al total de la provincia. El campo solo debe tener dos decimales.
```
round(($area / sum( $area ))*100,2)
```
