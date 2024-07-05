# TSP

# Algoritmos 2-opt y 3-opt en R

```
library(igraph)
library(gor) # Rutinas alternativas al paquete TSP
set.seed(1) # Generamos una colección de 25 ciudades
n <- 25
z <- cbind(runif(n,min=1,max=10),runif(n,min=1,max=10))
d <- compute_distance_matrix(z) # Matriz de distancias

plot(z) #**Imagen 1**

b <- build_tour_2tree(d, n) # Ciclo a mejorar:
b$distance # Distancia 48.639
b2 <- improve_tour_2opt(d, n, b$tour) # Mejora 2-opt
b3 <- improve_tour_3opt(d, n, b$tour) # Mejora 3-opt
b2$distance # Distancia 37.351
b3$distance # Distancia 35.221
plot_tour(z,b); #**Imagen 2**
plot_tour(z,b2); plot_tour(z,b3) #**Imagen 3**
```


![Imagen](Captura de pantalla 2024-04-24 a las 11.41.31.png){ width="450" }

![Imagen](Captura de pantalla 2024-04-24 a las 11.46.38.png){ width="450" }
> Como el resultado es muy malo, se calcula b2 y b3 y se hace el plot de los 3 a la vez. Al realizar esto reducimos la distancia de 48,63 a 35,22.

![Imagen](Captura de pantalla 2024-04-24 a las 11.40.23.png){ width="450" }