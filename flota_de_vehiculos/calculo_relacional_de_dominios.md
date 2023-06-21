a) Camiones de gasolina que han puesto más de 100 litros en algún repostaje:

```lua
{ v | ∃ m, t, c, f, e, l (    -- Conjunto de vehículos v donde existe un m, t, c, f, e, l
    VEHICULO(v, m, t, c) ∧    -- Vehículo v con matrícula m, tipo t y consumo de combustible c
    COMBUSTIBLE(m, f, e, l) ∧  -- Vehículo con matrícula m que repostó en la estación e con cantidad l de combustible
    (t = 'Camion') ∧           -- El tipo de vehículo es 'Camion'
    (c = 'Gasolina') ∧         -- El consumo de combustible es 'Gasolina'
    (l > 100)                  -- La cantidad de combustible es mayor a 100
)}
```

b) Vehículos que han puesto combustible en la estación E1 pero no en la E2:

```sql
{ v | ∃ m, f1, f2, e1, e2, l1, l2 (
    VEHICULO(v, m, _, _) ∧ 
    COMBUSTIBLE(m, f1, e1, l1) ∧ 
    COMBUSTIBLE(m, f2, e2, l2) ∧ 
    (e1 = 'E1') ∧ 
    (e2 = 'E2') ∧ 
    (e1 ≠ e2)
)}
```

c) Vehículos que siempre han repostado el mismo número de litros:

```sql
{ v | ∃ m, f1, f2, e1, e2, l1, l2 (
    VEHICULO(v, m, _, _) ∧ 
    COMBUSTIBLE(m, f1, e1, l1) ∧ 
    COMBUSTIBLE(m, f2, e2, l2) ∧ 
    (l1 = l2)
)}
```

d) Estaciones en las que han repostado vehículos de todos los tipos:

```sql
{ e | ∃ m, t, c (
    VEHICULO(m, t, c) ∧ 
    COMBUSTIBLE(m, _, e, _) ∧ 
    ∀x (VEHICULO(m, x, _) ⇒ ∃ y (COMBUSTIBLE(m, _, e, _) ∧ x = y))
)}
```
