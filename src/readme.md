# SRC presonalizado rejila Ntv2

Descarga de archivo de rejilla [https://www.ign.es/web/ign/portal/gds-rejilla-cambio-datum](https://www.ign.es/web/ign/portal/gds-rejilla-cambio-datum)

``
+proj=utm +zone=30 +ellps=intl +nadgrids=C:/rejillaIGN/PENR2009.gsb +units=m +wktext +no_defs
``
Explicación

+ **proj**: indica el nombre de la Proyección.
+ **Zone**: el huso de la proyección UTM.
+ **Ellps**: indica el nombre del elipsoideInternacional (1924).
+ **Ajuste del datum**:
     - Basado en un ajuste al elipsoide WGS84 mediante métodos de 3 o 7 parámetros (+towgs84)
     - Wn base a un archivo de rejilla NTv2 (+nadgrid) del cual indicamos su ubicación en el disco.
+ **Units**: indica las unidades del S.C.
+ **No_defs**: indica que no se emplea el archivo predeterminado

### Enlaces de interés

- https://www.cursosgis.com/re-proyeccion-de-capas-empleando-la-rejilla-ntv2/
- https://mappinggis.com/2015/03/como-transformar-de-ed50-a-etrs89-en-qgis-con-ntv2/
