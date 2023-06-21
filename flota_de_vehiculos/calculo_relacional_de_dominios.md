a) Camiones de gasolina que han puesto más de 100 litros en algún repostaje:

```sql
{ v | ∃ m,t,c,f,e,l 
(VEHICULO(v,m,t,c) ∧ 
COMBUSTIBLE(m,f,e,l) ∧ 
(t='Camion') ∧ 
(c='Gasolina' ∧ 
(l>100) }
```
