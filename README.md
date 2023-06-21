# BDD-Consultas
ejemplos Algebra relacional, Calculo relacional y SQL

## 1. Flota de vehículos

```plaintext
VEHICULO(M,T,C)
* significado: El vehiculo con matricula M es de tipo T y consume combustible de la clase C
* CP: (M)
```

```plaintext
COMBUSTIBLE(M,F,E,L)
* significado: El vehiculo con matricula M es de tipo T y consume combustible de la clase C
* CP: (M,F,E) CA:(M)
```

```plaintext
VEHICULO(E,CAD,F,C,P)
* significado: La estación E pertenece a la cadena CAD y en la fecha F el precio del litro de combustible de clase C es P
* CP: (E,F,C)
```
