## CatalogoCloud  
# Misiones de Auditoría  

**Misión 1: Mapeo de Seguridad (Navegación Absoluta/Relativa)**  
El equipo de redes necesita auditar el firewall de Francia. Extrae una lista con todos los puertos de los servicios que se están ejecutando exclusivamente en el centro de datos de la ubicación "Paris".  

Primero comenzamos con la ruta con la que se llega a la información que queremos, en este caso, queremos extraer una lista de puertos, asique la ruta será en principio:  

` /catalogo_cloud/centro_datos/servidor/software/servicios/servicio/@puerto

Y ahora aplicamos las correspondientes restricciones, que son que se estén ejecutando (estado="activo"), y que el centro de datos esté en París (ubicacion="Paris"):

` /catalogo_cloud/centro_datos[@ubicacion="Paris"]/servidor[@estado="activo"]/software/servicios/servicio/@puerto

Como queremos que el resultado de esta búsqueda sea un texto ponemos un string, por lo que el resultado final sería así:

` /catalogo_cloud/centro_datos[@ubicacion="Paris"]/servidor[@estado="activo"]/software/servicios/servicio/@puerto /string()  


**Misión 2: Auditoría de Mantenimiento (Filtrado por Valores)**  
Debemos planificar una ventana de actualización para sistemas operativos antiguos. Escribe una consulta que devuelva la versión del sistema operativo (SO) del servidor cuyo identificador (id) sea exactamente srv-db-01.  

Primero comenzamos con la ruta con la que se llega a la información que queremos, en este caso, queremos extraer la versión del sistema operativo de un servidor, asique la ruta será en principio:

` /catalogo_cloud/centro_datos/servidor/software/so/@version

Y ahora aplicamos la correspondiente restricción, que es que su id se axáctamente svr-db-01 (id="srv-db-01"):

` /catalogo_cloud/centro_datos/servidor[@id="srv-db-01"]/software/so/@version

Como queremos que el resultado de esta búsqueda sea un texto ponemos un string, por lo que el resultado final sería así:

` /catalogo_cloud/centro_datos/servidor[@id="srv-db-01"]/software/so/@version /string()  


**Misión 3: Inventario de Alta Capacidad (Predicados Matemáticos)**  
El departamento de compras quiere saber qué infraestructura pesada tenemos. Recupera los nodos completos de los discos que tengan una capacidad igual o superior a 8 TB (independientemente de si son HDD o NVMe).  

Primero comenzamos con la ruta con la que se llega a la información que queremos, en este caso, los nodos completos de los discos duros, asique la ruta será en principio:

` /catalogo_cloud/centro_datos/servidor/hardware/discos/disco

Y ahora aplicamos la correspondiente restricción, que es que la capacidad de lo discos sea igual o superior a 8 TB, dando igual si son HBB o NVMe:

` /catalogo_cloud/centro_datos/servidor/hardware/discos/disco[@capacidad_tb>=8]

Como queremos que el resultado de esta búsqueda sea el contenido de los nodos completo con todos sus elementos, no vamos a poner string, por lo que el resultado final sería así:

` /catalogo_cloud/centro_datos/servidor/hardware/discos/disco[@capacidad_tb>=8]  


**Misión 4: Eficiencia Energética (Uso de Funciones o Índices)**  
Para apagar temporalmente el hardware menos crítico, necesitamos identificar el primer servidor (nodo completo) que aparece registrado dentro de toda la infraestructura y que se encuentra actualmente en estado "apagado".

Primero comenzamos con la ruta con la que se llega a la información que queremos, en este caso, queremos extraer el nodo completo del servidor, asique la ruta será en principio:

` /catalogo_cloud/centro_datos/servidor

Y ahora aplicamos la correspondiente restricción, que es que sea el primer servidor que pararezca como apagado, por lo que no solo pondremos "estado="apagado"" sino que también indicaremos que tiene que ser el primer servidor que aparezca utilizando [1]:

` /catalogo_cloud/centro_datos/servidor[@estado="apagado"][1]

Como queremos que el resultado de esta búsqueda sea el contenido de los nodos completo con todos sus elementos, no vamos a poner string, por lo que el resultado final sería así:

` /catalogo_cloud/centro_datos/servidor[@estado="apagado"][1]  


**Misión 5: Desafío del Auditor Senior (Navegación Inversa / Existencia)**  
Necesitamos saber qué arquitectura de CPU se está utilizando en las máquinas de inteligencia artificial. Extrae el atributo arquitectura de la CPU que pertenezca al servidor que tiene instalada una GPU.  

Primero comenzamos con la ruta con la que se llega a la información que queremos, en este caso, queremos extraer la arquitectura de la CPU del servidor que tiene GPU. Para ello, primero buscaremos los los centros de datos con GPU, es decir:

` /catalogo_cloud/centro_datos/servidor/hardware/gpu

Y como queremos llegar a la CPU, subimos al nodo padre, estando en "hardware" de servidores con GPU. Apartir de ahí buscamos la arquitectura de la CPU, acotando la búsqueda a la arquetectura de la CPU de los servidores con GPU. Por lo que el código queda así:

` /catalogo_cloud/centro_datos/servidor/hardware/gpu/../cpu/@arquitectura

Como queremos que el resultado de esta búsqueda sea un texto ponemos un string, por lo que el resultado final sería así:

`/catalogo_cloud/centro_datos/servidor/hardware/gpu/../cpu/@arquitectura /string()  
