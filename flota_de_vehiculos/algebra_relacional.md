1) Estaciones de la cadena DISA que hoy tienen el precio de algún combustible inferior a 1.15 euros/litro:
```sql
Π(E) Σ((CAD='DISA') ∧ (P<1.15)) (ESTACION)
```

2) Vehículos que no han repostado nunca en la estación E1:
```sql
VEHICULOS_REPOSTADOS_E1 = Π(M) Σ(E='E1') (COMBUSTIBLE))
VEHICULO - VEHICULOS_REPOSTADOS_E1
```
