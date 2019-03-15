# Simbología y etiquetado

## Enlaces
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
