# Distancia entre coordenadas en MYSQL
#### **Función para calcular distancias entre 2 puntos basado en su latitud y longitud.**
> El valor que retorna `fn_calcular_distancia` sera en **metros** y contara con **2 decimales**, para cambiar la cantidad de decimales que retorna la función tendremos que editar el segundo parametro de la función  `ROUND(código,decimales_mostrados)` 
***
```MYSQL
DELIMITER $$
CREATE  FUNCTION `fn_calcular_distancia`(`_A_LAT` DOUBLE, `_A_LON` DOUBLE, `_B_LAT` DOUBLE, `_B_LON` DOUBLE) RETURNS double
BEGIN
RETURN 
ROUND( -- Para un resultado exacto remover esta función
(111.111 *
DEGREES(ACOS(LEAST(1.0, COS(RADIANS(_A_LAT))
* COS(RADIANS(_B_LAT))
* COS(RADIANS(_A_LON - _B_LON))
+ SIN(RADIANS(_A_LAT))
* SIN(RADIANS(_B_LAT)))))) * 1000, -- Remover esta multiplicación `* 1000` para obtener el resultado en Kilometros o bien cambiarla por el tipo de conversión deseada
2); -- Cambiar a la cantidad de decimales a mostrar
END$$
DELIMITER ;
```
Llamar a la función desde una consulta y ordenandolo de manera decendiente
```MYSQL
SELECT 
fn_calcular_distancia(28.682974,-100.5396737,tabla.latitud,tabla.longitud) AS 'Distancia en metros'
FROM tabla
ORDER BY 1 DESC; -- Por que es el primer parametro seleccionado, va en la posición en la que llamaste la función
```
#### **Por ejemplo, al ejecutar esta consulta en mi proyecto retorna los siguientes valores.**
Distancia en metros | 
--- |
2978.48 |
1278.18 |
920.62 |
420.12 |
