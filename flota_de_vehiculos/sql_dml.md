a) Crear una vista que indique para cada estación el total de litros de gasolina que vende cada día:
```sql
CREATE VIEW VentaLitrosPorDia AS
SELECT E, F, C, SUM(L) AS TotalLitros
FROM VEHICULO
GROUP BY E, F, C;
```

b) Eliminar de la base de datos las estaciones de servicio que no hayan vendido nada durante el mes de junio de 2023:
```sql
DELETE FROM VEHICULO
WHERE (E, F) IN (
    SELECT E, F
    FROM VEHICULO
    WHERE F LIKE '2023-06%'
    GROUP BY E, F
    HAVING SUM(L) = 0
);
```

c) Actualizar la base de datos con los precios de la gasolina para mañana incrementándolos en un 2% respecto al valor de hoy:
```sql
UPDATE VEHICULO
SET P = P * 1.02
WHERE F = CURRENT_DATE;
```

d) Crear una regla de integridad referencial entre las tablas COMBUSTIBLE y VEHICULO usando como clave ajena M y como acción compensatoria borrado en cascada:
```sql
ALTER TABLE VEHICULO
ADD CONSTRAINT FK_COMBUSTIBLE_VEHICULO
FOREIGN KEY (M)
REFERENCES COMBUSTIBLE (M)
ON DELETE CASCADE;
```

e) Imponer la restricción a la base de datos de que todas las estaciones de una misma cadena cada día venden cada clase de combustible al mismo precio:
```sql
ALTER TABLE VEHICULO
ADD CONSTRAINT CK_PrecioCombustible
CHECK (
    NOT EXISTS (
        SELECT E, F, CAD, C, COUNT(DISTINCT P) AS NumPrecios
        FROM VEHICULO
        GROUP BY E, F, CAD, C
        HAVING NumPrecios > 1
    )
);
```
