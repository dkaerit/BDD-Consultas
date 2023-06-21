a) Camiones de gasolina que han puesto más de 100 litros en algún repostaje:

```lua
{ v | ∃m, t, c, f, e, l (             -- Conjunto de vehículos v donde existe un m, t, c, f, e, l
    VEHICULO(v, m, t, c) ∧            -- Vehículo v con matrícula m, tipo t y consumo de combustible c
    COMBUSTIBLE(m, f, e, l) ∧         -- Vehículo con matrícula m que repostó en la estación e con cantidad l de combustible
    (t = 'Camion') ∧                  -- El tipo de vehículo es 'Camion'
    (c = 'Gasolina') ∧                -- El consumo de combustible es 'Gasolina'
    (l > 100)                         -- La cantidad de combustible es mayor a 100
)}
```

b) Vehículos que han puesto combustible en la estación E1 pero no en la E2:

```lua
{ v | ∃m, f1, f2, e1, e2, l1, l2 (    -- Conjunto de vehículos v donde existe un m, f1, f2, e1, e2, l1, l2
    VEHICULO(v, m, _, _) ∧            -- Vehículo v con matrícula m
    COMBUSTIBLE(m, f1, e1, l1) ∧      -- Vehículo con matrícula m que repostó en la estación e1 con cantidad l1 de combustible
    COMBUSTIBLE(m, f2, e2, l2) ∧      -- Vehículo con matrícula m que repostó en la estación e2 con cantidad l2 de combustible
    (e1 = 'E1') ∧                     -- La estación e1 es 'E1'
    (e2 = 'E2') ∧                     -- La estación e2 es 'E2'
    (e1 ≠ e2)                         -- e1 no es igual a e2
)}
```

c) Vehículos que siempre han repostado el mismo número de litros:

```lua
{ v | ∃m, f1, f2, e1, e2, l1, l2 (    -- Conjunto de vehículos v donde existe un m, f1, f2, e1, e2, l1, l2
    VEHICULO(v, m, _, _) ∧            -- Vehículo v con matrícula m
    COMBUSTIBLE(m, f1, e1, l1) ∧      -- Vehículo con matrícula m que repostó en la estación e1 con cantidad l1 de combustible
    COMBUSTIBLE(m, f2, e2, l2) ∧      -- Vehículo con matrícula m que repostó en la estación e2 con cantidad l2 de combustible
    (l1 = l2)                         -- La cantidad de combustible l1 es igual a l2
)}
```

d) Estaciones en las que han repostado vehículos de todos los tipos:

```lua
{ e | ∃m, t, c (                      -- Conjunto de estaciones e donde existe un m, t, c
    VEHICULO(m, t, c) ∧               -- Vehículo con matrícula m de tipo t y consumo de combustible c
    COMBUSTIBLE(m, _, e, _) ∧ ∀x      -- Vehículo con matrícula m que repostó en la estación e, y para todo tipo x de vehículo
        (VEHICULO(m, x, _) ⇒ ∃y      -- si el vehículo m es de tipo x, entonces existe una estación 'y' 
        (COMBUSTIBLE(m, _, e, _) ∧    -- en la que repostó el vehículo m
        x = y))                       -- y el tipo de vehículo es igual a x
)}
```

```lua
{ e | ∃m, t, c (                               -- El vehículo con matrícula 'm' es de tipo 't' y tiene un consumo de combustible 'c'
    VEHICULO(m, t, c) ∧                        -- El vehículo con matrícula 'm' ha repostado en la estación 'e'
    COMBUSTIBLE(m, _, e, _) ∧ ∀x               -- Para todo tipo 'x' diferente de 't', si el vehículo 'm' es de tipo 'x'
        ((VEHICULO(m, x, _) ∧ x ≠ t) ∨ ∃y      -- Entonces existe una estación 'y     
            (COMBUSTIBLE(m, _, e, _) ∧         -- en la que el vehículo 'm'
            x = y))                            -- ha repostado y es igual a 'x'
)}
```

e) Estaciones en las que han repostado todos los vehículos:

```lua
{ e | ∀m, t, c (∃x                     -- Conjunto de estaciones e para todo m, t, c
    (VEHICULO(m, t, c) ⇒ ∀y       -- Existe un tipo x tal que, si el vehículo m es de tipo x,
    (COMBUSTIBLE(m, _, y, _) ⇒    -- entonces para toda estación y en la que repostó el vehículo m,
    x = y))                        -- el tipo de vehículo es igual a x
)}
```

```lua
{ e | ∀m, t, c (∃x                    -- Para cada elemento 'e', para todo 'm', 't' y 'c' ...
    (¬(VEHICULO(m, t, c)) ∨ ∀y        -- Si el vehículo con matrícula 'm' no es de tipo 't' y tiene un consumo de combustible 'c',
        (¬(COMBUSTIBLE(m, _, y, _)) ∨ -- o bien, si el vehículo con matrícula 'm' no ha repostado en la estación 'y',
        x = y))                       -- entonces 'x' es igual a 'y'.
)}
```
