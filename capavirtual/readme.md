# Ejemplo intersección

select equipamientos.*, EENN_donana.geometry as geom,
EENN_donana.CODIGOESPA
from equipamientos, EENN_donana
where st_within(equipamientos.geometry, EENN_donana.geometry)
