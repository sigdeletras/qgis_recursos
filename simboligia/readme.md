# Simbología y etiquetado


Etiquetado/simbología según expresiones (ej. curvasde nivel /contours)

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
