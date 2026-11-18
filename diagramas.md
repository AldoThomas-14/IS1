# Diagramas de arquitectura: VaultofMusic_Managment

Diagramas en Mermaid (texto), según la Guía rápida de Mermaid de la Unidad 3. Se ven renderizados directo en GitHub o pegando cada bloque en https://mermaid.live.

## 1. Contexto (C4 nivel 1)

Quién usa el sistema y con qué se relaciona. Solo existe un tipo de usuario (el propietario o su socio). Las plataformas de venta no se integran: se publica y se cobra a mano.

```mermaid
flowchart TD
adm(["Administrador<br/>propietario o socio"])
sis["VaultofMusic_Managment<br/>inventario y finanzas"]
plat["Plataformas de venta<br/>Marketplace y redes sociales"]
adm -->|registra y consulta| sis
adm -.->|publica y cobra a mano| plat
```

## 2. Contenedores (C4 nivel 2)

Qué se instala y dónde. Es software instalado en un dominio propio: una aplicación web (monolito modular), una sola base de datos y un respaldo cada 24 horas.

```mermaid
flowchart TD
adm(["Administrador"])
subgraph sistema["VaultofMusic_Managment"]
app["Aplicación web<br/>monolito modular"]
db[("Base de datos<br/>una sola")]
resp[("Respaldos<br/>copia cada 24 horas")]
end
adm -->|usa en el navegador por HTTPS| app
app -->|lee y escribe| db
db -->|copia diaria| resp
```

## 3. Componentes (C4 nivel 3)

Los cuatro módulos dentro del monolito. Las flechas sólidas son dependencias de una sola vía; Inventario no depende de nadie. La flecha punteada es el aviso del patrón Observer: Inventario anuncia que un disco cambió y Acceso e historial lo registra.

```mermaid
flowchart TD
adm(["Administrador"])
subgraph app["Aplicación web: monolito modular"]
acc["Acceso e historial<br/>sesión y cambios"]
inv["Inventario<br/>discos y pedidos"]
ven["Ventas y bajas<br/>salidas del stock"]
fin["Finanzas<br/>ganancia y reportes"]
end
db[("Base de datos")]
adm --> acc
adm --> inv
adm --> ven
adm --> fin
ven -->|apartar vender y dar de baja| inv
fin -->|costos del disco y envío| inv
fin -->|pregunta ingresos y pérdidas| ven
inv -.->|anuncia: disco cambió| acc
acc --> db
inv --> db
ven --> db
fin --> db
```

## 4. Caso: el dueño inicia sesión y registra un disco nuevo

```mermaid
sequenceDiagram
actor Dueno as Dueño
participant Acc as Acceso e historial
participant Inv as Inventario
participant BD as Base de datos
Dueno->>Acc: Inicia sesión
Acc->>BD: Consulta la cuenta
BD-->>Acc: Cuenta válida
Acc-->>Dueno: Sesión iniciada
Dueno->>Inv: Registra un disco nuevo con sus siete datos
Inv->>BD: ¿Existe un disco igual?
BD-->>Inv: No existe
Note over Inv,BD: Si existe, avisa y pide confirmar (RF-026)
Inv->>BD: Guarda el disco
BD-->>Inv: Listo
Inv->>Acc: Anuncia: disco nuevo
Acc->>BD: Guarda el cambio con autor, fecha y hora
BD-->>Acc: Listo
Inv-->>Dueno: Disco registrado
```
