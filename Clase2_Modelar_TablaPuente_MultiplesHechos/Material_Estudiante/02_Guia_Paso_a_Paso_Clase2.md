# Guía paso a paso — Clase 2

**Los 3 movimientos · 40 minutos · Se hace en TU propio `.pbix`**

---

> **Cómo usar esta guía.** Vamos todos juntos, al mismo ritmo. Cada paso
> empieza diciendo **en qué vista estás** (📍). Si no estás ahí, andá
> primero. Cada movimiento termina con un **VERIFICÁ** con números: si tu
> número no coincide, no sigas, avisá.

---

## Las tres vistas de Power BI (para no perderse)

Son los íconos de la barra vertical izquierda, de arriba hacia abajo:

| Ícono | Vista | Para qué la usamos hoy |
|---|---|---|
| 1° (gráfico de barras) | **Vista de informe** | páginas y **objetos visuales** (tablas, tarjetas) |
| 2° (grilla) | **Vista de tabla** | mirar los datos de una tabla |
| 3° (diagrama) | **Vista de modelo** | ver y crear **relaciones** |

> ### ⚠️ El modelo es UNO solo
> Todo lo que hagas en la **Vista de modelo** afecta a todas las páginas del
> informe. Las pestañas de abajo de la Vista de modelo (`Todas las tablas` y
> las que agregues con **+**) son sólo *dibujos* distintos del **mismo**
> modelo: **no aíslan nada**. Hoy no vamos a crear ninguna. Si ya creaste
> una, no pasa nada: clic derecho sobre la pestaña → **Eliminar**.

---

# PASO 0 · Antes de empezar: ¿tu presupuesto está bien?

📍 **Vista de informe** — cualquier página.

Insertá una **Tabla** con dos campos de `HECHOS_PRESUPUESTO`:
`Categoria` y `Presupuesto_Ingresos`.

### 📋 VERIFICÁ — Paso 0 (son dos controles)

**Control 1 — las filas.** Tiene que haber **exactamente 6**, con estos valores:

| Categoria | Presupuesto_Ingresos |
|---|---|
| Accesorios | **50.120** |
| Audio | **14.740** |
| Celulares | **106.750** |
| Laptops | **185.940** |
| Tablets | **31.330** |
| Television | **86.950** |

**Control 2 — el total.** Tiene que decir **475.830**.

| Si ves… | Qué significa |
|---|---|
| 6 filas y total **475.830** | ✅ Bien. Borrá la tabla y seguí. |
| **Más de 6 filas** (por ejemplo `laptops` o `accesorios` escritas aparte, con un espacio adelante) — y Laptops da **156.760**, Accesorios **46.860** | ❌ En la Clase 1 no se aplicó **Recortar** a la categoría. Ver **Arreglo A**. |
| Total **463.812,03** — con centavos | ❌ Power Query leyó `2.920` como **2,92**. Ver **Arreglo B**. |
| Total **488.690** | ❌ No quitaste duplicados en la Clase 1. |

> **Por qué el total puede estar bien y las filas no:** las filas con
> espacios siguen sumando en el total, pero no coinciden con ninguna
> categoría. El modelo de Power BI no distingue mayúsculas (`LAPTOPS` =
> `Laptops`), pero **sí distingue espacios** (`" laptops "` ≠ `Laptops`).
> Si no lo arreglás ahora, **todos los números de hoy te van a dar menos**
> que los de esta guía, y la tabla puente te va a dar más de 6 filas.

> **Arreglo A — categorías con espacios.**
>
> 1. **Inicio → Transformar datos**.
> 2. Consulta `HECHOS_PRESUPUESTO` → clic derecho en el encabezado
>    `Categoria` → **Transformar → Recortar**.
> 3. Otra vez clic derecho → **Transformar → Poner En Mayúsculas Cada
>    Palabra**.
> 4. **Cerrar y aplicar**. La tabla tiene que quedar en **6 filas**.

> **Arreglo B — si te dio 463.812,03.** Es el Aviso 2 del taller de la Clase 1. En el
> CSV hay tres importes escritos con punto de miles (`2.920`, `1.520`,
> `7.590`), y el cambio de tipo los tomó como decimales. Se arregla así:
>
> 1. **Inicio → Transformar datos**.
> 2. Consulta `HECHOS_PRESUPUESTO` → en **Pasos aplicados**, clic en el paso
>    donde cambiaste el tipo de las columnas → **❌** para borrarlo.
>
>    ⚠️ **Ese paso casi siempre cambiaba también el tipo de `Mes`.** Al
>    borrarlo, `Mes` vuelve a ser **texto**. Por eso el punto 3 tiene
>    **tres** columnas, no dos. Si te olvidás de `Mes`, en el Movimiento 3
>    todo el presupuesto va a caer en una fila en blanco.
>
> 3. Para **cada una** de estas tres columnas: clic derecho en el encabezado
>    → **Cambiar tipo → Usando configuración regional…** →
>    **Configuración regional: Español (Argentina)** → **Aceptar**:
>
>    | Columna | Tipo de datos |
>    |---|---|
>    | `Mes` | **Fecha** |
>    | `Presupuesto_Ingresos` | **Número decimal fijo** |
>    | `Presupuesto_Utilidad` | **Número decimal fijo** |
>
>    > **¿Por qué Español (Argentina) también para `Mes`?** `Mes` viene como
>    > `01/03/2025`. En español es **1 de marzo**; con la configuración en
>    > inglés se lee **3 de enero**. Los totales por año te darían bien igual,
>    > pero casi todo el presupuesto quedaría en enero. Es un error que
>    > **no se ve** mirando el año.
>
> 4. **Cerrar y aplicar**. La tabla del Paso 0 tiene que quedar en **6 filas**
>    y total **475.830**.
>
> Hacelo **ahora**: si no, todos los números de hoy te van a dar distinto.

---

# MOVIMIENTO 1 · La tentación

## La idea, primero

El presupuesto está por **categoría**. `DIM_PRODUCTOS` tiene una columna
`Producto_Categoria`. La intuición dice: *"los uno por ahí y listo"*.

Vamos a hacer exactamente eso. **A propósito**, para ver qué pasa.

## 1.1 · Crear la página `Laboratorio`

📍 **Vista de informe** (primer ícono).

Abajo están las pestañas de las páginas de tu informe (`Portada`, `Kpis`…).
Hacé clic en el **+** que está **al lado de esas pestañas** → renombrá la
página nueva a **`Laboratorio`** (doble clic sobre el nombre).

> Es una **página del informe**. No es un diseño de la Vista de modelo.

## 1.2 · Crear la relación "obvia"

📍 **Vista de modelo** (tercer ícono).

Vamos a crear la relación desde un diálogo, no arrastrando: así ves y
elegís todas las opciones, sin depender de la versión de Power BI.

1. En la cinta: **Inicio → Administrar relaciones**.
2. **+ Nueva relación…**
3. Completá:

   | Campo | Qué elegís |
   |---|---|
   | Primera tabla | `DIM_PRODUCTOS` → clic en la columna **`Producto_Categoria`** |
   | Segunda tabla | `HECHOS_PRESUPUESTO` → clic en la columna **`Categoria`** |
   | **Cardinalidad** | Power BI pone solo **Varios a varios (\*:\*)** y muestra un aviso amarillo. **Leelo.** |
   | **Dirección del filtro cruzado** | la opción que dice **`DIM_PRODUCTOS` filtra `HECHOS_PRESUPUESTO`** (en algunas versiones: **Única** + esa aclaración) |
   | **Activar esta relación** | ✔ tildado |

4. **Guardar** / **Aceptar**. Sí, aunque avise. Hoy queremos ver el daño.

> ### ¿Por qué "Varios a varios"?
> Porque `Producto_Categoria` se repite en `DIM_PRODUCTOS` (Accesorios está
> 4 veces, Laptops 2) **y** se repite en `HECHOS_PRESUPUESTO` (una vez por
> mes). Ninguno de los dos lados tiene valores únicos. Power BI te dice:
> *"acá no hay lado uno"*.

> ### ⚠️ La dirección es lo que hace funcionar la demo
> Con **`DIM_PRODUCTOS` filtra `HECHOS_PRESUPUESTO`**, el producto de cada
> fila filtra el presupuesto. Si queda al revés, el filtro no llega y vas a
> ver **el mismo número en todas las filas** — que parece "otro" error y
> arruina la comparación. En el diagrama, la flechita de la línea tiene que
> apuntar **hacia `HECHOS_PRESUPUESTO`**.

## 1.3 · Mirar el daño

📍 **Vista de informe** → página **`Laboratorio`**. *(Cambiaste de vista:
volvé al primer ícono.)*

En el panel **Visualizaciones** elegí **Tabla** y arrastrá desde el panel
**Datos**:

- `DIM_PRODUCTOS` → `Producto_Nombre`
- `HECHOS_PRESUPUESTO` → `Presupuesto_Ingresos` (aparece como *Suma de…*)
- `#Medidas` (o donde la tengas) → `Ingresos Totales`

### 📋 VERIFICÁ — Movimiento 1

| Fila | Suma de Presupuesto_Ingresos | Ingresos Totales |
|---|---|---|
| Mouse Inalambrico | **50.120** | ≈ 10.450 |
| Cable HDMI · Teclado Mecanico · Cargador Rapido | **50.120 cada uno** | |
| Laptop Pro 15 **y** Laptop Pro 15" | **185.940 cada una** | |
| **Total** | **475.830** | |
| Sumá a mano las 10 filas | **812.130** | |

**Las filas suman 812.130 y el total dice 475.830.** Mirá el Mouse:
facturó unos **10.450**; la tabla dice que su "presupuesto" es **50.120**.
Cualquier gerente concluye *"el Mouse cumplió el 21 % del objetivo, hay
que discontinuarlo"*.

Pero 50.120 **no es el objetivo del Mouse**: es el de los cuatro accesorios
juntos. **El Mouse no tiene objetivo.** Nadie se lo puso.

> **Un error que no da error.** Ni un ícono rojo. Los números se ven
> prolijos. Eso es lo peligroso.

### Si tu tabla no se ve así

| Lo que ves | Causa | Arreglo |
|---|---|---|
| **El mismo número en todas las filas** (el total) | La dirección quedó al revés | 📍 Vista de modelo → **Inicio → Administrar relaciones** → seleccioná la relación → **Editar** → **Dirección del filtro cruzado**: `DIM_PRODUCTOS` filtra `HECHOS_PRESUPUESTO` |
| Accesorios **46.860** y Laptops **156.760** (menos que la guía) | Categorías con espacios: falta **Recortar** | Volvé al Paso 0, Arreglo A |
| Números con **centavos** (463.812,03) | Punto de miles leído como decimal | Volvé al Paso 0, Arreglo B |
| Una fila **en blanco** en `Producto_Nombre` | Algún presupuesto con una categoría que no existe en productos | Avisá: mirá los valores de `Categoria` en la Vista de tabla |

## 1.4 · Deshacer

📍 **Vista de modelo** → **Inicio → Administrar relaciones** → seleccioná la
relación `DIM_PRODUCTOS` ↔ `HECHOS_PRESUPUESTO` → **Eliminar**.

**Dejá la tabla de la página `Laboratorio`**: la vamos a reusar. (La
columna de presupuesto ahora va a mostrar el total en todas las filas: es
lo esperado, ya no hay relación.)

---

# MOVIMIENTO 2 · La tabla puente (ya la conocés)

## La idea, primero

En la **Semana 7 de Nivel 1**, con el ejercicio de reclamos, aprendieron:

> *"La tabla puente la generamos cuando tenemos relaciones de muchos a
> muchos, identificando el campo en común entre las tablas y creando la
> tabla puente a partir de ese campo."*

Acabás de ver un muchos a muchos. El campo en común es la **categoría**.
Mismo problema, ahora en tu propio caso.

## 2.1 · Las dos columnas de categoría

📍 **Power Query**: **Inicio → Transformar datos**.

**Primera:**
1. En el panel izquierdo, clic derecho sobre `DIM_PRODUCTOS` → **Referencia**.
2. En la consulta nueva: clic en el encabezado `Producto_Categoria` → clic
   derecho → **Quitar otras columnas**.
3. Doble clic en el encabezado → renombrala **`Categoria`**.
4. A la derecha, en **Configuración de la consulta → Nombre**: **`Cat_Productos`**.
5. Clic derecho sobre la consulta (panel izquierdo) → destildá **Habilitar
   carga**.

**Segunda:**
1. Clic derecho sobre `HECHOS_PRESUPUESTO` → **Referencia**.
2. Encabezado `Categoria` → clic derecho → **Quitar otras columnas**.
3. **Nombre**: **`Cat_Presupuesto`** → clic derecho → destildá **Habilitar carga**.

> **¿Por qué renombrar a `Categoria` en la primera?** Al anexar, Power Query
> apila por **nombre de columna**. Si una se llama `Producto_Categoria` y la
> otra `Categoria`, quedan dos columnas medio vacías en vez de una.

## 2.2 · Anexar y quitar duplicados

📍 Seguís en **Power Query**.

1. **Inicio → Anexar consultas ▾** (la flechita) **→ Anexar consultas como
   nuevas**.

   > ## ⚠️ Esta vez SÍ es "como nuevas"
   >
   > | | Qué elegimos | Por qué |
   > |---|---|---|
   > | Clase 1, Mov. 2 | **Anexar consultas** (no como nuevas) | metíamos un paso **dentro** de `HECHOS_VENTAS` |
   > | **Hoy** | **Anexar consultas como nuevas** | queremos una tabla **nueva**, sin tocar las otras |

2. **Primera tabla**: `Cat_Productos` · **Segunda tabla**: `Cat_Presupuesto` → **Aceptar**.
3. Clic derecho en el encabezado `Categoria` → **Quitar duplicados**.
4. **Nombre**: **`DIM_CATEGORIA`**. *(Ésta sí queda con la carga habilitada.)*

### 📋 VERIFICÁ — antes de cerrar Power Query

| Qué mirar | Tiene que dar |
|---|---|
| Filas de `DIM_CATEGORIA` (abajo a la izquierda) | **6** |
| Los valores | Accesorios · Audio · Celulares · Laptops · Tablets · Television |

**¿Te dio más de 6?** Tenés la misma categoría escrita de dos formas:
`LAPTOPS` y `Laptops`, o `Laptops` y `" Laptops"`. Mirá cuál está distinta
y arreglalo **en el origen** (`HECHOS_PRESUPUESTO`): **Transformar →
Formato → Poner En Mayúsculas Cada Palabra** y **Recortar**. No lo arregles
en `DIM_CATEGORIA`.

> **Por qué importa (y no es obvio):** Power Query **distingue** mayúsculas:
> para él `LAPTOPS` y `Laptops` son dos categorías. El modelo de Power BI
> **no** las distingue: para él son la misma, repetida. Si llegás al modelo
> con esas dos filas, Power BI **se niega a crear la relación** ("valor
> duplicado" en el lado uno). Dos motores, dos reglas.

5. **Inicio → Cerrar y aplicar**.

## 2.3 · Conectar la puente

📍 **Vista de modelo** → **Inicio → Administrar relaciones → + Nueva
relación…** Dos relaciones, **siempre con `DIM_CATEGORIA` como primera
tabla**:

| Primera tabla / columna | Segunda tabla / columna | Cardinalidad | Dirección del filtro cruzado |
|---|---|---|---|
| `DIM_CATEGORIA` / `Categoria` | `DIM_PRODUCTOS` / `Producto_Categoria` | **Uno a varios (1:\*)** | **Única** |
| `DIM_CATEGORIA` / `Categoria` | `HECHOS_PRESUPUESTO` / `Categoria` | **Uno a varios (1:\*)** | **Única** |

Si Power BI propone **Varios a varios**, `DIM_CATEGORIA` no tiene valores
únicos: volvé al VERIFICÁ de 2.2. Si propone **Ambos**, cambialo a **Única**.

## 2.4 · La misma tabla, otra vez

📍 **Vista de informe** → página **`Laboratorio`**. *(Otra vez el primer
ícono.)*

1. En la tabla que ya tenés: en el panel **Visualizaciones**, sacá
   `Producto_Nombre` (la **✕**) y poné **`DIM_CATEGORIA` → `Categoria`**.
2. Insertá **una segunda Tabla** con `DIM_PRODUCTOS` → `Producto_Nombre` +
   `HECHOS_PRESUPUESTO` → `Presupuesto_Ingresos`.

### 📋 VERIFICÁ — Movimiento 2

| Tabla | Qué tiene que pasar |
|---|---|
| Por **`Categoria`** (de `DIM_CATEGORIA`) | cada categoría lo suyo: Accesorios **50.120**, Laptops **185.940**… y **la suma de las 6 filas = 475.830 = Total** ✔ |
| Por **`Producto_Nombre`** | **las 10 filas dicen 475.830** |

La segunda tabla parece rota. **No lo está.** El filtro de producto no
llega al presupuesto porque el presupuesto **no existe por producto**. En
vez de inventar un número como en el Movimiento 1, el modelo te dice
*"no sé"*.

> Un modelo que dice *"no sé"* es mejor que uno que miente con seguridad.
> En la Sesión 3 vamos a hacer que ese *"no sé"* se vea como una celda en
> blanco en vez de un total repetido.

> **"Pero en el Movimiento 1, cuando la dirección estaba al revés, también
> veía el total repetido."** Exacto, y es el mismo motivo: el filtro no
> llegaba. La diferencia es que acá **es la respuesta correcta**, y allá
> era un accidente de configuración.

---

# MOVIMIENTO 3 · El presupuesto y el calendario

## La idea, primero

El presupuesto es **mensual**: `HECHOS_PRESUPUESTO[Mes]` siempre es el
**día 1** de cada mes (01/01/2025, 01/02/2025…). Tu `DIM_TIEMPO` tiene
**una fila por día**. La intuición dice: *"es mensual, lo uno con la
columna de mes"*.

## 3.1 · La trampa (pensalo, no lo hagas)

Tu `DIM_TIEMPO` tiene columnas de mes: el número de mes (1 a 12) y el
nombre del mes.

**¿Cuántas veces aparece enero en la columna del nombre del mes?** Hay 2
años, y cada enero tiene 31 días.

`______` veces.

Una columna que se repite **no puede ser el lado "uno"**: te llevaría otra
vez a un **Varios a varios**, el problema del Movimiento 1.

## 3.2 · La relación que sí funciona

📍 **Vista de modelo** → **Inicio → Administrar relaciones → + Nueva
relación…**

| Primera tabla / columna | Segunda tabla / columna | Cardinalidad | Dirección del filtro cruzado |
|---|---|---|---|
| `DIM_TIEMPO` / `Fecha` | `HECHOS_PRESUPUESTO` / `Mes` | **Uno a varios (1:\*)** | **Única** |

**¿Por qué funciona con la fecha diaria?** Porque `Mes` siempre cae en el
día 1, y el día 1 de cada mes existe **una sola vez** en `DIM_TIEMPO`.
Cuando filtrás por año o por mes, el día 1 queda adentro del filtro.

### 📋 VERIFICÁ — Movimiento 3

📍 **Vista de informe** → página **`Laboratorio`** → nueva **Tabla** con:

- la columna de **año** de tu `DIM_TIEMPO` (en tu modelo se llama `Year`;
  es un número entero, está bien así),
- la columna de **número de mes** de tu `DIM_TIEMPO` (`Month`),
- `HECHOS_PRESUPUESTO` → `Presupuesto_Ingresos`.

> Si en los encabezados aparece **"Suma de Year"** o **"Suma de Month"**,
> en el panel **Visualizaciones** hacé clic en la flechita del campo →
> **No resumir**. Son columnas para agrupar, no para sumar.

**Control 1 — por año** (mirá los subtotales, o sacá `Month` un momento):

| Año | Tiene que dar |
|---|---|
| 2025 | **214.280** |
| 2026 | **261.550** |
| Total | **475.830** |

**Control 2 — por mes.** Con `Month` puesto, fijate dos filas de 2025:

| Año · Mes | Tiene que dar |
|---|---|
| 2025 · 1 (enero) | **8.740** |
| 2025 · 12 (diciembre) | **29.770** |

Tiene que haber **24 filas** con valor (12 meses × 2 años).

### Si tu tabla no se ve así

| Lo que ves | Causa | Arreglo |
|---|---|---|
| **Una sola fila con el año en blanco** y 475.830 | Hay relación, pero ningún `Mes` encuentra su fecha: `Mes` quedó como **texto** (pasa si hiciste el Arreglo B y no retipaste `Mes`) | Paso 0, Arreglo B, punto 3: `Mes` → Fecha con **Español (Argentina)** |
| 2025 y 2026 con **475.830 cada uno** | No hay relación entre `DIM_TIEMPO` y `HECHOS_PRESUPUESTO`, o está inactiva | 3.2: crearla desde **Administrar relaciones** y verificar **Activar esta relación** |
| Años bien, pero **enero de 2025 da 212.240** y casi no hay otros meses | `Mes` se leyó como mes/día (`01/03` = 3 de enero) | Paso 0, Arreglo B, punto 3: `Mes` con **Español (Argentina)** |

> **El límite honesto de esta relación:** si ponés el presupuesto por
> **día**, sólo vas a ver valores el día 1 de cada mes. Es correcto: el
> presupuesto no existe por día. Otra vez el grano.

---

## 🧠 Antes del corte

📍 **Vista de modelo**, pestaña `Todas las tablas`. Contá:

- Tablas de hechos: `______` (tienen que ser 3)
- Relaciones (líneas): `______`

Falta conectar **una tabla de hechos entera**. ¿Cuál?
`______________________`

**Eso es el taller.**

---

## ☕ Corte — 15 minutos

`Ctrl + S` antes de levantarte.
