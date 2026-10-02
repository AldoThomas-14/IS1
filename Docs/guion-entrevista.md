# Guion de entrevista

**Sistema:** VaultofMusic_Managment (gestión de inventario y finanzas para The Vault of Music, venta de vinilos y CDs)

**Entrevistado:** cofundador de The Vault of Music, interpretado por la dupla a partir de la ficha de dominio (al final de este documento).

**Cómo leer este guion:** las preguntas están organizadas en seis tramos y todas son abiertas, sin ejemplos que sugieran la respuesta. Las marcadas con † no se hicieron en la entrevista aplicada y quedan para una segunda ronda. Las respuestas obtenidas están en "Notas de la entrevista" y lo que cambiaron en la "Bitácora".

## 1. Contexto

1. ¿Podrías describirme cómo es tu proceso típico cuando llega un nuevo lote de discos para vender?
2. Dentro de tu día a día manejando el inventario y las ventas, ¿cuáles son las tareas que más tiempo te consumen?
3. † ¿Quién más participa en el negocio y qué hace cada quien?

## 2. Proceso actual

4. Cuéntame paso a paso cómo registras hoy un disco nuevo que acabas de adquirir, desde que lo recibes hasta que queda listo para la venta.
5. Dame un ejemplo concreto de cómo llevas el control de cuánto gastaste en un disco y en cuánto lo vendiste después.
6. Muéstrame o descríbeme cómo sabes hoy, en cualquier momento, cuánta ganancia lleva el negocio.
7. † Cuando un cliente te pregunta por una pieza, ¿qué haces para responderle?
8. † ¿Por qué canales publicas y vendes tus discos, y cómo cierras una venta en cada uno?

## 3. Dolores

9. † ¿Qué es lo que más te frustra de cómo llevas el inventario hoy?
10. † Cuéntame de la última vez que algo salió mal con el inventario o con las cuentas. ¿Qué pasó y cómo lo resolviste?
11. † Si pudieras cambiar una sola cosa de tu forma de trabajar, ¿cuál sería y por qué?

## 4. Excepciones

12. ¿Qué sucede cuando un disco se daña, se pierde o resulta defectuoso antes de poder venderse?
13. ¿Cómo manejan un caso donde el mismo disco se ofrece en dos canales de venta distintos y alguien lo compra en ambos casi al mismo tiempo?
14. † ¿Qué haces entre que un cliente te dice que quiere un disco y el momento en que ya tienes el pago?
15. † ¿Qué pasa cuando un cliente cancela o devuelve una compra?

## 5. Verificación de supuestos

Cada pregunta nace de un requisito que el equipo está suponiendo.

16. Además de lo que pagas por el disco, ¿qué otros gastos tienes por cada pieza y cómo los tomas en cuenta hoy? (RF-012, RF-013)
17. ¿Cómo describes hoy la condición de un disco? (RF-001)
18. Cuando tienes dos copias del mismo álbum, ¿cómo las manejas hoy y cómo te gustaría manejarlas? (RF-002)
19. Cuando un disco sale del inventario sin venderse, ¿qué razones puede haber y cuáles te importa distinguir? (RF-023, RF-024)
20. † Cuando un envío o lote trae varios discos, ¿cómo repartes su costo entre ellos? (RF-011)
21. † ¿Cómo separas hoy lo que costó el disco de lo que gastas por venderlo, y cómo quieres verlo al cierre? (RF-014)
22. † ¿En qué momento consideras que un disco ya está vendido? (RF-022)
23. † ¿Cuánto tiempo te parece razonable para registrar una venta? (RNF-USA-001)
24. † Cuando tú o tu socio cambian un dato de un disco, ¿cómo quieren enterarse? (RF-004)
25. † ¿Quién debe poder entrar al sistema y desde dónde? (RF-016)

## 6. Cierre

26. Para asegurarme de haber comprendido todo correctamente: ¿hay alguna otra situación del manejo del inventario o del negocio que no hayamos mencionado y que consideres importante tomar en cuenta?

## Notas de la entrevista

En la entrevista se aplicó una primera versión del guion en la que las preguntas de requisitos eran cerradas ("¿el sistema permite…?"). Por eso las respuestas confirman los requisitos, pero no exploran alternativas. Las preguntas de este documento son la versión abierta que debe usarse en una segunda ronda.

**Contexto y proceso actual (preguntas 1, 2, 4, 5 y 6)**

- Cuando llega un lote, abre la caja, saca disco por disco, revisa la condición del vinilo o CD y de la funda, toma fotografías, fija el precio según estado y edición y lo publica en redes sociales y Marketplace.
- Lo que más tiempo le consume es evaluar la condición de cada disco, responder mensajes de clientes que preguntan si un título está disponible y sacar las cuentas de ganancias, gastos de importación y comisiones al final de la semana o del mes.
- Para registrar un disco anota sus datos y condición, le asigna precio y escribe renglón por renglón artista, título, país, estado y precio en una hoja de cálculo antes de fotografiarlo y subirlo a la venta.
- Controla el gasto anotando en celdas el costo de compra más lo que costó traerlo, y al lado el precio de venta para ver la diferencia.
- Para saber la ganancia total, a fin de mes junta a mano las notas de gastos de importación, comisiones y envíos y las resta de lo cobrado en las ventas registradas.

**Requisitos (versión cerrada aplicada)**

- Registrar un disco en una sola operación con artista, álbum, año de edición, país de origen, condición, costo y precio de venta es esencial.
- Quiere ver la ficha completa de forma rápida y clara al buscar o seleccionar un disco.
- Necesita marcar un disco como vendido y que el ingreso se registre automáticamente en la contabilidad.
- Quiere poder dar de baja un disco por daño, pérdida o extravío sin que cuente como venta.
- Quiere el cálculo automático de la ganancia total con base en compras y ventas.
- Las búsquedas deben tardar menos de 2 segundos aunque el catálogo crezca.
- Una persona sin capacitación debe poder dar de alta un disco en menos de 3 minutos.
- Es vital evitar registros duplicados y no perder lo capturado si la aplicación se cierra por accidente.

**Excepciones (preguntas 12 y 13)**

- Si un disco se daña o se pierde, lo borra o lo anota en la hoja para no contarlo como disponible, pero el impacto financiero no queda bien registrado.
- Como el inventario no se actualiza al instante en todos los canales, a veces dos personas compran el mismo disco casi al mismo tiempo; debe cancelarle la orden a uno, disculparse y devolverle el dinero, lo que deja una mala impresión.

**Verificación de supuestos (preguntas 16 a 19)**

- Quiere registrar, además del costo directo de compra, los gastos de importación o envío, empaque y comisiones de la plataforma, para restarlos del ingreso y obtener la ganancia neta real.
- Describe la condición con escalas estándar de coleccionismo, notas libres sobre detalles específicos y fotos.
- Dos copias del mismo álbum en condiciones distintas deben manejarse como fichas separadas, porque al cambiar la condición cambia el precio de venta.
- Quiere categorizar la razón de una baja para saber exactamente a qué se deben las pérdidas.

**Cierre (pregunta 26):** no hubo respuesta registrada.

## Bitácora

| Supuesto o hallazgo | Resultado | Qué cambió en la especificación |
| --- | --- | --- |
| Un disco solo sale del stock al venderse | **Cayó.** También sale por daño, pérdida o extravío, con su motivo, y hoy ese impacto financiero no se registra. | RF-009 reformulado; nuevos RF-023, RF-024 y RF-025. |
| Un disco se describe con seis datos | **Cayó.** Falta el país de origen, que influye en el precio. | RF-001 y RF-006 incluyen el país de origen. |
| La condición es un dato simple | **Matiz.** Usa una escala estándar de coleccionismo, notas libres y fotos. | RF-001 admite condición en escala estándar y nota libre; las fotos quedan fuera del alcance. |
| Dos copias con distinta condición son artículos separados | **Confirmado.** | RF-002 con origen confirmado en la entrevista. |
| Los gastos se suman al costo para la ganancia real | **Confirmado**, y se concretó en importación o envío, empaque y comisión de la plataforma. | RF-012 y RF-013 nombran los tres tipos de gasto. |
| Un pedido es un lote que llega en un mismo envío | **Confirmado.** | RF-010 sin supuesto. |
| La búsqueda debe tardar menos de 2 segundos | **Confirmado**, con un catálogo de varios cientos de discos que crece. | RNF-REN-001 con origen confirmado; los 1,000 discos son propuesta del equipo. |
| Registrar una venta toma menos de un minuto | **No salió**, y no se preguntó. | RNF-USA-001 queda marcado como límite sin verificar. |
| Cuentas solo mensuales | **Cayó.** Las cuentas se sacan al final de la semana o del mes. | RF-014 y RF-015 con periodo semanal o mensual. |
| Inesperado: doble venta del mismo disco en dos canales | **Apareció.** Hay que cancelar la orden a un comprador. | Nuevo RF-021; el apartado se marca a mano porque no habrá integración con plataformas. |
| Inesperado: no perder un registro a medias | **Apareció.** Es vital conservar lo capturado si la aplicación se cierra. | Nuevo RNF-CON-005. |
| Inesperado: alta sin capacitación en menos de 3 minutos | **Apareció.** | Nuevo RNF-USA-002. |
| Inesperado: registros duplicados | **Apareció.** Se quieren evitar. | Nuevo RF-026, con el supuesto de avisar y pedir confirmación. |
| Regla de la ficha que nadie preguntó: un disco no se marca como vendido hasta confirmar el pago | **Descubierta por la ficha.** | Nuevo RF-022, con el supuesto del estado apartado. |
| Prorrateo del envío, historial de cambios, acceso y dominio propio | **No se abordaron en la entrevista.** Son decisiones del propietario. | RF-011 conserva su supuesto; RF-004, RF-016 a RF-020 y los RNF de seguridad quedan con origen en el dueño. |

## Ficha de dominio

**Quién eres**

Eres cofundador de The Vault of Music, un emprendimiento de venta de vinilos y CDs, muchos de ellos ediciones japonesas. Antes de iniciar el negocio trabajaste un año en una tienda de discos física, así que conoces bien cómo catalogar y valuar piezas de colección. Te encargas de recibir los lotes de discos, revisarlos, evaluar su condición, ponerles precio y darles seguimiento hasta que se venden.

**Cómo es tu día**

Recibes discos que compras por importación o a coleccionistas locales, los revisas uno por uno para evaluar su condición física y la del empaque, los fotografías y los publicas para la venta en redes sociales y Marketplace. Respondes mensajes de clientes preguntando por piezas específicas, gestionas los envíos de lo que se vende y, al final de cada semana, intentas sacar cuentas de cuánto gastaste, cuánto vendiste y cuánto ganaste.

**Reglas que conoces y no vas a decir si no te preguntan**

Cada disco se registra con artista, álbum, año de edición, país de origen (las prensas japonesas suelen valer más), condición y precio de venta. Un disco no se marca como vendido hasta que el pago está confirmado. Los gastos de importación y envío se deben sumar al costo del disco para calcular la ganancia real, no solo lo que costó comprarlo. Cuando hay dos copias del mismo álbum con condición distinta, se manejan como registros separados porque su precio es diferente.

**Una excepción que ocurre a veces**

A veces el mismo disco queda publicado a la vez en Instagram y en un marketplace, y como el inventario no se actualiza al instante, dos personas terminan comprando la misma pieza casi al mismo tiempo. Ahí tienes que cancelarle la compra a una de las dos personas y disculparte, lo cual no se siente nada bien para el negocio.

**Lo que te molesta de cómo trabajas hoy**

Llevar todo en una hoja de cálculo que se va desordenando con el tiempo, tener que buscar manualmente cada disco cuando un cliente pregunta por una pieza específica, y sacar las cuentas de ganancia a mano al final del mes, juntando gastos de importación, envíos y comisiones de las plataformas.

**Cómo responder**

Contesta solo lo que te pregunten. Si te preguntan algo que no está en esta ficha (como métodos de pago, proveedores específicos o logística de envíos internacionales), inventa una respuesta coherente con el negocio. Si te preguntan de forma vaga, responde de forma vaga.
