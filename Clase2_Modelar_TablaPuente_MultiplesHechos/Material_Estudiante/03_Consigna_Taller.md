# Taller aplicado — Clase 2

**55 minutos · Se trabaja solo/a · Tu propio `.pbix`**

---

## Por qué no hay paso a paso

Igual que la semana pasada: **es a propósito.** La Tarea A es conectar una
tabla de hechos que tiene **el mismo grano que Ventas**. Ya conectaste Ventas
en Nivel 1. Lo que se evalúa es si podés darte cuenta de que es el mismo
caso, y resolverlo sin que te lo dicten.

Consultá al de al lado y levantá la mano. No esperes al proyector.

---

# Tarea A · Conectar `HECHOS_DEVOLUCIONES` (≈ 10 min)

**Antes de tocar nada, contestá:**

¿Cuál es el grano de `HECHOS_DEVOLUCIONES`? 1 fila = `______________________`

¿Es el mismo que el de `HECHOS_VENTAS`? **SÍ / NO**

¿Entonces necesita una tabla puente? **SÍ / NO** — ¿Por qué?

`___________________________________________________________________`

**Criterios de aceptación:**

- [ ] `HECHOS_DEVOLUCIONES` está conectada a **`DIM_TIEMPO`** (¿por qué columna?)
- [ ] `HECHOS_DEVOLUCIONES` está conectada a **`DIM_PRODUCTOS`**
- [ ] Las dos relaciones son **Uno a varios (1:\*)**, dirección **Única**,
      con la dimensión del lado uno

> ⚠️ **Puede que una ya exista.** Si en la ficha del principio encontraste
> una relación que "no creaste vos", probablemente sea ésta: Power BI la
> armó solo al cargar la tabla la semana pasada. **No la des por buena
> porque existe:** 📍 Vista de modelo → **Inicio → Administrar relaciones**
> → seleccionala → **Editar**, y verificá cardinalidad, dirección y columnas.

**¿Y con `DIM_VENDEDORES_TIENDAS`?** Intentá conectarla. ¿Por qué columna?

`___________________________________________________________________`

---

# Tarea B · La página de control (≈ 20 min)

Un modelo no se da por bueno porque "se ve lindo" en la Vista de modelo.
Se da por bueno cuando **los números cierran**.

📍 **Vista de informe** (primer ícono). Creá una página del informe llamada
**`Control`** (el **+** al lado de las pestañas de páginas) con una
**Tabla** que tenga:

| Columna de la tabla | De dónde sale |
|---|---|
| `Categoria` | **`DIM_CATEGORIA`** (no de `DIM_PRODUCTOS`) |
| Ingresos | tu medida `[Ingresos Totales]` |
| Presupuesto | `HECHOS_PRESUPUESTO[Presupuesto_Ingresos]` (*Suma de…*) |
| Unidades vendidas | `HECHOS_VENTAS[Cantidad_Vendida]` (*Suma de…*) |
| Unidades devueltas | `HECHOS_DEVOLUCIONES[Cantidad_Devuelta]` (*Suma de…*) |

**Criterios de aceptación:**

- [ ] La tabla tiene **6 filas** de categoría + la fila **Total**
- [ ] En **las cuatro columnas numéricas**, la suma de las 6 filas es igual
      a la fila Total
- [ ] Presupuesto total: **475.830**
- [ ] Unidades devueltas total: **106**

> **Por qué la columna `Categoria` tiene que salir de `DIM_CATEGORIA`:**
> es la única dimensión que llega a los **tres** hechos. Probá cambiarla por
> `DIM_PRODUCTOS[Producto_Categoria]` y mirá qué le pasa a la columna de
> Presupuesto. Anotalo:
>
> `_______________________________________________________________`

### 🔎 La pregunta que ahora se puede contestar

Con la tabla terminada, calculá a mano (sin DAX, con la calculadora):

**Tasa de devolución de Laptops** = devueltas ÷ vendidas = `______ %`

**Tasa de devolución de Accesorios** = `______ %`

¿Qué te dice eso sobre ElectroMarket?

`___________________________________________________________________`

> La semana pasada, en la ficha de auditoría, la pregunta *"de lo que
> vendimos, ¿cuánto nos volvió devuelto?"* tenía un **NO**. Mirá tu tabla.

---

# Tarea C · La matriz de bus (≈ 15 min)

Completá la matriz: poné una **X** donde el hecho está conectado a la
dimensión (directo o pasando por la puente). Mirá tu Vista de modelo, no
adivines.

| Hecho \ Dimensión | `DIM_TIEMPO` | `DIM_PRODUCTOS` | `DIM_CATEGORIA` | `DIM_VENDEDORES_TIENDAS` |
|---|:-:|:-:|:-:|:-:|
| `HECHOS_VENTAS` | | | | |
| `HECHOS_DEVOLUCIONES` | | | | |
| `HECHOS_PRESUPUESTO` | | | | |

**¿Qué dimensiones tienen X en las tres filas?**

`___________________________________________________________________`

Ésas se llaman **dimensiones conformadas**: son las únicas por las que se
pueden comparar los tres hechos a la vez.

### Tres preguntas de la Dirección Comercial

Para cada una: ¿se puede contestar con tu modelo? Si no, ¿por qué?

| Pregunta | ¿Se puede? | Por qué |
|---|---|---|
| "¿Qué vendedor tiene más devoluciones?" | SÍ / NO | |
| "¿Cuál es el presupuesto de la sucursal Norte?" | SÍ / NO | |
| "¿Cómo venimos contra presupuesto por categoría y trimestre?" | SÍ / NO | |

**Ahora escribí la regla con tus palabras.** ¿Cuándo se pueden comparar
dos tablas de hechos?

`___________________________________________________________________`

`___________________________________________________________________`

---

# Tarea D · Higiene del modelo (≈ 5 min)

- [ ] **Desactivá la detección automática de relaciones**, para que Power BI
      no vuelva a crear relaciones que nadie revisó.
      *Archivo → Opciones y configuración → Opciones → **Archivo actual** →
      Carga de datos → destildá "Detectar automáticamente nuevas relaciones
      después de cargar los datos".*
- [ ] Si `DEVOLUCIONES_HUERFANAS` aparece en la Vista de modelo, **deshabilitá
      su carga** en Power Query. Es una consulta de control, no una tabla
      del modelo. (Si Power BI la había conectado a algo, esa relación
      desaparece con ella.)
- [ ] Verificá (**Inicio → Administrar relaciones**) que **ninguna** relación
      tenga dirección **Ambos** y que no
      haya **ninguna línea punteada**.

---

# ⭐ Estiramiento opcional — una dimensión que juega dos roles

**No entra en el entregable. Hacelo sólo si terminaste las tareas A a D.**

## Qué vamos a hacer y para qué

Hoy cada tabla de hechos tiene **una sola fecha**. `HECHOS_DEVOLUCIONES`
tiene `Fecha_Devolucion`, que ya está conectada a `DIM_TIEMPO`.

Pero toda devolución tiene detrás **una venta**, y esa venta tiene su
propia fecha. Si le traemos a cada devolución la **fecha de su venta
original**, la tabla va a tener **dos fechas**, y `DIM_TIEMPO` va a tener
que cumplir dos papeles: *calendario de devoluciones* y *calendario de
ventas originales*. Eso se llama **dimensión que juega roles**
(*role-playing*).

**El resultado final** son tres cosas:

1. Una columna nueva `Fecha_Venta_Original` en `HECHOS_DEVOLUCIONES`,
   con fechas, no con "Table".
2. Una segunda relación entre `DIM_TIEMPO` y `HECHOS_DEVOLUCIONES`,
   dibujada con **línea punteada**.
3. Entender por qué es punteada.

---

## Paso 1 · Combinar (traer la venta de cada devolución)

📍 **Power Query**: **Inicio → Transformar datos**.

1. En el panel izquierdo, seleccioná la consulta **`HECHOS_DEVOLUCIONES`**.
2. **Inicio → Combinar consultas** (la opción de arriba, **no** "Combinar
   consultas como nuevas": queremos agregar una columna a esta tabla, no
   crear otra).
3. Se abre una ventana con **dos tablas**:

   | | Qué hacés |
   |---|---|
   | Tabla de arriba | ya aparece `HECHOS_DEVOLUCIONES`. Clic en el encabezado **`Ticket_ID`**, después **Ctrl + clic** en **`Producto_ID`**. Van a aparecer unos numeritos **1** y **2** en los encabezados. |
   | Desplegable de abajo | elegí **`HECHOS_VENTAS`**. Clic en **`Ticket_ID`**, después **Ctrl + clic** en **`Producto_ID`**. Tienen que quedar con el mismo **1** y **2**. |
   | Tipo de combinación | **Externa izquierda (todas de la primera, coincidencias de la segunda)** |

   > **¿Por qué dos columnas?** Un ticket puede tener varios productos. Si
   > combinamos sólo por `Ticket_ID`, una devolución de un Mouse se cruzaría
   > también con la Laptop del mismo ticket. Con ticket **y** producto, cada
   > devolución encuentra exactamente su línea de venta.

4. **Antes de aceptar**, mirá el mensaje abajo de la ventana. Tiene que
   decir que la selección coincide con **61 de las 65 filas** de la primera
   tabla. Anotá tu número: `______`
5. **Aceptar.**

**Lo que vas a ver ahora:** una columna nueva llamada `HECHOS_VENTAS`, con la
palabra **Table** en cada celda.

> **Esto es normal y todavía no terminaste.** Cada celda "Table" es una
> mini-tabla con la venta que le corresponde a esa devolución. Hay que
> **abrirla** para sacar el dato que nos interesa. Eso es el paso 2.

---

## Paso 2 · Expandir (sacar sólo la fecha de venta)

📍 Seguís en **Power Query**, en `HECHOS_DEVOLUCIONES`.

1. En el encabezado de la columna `HECHOS_VENTAS`, a la derecha del nombre,
   hay un botón con **dos flechitas que se separan** (↔). Hacé clic ahí.
2. Se abre una lista con todas las columnas de ventas:
   - Destildá **(Seleccionar todas las columnas)**.
   - Tildá **sólo `Fecha_Venta`**.
   - **Abajo de todo**, destildá **"Usar el nombre de columna original como
     prefijo"**. (Si no, la columna se va a llamar
     `HECHOS_VENTAS.Fecha_Venta`.)
3. **Aceptar.**
4. Doble clic en el encabezado de la columna nueva → renombrala
   **`Fecha_Venta_Original`**.

**Lo que tenés que ver ahora:** la columna `Fecha_Venta_Original` con
**fechas** (ya no dice "Table"), y el ícono de calendario en el encabezado.
Si el ícono es **ABC** (texto), clic derecho → **Cambiar tipo → Fecha**.

5. **Inicio → Cerrar y aplicar.**

### 📋 VERIFICÁ — Pasos 1 y 2

📍 **Vista de tabla** (segundo ícono) → tabla `HECHOS_DEVOLUCIONES`.

| Qué mirar | Tiene que dar |
|---|---|
| Filas (abajo a la izquierda) | **65**, las mismas que antes |
| Filas con `Fecha_Venta_Original` **vacía** | **4** |

> **Si tenés más de 65 filas:** el combinar **duplicó** devoluciones. Pasa
> cuando una devolución encuentra **más de una** venta que coincide (por
> ejemplo, si combinaste sólo por `Ticket_ID`). Revisá el paso 1.3.

**¿Cuáles son las 4 vacías?** Filtrá `Fecha_Venta_Original` por **(en
blanco)** y anotá los tickets:

`__________  __________  __________  __________`

Pistas:

- **Tres** ya las conocés: son las **devoluciones huérfanas** de la Clase 1.
  El ticket no existe en ventas, así que no hay fecha de venta que traer.
- **La cuarta es distinta:** su ticket **sí existe** en ventas. Buscalo en
  `HECHOS_VENTAS` y compará el `Producto_ID` de la venta con el de la
  devolución. ¿Qué pasó?

`___________________________________________________________________`

---

## Paso 3 · La segunda relación (el "rol")

📍 **Vista de modelo** → **Inicio → Administrar relaciones → + Nueva
relación…**

| Campo | Qué elegís |
|---|---|
| Primera tabla / columna | `DIM_TIEMPO` / **`Fecha`** |
| Segunda tabla / columna | `HECHOS_DEVOLUCIONES` / **`Fecha_Venta_Original`** |
| Cardinalidad | **Uno a varios (1:\*)** |
| Dirección del filtro cruzado | **Única** |

**Guardar / Aceptar.** Power BI va a dejar la relación **inactiva**: la
casilla **Activar esta relación** queda destildada, o aparece un aviso que
no te deja activarla. **Está bien: no la fuerces.**

### 📋 VERIFICÁ — Paso 3

📍 **Vista de modelo**, pestaña `Todas las tablas`. Entre `DIM_TIEMPO` y
`HECHOS_DEVOLUCIONES` ahora hay **dos líneas**:

| Línea | Columna | Cómo se ve | Estado |
|---|---|---|---|
| La de siempre | `Fecha_Devolucion` | **continua** | activa |
| La nueva | `Fecha_Venta_Original` | **punteada** | inactiva |

**¿Por qué Power BI la dibujó punteada?**

`___________________________________________________________________`

> **La respuesta:** entre dos tablas puede haber **un solo camino activo**.
> Si las dos relaciones estuvieran activas, al filtrar "marzo 2026" Power BI
> no sabría si mostrar las devoluciones **hechas** en marzo o las de ventas
> **hechas** en marzo. Por eso deja una activa (la de siempre) y la otra en
> reserva.
>
> La relación punteada **no filtra nada por sí sola**. Si hacés una tabla
> con el año de `DIM_TIEMPO` y la suma de `Cantidad_Devuelta`, vas a ver las
> devoluciones por fecha de **devolución**, aunque la otra relación exista.
> Para usar el rol "fecha de venta" hace falta una función de DAX,
> `USERELATIONSHIP`, que activa la relación punteada sólo dentro de un
> cálculo. **Eso es la Sesión 3.**

---

# Últimos 5 minutos: guardá y verificá

1. `Ctrl + S`.
2. Completá el **checklist del entregable** (documento 04).
3. Captura de la **Vista de modelo** entera, pestaña `Todas las tablas` (la vas a necesitar).
4. **Copiá el `.pbix` al pendrive / Drive.** Ya viste hoy por qué.
