a) Estaciones de la cadena DISA que hoy tienen el precio de algún combustible inferior a 1.15 euros/litro:
```sql
Π(E) Σ((CAD='DISA') ∧ (P<1.15)) (ESTACION)
```

b) Vehículos que no han repostado nunca en la estación E1:
```sql
VR_E1 = Π(M) Σ(E='E1') (COMBUSTIBLE)) # Vehiculos repostados en E1
VEHICULO - VR_E1
```

c) Vehículos que han repostado en todas las estaciones de la cadena TEXACO:
```sql
ET = Π(E) Σ(CAD='TEXACO') (ESTACION) # Estaciones TEXACO
VR_T = Π(M,E) (COMBUSTIBLE ⨝ ET) (COMBUSTIBLE) # Vehículos repostados en estaciones TEXACO
VR_TT = Π(M) (VR_TEXACO / Π(M) VEHICULO) # Vehículos que han repostado en todas las estaciones TEXACO
```

d) Estaciones que algún día han vendido combustibles de todas las clases:
```sql
TODAS_CLASES = Π(C) COMBUSTIBLE # Todas las clases de combustible
Π(E) (Π(E, C) Σ(C IN TODAS_CLASES) (ESTACION)) # Estaciones con todas las clases de combustible
```
