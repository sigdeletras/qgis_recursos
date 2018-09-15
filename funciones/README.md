#Funciones

Algunos ejemplos de funciones Pyhton para usar dentro de expresiones.

**Hay que revisar la versión de la API. Seguramente**

Primera aproximación al uso de las funciones propias con Python https://geoinnova.org/blog-territorio/funciones-qgis-empezando-con-python/

```python
```

Using Custom Python Expression Functions https://www.qgistutorials.com/en/docs/custom_python_functions.html

```python
import math
from qgis.core import *
from qgis.gui import *

@qgsfunction(args=0, group='Custom', usesgeometry=True)
def GetUtmZone(value1, feature, parent):
    centroid = feature.geometry()
    longitude = centroid.asPoint().x()
    latitude = centroid.asPoint().y()
    zone_number = math.floor(((longitude + 180) / 6) % 60) + 1

    if latitude >= 0:
        zone_letter = 'N'
    else:
        zone_letter = 'S'

    return '%d%s' % (int(zone_number), zone_letter)
````

Function editor for QGIS expressions https://nathanw.net/2015/01/19/function-editor-for-qgis-expressions/

User defined expression functions for QGIS https://nathanw.net/2012/11/10/user-defined-expression-functions-for-qgis/

```python
from qgis.utils import qgsfunction
from qgis.core import QGis
 
@qgsfunction(0, "Python")
def vertices(values, feature, parent):
    """
        Returns the number of vertices for a features geometry
    """
    count = None
    geom = feature.geometry()
    if geom is None: return None
    if geom.type() == QGis.Polygon:
        count = 0
        if geom.isMultipart():
          polygons = geom.asMultiPolygon()
        else:
          polygons = [ geom.asPolygon() ]
        for polygon in polygons:
          for ring in polygon:
            count += len(ring)
    return count
 ```
How to create custom functios in QGIS using the function editor  https://howtoinqgis.wordpress.com/2017/05/20/how-to-create-custom-functions-in-qgis-using-the-function-editor/

```python
@qgsfunction(args='auto', group='Custom')
def factor_area(factor, feature, parent):
    """ This function returns the area of the current geometry multiplied by a user-defined factor. """
    geom_area = feature.geometry().area()
    new_area = factor * geom_area
    return new_area
```

