# Ciclo de vida de un contenedor

Cada vez que un contenedor se ejecuta, en realidad lo que ejecuta es un proceso del sistema operativo. Este proceso se le conoce como **Main process**.

### **Main process**

Determina la vida del contenedor, un contenedor corre siempre y cuando su proceso principal este corriendo.

### **Sub process**

Un contenedor puede tener o lanzar procesos alternos al main process, si estos fallan el contenedor va a seguir encendido a menos que falle el main.

- Batch como Main process
- Agujero negro (/dev/null) como Main process

### Ejecutar un main proces

**`docker run --name [alias] -d [nombre-general] tail -f[proceso]`**

Lo que hace esta linea es correr un contenedor x con alias en un proceso que ejecute

**Ejemplo: `docker run --name notienenombre -d ubuntu tail -f /dev/null`**

### Ejecutar un sub proceso

Te puedes conectar al contenedor y hacer cosas dentro del él con el siguiente comando (sub proceso)

**`docker exec -it [alias] bash`** ⇒ Ejecutas un subproceso

**Ejemplo:**  **`docker exec -it notienenombre bash`**

### Kill main process

Se puede matar un Main process desde afuera del contenedor, esto se logra conociendo el id del proceso principal del contenedor que se tiene en la maquina. Para saberlo se ejecuta los siguientes comandos

**`dockerinspect --format '{{.State.Pid}}' [alias]`

Para matar el proceso principal del contenedor desde afuera se ejecuta el siguiente comando (solo funciona en linux)

**`sudo kill -9 [id-process]`
