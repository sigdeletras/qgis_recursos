#Funciones

Algunos ejemplos de funciones Pyhton para usar dentro de expresione.

- Primera aproximación al uso de las funciones propias con Python https://geoinnova.org/blog-territorio/funciones-qgis-empezando-con-python/

'''

'''
- Using Custom Python Expression Functions https://www.qgistutorials.com/en/docs/custom_python_functions.html

'''python
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
  '''
