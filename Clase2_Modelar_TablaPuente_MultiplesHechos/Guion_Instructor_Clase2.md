# Guion del instructor — Clase 2

**Nivel 2 · Power BI Avanzado — ElectroMarket S.A.**
**Sesión 2 · Modelar: tabla puente y múltiples hechos**
**180 minutos · corte de 15 min · hasta 12 estudiantes/grupos**

---

## Lo que tiene que pasar hoy, en una frase

> Que cada uno **vea con sus propios números** qué pasa cuando conecta dos
> tablas de distinto grano como si fueran iguales, y salga con un modelo de
> 3 hechos y 4 dimensiones que **no miente**.

**Objetivo de aprendizaje real (el mecanismo):** *se puede subir el grano
(sumar), no se puede bajar sin inventar una regla.* Todo lo demás de hoy
—cardinalidad, puente, dirección del filtro, dimensiones conformadas— es
consecuencia de esa frase. Si al final alguien puede explicar por qué el
Mouse "no tiene presupuesto", la clase funcionó.

---

## Reparto del tiempo

| Bloque | Min | Reloj | Tipo | Quién habla |
|---|---|---|---|---|
| 1 · Restaurar + auditar la Vista de modelo | 20 | 00–20 | Autónomo | Ellos |
| 2 · Marco: grano, cardinalidad, dirección | 15 | 20–35 | Facilitador | **Vos** |
| 3 · Demo guiada — los 3 movimientos | 40 | 35–75 | Guiado | Vos guiás, ellos hacen |
| 4 · Preguntas v1 (anónimas) | 10 | 75–85 | Autónomo | Ellos |
| ☕ **Corte** | 15 | 85–100 | — | — |
| 5 · Taller aplicado | 55 | 100–155 | Autónomo | Ellos |
| 6 · Puesta en común | 15 | 155–170 | Autónomo | Ellos |
| 7 · Compromiso + cierre | 10 | 170–180 | Autónomo | Ellos |

**Vos al frente: 15 de 165 minutos (9 %).** Igual que la Clase 1.

---

## Checklist del instructor — la noche anterior

- [ ] **Crear `Clase1_Punto_de_Partida.pbix` y subirlo a Classroom.**
      Es tu propio `.pbix` al final de la Clase 1 (6 tablas, 3 parámetros,
      **sin** relaciones nuevas). No lo puedo generar yo: un `.pbix` sólo
      sale de Power BI Desktop. Es el plan de rescate de hoy, y vale oro:
      el que llega sin archivo arranca en 30 segundos en vez de perder la
      clase.
      > Antes de subirlo: **dejá `pRutaDatos` apuntando a una carpeta
      > cualquiera**. El estudiante que lo use igual va a tener que
      > cambiarla — y es exactamente el ejercicio del Paso 0.
- [ ] Verificar que la entrada **"Clase 1 — Preparar"** de Classroom sigue
      teniendo `Datos_Nuevos` para descargar (hoy no hay datos nuevos).
- [ ] `Material_Estudiante/` de hoy subido a Classroom.
- [ ] **Imprimir `01_Ficha_Auditoria_Modelo`**, 1 por estudiante + 3.
- [ ] Recordarles por mensaje: **traer la ficha de auditoría de la Clase 1**.
- [ ] **Leer las tareas puente de la Clase 1** y armar la lista de
      *preguntas abiertas* (se lee en el bloque 1). Y el pizarrón "parking".
- [ ] Tu `.pbix` de demo **en el estado de fin de la Clase 1**, proyectado
      al 150 %.
- [ ] `Cifras_de_Control.md` y `Relaciones_Esperadas.md` abiertos en una
      ventana que **no** proyectes.
- [ ] `Clase2_Pizarra.excalidraw` cargado en excalidraw.com.

---

# BLOQUE 1 · 00–20 · Restaurar + auditar

## 00–08 · "La máquina se borró. Bien." — el pago del parámetro

Diapositiva 3 proyectada. Documento `00_LEEME_PRIMERO`.

> *"La semana pasada les dije que esta máquina iba a borrar todo. Lo hizo.
> Hoy vamos a comprobar si lo que armamos sirvió."*

Bajan otra vez `Datos_Nuevos`, abren su `.pbix`, cambian **un** valor en
`pRutaDatos`, actualizan.

**Cuando la mayoría haya terminado, pedí las manos:**

> *"¿Cuántos lugares tuvieron que editar?"* → **uno**.
> *"¿Y si no hubiéramos hecho el parámetro?"* → seis, o más.

Diez segundos, en voz alta. **Es el momento en que el parámetro deja de ser
un concepto de la clase pasada.** Knowles: el adulto valora lo que le
resolvió un problema propio. No lo apures.

| Síntoma | Qué hacés |
|---|---|
| No trajo el `.pbix` | `Clase1_Punto_de_Partida.pbix` de Classroom. 30 segundos. |
| "Actualicé y una tabla sigue con error" | Esa consulta tiene la ruta escrita a mano. **Es el mejor error posible hoy:** que lo arregle con `pRutaDatos` ahí mismo. |
| Descarga lenta | Pendrive. Minuto 5, sin debate. |

## 08–20 · Auditar la Vista de modelo (ficha, de a dos)

Ficha `01_Ficha_Auditoria_Modelo`, **en papel**. Parte A: inventario de
tablas y relaciones. Parte B: su intuición de la semana pasada sobre cómo
conectar el presupuesto.

### Lo que vas a encontrar (anticipalo, no lo digas)

**Relaciones que nadie creó.** Al cargar `HECHOS_DEVOLUCIONES` la semana
pasada, la detección automática probablemente conectó
`DIM_PRODUCTOS[Producto_ID]` → `HECHOS_DEVOLUCIONES[Producto_ID]` (mismo
nombre de columna). Y quizás `DEVOLUCIONES_HUERFANAS` también.

> **Ése es el hallazgo del bloque.** Cuando alguien diga *"hay una relación
> que no hice"*: *"¿Y la revisaste? ¿Sabés qué cardinalidad tiene?"*. Se
> resuelve en el taller (Tarea D).

### Cierre del bloque (3 min)

Anotá en el pizarrón las **propuestas de conexión** de la Parte B. La
mayoría va a decir *"por la categoría, directo"*. **No los corrijas.**
Escribí la propuesta más votada con un círculo:

> *"Ésta. Es la que vamos a probar primero."*

Y leé 2 o 3 **preguntas abiertas de la tarea puente** de la Clase 1.
Contestá las cortas; las de hoy, al parking con su nombre.

---

# BLOQUE 2 · 20–35 · Marco conceptual

**15 minutos. El único bloque donde hablás vos.** Diapositivas 6 a 10 +
Excalidraw escenas 1 y 2.

### 1 · Una fila, ¿de qué? (5 min) — la idea madre

Escena 1 de Excalidraw. **Dibujala en vivo.**

| Tabla | Una fila es… |
|---|---|
| `HECHOS_VENTAS` | una línea de ticket: **día × producto × vendedor** |
| `HECHOS_DEVOLUCIONES` | una devolución: **día × producto** |
| `HECHOS_PRESUPUESTO` | un objetivo: **mes × categoría** |

> *"Eso se llama **grano**. Y hay una regla que no tiene excepciones:
> **se puede subir el grano, no se puede bajar.** De ventas por día puedo
> sacar ventas por mes: sumo. Del presupuesto por mes, ¿puedo sacar el
> presupuesto del 14 de marzo? ¿Del Mouse? No: tendría que inventar cómo
> repartirlo."*

### 2 · El lado "uno" tiene que ser único (5 min)

> *"Toda relación que conocen de Nivel 1 es 1:N. El 1 es la dimensión: cada
> producto aparece **una** vez en `DIM_PRODUCTOS`. Si en los dos lados los
> valores se repiten, no hay lado uno, y Power BI arma otra cosa: un
> **varios a varios**. Hoy vamos a ver qué hace."*

### 3 · El filtro baja por la flecha (3 min)

Escena 2 de Excalidraw: la flecha va del 1 al \*. El filtro viaja **en esa
dirección**, como el agua. De una dimensión hacia los hechos. No sube.

> *"Esto va a explicar el resultado más raro de la clase. Guárdenlo."*

### 4 · Colchón (2 min)

### Lo que NO se dice hoy

- ❌ **Dirección "Ambos"** como solución. Si alguien la propone: *"funciona,
  y con tres tablas de hechos es la forma más rápida de tener un modelo
  ambiguo. La Sesión 3 lo resuelve con DAX, sin romper nada."* Al parking.
- ❌ **`TREATAS`, `CALCULATE`**: Sesión 3.
- ❌ **Role-playing** en detalle: una frase (*"a veces una tabla tiene dos
  fechas; hay un estiramiento opcional en el taller"*) y listo.

---

# BLOQUE 3 · 35–75 · Demo guiada — los 3 movimientos

Guía `02_Guia_Paso_a_Paso_Clase2`. **Cada movimiento cierra con números.**

## Movimiento 1 · La tentación (35–47, 12 min)

**Hacé exactamente lo que propusieron en el pizarrón.** Señalá el círculo:

> *"Lo que ustedes propusieron. Vamos."*

`DIM_PRODUCTOS[Producto_Categoria]` → `HECHOS_PRESUPUESTO[Categoria]`.
Aparece **Varios a varios** y un aviso amarillo. **Leelo en voz alta.**
Aceptá igual, dirección Única de Productos a Presupuesto.

Tabla en `Laboratorio`: `Producto_Nombre` + `Presupuesto_Ingresos` +
`[Ingresos Totales]`.

✅ **Verificación:** los 4 accesorios dicen **50.120**; el total dice
**475.830**; las filas suman **626.190**.

**El momento del Mouse — hacelo despacio:**

> *"El Mouse facturó unos 10.450. Esta tabla dice que su objetivo era
> 50.120. ¿Qué concluye un gerente? Que el Mouse cumplió el 21 %. Que hay
> que discontinuarlo. (pausa) ¿Cuál es el objetivo del Mouse?"*

Dejá que contesten. Alguien va a decir *"50.120"*. Otro *"no sé"*.

> *"El que dijo 'no sé' tiene razón. 50.120 es el objetivo de los cuatro
> accesorios juntos. **Nadie le puso objetivo al Mouse.** Y este tablero lo
> inventó, sin avisar, con una tipografía prolija."*

Eliminá la relación. **Dejá la tabla.**

## Movimiento 2 · La puente (47–63, 16 min)

**El gancho con Nivel 1 — decilo literal:**

> *"Esto ya lo resolvieron. Semana 7 de Nivel 1, el ejercicio de reclamos:
> 'cuando hay un muchos a muchos, identifico el campo en común y creo la
> tabla puente a partir de él'. Hoy es el mismo problema, en su propio
> caso."*

Dos referencias, **anexar COMO NUEVAS**, quitar duplicados.

❗ **Remarcá el contraste con la Clase 1**, porque ya hubo confusión con
instrucciones parecidas: *"La semana pasada era 'Anexar consultas', NO como
nuevas. Hoy SÍ es como nuevas. ¿Por qué la diferencia?"*. Que contesten.

✅ **Verificación: `DIM_CATEGORIA` = 6 filas.**

❗ **Si a alguien le da 12:** es la trampa de las mayúsculas. **Es el mejor
error de la clase, usalo:**

> *"Power Query distingue mayúsculas: para él son dos categorías. El modelo
> de Power BI no: para él es la misma, repetida. Si llevás esto al modelo,
> no te deja crear la relación. Dos motores, dos reglas."*

> 📌 **Corrección a lo que se dijo en la Clase 1:** la consigna del taller
> decía que con mayúsculas "la relación no va a encontrar nada". El
> **consejo** era correcto; el **motivo** no. El modelo no distingue
> mayúsculas, así que una relación *directa* sí matchearía. Lo que se
> rompe es la **puente** (este caso). Si alguien lo recuerda, reconocelo
> sin vueltas: *"lo expliqué mal la semana pasada, así es como funciona"*.
> Un instructor que corrige en voz alta enseña más que uno que nunca se
> equivoca.

Conectar la puente: dos relaciones **desde** `DIM_CATEGORIA`, las dos 1:\*.

Volver a la tabla del `Laboratorio`:

- Por **Categoria**: correcto, suma = total.
- Por **Producto_Nombre**: **todas las filas dicen 475.830.**

**El segundo momento fuerte:**

> *"Parece roto. No lo está. El filtro baja por la flecha (escena 2): de
> Categoría a Productos, de Categoría a Presupuesto. Un filtro puesto en
> Productos **no puede subir** a Categoría para bajar después al
> presupuesto. El modelo no inventa: te dice 'no sé'. Un modelo que dice
> 'no sé' es mejor que uno que miente con seguridad."*

## Movimiento 3 · El calendario (63–75, 12 min)

> *"El presupuesto es mensual. ¿Con qué columna de `DIM_TIEMPO` lo unimos?"*

La intuición: con una columna de mes. Pregunta a la sala:

> *"¿Cuántas veces aparece enero en `Month Name`?"* → **62** (31 días ×
> 2 años). (Según el idioma de su Power BI, dice `enero` o `January`.) *"¿Puede ser el lado uno?"* → No.

> **Si tu `.pbix` de demo tiene `Inicio_Mes`** (lo tiene si armaste
> `DIM_TIEMPO` con el código de referencia de la Clase 1), **arrastrala
> sobre `Mes` en vivo**: Power BI propone *Varios a varios*. Cancelá. Es
> la demostración más clara. Los estudiantes **no** tienen esa columna:
> su `DIM_TIEMPO` es la de la guía de Nivel 1 (`Year`, `Quarter`, `Month`,
> `Month Name`).
>
> 📌 **Corrección a la Clase 1:** en el código de referencia de la Clase 1
> se decía que `Inicio_Mes` era "por donde se enganchaba el presupuesto".
> Era falso, por exactamente esta razón. Si lo dijiste en voz alta, hoy es
> el momento de corregirlo.

La correcta: `DIM_TIEMPO[Fecha]` → `HECHOS_PRESUPUESTO[Mes]`. Funciona
porque `Mes` siempre es día 1, y el día 1 existe una sola vez.

✅ **Verificación:** por año, **2025 = 214.280**, **2026 = 261.550**.

Cierre del movimiento: *"Falta conectar una tabla de hechos entera. Es el
taller."*

---

# BLOQUE 4 · 75–85 · Preguntas v1

Mismo formato que la Clase 1: **2 minutos en silencio, un papel, anónimo.**
Leés vos.

> **Promesa pendiente de la Clase 1:** el código de referencia decía que si
> nadie lograba `fnLimpiarFecha`, "se retoma como demo en la Sesión 2". Si
> alguien la pide en las preguntas, mostrala 3 minutos (`M_07` de la
> Clase 1). Si nadie la pide, no le robes tiempo al taller: ofrecela como
> material para quien termine antes.

---

# ☕ 85–100 · CORTE

`Ctrl + S`. Volvés a horario.

---

# BLOQUE 5 · 100–155 · Taller aplicado

**55 minutos. Solos. No explicás al frente.**

| Tarea | Min | Qué | Verificación |
|---|---|---|---|
| A | 10 | Conectar `HECHOS_DEVOLUCIONES` | 2 relaciones 1:\* |
| B | 20 | Página `Control` por `DIM_CATEGORIA` | presupuesto 475.830 · devueltas 106 · filas = total |
| C | 15 | Matriz de bus + 3 preguntas | ver `Relaciones_Esperadas.md` |
| D | 5 | Higiene: autodetección off, huérfanas sin cargar | sin punteadas, sin "Ambos" |
| — | 5 | Guardar, checklist, captura | |
| ⭐ | — | Role-playing (opcional) | 65 filas · 3 sin fecha · línea punteada |

### Tu trabajo: preguntar, no resolver

La misma secuencia de la Clase 1: *¿Qué número te dio? ¿Cuál tendría que
darte? ¿En qué paso se te fue?*

### Las trampas del taller

| Síntoma | Pregunta que hacés |
|---|---|
| Quiere conectar Devoluciones a Vendedores | *"¿Qué columna de Devoluciones usarías?"* (no hay) |
| La columna Presupuesto de la tabla `Control` repite 475.830 | *"¿De qué tabla sacaste `Categoria`?"* (de `DIM_PRODUCTOS`, no de la puente) |
| Filas que no suman el total | *"¿Hay alguna relación en Ambos, o alguna punteada?"* |
| Se da cuenta de que Laptops devuelve 21,8 % | **No digas nada. Anotá su nombre.** Es quien abre la puesta en común. |

### Marcas de tiempo en voz alta

- **Min 110:** *"Devoluciones conectada. Si no, pedí ayuda ahora."*
- **Min 130:** *"Página de control terminada, pasen a la matriz."*
- **Min 145:** *"Higiene y guardar."*

---

# BLOQUE 6 · 155–170 · Puesta en común

**No se recorta nunca.**

### 1 · El hallazgo (5 min)

Abre quien encontró la tasa de devolución de Laptops (lo anotaste en el
taller). Si nadie la calculó, pedilo en vivo: *"Laptops: devueltas sobre
vendidas."* → **21,8 %** contra **1,6 %** de accesorios.

> *"Una de cada cinco laptops vuelve. La semana pasada esta pregunta tenía
> un NO en su ficha. Hoy la contestaron. Eso hizo el modelo."*

No adelantes la historia del margen (es el premio de la Sesión 4). Si
alguien la intuye: *"guardala, la vamos a probar con números."*

### 2 · "¿Cuál es el presupuesto del Mouse?" (6 min)

La pregunta central de la clase. **Dejá que discutan.** Van a aparecer:

| Propuesta | Lo que supone (decilo vos al final) |
|---|---|
| 50.120 | que tiene el objetivo de toda la categoría |
| 12.530 (50.120 ÷ 4) | que los 4 accesorios pesan igual |
| proporcional a lo vendido | que el pasado define el objetivo |

> *"Las tres son reglas de reparto. Legítimas si alguien del negocio las
> decide y las firma. Pero **no son un dato**. El presupuesto del Mouse no
> existe. Bajar el grano siempre es inventar una regla; subirlo, no."*

### 3 · La regla de la matriz de bus (4 min)

Que alguien lea su regla de la Tarea C. La que tiene que quedar:

> **"Dos hechos se comparan sólo por las dimensiones que comparten, y sólo
> a un grano igual o más grueso que el del más grueso de los dos."**

---

# BLOQUE 7 · 170–180 · Compromiso y cierre

1. **Las dos fichas (3 min).** Clase 1, pregunta 3: se tacha. Ficha de hoy,
   Parte B: *"¿cómo pensaban conectar el presupuesto, y qué pasó?"*.
2. **Compromiso (5 min)**, con día y hora, dicho en voz alta.
3. **Cierre (2 min):**

> *"Hoy no aprendieron un botón. Aprendieron a preguntarse 'una fila, ¿de
> qué?' antes de conectar nada. Esa pregunta los va a salvar en cualquier
> herramienta de datos que toquen."*

Y: **pendrive o Drive antes de irse.** Hoy empezaron la clase por eso.

---

# Seguimiento

| Cuándo | Qué |
|---|---|
| **+48 hs** | Mensaje breve en `Participantes/`: qué salió, qué se trabó. |
| **+4 días** | Leer las tareas puente. **Revisar el párrafo del grano**: es el mejor termómetro de si la clase funcionó. Los que confundan grano con "categoría" necesitan un minuto al inicio de la Sesión 3. |
| **Inicio Sesión 3** | Leer las preguntas abiertas y el parking. Y retomar la tabla de `Producto_Nombre` que dice 475.830 en todas las filas: **es el punto de partida de la Sesión 3.** |

---

# Contingencias

| Si pasa esto | Hacés esto |
|---|---|
| Más de 3 sin `.pbix` | Todos con `Clase1_Punto_de_Partida.pbix`. Por eso existe. |
| Alguien no llega a 6 filas en `DIM_CATEGORIA` y el tiempo corre | Que siga con la demo mirando al compañero; lo arregla en el taller (Tarea D tiene 5 min de colchón). |
| Vas atrasado al corte | Recortá el Movimiento 3 a lo esencial (relación correcta + verificación). La trampa del mes se puede contar en 1 minuto sin hacerla. |
| El taller se estira | Sacá la Tarea C del taller y mandala como tarea puente. **La puesta en común no se toca.** |
| Alguien pone "Ambos" para que la tabla por producto "ande" | *"Funciona. Y te acabo de mostrar por qué no quiero que funcione."* Llevalo al Movimiento 1. |
| Power BI no deja crear la relación de la puente | 99 %: `DIM_CATEGORIA` con más de 6 filas. Ver `M_01`. |

---

## Materiales

```
03_Clase2_Modelar_TablaPuente_MultiplesHechos/
├── Guion_Instructor_Clase2.md          ← este documento
├── Clase2_Presentacion.pptx            ← proyector
├── Clase2_Pizarra.excalidraw           ← 5 escenas para dibujar en vivo
├── Material_Estudiante/                ← A CLASSROOM
├── Solucion_Instructor/                ← NO repartir
│   ├── Cifras_de_Control.md
│   ├── Relaciones_Esperadas.md
│   ├── M_01_DIM_CATEGORIA.pq
│   └── M_02_Estiramiento_RolePlaying.pq
└── _fuentes/
```

Datos: **los mismos de la Clase 1** (`02_Clase1_.../Datos_Nuevos/`).
