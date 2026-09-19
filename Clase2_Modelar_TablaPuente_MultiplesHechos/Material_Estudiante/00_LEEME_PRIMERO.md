# Clase 2 — Leeme primero (8 minutos)

**Nivel 2 · Power BI Avanzado — ElectroMarket S.A.**
Sesión 2: *Modelar — tabla puente y múltiples hechos*

---

## La máquina se borró. Bien. Para eso armamos el parámetro.

La notebook se congeló y borró todo lo de la semana pasada. Si tu `.pbix`
intentara leer los CSV desde la carpeta de la Clase 1, ya no los
encontraría: esa carpeta no existe más.

**En la Clase 1 dijimos que esto iba a pasar, y armamos `pRutaDatos` para
esto.** Hoy vas a comprobar si funcionó.

---

## Paso 1 · Traé tu `.pbix` de la Clase 1

Del pendrive o de tu Drive personal, donde lo hayas guardado. Copialo a
`Descargas` y **todavía no lo abras**.

> ### ¿No lo tenés?
> Avisá ahora, no a los 40 minutos. En Classroom hay un
> **`Clase1_Punto_de_Partida.pbix`** con la Clase 1 terminada. Arrancás
> desde ahí y no perdés nada de hoy.

## Paso 2 · Bajá de nuevo los datos

Los datos **son los mismos de la Clase 1**: hoy no hay archivos nuevos.
Pero la máquina los borró, así que hay que volver a bajarlos.

1. En `Descargas`, creá otra vez la carpeta `ElectroMarket_Nivel2`.
2. De la entrada de Classroom **"Clase 1 — Preparar"**, bajá `Datos_Nuevos`.
3. **Clic derecho → Extraer todo** dentro de `ElectroMarket_Nivel2`.
4. Entrá a `Datos_Nuevos` y **copiá la ruta** de la barra de direcciones.

## Paso 3 · El momento de la verdad

1. Abrí tu `.pbix`.
2. Si Power BI te muestra errores de "no se encuentra el archivo":
   **perfecto, es lo esperado.** Cerralos.
3. **Inicio → Transformar datos ▾** (la flechita) **→ Editar parámetros**.
4. En `pRutaDatos` pegá la ruta nueva. **Aceptar.**
5. **Inicio → Actualizar**.

Anotá qué pasó:

| | |
|---|---|
| ¿Cuántos lugares tuviste que editar? | `______` |
| ¿Volvieron todas tus tablas? | **SÍ / NO** |

> Si pusiste **1** y **SÍ**: eso es lo que hace un parámetro. La semana
> pasada era un concepto. Hoy te ahorró reescribir seis rutas a mano.
>
> Si alguna tabla no volvió, mirá su paso `Origen`: casi seguro tiene la
> ruta escrita a mano, sin `pRutaDatos`. Arreglala ahora — es exactamente
> el problema que el parámetro evita.

---

## Qué vamos a hacer hoy

| | Bloque | Cuánto |
|---|---|---|
| 1 | Restaurar + **auditar tu Vista de modelo**, de a dos | 20 min |
| 2 | Marco: el grano, y por qué no todo se conecta igual | 15 min |
| 3 | **Demo guiada**: 3 movimientos en tu archivo | 40 min |
| 4 | Preguntas | 10 min |
| — | ☕ **Corte** | 15 min |
| 5 | **Taller**: conectás Devoluciones y validás el modelo, solo/a | 55 min |
| 6 | Puesta en común | 15 min |
| 7 | Compromiso + cierre | 10 min |

**Al final de hoy tu modelo tiene 3 tablas de hechos y 4 dimensiones
conectadas, y puede contestar una pregunta que la semana pasada no
podía:** *"de lo que vendimos, ¿cuánto nos volvió devuelto?"* — por
categoría.

**Traé la ficha de auditoría de la Clase 1.** La vamos a usar.
