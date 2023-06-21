a) Camiones de gasolina que han puesto más de 100 litros en algún repostaje:

```sql
{ v | ∃m,t,c,f,e,l (
  VEHICULO(v, m, t, c) ∧ 
  COMBUSTIBLE(m, f, e, l) ∧ 
  (t = 'Camion') ∧ 
  (c = 'Gasolina' ∧ 
  (l > 100) 
)}
```

b) Vehículos que han puesto combustible en la estación E1 pero no en la E2:

```sql
{ v | ∃ m,f1,f2,e1,e2,l1,l2 (
    VEHICULO(v, m, _, _) ∧ 
    COMBUSTIBLE(m, f1, e1, l1) ∧ 
    COMBUSTIBLE(m, f2, e2, l2) ∧ 
    (e1 = 'E1') ∧ 
    (e2 = 'E2') ∧ 
    (e1 ≠ e2)
)}
```
