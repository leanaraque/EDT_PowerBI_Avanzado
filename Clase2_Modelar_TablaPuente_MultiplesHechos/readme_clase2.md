# Clase 2 · Modelar — Tabla puente y múltiples hechos

**Nivel 2 · Power BI Avanzado — ElectroMarket S.A., Expansión Nacional**
**180 minutos · corte de 15 min · hasta 12 estudiantes/grupos**

Kit completo de la Sesión 2 del programa (`../Programa_8_Clases.md`).

---

## Qué se lleva el estudiante

| | |
|---|---|
| **Entregable** | Modelo de **7 tablas** (3 hechos + 4 dimensiones) y **8 relaciones** 1:N, Única, sin ambigüedad. Página `Control` que valida que los números cierran. |
| **Hallazgo** | **1 de cada 5 laptops se devuelve** (21,8 %, contra 1,6 % de accesorios). Una pregunta que la semana pasada no se podía contestar. |
| **Tarea puente** | Captura del modelo + un párrafo sobre por qué Presupuesto necesitó puente y Devoluciones no (con la palabra *grano* bien usada) + 1 pregunta. |

**Lo que se aprende (el mecanismo):** *se puede subir el grano (sumar), no
se puede bajar sin inventar una regla.* Cardinalidad, puente, dirección del
filtro y dimensiones conformadas son consecuencias de esa frase.

---

## Contenido

```
03_Clase2_Modelar_TablaPuente_MultiplesHechos/
├── README_Clase2.md                  ← este archivo
├── Guion_Instructor_Clase2.md        ← 📕 EMPEZÁ POR ACÁ
├── Clase2_Presentacion.pptx          ← 27 diapositivas + notas del orador
├── Clase2_Pizarra.excalidraw         ← 5 escenas (excalidraw.com)
├── Material_Estudiante/              ← ⬆️ A CLASSROOM (.docx)
│   ├── 00_LEEME_PRIMERO                 recuperar el .pbix: el parámetro paga
│   ├── 01_Ficha_Auditoria_Modelo        🖨️ IMPRIMIR
│   ├── 02_Guia_Paso_a_Paso_Clase2       los 3 movimientos
│   ├── 03_Consigna_Taller               sin paso a paso, a propósito
│   └── 04_Checklist_Entregable_y_Tarea_Puente
├── Solucion_Instructor/              ← 🔒 NO REPARTIR
│   ├── Cifras_de_Control.md
│   ├── Relaciones_Esperadas.md          las 8 relaciones + matriz de bus
│   ├── M_01_DIM_CATEGORIA.pq            la puente
│   └── M_02_Estiramiento_RolePlaying.pq
└── _fuentes/
    ├── calcular_cifras_clase2.py        recalcula todo desde los CSV
    ├── construir_presentacion_clase2.py
    └── construir_pizarra_clase2.py
```

**Datos: los mismos de la Clase 1** (`../02_Clase1_.../Datos_Nuevos/`). Hoy
no hay archivos nuevos.

---

## ⚠️ Lo único que tenés que hacer vos antes de la clase

**Crear `Clase1_Punto_de_Partida.pbix` y subirlo a Classroom**: tu `.pbix`
al final de la Clase 1. Es el plan de rescate para quien llegue sin archivo,
y no lo puedo generar: un `.pbix` sólo sale de Power BI Desktop. El resto
del checklist está en el guion.

---

## Decisiones de diseño

**Se empieza por el error, no por la solución.** El Movimiento 1 conecta el
presupuesto *exactamente como los estudiantes proponen* (por categoría,
directo) para que vean el daño con sus números: el Mouse "cumple el 21 %
de un objetivo" que no es suyo. La puente se entiende porque primero se
vio por qué hace falta.

**La puente se construye con el método de Nivel 1**, no con el que decía el
programa. En la Semana 7 de Nivel 1 la armaron *anexando* el campo común de
las dos tablas y quitando duplicados. Es más robusto (cubre una categoría
presupuestada que todavía no tiene productos) y es lo que ya saben.

**La tabla que dice 475.830 en todas las filas es contenido, no un bug.**
Es el modelo diciendo "no sé": el presupuesto no existe por producto. Es el
punto de partida de la Sesión 3.

**El parámetro de la Clase 1 se cobra en el minuto 0.** La máquina borró
todo; cambian un solo valor y el modelo vuelve. Es el cierre andragógico de
la Clase 1.

---

## Correcciones a la Clase 1 que surgieron al armar ésta

Aplicadas al kit de la Clase 1 (para futuras cohortes) y tratadas en el
guion de hoy como correcciones en voz alta:

1. **`Inicio_Mes` no sirve para relacionar el presupuesto.** El código de
   referencia decía que sí. Se repite ~30 veces por mes: no puede ser lado
   "uno". La relación correcta es `DIM_TIEMPO[Fecha]` → `HECHOS_PRESUPUESTO[Mes]`.
   (Los estudiantes no tienen esa columna: su `DIM_TIEMPO` es la de la guía
   de Nivel 1. El error sólo pudo llegarles si se dijo en voz alta.)
2. **Mayúsculas: el consejo era correcto, el motivo no.** El modelo de
   Power BI no distingue mayúsculas; Power Query sí. Lo que se rompe es la
   **puente** (dos filas en Power Query, un duplicado para el modelo), no
   una relación directa.
3. **`M_03` de la Clase 1 seleccionaba una columna que el Taller B borra**
   → la consulta de huérfanas habría dado error al refrescar. Corregido.

---

## Pendiente para la Sesión 3 (importante)

La medida `Utilidad vs Presupuesto` del programa usa `TREATAS` con
`VALUES(DIM_PRODUCTOS[Producto_Categoria])`. En una fila de **producto**,
eso trae el presupuesto de **toda su categoría**: es el mismo error del
Movimiento 1 de hoy, escrito en DAX. Al armar la Clase 3 hay que decidir
qué devuelve la medida por debajo del grano de categoría. Lo coherente con
lo que se enseña hoy: **en blanco**.
