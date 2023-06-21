a) Vehículos que solo han repostado en estaciones de la cadena DISA:
```lua
-- Selecciona los vehículos que solo han repostado en estaciones de la cadena DISA
SELECT DISTINCT V.M
FROM VEHICULO V
WHERE NOT EXISTS (
    -- Verifica que no exista ninguna combinación de combustible y estación que no sea de la cadena DISA para el vehículo
    SELECT *
    FROM COMBUSTIBLE C
    JOIN ESTACION E ON C.E = E.E
    WHERE V.M = C.M
    AND E.CADENA <> 'DISA'
);
```

b) Precio medio del litro de gasolina en cada una de las estaciones de CEPSA durante el mes de enero de 2023:
```lua
-- Calcula el precio medio del litro de gasolina en cada estación de CEPSA durante enero de 2023
SELECT E.E, AVG(P)
FROM ESTACION E
JOIN VEHICULO V ON E.E = V.E
JOIN COMBUSTIBLE C ON V.M = C.M
WHERE E.CADENA = 'CEPSA'
AND MONTH(C.F) = 1
AND YEAR(C.F) = 2023
GROUP BY E.E;
```

c) Estaciones que han vendido más de 5000 litros de gasolina en un mismo día:
```lua
-- Selecciona las estaciones que han vendido más de 5000 litros de gasolina en un mismo día
SELECT E.E
FROM ESTACION E
JOIN COMBUSTIBLE C ON E.E = C.E
WHERE C.C = 'gasolina'
GROUP BY E.E, C.F
HAVING SUM(C.L) > 5000;
```

d) Estación que el día 1 de junio de 2023 vendía la gasolina más barata:
```lua
-- Selecciona la estación que vendía la gasolina más barata el día 1 de junio de 2023
SELECT E.E
FROM ESTACION E
JOIN COMBUSTIBLE C ON E.E = C.E
WHERE C.C = 'gasolina'
AND C.F = '2023-06-01'
AND C.P = (
    -- Busca el precio mínimo de la gasolina el día 1 de junio de 2023
    SELECT MIN(P)
    FROM COMBUSTIBLE
    WHERE C = 'gasolina'
    AND F = '2023-06-01'
);
```

e) Vehículos tales que al menos el 30% de sus repostajes los han hecho en una misma estación:
```lua
-- Selecciona los vehículos que han realizado al menos el 30% de sus repostajes en una misma estación
SELECT V.M
FROM VEHICULO V
JOIN COMBUSTIBLE C ON V.M = C.M
GROUP BY V.M
HAVING SUM(CASE WHEN C.E = V.E THEN 1 ELSE 0 END) >= 0.3 * COUNT(*) ;
```
