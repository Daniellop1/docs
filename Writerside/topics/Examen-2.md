# Examen 2

## Ejercicio 1

![Imagen](Captura de pantalla 2024-05-08 a las 11.22.45.png){ width="450" }

**A)**
En el ejercicio 1 el grafo no será dirigido mientras que para el ejercicio 2 si lo será

```
library(gor)
library(igraph)

G <- make_graph(16, directed=FALSE)

G <- add_edges(G,
  rbind(c(1,1,1,2,2,2,3,3,4,4,4,5,5,6,6,7,7,8,8,9,9,10,10,11,11,12,12,13,14,15),
        c(2,3,4,5,6,7,6,7,6,7,8,9,10,9,11,10,12,11,12,13,14,13,14,14,15,14,15,16,16,16))
)

cap <- c(5,4,6,6,4,6,4,7,6,6,5,3,5,5,3,7,1,4,4,5,4,5,5,4,6,8,3,5,5,6)

G <- set_edge_attr(G, "weight", value = cap) 
G # Tiene que aparecer en el output: + attr: peso (e/n)

Tm <- mst(G, cap)
Tm # Sale el resultado para dibujarlo no hace falta hacer plot
plot(Tm,layout=z,add=TRUE) # add=TRUE sirve para que se muestre encima del otro grafo
sum(E(Tm)$weight)
```

**B)**
```
sp <- shortest_paths(G,1,output="epath")
sp
dG <- distances(G) # Matriz de distancias
dG
```
Los números más altos de la matriz de distancias son la solución, en este caso: 13 y 16.

## Ejercicio 2

**A)**
```
G <- make_graph(16, directed=TRUE)

G <- add_edges(G,
  rbind(c(1,1,1,2,2,2,3,3,4,4,4,5,5,6,6,7,7,8,8,9,9,10,10,11,11,12,12,13,14,15),
        c(2,3,4,5,6,7,6,7,6,7,8,9,10,9,11,10,12,11,12,13,14,13,14,14,15,14,15,16,16,16))
)

cap <- c(5,4,6,6,4,6,4,7,6,6,5,3,5,5,3,7,1,4,4,5,4,5,5,4,6,8,3,5,5,6)

fm <- max_flow(G,1,16,cap)
fm

plot(G,layout=z,asp=0.5,edge.label=paste(fm$flow, "/", cap))
K <- subgraph.edges(G,fm$cut,delete.vertices=FALSE)
plot(K,layout=z,add=TRUE,edge.color="green3")
```

**B)**
Vértices: 5 y 9.

## Ejercicio 3

**A)**

```
t1 <- build_tour_nn_best(D,n)
plot_tour(Z, t1)
```

![Imagen](Captura de pantalla 2024-05-08 a las 11.01.22.png){ width="450" }

**B)**

```
t1
```

![Imagen](Captura de pantalla 2024-05-08 a las 11.03.05.png){ width="450" }

```
t2 <- improve_tour_2opt(D,n,t1$tour)
plot_tour(Z, t2)
```

**C)**

```
t3 <- search_tour_genetic(D, n, Npop=5, Ngen=10)
plot_tour(Z,t3)
```

> Cuánto más grande el grafo mejor hacer menos búsquedas porque si no tardará mucho

![Imagen](Captura de pantalla 2024-05-08 a las 11.05.37.png){ width="450" }

![Imagen](Captura de pantalla 2024-05-08 a las 11.07.39.png){ width="450" }

**D)**

```
K <- compute_lower_bound_HK(D,n,U=36.9,it=100,tsmall=1e-6)
K
t3$distance/K # Elegimos t3 porque es el mejor
```

> Interpretación del intput
> **it** = Número de iteraciones; 
> **tsmall** = criterio de parada del algoritmo

El resultado se tiene multiplicar por 100 lo que va detrás de la coma. En este caso el resultado es 1.006 por lo que da 0.66% por lo que podemos decir que está muy bien.
