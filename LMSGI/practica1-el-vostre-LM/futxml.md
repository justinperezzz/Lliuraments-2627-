# Pràctica 1

# FUTXML: un lenguaje de marcas para el fútbol

**Módulo:** Lenguajes de marcas (LMSGI) · **Curso:** ASIX
**Integrantes:** Kaw, Ayman y Justin

---

## 1. Introducción a los lenguajes de marcas

### ¿Qué son?

Un lenguaje de marcas sirve para **organizar información usando etiquetas**. Las etiquetas se escriben dentro del texto y dicen **qué es** cada dato. Por ejemplo, en HTML:

```html
<h1>Mi página</h1>
<p>Esto es un párrafo.</p>
```

Aquí `<h1>` indica que "Mi página" es un título y `<p>` indica que lo otro es un párrafo.

No son lenguajes de programación: no hacen cálculos ni ejecutan instrucciones, solo describen datos.

### Un poco de historia

- A finales de los años 60, IBM creó **GML** para poder reutilizar documentos en diferentes sistemas.
- En 1986 apareció **SGML**, que fue el estándar en el que se basaron los siguientes.
- En 1991 se creó **HTML**, para hacer páginas web.
- En 1998 salió **XML**, una versión más sencilla de SGML para guardar y compartir datos.

### ¿Para qué se usan?

- Para hacer **páginas web** (HTML).
- Para **guardar e intercambiar datos** entre programas (XML).
- Para escribir **documentos con formato** de forma sencilla (Markdown).

### Requisitos que debe cumplir

Según el enunciado, para ser un lenguaje de marcas tiene que:

1. Basarse en **texto plano**.
2. Usar **metadatos**.
3. Facilitar que un **programa procese los datos** automáticamente.
4. Facilitar la **representación o interpretación** de los datos guardados.

---

## 2. Nuestro lenguaje: FUTXML

**FUTXML** es un lenguaje que hemos inventado para **guardar datos de partidos de fútbol**: equipos, fecha, estadio, goles y competición.

Se parece a XML, porque también usa etiquetas con apertura y cierre. Por ejemplo:

```xml
<equipo>Real Madrid</equipo>
```

La etiqueta `<equipo>` nos dice que "Real Madrid" es el nombre de un equipo.

### Reglas del lenguaje

| N.º | Regla | Explicación |
|---|---|---|
| 1 | Etiquetas | Todo elemento se abre y se cierra: `<fecha>...</fecha>`. |
| 2 | Elemento raíz | Todo el partido va dentro de `<partido>`. |
| 3 | Datos obligatorios | Hay que poner equipo local, equipo visitante, fecha y goles. El estadio es opcional. |
| 4 | Metadatos | La temporada y la competición se ponen como atributos de `<partido>`, entre comillas. |
| 5 | Orden correcto | Las etiquetas se cierran en orden: la última que se abre es la primera que se cierra. |
| 6 | Texto plano | Se escribe en un archivo de texto, por ejemplo `partido.xml`. |

### Ejemplos de errores

**Falta una etiqueta de cierre (regla 1):**

```xml
<fecha>2026-10-25
```

**Atributos sin comillas (regla 4):**

```xml
<partido temporada=2026-2027 competicion=Liga>
```

**Etiquetas mal ordenadas (regla 5):**

```xml
<equipo_local>
  <nombre>Real Madrid</equipo_local>
</nombre>
```

---

## 3. Clasificación de FUTXML

FUTXML es un lenguaje **descriptivo**.

- **Es descriptivo** porque sus etiquetas explican qué significa cada dato (`<fecha>`, `<goles>`, `<nombre>`...).
- **No es procedimental**, porque no tiene instrucciones que se ejecuten, solo guarda datos.
- **No es de presentación**, porque no dice cómo se ve el partido en pantalla (colores, tamaños, etc.).

---

## 4. Caso de uso en el que sí sirve

FUTXML se podría usar en una **aplicación de resultados de fútbol**. Cada partido se guardaría en un archivo y la aplicación lo leería para mostrar:

| Local | Visitante | Resultado |
|---|---|---|
| Real Madrid | Barcelona | 2 - 1 |

Con los datos guardados así, la aplicación podría:

- Buscar los partidos de un equipo.
- Ver los resultados de una temporada concreta.
- Compartir los datos con otros programas que entiendan el formato.

---

## 5. Ejemplo de uso

Este es un partido escrito en FUTXML:

```xml
<partido temporada="2026-2027" competicion="Liga">
  <fecha>2026-10-25</fecha>
  <estadio>Bernabeu</estadio>
  <equipo_local>
    <nombre>Real Madrid</nombre>
    <goles>2</goles>
  </equipo_local>
  <equipo_visitante>
    <nombre>Barcelona</nombre>
    <goles>1</goles>
  </equipo_visitante>
</partido>
```

### Explicación

- `<partido temporada="2026-2027" competicion="Liga">` abre el partido. La temporada y la competición son los **metadatos**: datos sobre el partido.
- `<fecha>` guarda el día del partido y `<estadio>` dónde se juega.
- `<equipo_local>` agrupa el nombre y los goles del equipo que juega en casa.
- `<equipo_visitante>` hace lo mismo con el equipo de fuera.
- `</partido>` cierra el partido.

### Cómo se interpretaría

Un programa que lea este archivo podría mostrar el resultado así:

> **Real Madrid 2 - 1 Barcelona** (Liga 2026-2027, estadio Bernabeu, 25/10/2026)

### Cómo lo hemos comprobado

Hemos pegado el código en un validador XML online y nos ha dicho que estaba bien escrito. También hemos probado el ejemplo incorrecto de las etiquetas mal ordenadas y nos ha dado un error.

---

## 6. Caso de uso en el que no sirve

FUTXML **no sería adecuado para hacer un videojuego de fútbol**. Solo puede guardar los datos de un partido, pero un videojuego necesita:

- Gráficos y animaciones de los jugadores.
- Programar cómo se mueve el balón.
- Controlar lo que hace el jugador con el mando.

Para eso hace falta un lenguaje de programación y un motor de videojuegos. FUTXML solo podría guardar los resultados.

---

## 7. ¿Por qué FUTXML es un lenguaje de marcas?

- **Texto plano:** los datos se escriben como texto, así que se pueden abrir con cualquier editor.
- **Metadatos:** la temporada y la competición son atributos que dan información sobre el partido.
- **Procesamiento automático:** como las etiquetas siempre siguen las mismas reglas, un programa puede encontrar cada dato (por ejemplo, los goles) y usarlo.
- **Interpretación:** cada etiqueta indica qué es cada dato, así que se puede mostrar como un marcador o una tabla.

Por todo esto, FUTXML cumple los cuatro requisitos y se puede considerar un lenguaje de marcas.
