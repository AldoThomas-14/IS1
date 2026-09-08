# VaultofMusic_Managment — Documento de especificación

**Autor:** Aldo Thomas Trejo
**Fecha de la última versión:** 20/08/2026
**Repositorio:** VaultofMusic

---

## 1. Descripción del sistema

**Nombre del sistema:** VaultofMusic_Managment

**Descripción:**

El sistema es un control de inventario y finanzas de la tienda de discos "Vault of Music". Llevará un registro de los productos en stock, los que han sido vendidos y las ganancias y costos de los mismos. Su principal objetivo será ayudar al propietario y a su socio a llevar las finanzas, analizando los costos por disco y de envío respecto a las ganancias por disco. También busca facilitar la revisión rápida de datos de cada disco (artista, álbum, año de la edición, precio, condición) y permitir eliminarlo del stock cuando se venda, para tener mayor facilidad al hacer pedidos y decidir si conseguir más material o no.

---

## 2. Problema y usuarios

### El problema

Resuelve el problema que representa no tener fácil acceso a los datos de cada disco, no conocer el número exacto de discos en stock, no contar con una forma asertiva de eliminar artículos del stock y, sobre todo, perder de vista la parte financiera del negocio.

### Cómo se resuelve hoy sin el sistema

Actualmente el dueño y su socio lo resuelven utilizando hojas de Excel (tediosas y lentas de usar), Google Notes o la memoria de los mismos involucrados. Esto genera caos, ya que pueden olvidar la venta de un disco, su precio o parte de sus datos. También suelen equivocarse al ingresar datos y tienen que corregir muchas partes, siendo usual que olviden aplicar los cambios en todos los lugares donde correspondía.

### Usuarios del sistema

El propietario y su socio son los únicos que deben tener acceso al sistema. Ambos desempeñan el mismo trabajo, por lo que existe un solo tipo de usuario.

| Tipo de usuario | Qué necesita del sistema | Qué le preocupa |
|---|---|---|
| Administrador (propietario / socio) | Una interfaz rápida para ubicar discos específicos y consultar sus datos (artista, álbum, año, condición, precio) de forma clara; poder dar de baja discos del stock al venderse; un módulo de finanzas que registre costo por disco, ganancia por disco, costos de envío, otros gastos y ganancia total mensual | Introducir un dato erróneo y que el otro socio no se entere; perder de vista una venta o un costo mal calculado; que los datos financieros no cuadren al cierre del mes; duplicar o confundir discos de distinta edición/condición |

### Un conflicto entre usuarios

Al momento de introducir o actualizar un dato, puede ser que ambos usuarios discrepen, introduzcan el dato erróneo y generen inconsistencias. También pueden olvidar reportar una venta física o registrar mal un costo. Puede haber dos discos de diferente edición o condición que los administradores confundan entre sí. Asimismo, pueden surgir errores al decidir qué discos reabastecer, generando duplicados o desacuerdos en las elecciones.

---

## 3. Alcance

### Dentro del alcance

- Registro de discos con sus datos: artista, álbum, año de edición, condición, precio de venta y costo de adquisición.
- Baja automática del stock al registrar una venta.
- Registro de costos de envío y otros gastos asociados a cada disco o pedido.
- Cálculo de ganancia por disco (precio de venta − costo − envío − gastos asociados).
- Reporte financiero mensual con ganancia total, costos totales y gastos totales.
- Búsqueda y filtrado rápido de discos por artista, álbum, año o condición.
- Acceso para los dos administradores con los mismos permisos.

### Explícitamente fuera del alcance

| Exclusión | Por qué queda fuera |
|---|---|
| Reportes de ventas mensuales exportables a PDF o Excel | No es indispensable para la operación diaria; se puede consultar directamente en el sistema. Se prioriza el registro correcto sobre la exportación en esta primera versión. |
| Integración con plataformas de venta en línea (Discogs, eBay, Mercado Libre) | Requiere manejo de APIs externas y sincronización en tiempo real, lo cual excede el tiempo y la complejidad disponibles para este proyecto. |
| Facturación electrónica / timbrado fiscal | Es un requerimiento legal-contable independiente del control de inventario y finanzas internas; se maneja hoy con otro proceso y no es el problema central que resuelve el sistema. |
| Aplicación móvil nativa | El sistema se usará desde la tienda en una sola computadora; una app móvil no aporta valor adicional al problema identificado. |
| Gestión de empleados o nóminas | Solo hay dos usuarios (dueño y socio) con el mismo rol; no existe una estructura de personal que administrar. |
| Predicción o recomendación automática de qué discos reabastecer (analítica avanzada / IA) | El objetivo es dar visibilidad clara de los datos para que los administradores decidan; automatizar la decisión añade complejidad de modelado que no es necesaria en esta etapa. |

---

## 4. Tipo de sistema y restricciones

**Tipo de sistema:** De datos y análisis

**Por qué es de ese tipo:** Debido a que el propósito del sistema es llevar el inventario y analizar las finanzas, es el tipo de sistema indicado para este proyecto.

**Atributos de calidad que impone:** El control de acceso y el manejo de datos son esenciales para el sistema, además de la precisión en la parte analítica. Con estos atributos, el sistema será una herramienta útil para la tienda y le dará ventaja sobre competidores que sigan trabajando de forma manual. Sin ellos, los datos mostrados pueden ser erróneos y generar confusiones y pérdidas. Si el módulo analítico falla, la contabilidad será incorrecta y no se podrán tomar decisiones acertadas, lo que puede llevar a una pérdida significativa de ganancias.

### Reglas de negocio que ya identifiqué

1. **Un disco no puede eliminarse del stock sin quedar registrado como "vendido"**, con precio de venta y fecha: si se borra directamente se pierde el historial necesario para el reporte financiero mensual.
2. **El costo de envío de un pedido con varios discos debe prorratearse entre todos los discos de ese pedido**, no puede cargarse completo a uno solo, porque distorsionaría la ganancia real por disco.
3. **Dos copias del mismo álbum con distinta condición o edición se tratan como artículos distintos** (no se suman como stock del mismo ítem), ya que su precio y su margen de ganancia son diferentes.
4. **La ganancia mensual se calcula por fecha de venta, no por fecha de registro del disco en el sistema**: un disco puede llevar meses en inventario antes de venderse, y el reporte del mes debe reflejar solo lo efectivamente vendido en ese periodo.
5. **Cualquier edición de un dato ya guardado debe quedar visible para ambos administradores** (no solo para quien la hizo), dado el conflicto identificado de discrepancias entre los dos usuarios con el mismo nivel de acceso.

---

## 5. Ciclo de vida elegido

**Modelo elegido:** Prototipado rápido

### Por qué le conviene a este proyecto

- **Es un proyecto propio:** yo mismo desarrollo el sistema y tengo contacto directo y constante con los usuarios (dueño y socio), así que no hace falta un proceso formal de levantamiento de requisitos ni entregas planeadas de antemano; puedo construir una primera versión funcional y ajustarla según se va usando.
- **Retroalimentación inmediata:** al no depender de que un cliente externo revise y apruebe cada entrega, cada cambio o corrección puede probarse casi de inmediato en el uso real en la tienda, lo que hace más eficiente ir modificando sobre la marcha que planificar incrementos formales.
- **Requisitos que se descubren usando el sistema:** varios detalles (cómo prorratear el envío, qué tan detallado debe ser el reporte mensual, cómo distinguir ediciones) probablemente solo se ven claros una vez que el sistema ya está en uso; el prototipado rápido está pensado justamente para ese tipo de descubrimiento iterativo sin necesidad de re-planear el proyecto completo.
- **Nivel de riesgo:** es un sistema interno de bajo riesgo (no es crítico de seguridad ni de misión crítica), por lo que ir probando versiones funcionales directamente es aceptable, a diferencia de un sistema donde un error en producción sea costoso.
- **Tamaño del equipo:** al ser un desarrollador único, un modelo ligero sin ceremonias de planeación formal (como reuniones de incremento o sprints) es más manejable que modelos que asumen un equipo con roles distintos.

### Alternativas descartadas

**Alternativa 1: Cascada (Waterfall)**
*Por qué la descarté:* Exige cerrar por completo los requisitos antes de empezar a construir, pero en este proyecto es probable que el uso real en la tienda revele necesidades que no son evidentes desde el inicio (como el prorrateo de envíos). Un cambio tardío en cascada implicaría retroceder a la fase de análisis, lo cual es costoso e innecesario para un proyecto de este tamaño y de uso propio.

**Alternativa 2: Iterativo e incremental**
*Por qué la descarté:* Es similar en flexibilidad al prototipado rápido, pero normalmente implica planear incrementos con alcance definido y revisarlos formalmente antes de pasar al siguiente. Al ser un proyecto para uso propio y de una sola persona, resulta más práctico ir construyendo y modificando el sistema directamente sobre la marcha, sin necesidad de planear y cerrar incrementos formales en cada ciclo.

---

## Antes de entregar

- [x] El alcance dice qué queda fuera, no solo qué queda dentro
- [x] Las exclusiones son específicas, no genéricas
- [x] Anoté al menos tres reglas de negocio no obvias
- [x] Justifiqué el ciclo de vida contra dos alternativas descartadas
- [ ] El documento está en mi repositorio y se puede leer desde el navegador
- [x] Borré todas las instrucciones en cursiva de la plantilla
