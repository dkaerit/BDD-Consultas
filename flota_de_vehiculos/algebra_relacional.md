a) Estaciones de la cadena DISA que hoy tienen el precio de algún combustible inferior a 1.15 euros/litro:
```sql
Π(E) Σ((CAD='DISA') ∧ (P<1.15)) (ESTACION)
```

b) Vehículos que no han repostado nunca en la estación E1:
```sql
# Vehiculos repostados en E1
VE_REP_E1 = Π(M) Σ(E='E1') (COMBUSTIBLE)) 
VEHICULO - VE_REP_E1
```

c) Vehículos que han repostado en todas las estaciones de la cadena TEXACO:
```sql
# Estaciones TEXACO
ESTACIONES_TEXACO = Π(E) Σ(CAD='TEXACO') (ESTACION) 

# Vehículos repostados en estaciones TEXACO
VE_REP_TEXACO = Π(M,E) (COMBUSTIBLE ⨝ ESTACIONES_TEXACO) (COMBUSTIBLE)

# Vehículos que han repostado en todas las estaciones TEXACO
Π(M) (VE_REP_TEXACO / Π(M) VEHICULO) 
```

d) Estaciones que algún día han vendido combustibles de todas las clases:
```sql
# Todas las clases de combustible
TODAS_CLASES = Π(C) COMBUSTIBLE 

# Estaciones con todas las clases de combustible
Π(E) (Π(E, C) Σ(C IN TODAS_CLASES) (ESTACION)) 
```

e) Vehículos que han repostado en todas las estaciones de alguna cadena:
```sql
# Cadenas y estaciones disponibles
CADENAS_ESTACIONES = Π(CAD, E) (Π(CAD) ESTACION) 

# Vehículos repostados en estaciones de cada cadena
VEHICULOS_REPOSTADOS_CADENA = Π(M, CAD) Σ(E IN CADENAS_ESTACIONES) (COMBUSTIBLE) 

# Vehículos que han repostado en todas las estaciones de alguna cadena
VEHICULOS_REPOSTADOS_TODAS_ESTACIONES = Π(M) (Π(M) VEHICULOS_REPOSTADOS_CADENA / Π(M) VEHICULO) 
```
