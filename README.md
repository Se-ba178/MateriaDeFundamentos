# Guía de estudio: Arquitectura de un Sistema Operativo

> Material de repaso para una prueba teórica.
> Las preguntas del final son de práctica; no son preguntas confirmadas del examen.

## 1. ¿Qué es un sistema operativo?

Un sistema operativo (SO) es el software que administra los recursos del hardware y proporciona servicios para que las aplicaciones puedan ejecutarse.

Actúa como intermediario entre las aplicaciones y el hardware.

### Sus dos funciones principales

1. **Administrar recursos:** distribuir CPU, memoria, almacenamiento y dispositivos de entrada/salida.
2. **Proporcionar abstracciones:** ocultar la complejidad del hardware mediante conceptos fáciles de utilizar, como archivos, procesos y memoria virtual.

### ¿Qué es una abstracción?

Es una representación sencilla que permite utilizar un recurso sin conocer todos sus detalles físicos.

**Ejemplo:** una aplicación trabaja con un archivo sin tener que controlar físicamente el disco.

### Otras responsabilidades del SO

- Registrar qué programa utiliza cada recurso.
- Atender solicitudes de recursos.
- Controlar y contabilizar su utilización.
- Resolver conflictos entre programas y usuarios.
- Proteger los recursos del sistema.

### ¿Quiénes son sus clientes directos?

Los programas de aplicación, que utilizan sus servicios y abstracciones.

### ¿Qué ocurriría sin un SO?

Cada aplicación tendría que:

- Conocer el funcionamiento de los dispositivos.
- Administrar la memoria.
- Controlar el procesador.
- Implementar su sistema de archivos.
- Resolver la seguridad y la protección.
- Gestionar la entrada y salida.

**Respuesta para memorizar:**

> El sistema operativo administra los recursos del hardware y proporciona servicios y abstracciones para facilitar la ejecución de aplicaciones.

## 2. Historia y evolución

Los sistemas operativos evolucionan junto con el hardware y las necesidades de los usuarios.

| Etapa del material | Característica |
|---|---|
| 1940-1950 | Procesamiento manual. |
| 1950-1960 | Procesamiento por lotes. |
| 1960-1970 | Multiprogramación. |
| 1970-1990 | Tiempo compartido. |
| 1980-2000 | Computadoras personales. |
| 2000 en adelante | Multicore, móviles y virtualización. |
| Etapa actual presentada | Cloud, contenedores e IoT. |

### Procesamiento por lotes

Los trabajos se agrupan y ejecutan sin interacción directa del usuario.

**Problema:** la CPU puede quedar ociosa mientras un trabajo espera una operación de entrada/salida.

### Multiprogramación

Varios programas permanecen disponibles en memoria.

Cuando uno espera una operación de E/S, la CPU puede ejecutar otro.

**Objetivo:** mejorar la utilización del procesador.

### Tiempo compartido

El tiempo del procesador se distribuye entre tareas o usuarios para permitir una interacción frecuente con el sistema.

### Conceptos que no debes confundir

- **Multiprogramación:** mantiene varios programas disponibles para aprovechar la CPU.
- **Multitarea:** permite que varias tareas progresen concurrentemente.
- **Concurrencia:** varias tareas progresan durante un mismo intervalo, aunque se alternen.
- **Paralelismo:** varias tareas se ejecutan simultáneamente, por ejemplo, en diferentes núcleos.

## 3. Tipos de sistemas operativos

### Según la administración de tareas

- **Monotarea:** permite ejecutar una tarea a la vez.
- **Multitarea:** permite que varias tareas progresen concurrentemente.

### Según la administración de usuarios

- **Monousuario:** orientado a un usuario a la vez.
- **Multiusuario:** administra recursos y permisos para múltiples usuarios.

**Importante:** multitarea y multiusuario son clasificaciones diferentes. Un sistema puede tener ambas características.

### Según su uso

| Tipo | Uso |
|---|---|
| Escritorio | Computadoras personales y estaciones de trabajo. |
| Servidor | Servicios web y bases de datos. |
| Móvil | Teléfonos y tabletas. |
| Embebido | Dispositivos con funciones específicas, como electrodomésticos. |
| Tiempo real | Sistemas que requieren respuestas dentro de plazos definidos. |
| IoT/Edge | Sensores y dispositivos inteligentes. |

**Tiempo real:** no significa solamente “rápido”; importa responder dentro del tiempo requerido.

## 4. Hardware y funcionamiento general

Un sistema de computación de propósito general incluye una CPU y controladores de dispositivos conectados mediante un bus.

### Relación entre SO y hardware

El SO está estrechamente relacionado con el hardware porque debe controlar y administrar sus recursos.

### Programa de arranque

Es el programa que inicia el equipo y permite cargar el sistema operativo.

### Funcionamiento general

1. Se inicia el equipo.
2. Se carga el sistema operativo.
3. Se ejecutan procesos.
4. El sistema atiende sucesos, solicitudes e interrupciones.
5. Si no hay trabajo pendiente, espera a que ocurra un suceso.

## 5. Procesador o CPU

La CPU obtiene instrucciones de la memoria y las ejecuta.

### Ciclo básico

1. **Obtener:** buscar la instrucción en memoria.
2. **Decodificar:** identificar la operación y sus operandos.
3. **Ejecutar:** realizar la operación.
4. Repetir con la siguiente instrucción.

**Para memorizar:** obtener → decodificar → ejecutar.

### Registros

Son pequeñas ubicaciones de almacenamiento dentro del procesador.

#### Registros generales

Guardan variables, operandos y resultados temporales.

#### Registros especiales

| Registro | Función |
|---|---|
| Contador de programa | Indica la dirección de la siguiente instrucción. |
| Apuntador de pila | Señala la posición de la cima de la pila. |
| Palabra de estado del programa (PSW) | Contiene información del estado del procesador y, en el modelo presentado, del modo de ejecución. |

### Modo usuario y modo kernel

| Modo usuario | Modo kernel |
|---|---|
| Ejecuta normalmente las aplicaciones. | Ejecuta el núcleo del SO. |
| Tiene acceso restringido. | Permite operaciones privilegiadas. |
| No permite controlar libremente todo el hardware. | Permite controlar los recursos del hardware. |

**¿Por qué existen estos modos?**

Para proteger el sistema e impedir que una aplicación realice operaciones privilegiadas sin control.

### Núcleos e hilos

- **Core:** núcleo físico de procesamiento.
- **Multicore:** procesador con varios núcleos; permite paralelismo entre ellos.
- **Hardware thread:** contexto de ejecución que puede mantener el procesador.
- **Software thread:** flujo de ejecución administrado por el SO o el entorno de ejecución.

**Importante:** un hilo de software no es lo mismo que un núcleo físico.

## 6. Interrupciones

Una interrupción es una señal que hace que la CPU desvíe temporalmente su ejecución para atender un suceso.

**Ejemplo:** un dispositivo avisa que terminó una lectura de disco.

### ¿Cómo se atiende una interrupción?

1. Ocurre un suceso.
2. Se genera la interrupción.
3. Se guarda el estado necesario de la ejecución actual.
4. Se identifica la rutina de servicio correspondiente.
5. Se ejecuta la rutina.
6. Se restaura el estado y se continúa la ejecución.

### Vector de interrupciones

Permite localizar las rutinas de servicio que atienden los distintos tipos de interrupción.

### Rutina de servicio

Es el código que atiende una interrupción específica.

### Prioridades

Una interrupción de mayor prioridad puede atenderse mientras se procesa una de menor prioridad, si el sistema lo permite.

### ¿Por qué guardar el estado?

Para poder continuar correctamente el trabajo que estaba ejecutándose.

**Para memorizar:** guardar → atender → restaurar → continuar.

## 7. Memoria

Los programas necesitan tener sus instrucciones y datos disponibles en memoria principal durante la ejecución.

Cada ubicación de memoria tiene una dirección.

### Operaciones básicas

- **Cargar:** transferir información de memoria a un registro de la CPU.
- **Almacenar:** transferir información de un registro de la CPU a memoria.

### Jerarquía de memoria

De los niveles más rápidos hacia los más lentos, según el esquema del material:

1. Registros.
2. Caché.
3. Memoria principal.
4. Disco de estado sólido.
5. Disco magnético.
6. Disco óptico.
7. Cintas magnéticas.

### Regla general

Hacia los niveles superiores:

- Mayor velocidad.
- Menor capacidad.
- Mayor costo por bit.

Hacia los inferiores:

- Menor velocidad.
- Mayor capacidad.
- Menor costo por bit.

### Registros

- Están dentro de la CPU.
- Son muy rápidos.
- Guardan información inmediata para ejecutar instrucciones.

### Memoria caché

Memoria de alta velocidad que almacena copias de instrucciones y datos usados recientemente o con frecuencia.

**Objetivo:** reducir el tiempo medio de acceso a la información.

Se encuentra dentro o muy cerca de la CPU.

### Caché L1

- Es pequeña y muy rápida.
- Normalmente está integrada en cada núcleo.
- **L1I:** almacena instrucciones.
- **L1D:** almacena datos.

**Aclaración:** I significa instrucciones y D significa datos; no izquierda y derecha.

### Caché L2

- Tiene mayor capacidad que L1.
- Puede almacenar instrucciones y datos.
- Puede ser privada de un núcleo o compartida, según la arquitectura.
- Se consulta cuando la información no está en L1, según la organización de la CPU.

### RAM

- Es la memoria principal de trabajo.
- Contiene instrucciones y datos utilizados durante la ejecución.
- Es volátil: pierde su contenido al interrumpirse la energía.
- Tiene capacidad limitada.

### ROM

- Es memoria no volátil.
- Conserva su contenido sin energía.
- La ROM tradicional se programa de forma fija; existen otras tecnologías no volátiles que sí pueden reprogramarse.

### Memoria virtual

Permite que cada proceso trabaje con un espacio de direcciones virtuales.

El SO y el hardware traducen direcciones virtuales a direcciones físicas.

**Importante:** memoria virtual no significa simplemente “usar el disco como RAM”; el concepto central es el espacio de direcciones virtuales y su traducción.

### ¿Por qué se necesita almacenamiento secundario?

Porque la RAM:

- Tiene capacidad limitada.
- Pierde su contenido sin energía.

El almacenamiento secundario conserva programas y datos de forma persistente.

## 8. HDD y SSD

| HDD | SSD |
|---|---|
| Es mecánico. | Utiliza estado sólido. |
| Tiene partes móviles. | No tiene partes móviles. |
| Mayor latencia. | Menor latencia. |
| Se caracteriza por bajo costo por GB. | Se caracteriza por mayor rendimiento. |

**Importante:** SSD es un tipo de dispositivo; NVMe es un protocolo de acceso al almacenamiento que suele utilizar PCIe.

## 9. Dispositivos de entrada/salida

La entrada/salida permite intercambiar información entre el sistema y sus dispositivos.

Ejemplos: teclado, disco, impresora y tarjeta de red.

### Controlador de hardware

Chip o conjunto de chips que controla físicamente un dispositivo.

### Driver

Software que permite al SO manejar un dispositivo específico.

**Diferencia clave:**

- Controlador físico: hardware.
- Driver: software.

### Relación general

Aplicación → sistema operativo → driver → controlador físico y dispositivo.

## 10. Tres formas de realizar E/S

### 10.1. E/S programada o por sondeo

También se llama **polling**.

1. La aplicación solicita una operación.
2. El SO y el driver la inician.
3. La CPU consulta repetidamente el estado del dispositivo.
4. Cuando termina, se continúa.

**Espera ocupada:** la CPU permanece comprobando si el dispositivo terminó.

**Desventaja:** consume tiempo de CPU en esas consultas.

### 10.2. E/S por interrupciones

1. La CPU inicia la operación.
2. El dispositivo realiza el trabajo.
3. La CPU puede atender otras tareas.
4. El dispositivo genera una interrupción al terminar.
5. El SO atiende el resultado.

**Ventaja:** evita consultar continuamente al dispositivo.

### 10.3. DMA

DMA significa **acceso directo a memoria**.

Un controlador transfiere bloques de datos directamente entre un dispositivo y la memoria principal.

### Participación de la CPU en DMA

La CPU configura:

- La operación.
- La dirección de memoria.
- El dispositivo involucrado.
- La cantidad de datos.

Después, el controlador realiza la transferencia y genera una interrupción al finalizar.

### Ventajas del DMA

- Reduce la intervención de la CPU.
- Evita que la CPU mueva individualmente cada dato.
- Es eficiente para transferencias grandes.

**Ejemplo:** transferir un bloque desde un disco a la RAM.

### Comparación

| Método | Característica principal |
|---|---|
| Sondeo | La CPU consulta continuamente. |
| Interrupciones | El dispositivo avisa cuando requiere atención o termina. |
| DMA | Un controlador transfiere bloques directamente entre dispositivo y memoria. |

**Importante:** DMA puede utilizar una interrupción para notificar que terminó.

## 11. E/S síncrona y asíncrona

### Síncrona

La llamada devuelve el control al solicitante después de finalizar la operación.

### Asíncrona

La llamada devuelve el control antes de que finalice la operación.

El solicitante puede continuar y recibir o consultar el resultado posteriormente.

**Importante:** que un proceso espere una operación síncrona no significa que toda la CPU deba quedar inactiva.

### Tabla de estados de dispositivos

Permite al SO registrar:

- El dispositivo.
- Su estado.
- La operación solicitada.
- El proceso asociado.

Si existen varias solicitudes, pueden organizarse en una cola para cada dispositivo.

## 12. Buses e interfaces

Un bus permite comunicar componentes de la computadora.

El material menciona:

| Nombre | Qué debes recordar |
|---|---|
| ISA | Bus antiguo: Industry Standard Architecture. |
| PCI | Interconexión de componentes periféricos; sucesor de ISA. |
| SATA | Interfaz para conectar unidades de almacenamiento. |
| PCIe | Interconexión utilizada por distintos dispositivos. |
| NVMe sobre PCIe | Protocolo para acceder a almacenamiento no volátil. |
| USB | Conexión de periféricos. |
| eSATA | Conexión SATA externa. |

## 13. Estructuras de los sistemas operativos

Un SO es complejo. Dividirlo en componentes facilita organizar sus funciones y responsabilidades.

### 13.1. Sistema monolítico

Los servicios principales del sistema funcionan integrados en un mismo núcleo y en modo kernel.

**Ventajas:**

- Buen rendimiento.
- Comunicación directa entre componentes.

**Dificultades:**

- Mayor complejidad.
- Un fallo dentro del kernel puede afectar a todo el sistema.

**Importante:** un kernel monolítico puede admitir módulos.

### 13.2. Organización modular

Separa funcionalidades en módulos con responsabilidades definidas.

Permite extender determinadas funciones del sistema.

**Importante:** modular y monolítico no son necesariamente opuestos.

### 13.3. Arquitectura por capas

El sistema se organiza en niveles.

- La capa inferior corresponde al hardware.
- La superior corresponde a la interfaz con el usuario.
- Cada capa utiliza servicios de niveles inferiores.
- Una capa necesita saber qué hace un servicio, sin conocer todos sus detalles internos.

**Ventajas:**

- Organización.
- Ocultamiento de información.
- Facilita la depuración y la verificación.

**Dificultades:**

- Definir correctamente las capas.
- Sobrecarga al atravesar varios niveles.
- Puede ser menos eficiente.

### 13.4. Microkernel

Mantiene un núcleo pequeño en modo kernel y ejecuta otros servicios como procesos de usuario.

**Ventajas:**

- Aislamiento.
- Modularidad.
- Confiabilidad.

**Ejemplo:** si un driver de audio está aislado y falla, el problema puede limitarse al servicio de audio.

### 13.5. Arquitectura híbrida

Combina ideas de diferentes estructuras:

- Núcleos monolíticos.
- Módulos.
- Componentes en espacio de usuario.

### Comparación general

| Estructura | Idea principal |
|---|---|
| Monolítica | Servicios principales integrados en el kernel. |
| Modular | Funcionalidades organizadas en módulos. |
| Por capas | Servicios organizados por niveles. |
| Microkernel | Núcleo mínimo y servicios separados. |
| Híbrida | Combinación de enfoques. |

## 14. Máquinas virtuales

Una máquina virtual presenta un entorno de hardware virtual en el que puede ejecutarse un sistema operativo invitado.

Puede incluir:

- Procesadores virtuales.
- Memoria virtualizada.
- Dispositivos de E/S virtuales.
- Interrupciones.
- Modos de ejecución para el sistema invitado.

### Monitor de máquinas virtuales o hipervisor

Administra los recursos físicos y permite proporcionar varias máquinas virtuales.

**Ejemplo:** ejecutar Linux dentro de una máquina virtual en otro sistema operativo.

**Idea principal:** varios entornos de ejecución pueden compartir un equipo físico.

## 15. Componentes del sistema operativo

Los componentes deben tener funciones, entradas y salidas bien definidas.

### 15.1. Gestión de procesos

Un **programa** es un conjunto de instrucciones: una entidad pasiva.

Un **proceso** es un programa en ejecución: una entidad activa y una unidad de trabajo.

**Ejemplo:**

- El navegador instalado es un programa.
- Una instancia del navegador ejecutándose corresponde a uno o varios procesos.

### Responsabilidades del SO

- Crear y eliminar procesos.
- Asignar CPU.
- Suspender y reanudar procesos.
- Permitir comunicación entre procesos.
- Permitir sincronización entre procesos.
- Mantener información de cada proceso.

**Comunicación:** intercambio de información.

**Sincronización:** coordinación de la ejecución.

### 15.2. Gestión de memoria principal

El SO se encarga de:

- Asignar memoria.
- Liberar memoria.
- Proteger espacios de direcciones.
- Dar soporte a la memoria virtual.

### 15.3. Gestión de archivos

Un archivo es una unidad lógica de almacenamiento que oculta detalles físicos del dispositivo.

El SO se encarga de:

- Crear y eliminar archivos.
- Crear y eliminar directorios.
- Proporcionar operaciones para manipularlos.
- Relacionar los archivos con el almacenamiento secundario.

### 15.4. Gestión del sistema de E/S

Busca ocultar las particularidades de los dispositivos.

Incluye:

- Interfaces generales.
- Drivers específicos.
- Buffers.
- Cachés.
- Spool.

#### Buffer

Almacenamiento temporal utilizado durante una transferencia.

#### Caché

Conserva copias de información para acelerar accesos posteriores.

#### Spool

Mantiene trabajos en espera para un dispositivo.

**Ejemplo:** una cola de documentos para imprimir.

### 15.5. Gestión del almacenamiento secundario

El SO se encarga de:

- Administrar espacio libre.
- Asignar almacenamiento.
- Planificar operaciones de disco.

### 15.6. Sistema de protección

Controla que solamente usuarios y procesos autorizados puedan acceder a los recursos.

Incluye:

- Autenticación.
- Autorización.
- Permisos.
- Privilegios.
- Aislamiento.

**Autenticación:** comprobar quién eres.

**Autorización:** determinar qué puedes hacer.

### 15.7. Intérprete de órdenes o shell

Es una interfaz entre el usuario y el sistema operativo.

Su función básica es:

1. Obtener una orden.
2. Ejecutarla.
3. Esperar la siguiente.

**Importante:** el shell no es todo el sistema operativo.

## 16. Llamadas al sistema

Una llamada al sistema es el mecanismo mediante el cual una aplicación solicita un servicio al SO.

Es la interfaz entre un proceso y el sistema operativo.

### Ejemplo

Una aplicación necesita leer datos de un archivo.

1. Solicita el servicio.
2. Se transfiere el control al SO.
3. El SO identifica la operación e inspecciona los parámetros.
4. Realiza el servicio.
5. Devuelve el control al programa.

### ¿Por qué son necesarias?

Porque las aplicaciones necesitan acceder a servicios y recursos que requieren la intervención controlada del SO.

### Cinco categorías

#### 1. Control de procesos

- Crear y terminar procesos.
- Cargar y ejecutar programas.
- Finalizar o abortar.
- Consultar y establecer atributos.
- Esperar un tiempo.
- Esperar o indicar sucesos.
- Asignar y liberar memoria.

#### 2. Administración de archivos

- Crear y eliminar.
- Abrir y cerrar.
- Leer y escribir.
- Cambiar la posición de lectura o escritura.
- Consultar y modificar atributos.
- Administrar directorios.

#### 3. Administración de dispositivos

- Solicitar y liberar dispositivos.
- Leer y escribir.
- Consultar y modificar atributos.
- Conectar y desconectar lógicamente.

#### 4. Mantenimiento de información

- Consultar y establecer fecha y hora.
- Consultar información del sistema.
- Consultar y modificar atributos.
- Consultar o establecer identificadores de procesos cuando corresponda.

#### 5. Comunicaciones

Intercambiar información entre procesos:

- Dentro de la misma computadora.
- A través de una red.

**Para memorizar:** procesos, archivos, dispositivos, información y comunicaciones.

## 17. Diferencias que debes dominar

| Conceptos | Diferencia |
|---|---|
| Programa / proceso | Instrucciones almacenadas / programa en ejecución. |
| Multitarea / multiusuario | Varias tareas / múltiples usuarios. |
| Concurrencia / paralelismo | Progreso de varias tareas / ejecución simultánea. |
| Modo usuario / kernel | Acceso restringido / ejecución privilegiada. |
| RAM / ROM | Memoria de trabajo volátil / memoria no volátil. |
| Caché / RAM | Copias para acceso rápido / memoria principal de trabajo. |
| Dirección virtual / física | Dirección del espacio virtual / ubicación correspondiente en memoria física. |
| Driver / controlador físico | Software / hardware. |
| Sondeo / interrupciones | Consultar continuamente / recibir una señal. |
| DMA / transferencia mediante CPU | Controlador mueve bloques / CPU mueve los datos. |
| E/S síncrona / asíncrona | Retorno al finalizar / retorno antes de finalizar. |
| Monolítico / microkernel | Servicios integrados en kernel / núcleo reducido y servicios separados. |
| Autenticación / autorización | Quién eres / qué puedes hacer. |
| Shell / kernel | Intérprete de órdenes / núcleo del sistema. |

## 18. Diez preguntas teóricas para practicar

### 1. ¿Qué es un SO y cuáles son sus dos funciones principales?

Es el software que administra los recursos del hardware y proporciona servicios y abstracciones para ejecutar aplicaciones. Sus funciones principales son administrar recursos y ocultar la complejidad del hardware.

### 2. ¿Qué problema de los sistemas por lotes mejora la multiprogramación?

Reduce el tiempo en que la CPU queda ociosa durante operaciones de E/S, permitiendo ejecutar otro programa disponible en memoria.

### 3. ¿Cómo se clasifican los sistemas operativos?

Por tareas: monotarea y multitarea. Por usuarios: monousuario y multiusuario. Por uso: escritorio, servidor, móvil, embebido, tiempo real e IoT/Edge.

### 4. ¿Cuál es el ciclo básico de la CPU y qué son sus modos de ejecución?

La CPU obtiene, decodifica y ejecuta instrucciones. El modo usuario tiene restricciones; el modo kernel permite operaciones privilegiadas para administrar el sistema.

### 5. ¿Qué es la jerarquía de memoria?

Es la organización del almacenamiento en niveles con diferentes velocidades, capacidades y costos. En general, los niveles superiores son más rápidos, pequeños y costosos por bit.

### 6. ¿Qué es una interrupción y cómo se atiende?

Es una señal que desvía temporalmente la ejecución para atender un suceso. Se guarda el estado, se ejecuta la rutina de servicio y se restaura el estado para continuar.

### 7. ¿En qué se diferencian sondeo, interrupciones y DMA?

En sondeo, la CPU consulta continuamente. Con interrupciones, el dispositivo avisa. Con DMA, un controlador transfiere bloques directamente entre dispositivo y memoria.

### 8. ¿Qué estructuras puede tener un SO?

Monolítica, modular, por capas, microkernel e híbrida. Se diferencian por cómo distribuyen y comunican sus componentes.

### 9. ¿Cuáles son los componentes principales del SO?

Gestión de procesos, memoria principal, archivos, E/S, almacenamiento secundario, protección e interpretación de órdenes.

### 10. ¿Qué son las llamadas al sistema y cuáles son sus categorías?

Son solicitudes de servicios de una aplicación al SO. Sus categorías son control de procesos, archivos, dispositivos, mantenimiento de información y comunicaciones.

## 19. Preguntas adicionales

1. **¿Qué diferencia existe entre programa y proceso?**  
   Un programa es un conjunto de instrucciones; un proceso es ese programa ejecutándose.

2. **¿Para qué sirve el contador de programa?**  
   Guarda la dirección de la siguiente instrucción que ejecutará la CPU.

3. **¿Qué contiene la PSW?**  
   Información del estado del procesador, como los indicadores y el modo de ejecución.

4. **¿Qué diferencia hay entre un núcleo y un hilo?**  
   Un núcleo es una unidad física de procesamiento; un hilo es un flujo de ejecución.

5. **¿Por qué la RAM necesita apoyo del almacenamiento secundario?**  
   Porque tiene capacidad limitada y pierde sus datos al apagar el equipo.

6. **¿Qué almacenan L1I y L1D?**  
   L1I almacena instrucciones y L1D almacena datos.

7. **¿Qué es la memoria virtual?**  
   Permite que cada proceso use direcciones virtuales que se traducen a direcciones físicas.

8. **¿Qué es el vector de interrupciones?**  
   Es una tabla que permite localizar la rutina que atiende cada interrupción.

9. **¿Por qué se guarda el estado al atender una interrupción?**  
   Para retomar el trabajo donde se quedó después de atenderla.

10. **¿Qué significa espera ocupada?**  
    Que la CPU consulta continuamente si un dispositivo ya terminó.

11. **¿Qué configura la CPU en una operación DMA?**  
    La operación, las direcciones involucradas y la cantidad de datos que se transferirán.

12. **¿Qué contiene una tabla de estados de dispositivos?**  
    El dispositivo, su estado, la operación solicitada y el proceso asociado.

13. **¿Qué diferencia existe entre un driver y un controlador físico?**  
    El driver es software y el controlador físico es hardware que maneja el dispositivo.

14. **¿Qué ventajas tiene una arquitectura por capas?**  
    Organiza el sistema y facilita encontrar errores, verificarlo y mantenerlo.

15. **¿Por qué un microkernel favorece el aislamiento?**  
    Porque separa servicios en procesos, reduciendo el efecto de sus fallos sobre el resto del sistema.

16. **¿Puede un kernel monolítico utilizar módulos?**  
    Sí, puede utilizar módulos para agregar o ampliar funciones.

17. **¿Qué hace un hipervisor?**  
    Administra los recursos físicos y permite ejecutar varias máquinas virtuales.

18. **¿Qué diferencia hay entre buffer, caché y spool?**  
    El buffer guarda datos durante transferencias, la caché acelera accesos y el spool mantiene trabajos en cola.

19. **¿Qué diferencia existe entre autenticación y autorización?**  
    La autenticación comprueba quién eres y la autorización determina qué puedes hacer.

20. **¿Cuál es la función del shell?**  
    Recibir las órdenes del usuario y ejecutarlas.
    
## 20. Repaso rápido antes del examen

- **SO:** administra recursos y proporciona abstracciones.
- **Multiprogramación:** aprovecha la CPU mientras otro programa espera.
- **CPU:** obtiene, decodifica y ejecuta.
- **Usuario:** restringido.
- **Kernel:** privilegiado.
- **Proceso:** programa en ejecución.
- **Interrupción:** guardar, atender, restaurar y continuar.
- **Caché:** acelera accesos mediante copias.
- **RAM:** memoria principal volátil.
- **ROM:** no volátil.
- **Memoria virtual:** direcciones virtuales traducidas a físicas.
- **Sondeo:** consultar continuamente.
- **Interrupciones:** recibir aviso.
- **DMA:** transferir bloques con poca intervención de la CPU.
- **Monolítico:** servicios integrados.
- **Capas:** niveles que utilizan servicios inferiores.
- **Microkernel:** núcleo pequeño y servicios separados.
- **Híbrido:** combina enfoques.
- **Hipervisor:** administra máquinas virtuales.
- **Shell:** recibe y ejecuta órdenes.
- **Llamada al sistema:** solicitud de un servicio al SO.
- **Categorías de llamadas:** procesos, archivos, dispositivos, información y comunicaciones.



