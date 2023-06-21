1) Estaciones de la cadena DISA que hoy tienen el precio de algún combustible inferior a 1.15 euros/litro:
```sql
Π(E) Σ((CAD='DISA') ∧ (P<1.15)) (ESTACION)
```

2) Vehículos que no han repostado nunca en la estación E1:
```sql
VR_E1 = Π(M) Σ(E='E1') (COMBUSTIBLE)) # Vehiculos repostados en E1
VEHICULO - VR_E1
```

3) Vehículos que han repostado en todas las estaciones de la cadena TEXACO:
```
ET = Π(E) Σ(CAD='TEXACO') (ESTACION) # Estaciones TEXACO
VR_T = Π(M,E) (COMBUSTIBLE ⨝ ET) (COMBUSTIBLE) # Vehículos repostados en estaciones TEXACO
VR_TT = Π(M) (VR_TEXACO / Π(M) VEHICULO) # Vehículos que han repostado en todas las estaciones TEXACO
```
