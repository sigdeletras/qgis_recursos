# Simbología y etiquetado

## Enlaces
- Taller "Pedro-Juan Ferrer (https://twitter.com/vehrka) "Vuestros mapas son feos y no sabéis por qué"
 - https://tus-mapas-son-feos.readthedocs.io/es/develop/
 - https://geoinquietosvlc.github.io/tus_mapas_son_feos/
 - https://github.com/geoinquietosvlc/tus_mapas_son_feos
- Generación de cartográmas https://www.unigis.es/crear-cartogramas-qgis/
- Etiquetado basado en geometría. https://gitlab.com/GIS-projects/qgis-geometry-generator-examples


## Código

Etiquetado/simbología según expresiones (ej. curvasde nivel /contours)

[https://gis.stackexchange.com/questions/121585/choosing-only-one-contour-line-to-label-in-qgis](https://gis.stackexchange.com/questions/121585/choosing-only-one-contour-line-to-label-in-qgis)

```
 // select contours at vertical intervals of 50 metres
  ("z" % 50) = 0
 ```
  
 ```
 I.e. if you want to hide contourlines other than 500 m you can use this expression for the datadefined properties of the line symbol:

CASE WHEN Elevation / 500 - floor(Elevation / 500) =  0 then 
   color_rgba(255,255,255,100) 
else 
    color_rgba(255,255,255,0) 
end
i.e. for labeling only 500m intervals use this expression for:

CASE WHEN Elevation /500 - floor(Elevation / 500) = 0 THEN Elevation || ' m' END
i.e. for applying different line width use an expression like this for data defined properties:

CASE WHEN Elevation / 100 - floor(Elevation / 100) = 0 THEN 
    0.25 
WHEN Elevation / 50 - floor(Elevation / 50) = 0 THEN 
    0.15 
ELSE 
    0.1 
END
```

```
(step 100m)
"ELEV" LIKE '%00'  
"ELEV" LIKE '%00' OR "ELEV" LIKE '%50' (step 50m) or "ELEV" LIKE '%0' (step 10m)
```

Placing elevation numbers on contours with uphill orientation and position in QGIS

[https://gis.stackexchange.com/questions/26702/placing-elevation-numbers-on-contours-with-uphill-orientation-and-position-in-qg](https://gis.stackexchange.com/questions/26702/placing-elevation-numbers-on-contours-with-uphill-orientation-and-position-in-qg)

## Unidades para simbología/etiquetado
- Podemos usar milímetros, puntos, píxeles y pulgadas si queremos simbología dinámica que se ajuste según las escalas
cada una de ellas tiene su tamaño (lógico) no es lo mismos un etiquetado a 4 milímetros que a 4 puntos...
- si queremos trabajar con etiquetado estático podemos usar las unidades unidades de mapa o metros a escala. Estas van a coincidir si las unidades de nuestro mapa son metros Imagino que cambiarán si usamos src en unidades geográficas

La simbología/etiquetado en estas unidades es fija con independencia de la escala

Con este sistema nos acercamos más a lo que sería un etiquetado tipo CAD. Perdemos dinamismo en la vista de mapa pero nos aseguramos el tamaño en las composiciones

Equivalencia 
- 1 punto son 0,353 mm.
- 1 pulgada son 2,54 cm.

| pt  |  px |
|---|---|
|  2 | 4  |
|  3 | 5  |
|  4 |  6 |
|  5 |  7 |

https://reeddesign.co.uk/test/points-pixels.html

