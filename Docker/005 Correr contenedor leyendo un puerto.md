# Correr contener leyendo un puerto en mi maquina

Tipos: Clase

`**docker run -d --name [alias] -p <mipuerto>:<puertoContenedor> [nombre del contenedor]` ⇒ Corre un contenedor leyendo un puerto en mi maquina**

### Ejemplo

`**docker run -d --name proxy -p 8080:80 nginx**` (corro un nginx y expongo el puerto 80 del contenedor en el puerto 8080 de mi máquina)

### Observar los registros del contenedor

`docker logs [alias]` ⇒ Para ver los registros presentes en la ejecución

`docker logs -f [alias]` ⇒ Los muestra activo en la terminal

`**docker logs --tail 10 -f [alias]` ⇒** Hace el mismo proceso que arriba pero las ultimos 10 procesos

**Tambien se puede seguir:** 

`**docker logs --follow [alias]**`