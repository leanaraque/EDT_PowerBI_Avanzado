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

**No entra en el entregable.**

Una devolución tiene **fecha de devolución**… y también, en algún lado, la
**fecha de la venta original**. Si la traés, `DIM_TIEMPO` va a tener que
jugar dos papeles en la misma tabla.

1. En Power Query, en `HECHOS_DEVOLUCIONES`: **Inicio → Combinar consultas** (no
   "como nuevas") con `HECHOS_VENTAS`, usando **dos columnas a la vez**
   (Ctrl + clic): `Ticket_ID` y `Producto_ID`, en el mismo orden en las
   dos tablas. **Tipo de combinación: Externa izquierda**.
2. Expandí y quedate sólo con `Fecha_Venta`. Renombrala
   `Fecha_Venta_Original`.
3. **Verificá dos números:**
   - `HECHOS_DEVOLUCIONES` tiene que **seguir en 65 filas**. Si subió, el
     combinar duplicó devoluciones. ¿Por qué podría pasar eso?
   - ¿Cuántas filas quedaron **sin** fecha de venta? `______` ¿Cuáles son?
     (Pista: las conociste la semana pasada.)
4. En la Vista de modelo, **Inicio → Administrar relaciones → Nueva relación**:
   `DIM_TIEMPO[Fecha]` →
   `HECHOS_DEVOLUCIONES[Fecha_Venta_Original]`. **Mirá la línea.** ¿Por qué
   Power BI la dibujó distinta?

`___________________________________________________________________`

---

# Últimos 5 minutos: guardá y verificá

1. `Ctrl + S`.
2. Completá el **checklist del entregable** (documento 04).
3. Captura de la **Vista de modelo** entera, pestaña `Todas las tablas` (la vas a necesitar).
4. **Copiá el `.pbix` al pendrive / Drive.** Ya viste hoy por qué.
