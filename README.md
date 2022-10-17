# Distancia-entre-coordenadas-en-MYSQL
Función para calcular distancias entre 2 puntos basado en su latitud y longitud.
```MYSQL
DELIMITER $$
CREATE  FUNCTION `fn_calcular_distancia`(`_A_LAT` DOUBLE, `_A_LON` DOUBLE, `_B_LAT` DOUBLE, `_B_LON` DOUBLE) RETURNS double
BEGIN
RETURN 
ROUND((111.111 *
DEGREES(ACOS(LEAST(1.0, COS(RADIANS(_A_LAT))
* COS(RADIANS(_B_LAT))
* COS(RADIANS(_A_LON - _B_LON))
+ SIN(RADIANS(_A_LAT))
* SIN(RADIANS(_B_LAT)))))) * 1000,2);
END$$
DELIMITER ;
```
