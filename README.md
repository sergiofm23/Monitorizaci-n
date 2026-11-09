# Monitorización

## 1. Procesos y CPU

### `ps`
* **Nombre y finalidad:** `ps` (Process Status). Muestra una instantánea de los procesos que se están ejecutando en el sistema en un momento determinado.
* **Sintaxis y opciones:**
  * Sintaxis: `ps [opciones]`
  * Opciones principales:
    * `aux`: Muestra todos los procesos de todos los usuarios en formato detallado.
    * `-ef`: Muestra una lista completa de procesos con formato de jerarquía (PID y PPID).
* **Captura de pantalla:**
  ![Comando ps](capturas/ps.png)
* **Interpretación:** En la pantalla se observa la lista de procesos activos junto a su PID (Process ID), el porcentaje de CPU y memoria que consumen, el usuario que los ejecuta y el comando correspondiente. Permite a un administrador detectar qué procesos se están ejecutando y si hay alguno consumiendo recursos indebidos.

---

### `top`
* **Nombre y finalidad:** `top` (Table of Processes). Muestra una vista dinámica y en tiempo real de los procesos del sistema, la carga global de la CPU y la memoria.
* **Sintaxis y opciones:**
  * Sintaxis: `top [opciones]`
  * Opciones principales:
    * `-u [usuario]`: Filtra y muestra únicamente los procesos pertenecientes al usuario especificado.
    * `-d [segundos]`: Define el intervalo de refresco de la pantalla (por ejemplo, `top -d 2`).
* **Captura de pantalla:**
  ![Comando top](capturas/top.png)
* **Interpretación:** La parte superior muestra la carga del sistema (*load average*), el porcentaje de uso de CPU (usuario, sistema, inactivo) y el uso general de RAM y Swap. La parte inferior detalla los procesos ordenados por consumo de CPU. Es clave para diagnosticar rápidamente sobrecargas en el servidor en tiempo real.

---

### `htop`
* **Nombre y finalidad:** `htop` es una herramienta interactiva de monitorización de procesos, basada en texto, que ofrece una visualización más intuitiva y coloreada que `top`.
* **Sintaxis y opciones:**
  * Sintaxis: `htop [opciones]`
  * Opciones principales:
    * `-u [usuario]`: Muestra solo los procesos de un usuario específico.
    * `-C`: Inicia la interfaz en modo monocromo (sin colores).
* **Captura de pantalla:**
  ![Comando htop](capturas/htop.png)
* **Interpretación:** Muestra de forma visual (con barras de colores) el uso individual de cada núcleo de la CPU, la memoria RAM y la memoria de intercambio. Permite buscar, filtrar y finalizar (*kill*) procesos fácilmente con accesos directos de teclado.

---

### `atop`
* **Nombre y finalidad:** `atop` (Advanced System & Process Monitor). Monitoriza la actividad de todos los recursos del sistema a nivel global y por proceso de forma acumulativa e histórica.
* **Sintaxis y opciones:**
  * Sintaxis: `atop [opciones]`
  * Opciones principales:
    * `-m`: Enfoca la salida en la información sobre el uso de memoria de los procesos.
    * `-d`: Muestra estadísticas detalladas sobre el uso del disco.
* **Captura de pantalla:**
  ![Comando atop](capturas/atop.png)
* **Interpretación:** A diferencia de `top`, resaltará los recursos saturados (marcándolos en color) y analiza el impacto combinado de CPU, memoria, discos y red. Es útil para identificar exactamente qué recurso está actuando como cuello de botella.

---

## 2. Memoria RAM

### `free`
* **Nombre y finalidad:** Muestra la cantidad total, utilizada y disponible de memoria física (RAM) y memoria de intercambio (swap) en el sistema.
* **Sintaxis y opciones:**
  * Sintaxis: `free [opciones]`
  * Opciones principales:
    * `-h`: Muestra los datos en un formato legible para humanos (KB, MB, GB).
    * `-s [segundos]`: Actualiza la información continuamente según el intervalo especificado (ej. `free -h -s 3`).
* **Captura de pantalla:**
  ![Comando free](capturas/free.png)
* **Interpretación:** Muestra la RAM total, la usada, la libre y la columna **available** (disponible), que refleja la memoria real utilizable para nuevas aplicaciones sin recurrir a la swap. Un administrador la utiliza para comprobar si el servidor se está quedando sin memoria física.

---

## 3. Almacenamiento

### `df`
* **Nombre y finalidad:** `df` (Disk Free). Muestra el espacio ocupado y disponible en cada una de las particiones y sistemas de archivos montados.
* **Sintaxis y opciones:**
  * Sintaxis: `df [opciones]`
  * Opciones principales:
    * `-h`: Muestra el tamaño de las particiones en formato legible (MB, GB).
    * `-T`: Indica el tipo de sistema de archivos de cada partición (ext4, tmpfs, etc.).
* **Captura de pantalla:**
  ![Comando df](capturas/df.png)
* **Interpretación:** Muestra el punto de montaje, la capacidad total, el espacio usado y el porcentaje de ocupación de cada volumen. Permite prevenir que una partición de disco se llene al 100% y bloquee el sistema.

---

### `du`
* **Nombre y finalidad:** `du` (Disk Usage). Estima el espacio en disco que ocupa un archivo o directorio específico junto con sus subdirectorios.
* **Sintaxis y opciones:**
  * Sintaxis: `du [opciones] [directorio]`
  * Opciones principales:
    * `-s`: Muestra únicamente el resumen del tamaño total del directorio indicado, omitiendo el detalle de sus subcarpetas.
    * `-h`: Expresa los tamaños en un formato legible para humanos.
* **Captura de pantalla:**
  ![Comando du](capturas/du.png)
* **Interpretación:** Muestra el espacio exacto que está ocupando una carpeta concreta en el disco. Es vital para localizar qué archivos o directorios específicos están consumiendo demasiado almacenamiento cuando el espacio escasea.

---

### `iostat`
* **Nombre y finalidad:** `iostat` (Input/Output Statistics). Informa sobre la carga de los dispositivos de almacenamiento mediante la monitorización del tiempo de actividad y las tasas de transferencia de lectura/escritura (pertenece al paquete `sysstat`).
* **Sintaxis y opciones:**
  * Sintaxis: `iostat [opciones] [intervalo] [recuento]`
  * Opciones principales:
    * `-d`: Muestra únicamente las estadísticas de los dispositivos de almacenamiento (discos).
    * `-x`: Muestra estadísticas extendidas de entrada/salida (como tiempo de espera y porcentaje de utilización del dispositivo).
* **Captura de pantalla:**
  ![Comando iostat](capturas/iostat.png)
* **Interpretación:** Ofrece métricas como operaciones de lectura/escritura por segundo (tps), kilobytes leídos/escritos por segundo (kB_read/s, kB_wrtn/s) y el porcentaje de ocupación del disco (`%util`). Ayuda a detectar si el disco duro es el responsable del rendimiento lento del servidor.

---

## 4. Tráfico de red

### `tcpdump`
* **Nombre y finalidad:** Analizador de paquetes en línea de comandos que captura y muestra el tráfico de red TCP/IP que pasa por las interfaces del sistema.
* **Sintaxis y opciones:**
  * Sintaxis: `sudo tcpdump [opciones]`
  * Opciones principales:
    * `-i [interfaz]`: Especifica la interfaz de red a escuchar (ej. `tcpdump -i eth0` o `tcpdump -i lo`).
    * `-c [número]`: Captura únicamente el número exacto de paquetes indicado y se detiene.
* **Captura de pantalla:**
  ![Comando tcpdump](capturas/tcpdump.png)
* **Interpretación:** Muestra el origen, el destino, el protocolo y la carga útil de las tramas enviadas y recibidas. Sirve para auditar el tráfico, solucionar problemas de conectividad o inspeccionar anomalías de red.

---

## 5. Puertos y conexiones

### `ss`
* **Nombre y finalidad:** `ss` (Socket Statistics). Herramienta ligera que inspecciona y muestra las conexiones de red y puertos abiertos en el equipo local (reemplazo moderno de `netstat`).
* **Sintaxis y opciones:**
  * Sintaxis: `ss [opciones]`
  * Opciones principales:
    * `-tulpn`: Muestra sockets TCP (`-t`), UDP (`-u`), en modo escucha (`-l`), mostrando números de puerto (`-p`) y el proceso asociado (`-n`).
    * `-a`: Muestra todas las conexiones (tanto en escucha como establecidas).
* **Captura de pantalla:**
  ![Comando ss](capturas/ss.png)
* **Interpretación:** Lista los servicios del sistema que están escuchando en puertos concretos y las conexiones activas con otros equipos. Es primordial para comprobar qué servicios están activos y si hay servicios no autorizados expuestos.

---

### `nmap`
* **Nombre y finalidad:** `nmap` (Network Mapper). Herramienta de escaneo de puertos y auditoría de seguridad utilizada para descubrir hosts, puertos abiertos y servicios expuestos en la red.
* **Sintaxis y opciones:**
  * Sintaxis: `nmap [opciones] [IP/Host]`
  * Opciones principales:
    * `-p [puertos]`: Escanea solo los puertos indicados (ej. `nmap -p 80,443 127.0.0.1`).
    * `-sV`: Detecta la versión de los servicios que se ejecutan en los puertos abiertos.
* **Captura de pantalla:**
  ![Comando nmap](capturas/nmap.png)
* **Interpretación:** Indica el estado de los puertos (abierto, cerrado o filtrado por firewall) y el servicio asociado. Permite evaluar la seguridad de un servidor detectando vulnerabilidades o servicios accesibles desde el exterior.

---

## 6. Análisis de resultados

### 1. ¿Cómo comprobarías la cantidad de memoria RAM disponible?
Se comprueba mediante el comando **`free -h`**. En la salida obtenida, se debe consultar el valor de la columna **`available`**, el cual representa la cantidad de memoria que está disponible inmediatamente para ser asignada a nuevos procesos sin necesidad de utilizar memoria de intercambio (*swap*).

### 2. ¿Qué diferencia existe entre `df` y `du`?
* **`df` (Disk Free):** Trabaja a nivel de **sistema de archivos y particiones**, mostrando el espacio total, usado y disponible en cada punto de montaje.
* **`du` (Disk Usage):** Trabaja a nivel de **archivos y directorios**, calculando el espacio acumulado que ocupa una carpeta específica y sus ficheros contenidos.

### 3. ¿Qué diferencias existen entre `ss` y `nmap`?
* **`ss`:** Es una herramienta de consulta **interna** del kernel del propio sistema operativo. Muestra qué sockets, conexiones y puertos están activos en la máquina local.
* **`nmap`:** Es un escáner de red **externo** (o interno) que envía paquetes de prueba a través de la red para averiguar qué puertos se encuentran abiertos en una dirección IP determinada.

### 4. ¿Cómo comprobarías si un servidor tiene abierto el puerto 80?
* **Localmente:** Ejecutando `ss -tulpn | grep :80` para comprobar si hay algún servicio escuchando en dicho puerto.
* **A través de la red:** Ejecutando `nmap -p 80 <IP_del_servidor>` desde otro equipo para comprobar si el puerto responde a peticiones externas.

### 5. ¿Qué herramienta utilizarías para detectar un posible cuello de botella en el disco?
Se utilizaría **`iostat -x`** (o herramientas interactivas como **`iotop`**), prestando especial atención a la columna `%util` (porcentaje de utilización del dispositivo) y a los tiempos de espera del disco (`await`).

### 6. ¿Por qué es importante monitorizar los recursos de un servidor?
La monitorización constante permite:
* Garantizar el correcto funcionamiento y la disponibilidad continua de los servicios.
* Detectar fallos, cuellos de botella o intrusiones de seguridad antes de que causen una caida del sistema.
* Planificar ampliaciones de hardware (memoria, almacenamiento, CPU) con base en patrones reales de consumo.
