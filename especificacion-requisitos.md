# Especificación de requisitos

**Sistema:** VaultofMusic_Managment

**Autor:** Aldo Thomas Trejo

**Fecha:** 01/10/2026

## 1. Propósito y alcance

**Propósito del documento:** Especificar los requisitos funcionales y no funcionales de VaultofMusic_Managment, sistema de control de inventario y finanzas del emprendimiento de tienda de discos Vault of Music. Va dirigido al propietario, a su socio (los dos usuarios del sistema) y a quien desarrolla el prototipo, que en este caso es también el propietario, por lo que toda la información y requisitos son avalados por mí.

**Alcance del sistema:**

- Registro de discos con artista, álbum, año de edición, condición, precio de lista (varía según el disco) y costo de adquisición.
- Baja automática del stock al registrar una venta con su precio final de venta.
- Registro de costos de envío y otros gastos asociados a cada disco o pedido.
- Cálculo de ganancia por disco (precio final de venta − costo − envío − gastos asociados).
- Reporte financiero mensual con ganancia total, costos totales y gastos totales.
- Búsqueda y filtrado rápido de discos por artista, álbum, año o condición.
- Edición de datos de un disco con historial de cambios por campo, al estilo del historial de commits de Git, consultable por los dos administradores.
- Acceso por internet mediante un dominio propio de la tienda, solo para el propietario y su socio, con los mismos permisos.

**Fuera del alcance:**

- Reportes de ventas mensuales exportables a PDF o Excel: no son indispensables para la operación diaria; en esta primera versión se priorizan el registro correcto y la consulta dentro del sistema.
- Integración con plataformas de venta en línea (Discogs, eBay, Mercado Libre): requiere APIs externas y sincronización en tiempo real, lo que excede el tiempo disponible.
- Tienda en línea pública (catálogo, carrito de compras, pagos): el dominio aloja únicamente el sistema de gestión y no es visible para clientes.
- Facturación electrónica y timbrado fiscal: es un requerimiento legal-contable que hoy se maneja con otro proceso.
- Aplicación móvil nativa: el sistema se usa desde el navegador en el dominio de la tienda, por lo que una app nativa no aporta valor adicional.
- Gestión de empleados o nóminas: solo hay dos usuarios con el mismo rol.
- Predicción o recomendación automática de qué discos reabastecer: el sistema da visibilidad de los datos y los administradores deciden.

## 2. Usuarios y su contexto

| Usuario | Qué hace hoy sin el sistema | Qué espera del sistema |
| --- | --- | --- |
| Administrador (propietario y socio (ambos con el mismo rol y permisos) | Lleva el inventario y las finanzas en hojas de Excel, Google Notes o de memoria. Olvida ventas, precios o datos de un disco, se equivoca al capturar y no siempre aplica una corrección en todos los lugares donde correspondía. | Entrar al sistema desde el dominio de la tienda con su propia identificación; ubicar un disco rápido y consultar sus datos (artista, álbum, año, condición, precio); dar de baja del stock los discos vendidos; ver costo por disco, ganancia por disco, costos de envío, otros gastos y ganancia total mensual; revisar el historial de cambios de cada disco para saber qué cambió el otro administrador. |

**Conflictos identificados entre usuarios:**

- Al introducir o actualizar un dato, los dos administradores pueden discrepar o capturar un valor erróneo, y el otro no se entera.
- Uno de los dos puede olvidar reportar una venta física o registrar mal un costo.
- Dos discos de distinta edición o condición pueden confundirse entre sí.
- Al decidir qué discos reabastecer pueden surgir duplicados o desacuerdos.

## 3. Requisitos funcionales

El propietario, que es el cliente, confirmó los requisitos el 01/10/2026. En el campo Origen, "Confirmado" indica lo aprobado por él; "Supuesto" indica lo que sigue pendiente de definir o verificar en la entrevista.

### 3.1 Resumen

| ID | Nombre | Prioridad | Origen |
| --- | --- | --- | --- |
| RF-001 | Registro de disco | Imprescindible | Confirmado |
| RF-002 | Distinción de ediciones y condiciones | Imprescindible | Confirmado |
| RF-003 | Edición de datos de un disco | Importante | Confirmado |
| RF-004 | Visibilidad del historial de cambios para ambos administradores | Imprescindible | Confirmado |
| RF-005 | Búsqueda y filtrado de discos | Imprescindible | Confirmado |
| RF-006 | Consulta de los datos de un disco | Imprescindible | Confirmado |
| RF-007 | Registro de venta | Imprescindible | Confirmado |
| RF-008 | Baja automática del stock | Imprescindible | Confirmado |
| RF-009 | Conservación del historial de ventas | Imprescindible | Confirmado, con un supuesto |
| RF-010 | Registro del costo de envío de un pedido | Imprescindible | Confirmado, con un supuesto |
| RF-011 | Prorrateo del envío entre los discos del pedido | Imprescindible | Confirmado, con un supuesto |
| RF-012 | Registro de otros gastos asociados | Importante | Confirmado |
| RF-013 | Cálculo de ganancia por disco | Imprescindible | Confirmado |
| RF-014 | Reporte financiero mensual | Imprescindible | Confirmado, con un supuesto |
| RF-015 | Asignación de ventas al mes por fecha de venta | Imprescindible | Confirmado |
| RF-016 | Acceso exclusivo del propietario y su socio | Imprescindible | Confirmado |
| RF-017 | Mismos permisos para ambos administradores | Imprescindible | Confirmado |
| RF-018 | Identificación de cada administrador | Imprescindible | Confirmado |
| RF-019 | Registro de cada cambio en el historial | Imprescindible | Confirmado |
| RF-020 | Historial de cambios inalterable | Importante | Confirmado, con un supuesto |

### 3.2 Fichas

#### RF-001 · Registro de disco

| Campo | Contenido |
| --- | --- |
| Descripción | El sistema registra un disco con artista, álbum, año de edición, condición, precio de lista y costo de adquisición. |
| Origen | Confirmado por el dueño. Visión del producto, alcance. El precio de lista varía según el disco. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Al guardar un disco con los seis datos, este aparece en el stock con esos datos. Si falta alguno, el sistema no guarda y señala cuál falta. |
| Relacionado con | RF-002, RF-005, RNF-CON-001, RNF-CON-003 |

#### RF-002 · Distinción de ediciones y condiciones

| Campo | Contenido |
| --- | --- |
| Descripción | El sistema trata como artículos distintos dos copias del mismo álbum que difieren en edición o en condición. |
| Origen | Confirmado por el dueño. Visión del producto, regla de negocio 3: su precio y su margen de ganancia son diferentes. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Al registrar dos copias del mismo álbum con condiciones distintas, el stock muestra dos artículos, cada uno con su propio precio y costo, y no un solo artículo con cantidad 2. |
| Relacionado con | RF-001, RF-005 |

#### RF-003 · Edición de datos de un disco

| Campo | Contenido |
| --- | --- |
| Descripción | El sistema permite modificar cualquier dato de un disco ya guardado. |
| Origen | Confirmado por el dueño. Visión del producto, problema actual: hoy se olvida aplicar las correcciones en todos los lugares. |
| Prioridad | Importante |
| Criterio de aceptación | Al cambiar el precio de lista de un disco y guardar, el nuevo precio aparece en el stock y en la búsqueda de ese disco. |
| Relacionado con | RF-004, RF-019, RNF-CON-001 |

#### RF-004 · Visibilidad del historial de cambios para ambos administradores

| Campo | Contenido |
| --- | --- |
| Descripción | El sistema muestra a ambos administradores el historial de cambios de cada disco. |
| Origen | Confirmado por el dueño. Visión del producto, regla de negocio 5. El dueño pidió que el historial funcione como el de commits de GitHub. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Después de que un administrador edita el precio de lista de un disco, el otro administrador abre el historial de ese disco y ve el cambio, sin que el primero tenga que avisarle. |
| Relacionado con | RF-003, RF-018, RF-019, RF-020, RNF-CON-001 |

#### RF-005 · Búsqueda y filtrado de discos

| Campo | Contenido |
| --- | --- |
| Descripción | El sistema permite buscar y filtrar los discos en stock por artista, álbum, año o condición. |
| Origen | Confirmado por el dueño. Visión del producto, alcance. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Al filtrar por un artista, el sistema muestra solo los discos en stock de ese artista; al filtrar por artista y condición a la vez, muestra solo los que cumplen ambos. |
| Relacionado con | RF-006, RNF-REN-001 |

#### RF-006 · Consulta de los datos de un disco

| Campo | Contenido |
| --- | --- |
| Descripción | El sistema muestra los datos de un disco: artista, álbum, año de edición, condición y precio de lista. |
| Origen | Confirmado por el dueño. Visión del producto, usuarios: los administradores necesitan consultar esos datos de forma clara. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Al seleccionar un disco de los resultados de búsqueda, el sistema muestra sus cinco datos. |
| Relacionado con | RF-005, RNF-REN-001 |

#### RF-007 · Registro de venta

| Campo | Contenido |
| --- | --- |
| Descripción | El sistema registra la venta de un disco con su precio final de venta y su fecha de venta. |
| Origen | Confirmado por el dueño. Visión del producto, regla de negocio 1. El precio final de venta puede diferir del precio de lista y siempre deja una ganancia de al menos 70% sobre el costo de adquisición. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Al registrar la venta de un disco con precio final y fecha, el disco queda como vendido con esos dos datos. Si falta alguno, el sistema no guarda y señala cuál falta. |
| Relacionado con | RF-008, RF-009, RF-013, RF-015, RNF-USA-001 |

#### RF-008 · Baja automática del stock

| Campo | Contenido |
| --- | --- |
| Descripción | Al registrar la venta de un disco, el sistema lo da de baja del stock sin que el administrador lo haga aparte. |
| Origen | Confirmado por el dueño. Visión del producto, alcance. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Con 10 discos en stock, al registrar la venta de uno, el stock muestra 9, el disco vendido ya no aparece en la búsqueda de stock y sí aparece en la lista de vendidos. |
| Relacionado con | RF-007, RF-005, RNF-USA-001 |

#### RF-009 · Conservación del historial de ventas

| Campo | Contenido |
| --- | --- |
| Descripción | El sistema no permite eliminar un disco del stock sin registrarlo como vendido. |
| Origen | Confirmado por el dueño. Visión del producto, regla de negocio 1: si se borra directamente se pierde el historial necesario para el reporte mensual. Supuesto: un disco registrado por error se corrige editándolo (RF-003) y no se elimina; por definir en la entrevista. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Al intentar quitar un disco del stock, el sistema pide precio final de venta y fecha; sin ellos, el disco permanece en el stock. |
| Relacionado con | RF-007, RF-014 |

#### RF-010 · Registro del costo de envío de un pedido

| Campo | Contenido |
| --- | --- |
| Descripción | El sistema registra el costo de envío de un pedido junto con los discos que incluye. |
| Origen | Confirmado por el dueño. Visión del producto, alcance. Supuesto: un pedido agrupa los discos que llegan en un mismo envío; por definir en la entrevista. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Al guardar un pedido con envío de $300 y tres discos, el pedido queda registrado con ese monto y esos tres discos. |
| Relacionado con | RF-011, RF-012 |

#### RF-011 · Prorrateo del envío entre los discos del pedido

| Campo | Contenido |
| --- | --- |
| Descripción | El sistema reparte el costo de envío de un pedido entre todos los discos que incluye. |
| Origen | Confirmado por el dueño. Visión del producto, regla de negocio 2: cargarlo completo a un solo disco distorsionaría la ganancia real. Supuesto: el método de reparto (partes iguales o proporcional al costo) está por definir; el criterio de aceptación se cumple con cualquiera de los dos. |
| Prioridad | Imprescindible |
| Criterio de aceptación | En un pedido con envío de $300 y tres discos, ningún disco recibe los $300 completos y la suma de los envíos asignados a los tres discos es exactamente $300. |
| Relacionado con | RF-010, RF-013, RNF-CON-002 |

#### RF-012 · Registro de otros gastos asociados

| Campo | Contenido |
| --- | --- |
| Descripción | El sistema registra otros gastos asociados a un disco o a un pedido. |
| Origen | Confirmado por el dueño. Visión del producto, alcance. |
| Prioridad | Importante |
| Criterio de aceptación | Al registrar un gasto de $50 asociado a un disco, el gasto queda guardado ligado a ese disco y se puede consultar desde él. |
| Relacionado con | RF-010, RF-013, RF-014 |

#### RF-013 · Cálculo de ganancia por disco

| Campo | Contenido |
| --- | --- |
| Descripción | El sistema calcula la ganancia de cada disco vendido como precio final de venta menos costo de adquisición, menos envío asignado, menos gastos asociados. |
| Origen | Confirmado por el dueño. Visión del producto, alcance. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Para un disco con costo de adquisición de $400, vendido a un precio final de $1,000, con envío asignado de $100 y gastos asociados de $50, el sistema muestra una ganancia de $450. |
| Relacionado con | RF-007, RF-011, RF-012, RF-014, RNF-CON-002 |

#### RF-014 · Reporte financiero mensual

| Campo | Contenido |
| --- | --- |
| Descripción | El sistema muestra, para un mes elegido, la ganancia total, los costos totales y los gastos totales. |
| Origen | Confirmado por el dueño. Visión del producto, alcance. Supuesto: la definición exacta de "costos" frente a "gastos" está por afinar en la entrevista. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Al elegir un mes, el reporte muestra las tres cifras y cada una coincide con la suma de los valores de los discos vendidos en ese mes. |
| Relacionado con | RF-013, RF-015, RNF-CON-002 |

#### RF-015 · Asignación de ventas al mes por fecha de venta

| Campo | Contenido |
| --- | --- |
| Descripción | El sistema asigna cada venta al mes de su fecha de venta, no al de la fecha en que el disco se registró. |
| Origen | Confirmado por el dueño. Visión del producto, regla de negocio 4: un disco puede pasar meses en inventario antes de venderse. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Un disco registrado en marzo y vendido en junio aparece en el reporte de junio y no aparece en el de marzo. |
| Relacionado con | RF-007, RF-014, RNF-CON-002 |

#### RF-016 · Acceso exclusivo del propietario y su socio

| Campo | Contenido |
| --- | --- |
| Descripción | El sistema permite el acceso solo al propietario y a su socio. |
| Origen | Confirmado por el dueño (01/10/2026): solo él y su socio deben tener acceso. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Una persona que no es el propietario ni el socio no logra ver ni modificar ningún dato del sistema. |
| Relacionado con | RF-017, RF-018, RNF-SEG-001, RNF-SEG-002, RNF-SEG-003 |

#### RF-017 · Mismos permisos para ambos administradores

| Campo | Contenido |
| --- | --- |
| Descripción | El sistema da al propietario y al socio los mismos permisos. |
| Origen | Confirmado por el dueño. Visión del producto, alcance y usuarios: ambos desempeñan el mismo trabajo. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Registrar un disco, editarlo, registrar una venta y consultar el reporte mensual dan el mismo resultado hechos con la identificación del propietario o con la del socio. |
| Relacionado con | RF-016, RF-018 |

#### RF-018 · Identificación de cada administrador

| Campo | Contenido |
| --- | --- |
| Descripción | El sistema identifica a cada administrador al entrar. |
| Origen | Confirmado por el dueño. Visión del producto, regla de negocio 5: hay que saber quién hizo cada cambio. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Al entrar, el sistema reconoce si quien entró es el propietario o el socio, y esa identidad aparece como autor en las entradas del historial de cambios. |
| Relacionado con | RF-004, RF-016, RF-019 |

#### RF-019 · Registro de cada cambio en el historial

| Campo | Contenido |
| --- | --- |
| Descripción | El sistema guarda cada edición de un dato de un disco como una entrada del historial, con autor, fecha y hora, campo, valor anterior y valor nuevo. |
| Origen | Confirmado por el dueño (01/10/2026): historial por campo, al estilo de los commits de GitHub. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Al cambiar el precio de lista de un disco de $500 a $600, el historial muestra una entrada nueva con el administrador que lo hizo, la fecha y hora, el campo "precio de lista", el valor $500 y el valor $600. |
| Relacionado con | RF-003, RF-004, RF-018, RF-020 |

#### RF-020 · Historial de cambios inalterable

| Campo | Contenido |
| --- | --- |
| Descripción | El sistema no permite modificar ni borrar las entradas del historial de cambios. |
| Origen | Confirmado por el dueño (historial al estilo de los commits de GitHub). Supuesto: se interpreta ese modelo como un historial que no se reescribe; por verificar en la entrevista. |
| Prioridad | Importante |
| Criterio de aceptación | Ninguna pantalla ofrece una acción para editar o borrar una entrada del historial; al corregir un valor equivocado, la corrección aparece como una entrada nueva y la anterior permanece. |
| Relacionado con | RF-004, RF-019 |

## 4. Requisitos no funcionales

El sistema es de datos y análisis, y la Visión del producto le impone tres atributos de calidad: control de acceso (Seguridad), manejo de datos y precisión analítica (ambos, Confiabilidad). Que el dueño vaya a alojarlo en un dominio propio, en internet, suma protección de los datos en tránsito, disponibilidad y conservación ante fallas. Rendimiento y usabilidad salen de la necesidad de ser más rápido que Excel. Cada límite se justifica en "Por qué importa". Los límites numéricos fueron confirmados por el dueño el 01/10/2026.

### 4.1 Resumen

| ID | Atributo | Nombre | Prioridad | Origen |
| --- | --- | --- | --- | --- |
| RNF-SEG-001 | Seguridad | Acceso solo para los administradores | Imprescindible | Derivado del tipo de sistema; confirmado |
| RNF-SEG-002 | Seguridad | Bloqueo tras intentos fallidos de acceso | Importante | Derivado del dominio propio; confirmado |
| RNF-SEG-003 | Seguridad | Datos protegidos en tránsito | Imprescindible | Derivado del dominio propio; confirmado |
| RNF-CON-001 | Confiabilidad | Consistencia de un dato en todas las pantallas | Imprescindible | Derivado del tipo de sistema; confirmado |
| RNF-CON-002 | Confiabilidad | Exactitud de las cifras financieras | Imprescindible | Derivado del tipo de sistema; confirmado |
| RNF-CON-003 | Confiabilidad | Conservación de los datos ante fallas | Imprescindible | Derivado del dominio propio; confirmado |
| RNF-CON-004 | Confiabilidad | Disponibilidad del sistema | Importante | Derivado del dominio propio; confirmado |
| RNF-REN-001 | Rendimiento | Tiempo de búsqueda de un disco | Importante | Visión del producto; confirmado |
| RNF-USA-001 | Usabilidad | Rapidez para registrar una venta | Importante | Visión del producto; confirmado |

### 4.2 Fichas

#### RNF-SEG-001 · Acceso solo para los administradores

| Campo | Contenido |
| --- | --- |
| Atributo de calidad | Seguridad (control de acceso) |
| Descripción | Sin identificarse, nadie puede consultar ni modificar datos del sistema, y solo existen dos identidades válidas: la del propietario y la del socio. |
| Métrica | Funciones de consulta o modificación disponibles sin identificarse, revisadas en todas las pantallas del prototipo: 0. Identidades válidas registradas: exactamente 2. |
| Origen | Derivado del tipo de sistema: el control de acceso es esencial. Confirmado por el dueño. |
| Prioridad | Imprescindible |
| Por qué importa | El sistema guarda costos y ganancias del negocio. El límite es 0 y 2 porque basta una función abierta o una tercera identidad para exponer la parte financiera, y el dueño decidió que solo él y su socio acceden. |
| Afecta a | RF-016, RF-017, RF-018 |

#### RNF-SEG-002 · Bloqueo tras intentos fallidos de acceso

| Campo | Contenido |
| --- | --- |
| Atributo de calidad | Seguridad (control de acceso) |
| Descripción | El sistema bloquea el acceso después de varios intentos fallidos seguidos de identificación. |
| Métrica | Tras 5 intentos fallidos consecutivos, el acceso queda bloqueado durante 15 minutos; en una prueba de 6 intentos con datos incorrectos, el sexto es rechazado aunque se usen los datos correctos. |
| Origen | Derivado de la decisión del dueño de alojar el sistema en un dominio propio, accesible por internet. Confirmado por el dueño. |
| Prioridad | Importante |
| Por qué importa | Con el sistema en internet, cualquiera puede intentar entrar. Con 5 intentos, un error normal de captura no bloquea a un administrador, y 15 minutos de espera hacen impráctico adivinar la clave probando combinaciones. |
| Afecta a | RF-016, RF-018 |

#### RNF-SEG-003 · Datos protegidos en tránsito

| Campo | Contenido |
| --- | --- |
| Atributo de calidad | Seguridad (confidencialidad) |
| Descripción | Los datos que viajan entre el navegador del administrador y el sistema no pueden ser leídos por terceros. |
| Métrica | Porcentaje de solicitudes al dominio atendidas por una conexión cifrada: 100%; toda solicitud sin cifrar es rechazada o redirigida. |
| Origen | Derivado de la decisión del dueño de alojar el sistema en un dominio propio, accesible por internet. Confirmado por el dueño. |
| Prioridad | Imprescindible |
| Por qué importa | Los costos y las ganancias viajarían por internet, incluso desde redes públicas. El límite es 100% sin excepción porque una sola solicitud sin cifrar puede exponer la identificación de un administrador. |
| Afecta a | RF-014, RF-016, RF-018 |

#### RNF-CON-001 · Consistencia de un dato en todas las pantallas

| Campo | Contenido |
| --- | --- |
| Atributo de calidad | Confiabilidad (integridad de datos) |
| Descripción | Un dato guardado se muestra con el mismo valor en todas las pantallas donde aparece. |
| Métrica | Discrepancias entre pantallas (stock, búsqueda, historial, reporte) después de editar un dato, medidas con 20 ediciones de prueba de precio de lista, costo y condición: 0. |
| Origen | Derivado del tipo de sistema (manejo de datos) y de la Visión del producto, problema actual: hoy los cambios no se aplican en todos los lugares. Confirmado por el dueño. |
| Prioridad | Imprescindible |
| Por qué importa | El límite es 0 porque una sola discrepancia cambia la ganancia calculada y deja a los administradores sin saber qué dato creer. Con 20 ediciones, cada una de las tres clases de dato se prueba al menos 6 veces. |
| Afecta a | RF-001, RF-003, RF-004, RF-013, RF-014 |

#### RNF-CON-002 · Exactitud de las cifras financieras

| Campo | Contenido |
| --- | --- |
| Atributo de calidad | Confiabilidad (precisión analítica) |
| Descripción | Las ganancias por disco y las cifras del reporte mensual coinciden con el cálculo hecho a mano. |
| Métrica | Diferencia entre el reporte mensual del sistema y la suma calculada a mano, medida con al menos 20 ventas de prueba con montos con centavos: $0.00. |
| Origen | Derivado del tipo de sistema: si el módulo analítico falla, la contabilidad es incorrecta. Confirmado por el dueño. |
| Prioridad | Imprescindible |
| Por qué importa | Si las cifras no cuadran al cierre del mes, no se puede decidir con acierto si conseguir más material. El límite es $0.00 porque en contabilidad una diferencia pequeña se acumula; las 20 ventas deben incluir envíos que no se dividen exacto, como $100 entre 3 discos. |
| Afecta a | RF-011, RF-013, RF-014, RF-015 |

#### RNF-CON-003 · Conservación de los datos ante fallas

| Campo | Contenido |
| --- | --- |
| Atributo de calidad | Confiabilidad (conservación de datos) |
| Descripción | Los registros de discos, ventas, envíos y gastos se conservan aunque el sistema falle. |
| Métrica | Antigüedad máxima de la información que se puede recuperar tras una falla: 24 horas. |
| Origen | Derivado del tipo de sistema (manejo de datos) y de la decisión de alojarlo en un dominio propio. Confirmado por el dueño. |
| Prioridad | Imprescindible |
| Por qué importa | Los administradores capturan ventas y gastos a diario. Un día es lo máximo que pueden reconstruir con sus notas sin riesgo de error, y perder más dejaría el stock y las finanzas desalineados de la realidad. |
| Afecta a | RF-001, RF-007, RF-010, RF-012 |

#### RNF-CON-004 · Disponibilidad del sistema

| Campo | Contenido |
| --- | --- |
| Atributo de calidad | Confiabilidad (disponibilidad) |
| Descripción | El sistema está disponible para los administradores durante todo el mes. |
| Métrica | Disponibilidad mensual de al menos 99% de las horas del mes, es decir, hasta unas 7 horas de interrupción al mes. |
| Origen | Derivado de la decisión del dueño de alojar el sistema en un dominio propio. Confirmado por el dueño. |
| Prioridad | Importante |
| Por qué importa | Las ventas se registran cuando ocurren y una caída impide registrar y consultar. El 99% tolera mantenimientos cortos sin exigir un nivel de servicio de empresa grande, que no se justifica para un negocio de dos personas. |
| Afecta a | RF-005, RF-007, RF-014 |

#### RNF-REN-001 · Tiempo de búsqueda de un disco

| Campo | Contenido |
| --- | --- |
| Atributo de calidad | Rendimiento |
| Descripción | La búsqueda de un disco muestra sus resultados en menos de 2 segundos. |
| Métrica | Tiempo entre aplicar el filtro y mostrar los resultados, medido con 1,000 discos registrados: menos de 2 segundos. |
| Origen | Visión del producto: hoy Excel es tedioso y lento. Límites confirmados por el dueño. |
| Prioridad | Importante |
| Por qué importa | Dos segundos es lo que un administrador espera con un cliente enfrente antes de volver a Excel o a la memoria. Los 1,000 discos son un tope de inventario con holgura para que la búsqueda no se degrade cuando el stock crezca. |
| Afecta a | RF-005, RF-006 |

#### RNF-USA-001 · Rapidez para registrar una venta

| Campo | Contenido |
| --- | --- |
| Atributo de calidad | Usabilidad |
| Descripción | Registrar una venta toma menos de un minuto. |
| Métrica | Tiempo para registrar una venta, medido sin ayuda en 3 pruebas con cada administrador (6 en total): menos de 60 segundos en las 6. |
| Origen | Visión del producto: los administradores olvidan reportar ventas físicas. Límites confirmados por el dueño. |
| Prioridad | Importante |
| Por qué importa | Un minuto es lo que cabe en el mostrador sin que el registro se posponga; lo que se pospone se olvida, que es el problema actual. Probar con ambos administradores evita que el tiempo dependa de quién lo hizo. |
| Afecta a | RF-007, RF-008 |

## 5. Casos de uso

Borrador previo a la entrevista de la semana 7; se ajusta con lo que salga de ella. Cada caso de uso lo ejecuta un administrador (propietario o socio).

| ID | Caso de uso | Requisitos funcionales que realiza |
| --- | --- | --- |
| CU-01 | Registrar un disco | RF-001, RF-002 |
| CU-02 | Buscar y consultar un disco | RF-005, RF-006 |
| CU-03 | Editar los datos de un disco | RF-003, RF-004, RF-019, RF-020 |
| CU-04 | Registrar una venta | RF-007, RF-008, RF-009 |
| CU-05 | Registrar el envío y los gastos de un pedido | RF-010, RF-011, RF-012 |
| CU-06 | Consultar la ganancia de un disco vendido | RF-013 |
| CU-07 | Consultar el reporte financiero mensual | RF-014, RF-015 |
| CU-08 | Iniciar sesión | RF-016, RF-017, RF-018 |

## 6. Trazabilidad

Los nombres de las pantallas son una propuesta; deben reemplazarse por los del prototipo.

| Requisito | Origen | Caso de uso | Elemento del prototipo |
| --- | --- | --- | --- |
| RF-001 | Confirmado, Visión: alcance | CU-01 Registrar un disco | Pantalla de registro de disco |
| RF-002 | Confirmado, Visión: regla de negocio 3 | CU-01 Registrar un disco | Pantalla de registro de disco |
| RF-003 | Confirmado, Visión: problema actual | CU-03 Editar los datos de un disco | Pantalla de edición de disco |
| RF-004 | Confirmado, Visión: regla de negocio 5 | CU-03 Editar los datos de un disco | Historial de cambios del disco |
| RF-005 | Confirmado, Visión: alcance | CU-02 Buscar y consultar un disco | Pantalla de inventario con búsqueda y filtros |
| RF-006 | Confirmado, Visión: usuarios | CU-02 Buscar y consultar un disco | Ficha del disco |
| RF-007 | Confirmado, Visión: regla de negocio 1 | CU-04 Registrar una venta | Pantalla de registro de venta |
| RF-008 | Confirmado, Visión: alcance | CU-04 Registrar una venta | Pantalla de registro de venta e inventario |
| RF-009 | Confirmado, con supuesto, Visión: regla de negocio 1 | CU-04 Registrar una venta | Pantalla de registro de venta |
| RF-010 | Confirmado, con supuesto, Visión: alcance | CU-05 Registrar el envío y los gastos de un pedido | Pantalla de pedidos |
| RF-011 | Confirmado, con supuesto, Visión: regla de negocio 2 | CU-05 Registrar el envío y los gastos de un pedido | Pantalla de pedidos |
| RF-012 | Confirmado, Visión: alcance | CU-05 Registrar el envío y los gastos de un pedido | Pantalla de gastos |
| RF-013 | Confirmado, Visión: alcance | CU-06 Consultar la ganancia de un disco vendido | Ficha del disco vendido |
| RF-014 | Confirmado, con supuesto, Visión: alcance | CU-07 Consultar el reporte financiero mensual | Pantalla de reporte mensual |
| RF-015 | Confirmado, Visión: regla de negocio 4 | CU-07 Consultar el reporte financiero mensual | Pantalla de reporte mensual |
| RF-016 | Confirmado, dueño 01/10/2026 | CU-08 Iniciar sesión | Pantalla de inicio de sesión |
| RF-017 | Confirmado, Visión: alcance y usuarios | CU-08 Iniciar sesión | Pantalla de inicio de sesión |
| RF-018 | Confirmado, Visión: regla de negocio 5 | CU-08 Iniciar sesión | Pantalla de inicio de sesión |
| RF-019 | Confirmado, dueño 01/10/2026 | CU-03 Editar los datos de un disco | Historial de cambios del disco |
| RF-020 | Confirmado, con supuesto, dueño 01/10/2026 | CU-03 Editar los datos de un disco | Historial de cambios del disco |
| RNF-SEG-001 | Derivado del tipo de sistema; confirmado | CU-08 Iniciar sesión | Pantalla de inicio de sesión |
| RNF-SEG-002 | Derivado del dominio propio; confirmado | CU-08 Iniciar sesión | Pantalla de inicio de sesión |
| RNF-SEG-003 | Derivado del dominio propio; confirmado | Transversal | Todas las pantallas |
| RNF-CON-001 | Derivado del tipo de sistema; confirmado | Transversal | Todas las pantallas |
| RNF-CON-002 | Derivado del tipo de sistema; confirmado | CU-06, CU-07 | Ficha del disco vendido y pantalla de reporte mensual |
| RNF-CON-003 | Derivado del dominio propio; confirmado | Transversal | Todo el sistema |
| RNF-CON-004 | Derivado del dominio propio; confirmado | Transversal | Todo el sistema |
| RNF-REN-001 | Visión del producto; confirmado | CU-02 Buscar y consultar un disco | Pantalla de inventario con búsqueda y filtros |
| RNF-USA-001 | Visión del producto; confirmado | CU-04 Registrar una venta | Pantalla de registro de venta |

## 7. Registro de cambios

| Fecha | Requisito | Qué cambió | Por qué |
| --- | --- | --- | --- |
| 01/10/2026 | RF-001, RF-006, RF-007, RF-013 | "Precio de venta" se separó en precio de lista (varía según el disco) y precio final de venta (lo cobrado, con al menos 70% de ganancia sobre el costo). | El término tenía dos significados. |
| 01/10/2026 | RF-016 | Se dividió en RF-016 (acceso exclusivo), RF-017 (mismos permisos) y RF-018 (identificación de cada administrador). | Tenía más de una idea. |
| 01/10/2026 | RF-004, RF-019, RF-020 | RF-004 pasó a ser el historial visible para ambos; se agregaron RF-019 (registro de cada cambio) y RF-020 (historial inalterable). | El dueño pidió un historial por campo, como los commits de GitHub. |
| 01/10/2026 | RNF-INT-001, RNF-PRE-001 | Reemplazados por RNF-CON-001 y RNF-CON-002 dentro del atributo Confiabilidad; los identificadores anteriores no se reutilizan. | Coincidir con los atributos de calidad del curso. |
| 01/10/2026 | RNF-SEG-002, RNF-SEG-003, RNF-CON-003, RNF-CON-004 | Requisitos nuevos de bloqueo por intentos fallidos, cifrado en tránsito, conservación ante fallas y disponibilidad. | El dueño alojará el sistema en un dominio propio, accesible por internet. |
| 01/10/2026 | Todos los RNF | Cada ficha explica por qué se eligió su límite. | Hacer cada límite justificable. |
| 01/10/2026 | Todos los RF | El campo Origen indica si es confirmado por el dueño o supuesto. | Distinguir lo confirmado de lo que sigue por verificar. |
| 01/10/2026 | Sección 1 | Se agregaron al alcance el historial de cambios y el acceso por dominio propio; se agregó la tienda en línea pública como exclusión; la exclusión de la app móvil ya no se justifica por una sola computadora. | Coherencia con el alojamiento en dominio propio. |
