# Control 3

# Año 2021-2022

``` 
library(igraph)
plot(Ga, layout=Z, vertex.label=abrev)
```

![Imagen](Captura de pantalla 2024-04-11 a las 13.21.44.png){ width="450" }

``` 
da # Obtención del peso de las aristas
```

![Imagen](Captura de pantalla 2024-04-11 a las 13.22.53.png){ width="450" }

```
Ga
```

![Imagen](Captura de pantalla 2024-04-11 a las 13.25.50.png){ width="450" }

## (a) La red de comunicación más corta

### Búsqueda de árbol recubridor de peso mínimo

```
Tm <- mst(Ga, da)
sum(E(Tm)$weight) # Se suman los pesos para calcular el total
```

![Imagen](Captura de pantalla 2024-04-11 a las 13.29.47.png){ width="450" }

### Representación del árbol

```
plot(Tm, layout=Z, vertex.label=abrev, add=TRUE, edge.color="cyan4", edge.width=3, edge.label=E(Tm)$weight)
```

![Imagen](Captura de pantalla 2024-04-11 a las 13.32.17.png){ width="450" }

## (b) Ruta entre A Coruña y Barcelona

### Ruta de distancia mínima

```
Gb
```

![Imagen](Captura de pantalla 2024-04-11 a las 13.44.45.png){ width="450" }

### Comprobamos que tiene el atributo que necesitamos

```
E(Gb)$weight

sp <- shortest_paths(Gb, 1, output = "epath")
```

De todas las opciones elegimos la opción 3 ya que es la que corresponde con barcelona.

![Imagen](Captura de pantalla 2024-04-11 a las 13.47.22.png){ width="450" }

> Interpretación del output.
> **Trayectos:**
> (1-7) A coruña - Madrid
> (7-15) Madrid - Zaragoza
> (15- 3) Zaragoza - Barcelona
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

![Imagen](Captura de pantalla 2024-04-11 a las 13.47.22.png){ width="450" }

### Añadimos los vértices necesarios

```
H <- add_vertices(Gc, 10)
```

![Imagen](Captura de pantalla 2024-04-11 a las 14.04.59.png){ width="450" }

### Añadimos las aristas necesarias

```
H <- add_edges(H, rbind(c(1,1,4,10,3,15,3,3,15,12,2,9,6,8,11,16,17,18,19,20,21,22,23,24,24,24,24,24,24),
                        c(16,17,17,17,18,18,19,20,20,20,21,21,22,22,23,25,25,25,25,25,25,25,25,3,7,8,11,12,15)))
```

![Imagen](Captura de pantalla 2024-04-11 a las 14.17.40.png){ width="450" }

### Cálculo de las capacidades

```
cap <- c(rep(11,76),rep(9,15),rep(100,14))
```

![Imagen](Captura de pantalla 2024-04-11 a las 14.22.00.png){ width="450" }

### Flujo máximo

```
fm <- max_flow(H,24,25,cap)
```

![Imagen](Captura de pantalla 2024-04-11 a las 14.24.10.png){ width="450" }

El flujo máximo es 135

