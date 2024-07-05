# Control 3

# Año 2021-2022

``` 
library(igraph)
plot(Ga, layout=Z, vertex.label=abrev)
```

![[Captura de pantalla 2024-04-11 a las 13.21.44.png]]

``` 
da # Obtención del peso de las aristas
```

![[Captura de pantalla 2024-04-11 a las 13.22.53.png]]

```
Ga
```

![[Captura de pantalla 2024-04-11 a las 13.25.50.png]]

## (a) La red de comunicación más corta

### Búsqueda de árbol recubridor de peso mínimo

```
Tm <- mst(Ga, da)
sum(E(Tm)$weight) # Se suman los pesos para calcular el total
```

![[Captura de pantalla 2024-04-11 a las 13.29.47.png]]

### Representación del árbol

```
plot(Tm, layout=Z, vertex.label=abrev, add=TRUE, edge.color="cyan4", edge.width=3, edge.label=E(Tm)$weight)
```

![[Captura de pantalla 2024-04-11 a las 13.32.17.png]]

## (b) Ruta entre A Coruña y Barcelona

### Ruta de distancia mínima

```
Gb
```

![[Captura de pantalla 2024-04-11 a las 13.44.45.png]]

### Comprobamos que tiene el atributo que necesitamos

```
E(Gb)$weight

sp <- shortest_paths(Gb, 1, output = "epath")
```

De todas las opciones elegimos la opción 3 ya que es la que corresponde con barcelona.

![[Captura de pantalla 2024-04-11 a las 13.47.22.png]]

> Interpretación del output
> **Trayectos:**
> 1-7 A coruña - Madrid
> 7-15 Madrid - Zaragoza
> 15- 3 Zaragoza - Barcelona
> {style="note"}

```
ru <- sp$epath[[3]]
sum(E(Gb)[ru]$weight) # El resultado es 1230 km
```

```
Db <- distances(Gb)
Db[1,3] # El resultado es 1230 km
```

## (c) Operación salida

### Red de transporte

```
Gc
````

![[Captura de pantalla 2024-04-11 a las 14.01.57.png]]

### Añadimos los vértices necesarios

```
H <- add_vertices(Gc, 10)
```

![[Captura de pantalla 2024-04-11 a las 14.04.59.png]]

### Añadimos las aristas necesarias

```
H <- add_edges(H, rbind(c(1,1,4,10,3,15,3,3,15,12,2,9,6,8,11,16,17,18,19,20,21,22,23,24,24,24,24,24,24),
                        c(16,17,17,17,18,18,19,20,20,20,21,21,22,22,23,25,25,25,25,25,25,25,25,3,7,8,11,12,15)))
```

![[Captura de pantalla 2024-04-11 a las 14.17.40.png]]

### Cálculo de las capacidades

```
cap <- c(rep(11,76),rep(9,15),rep(100,14))
```

![[Captura de pantalla 2024-04-11 a las 14.22.00.png]]

### Flujo máximo

```
fm <- max_flow(H,24,25,cap)
```

![[Captura de pantalla 2024-04-11 a las 14.24.10.png]]

El flujo máximo es 135

