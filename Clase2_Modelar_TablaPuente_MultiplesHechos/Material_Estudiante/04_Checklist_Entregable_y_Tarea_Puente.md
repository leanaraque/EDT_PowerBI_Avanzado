# Entregable de la Clase 2 + tarea puente

Nombre: ______________________________   Fecha: ____ / ____ / 2026

---

## Parte 1 · Checklist del entregable (se completa en clase)

Marcá sólo lo que **verificaste**.

### Las tablas

| Tipo | Tabla | ✔ |
|---|---|---|
| Hecho | `HECHOS_VENTAS` | ☐ |
| Hecho | `HECHOS_PRESUPUESTO` | ☐ |
| Hecho | `HECHOS_DEVOLUCIONES` | ☐ |
| Dimensión | `DIM_TIEMPO` | ☐ |
| Dimensión | `DIM_PRODUCTOS` | ☐ |
| Dimensión | `DIM_VENDEDORES_TIENDAS` | ☐ |
| Dimensión (puente) | `DIM_CATEGORIA` — **6 filas** | ☐ |

### Las 8 relaciones

| # | Desde (lado uno) | Hacia (lado varios) | ✔ |
|---|---|---|---|
| 1 | `DIM_TIEMPO[Fecha]` | `HECHOS_VENTAS[Fecha_Venta]` | ☐ |
| 2 | `DIM_PRODUCTOS[Producto_ID]` | `HECHOS_VENTAS[Producto_ID]` | ☐ |
| 3 | `DIM_VENDEDORES_TIENDAS[Vendedor_ID]` | `HECHOS_VENTAS[Vendedor_ID]` | ☐ |
| 4 | `DIM_CATEGORIA[Categoria]` | `DIM_PRODUCTOS[Producto_Categoria]` | ☐ |
| 5 | `DIM_CATEGORIA[Categoria]` | `HECHOS_PRESUPUESTO[Categoria]` | ☐ |
| 6 | `DIM_TIEMPO[Fecha]` | `HECHOS_PRESUPUESTO[Mes]` | ☐ |
| 7 | `DIM_TIEMPO[Fecha]` | `HECHOS_DEVOLUCIONES[Fecha_Devolucion]` | ☐ |
| 8 | `DIM_PRODUCTOS[Producto_ID]` | `HECHOS_DEVOLUCIONES[Producto_ID]` | ☐ |

- [ ] Las 8 son **Uno a varios (1:\*)**
- [ ] Las 8 son dirección **Única**
- [ ] **Ninguna** línea punteada (salvo la del estiramiento, si lo hiciste)
- [ ] **Ninguna** relación varios a varios
- [ ] Detección automática de relaciones **desactivada**

### La página `Control`

- [ ] Tabla por `DIM_CATEGORIA[Categoria]`, con las 4 columnas numéricas
- [ ] En las 4 columnas, la suma de las filas = el Total
- [ ] Presupuesto total **475.830** · Unidades devueltas total **106**

---

## Parte 2 · Volvé a tus dos fichas

**Ficha de la Clase 1**, pregunta 3: *"de lo que vendimos, ¿cuánto nos
volvió devuelto?"*. ¿Sigue siendo un NO? **SÍ / NO**

**Ficha de hoy**, Parte B: ¿cómo pensabas conectar el presupuesto? ¿Qué pasó
cuando lo hiciste así?

`___________________________________________________________________`

---

## Parte 3 · Tu compromiso para la próxima clase

**Con día, hora y duración. Si no, no vale.**

> El **___________ ___ / ___** , a las **______ hs**, durante
> **______ minutos**,
>
> voy a: `_____________________________________________________________`
>
> y subo a `Participantes/<Mi nombre>/` : `_____________________________`

**Decíselo en voz alta a la persona de al lado.**

---

## Parte 4 · Tarea puente (antes de la Sesión 3)

Subí a `Participantes/<Tu nombre>/`:

### 1. Captura de tu Vista de modelo (pestaña `Todas las tablas`)

Las 7 tablas y las 8 relaciones, que se vean los **1** y los **\***.
`Clase2_Modelo_<TuNombre>.png`

### 2. Un párrafo: ¿por qué Presupuesto necesitó una puente y Devoluciones no?

No más de 6 renglones. Tiene que aparecer la palabra **grano** y tiene que
estar bien usada. `Clase2_Grano_<TuNombre>.txt`

> Pista de lo que se espera: no alcanza con *"porque Presupuesto es por
> categoría"*. Explicá **qué pasaba** cuando lo conectamos directo — con el
> ejemplo del Mouse, si querés.

### 3. Tu pregunta abierta

Una sola. *"No entendí X"* vale, y es de las mejores.
`Clase2_Pregunta_<TuNombre>.txt`

---

## Antes de irte

- [ ] `Ctrl + S`
- [ ] **`.pbix` copiado al pendrive o al Drive.** Hoy empezaste la clase
      recuperándolo. La próxima también.
