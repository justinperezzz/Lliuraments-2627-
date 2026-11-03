# Pràctica 1: Característiques dels llenguatges de marques

# FUTXML: un lenguaje de marcas para el mundo del fútbol

**Módulo:** Lenguajes de marcas (LMSGI) · **Curso:** ASIX
**Integrantes:** Kaw · Ayman · Justin

---

## Índice

1. [Introducción a los lenguajes de marcas]
2. [FUTXML y sus reglas]
3. [Clasificación de FUTXML]
4. [Caso de uso adecuado]
5. [Ejemplo de uso explicado]
6. [Caso de uso inadecuado]
7. [¿Por qué FUTXML es un lenguaje de marcas?]

---

## 1. Introducción a los lenguajes de marcas

### ¿Qué son?

Un **lenguaje de marcas** es una forma de **organizar y describir información mediante etiquetas** (marcas) escritas dentro del propio texto. Las etiquetas no son los datos: sirven para indicar **qué significa** cada dato o **cómo está estructurado** el documento.

### Características principales

| Característica | Explicación |
|---|---|
| **Texto plano** | Los datos se guardan como texto legible, sin formatos binarios. Se pueden abrir con cualquier editor (Bloc de notas, nano, VS Code...). |
| **Etiquetas** | Identifican qué significa cada dato. |
| **Automatización** | Un programa puede leer y procesar la información fácilmente. |
| **Representación** | Facilitan mostrar o interpretar los datos almacenados. |

### Orígenes 

- **Años 60:** IBM crea **GML**  para poder reutilizar documentos en distintos sistemas.
- **1986:** GML se convierte en el estándar **SGML**, la base de los lenguajes de marcas posteriores.
- **1991:** Tim Berners-Lee crea **HTML** para estructurar páginas web.
- **1998:** el W3C publica **XML**, una versión simplificada de SGML para guardar e intercambiar datos.

### ¿Para qué se utilizan?

- Crear y estructurar **páginas web** 
- **Guardar e intercambiar datos** entre aplicaciones distintas 
- **Documentación** y notas sencillas 

### Ejemplos conocidos

| Lenguaje | Para qué sirve | Ejemplo |
|---|---|---|
| **HTML** | Estructura páginas web | `<p>Hola</p>` |
| **XML** | Estructura e intercambia datos | `<nombre>Ana</nombre>` |
| **Markdown** | Da formato a texto de forma sencilla | `**negrita**` |
| **SVG** | Describe imágenes vectoriales | `<circle r="10"/>` |


### Requisitos para ser lenguaje de marcas

Según el enunciado, debe cumplir:

1. Basarse en **texto plano**.
2. Hacer uso de **metadatos** 
3. Facilitar el **procesamiento automático** de los datos por un programa.
4. Facilitar la **representación ** de los datos almacenados.

---

## 2.FUTXML y sus reglas

**FUTXML** es un lenguaje inventado por nosotros para **guardar información sobre partidos de fútbol**.

### ¿Qué puede almacenar?

- Equipos y jugadores
- Fechas y estadios
- Resultados y competiciones

### Idea básica

```xml
<equipo>Real Madrid</equipo>
```

La etiqueta `<equipo>` indica que el dato "Real Madrid" representa **el nombre de un equipo**.

### Reglas básicas del lenguaje

| N.º | Regla | Explicación |
|---|---|---|
| 1 | **Etiquetas** | Cada elemento tiene etiqueta de apertura y de cierre: `<fecha>...</fecha>`. |
| 2 | **Elemento raíz** | Todo partido está dentro de `<partido>`. |
| 3 | **Datos obligatorios** | Equipo local y visitante, fecha y goles. |
| 4 | **Metadatos** | La temporada y la competición se escriben como **atributos** de `<partido>`. |
| 5 | **Orden correcto** | Las etiquetas deben estar bien escritas (se cierra primero la última que se abrió). |
| 6 | **Texto plano** | Los datos se leen bien y son  fáciles de guardar en un archivo `.txt` o `.xml`. |

### Elementos de FUTXML

| Elemento / atributo | Tipo | ¿Obligatorio? | Contenido |
|---|---|---|---|
| `<partido>` | Elemento raíz | Sí | Contiene todo el partido |
| `temporada` | Atributo (metadato) | Sí | Por ejemplo `"2026-2027"` |
| `competicion` | Atributo (metadato) | Sí | Por ejemplo `"Liga"` |
| `<fecha>` | Elemento | Sí | Formato `AAAA-MM-DD` |
| `<estadio>` | Elemento | No | Nombre del estadio |
| `<equipo_local>` | Elemento | Sí | Contiene `<nombre>` y `<goles>` |
| `<equipo_visitante>` | Elemento | Sí | Contiene `<nombre>` y `<goles>` |
| `<nombre>` | Elemento | Sí | Nombre del equipo |
| `<goles>` | Elemento | Sí | Número de goles (entero) |

### Ejemplos de reglas bien y mal aplicadas

**Regla 1: etiquetas de apertura y cierre**

```xml
<!-- Correcto -->
<fecha>2026-10-25</fecha>

<!-- Incorrecto: falta la etiqueta de cierre -->
<fecha>2026-10-25
```

**Regla 4: metadatos como atributos entre comillas**

```xml
<!-- Correcto -->
<partido temporada="2026-2027" competicion="Liga">

<!-- Incorrecto: valores sin comillas -->
<partido temporada=2026-2027 competicion=Liga>
```

**Regla 5: orden correcto **

```xml
<!-- Correcto -->
<equipo_local>
  <nombre>Real Madrid</nombre>
</equipo_local>

<!-- Incorrecto: las etiquetas se cruzan -->
<equipo_local>
  <nombre>Real Madrid</equipo_local>
</nombre>
```

**Regla 3: datos obligatorios**

```xml
<!-- Incorrecto: falta el equipo visitante -->
<partido temporada="2026-2027" competicion="Liga">
  <fecha>2026-10-25</fecha>
  <equipo_local>
    <nombre>Real Madrid</nombre>
    <goles>2</goles>
  </equipo_local>
</partido>
```

---

## 3. Clasificación de FUTXML

FUTXML es un lenguaje **descriptivo / semántico**.

| Tipo | ¿Es FUTXML? | Justificación |
|---|---|---|
| **Descriptivo / semántico** | **Sí** | Describe **qué representa** cada dato (`<fecha>`, `<goles>`, `<equipo_local>`...). Usa etiquetas con significado y separa los datos de su aspecto visual. |
| **Procedimental** | **No** | No contiene una secuencia de instrucciones para ejecutar. |
| **De presentación** | **No** | No define colores, tamaños ni posiciones en pantalla. |

**Comparación con otros lenguajes:**

| Lenguaje | Clasificación |
|---|---|
| HTML (parte de estructura) | Descriptivo |
| XML | Descriptivo |
| LaTeX | Procedimental |
| FUTXML | **Descriptivo / semántico** |

---

## 4. Caso de uso adecuado

### Una aplicación de resultados deportivos

FUTXML podría almacenar **muchos partidos** para que una aplicación los consulte después.

**Qué se podría hacer:**

- Guardar los resultados de cada encuentro.
- Buscar partidos por equipo o por temporada.
- Filtrar encuentros según los goles.
- Intercambiar datos entre aplicaciones compatibles.

**Ejemplo de resultados que mostraría la aplicación:**

| Local | Visitante | Resultado |
|---|---|---|
| Real Madrid | Barcelona | 2–1 |
| Betis | Sevilla | 1–0 |
| Girona | Valencia | 0–0 |

**Cómo se guardaría una jornada completa** (para agrupar varios partidos usamos un archivo por jornada con una etiqueta `<jornada>` que contiene los `<partido>`):

```xml
<jornada numero="9" competicion="Liga">
  <partido temporada="2026-2027" competicion="Liga">
    <fecha>2026-10-25</fecha>
    <equipo_local>
      <nombre>Real Madrid</nombre>
      <goles>2</goles>
    </equipo_local>
    <equipo_visitante>
      <nombre>Barcelona</nombre>
      <goles>1</goles>
    </equipo_visitante>
  </partido>

  <partido temporada="2026-2027" competicion="Liga">
    <fecha>2026-10-25</fecha>
    <equipo_local>
      <nombre>Betis</nombre>
      <goles>1</goles>
    </equipo_local>
    <equipo_visitante>
      <nombre>Sevilla</nombre>
      <goles>0</goles>
    </equipo_visitante>
  </partido>

  <partido temporada="2026-2027" competicion="Liga">
    <fecha>2026-10-26</fecha>
    <equipo_local>
      <nombre>Girona</nombre>
      <goles>0</goles>
    </equipo_local>
    <equipo_visitante>
      <nombre>Valencia</nombre>
      <goles>0</goles>
    </equipo_visitante>
  </partido>
</jornada>
```

**Ejemplos de consultas que un programa podría hacer con este archivo:**

- "¿Cuántos partidos acabaron 0–0?" → buscar los `<partido>` donde ambos `<goles>` valgan 0.
- "¿Qué ha jugado el Betis?" → buscar `<nombre>Betis</nombre>`.
- "¿Cuántos goles se marcaron en total?" → sumar todos los `<goles>`.

---

## 5. Ejemplo de uso explicado

### Un partido escrito en FUTXML

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

### Explicación línea a línea

| Línea | Qué significa |
|---|---|
| `<partido temporada="2026-2027" competicion="Liga">` | Abre el elemento raíz. Los **atributos** son los **metadatos**: temporada y competición. |
| `<fecha>2026-10-25</fecha>` | Fecha del partido. |
| `<estadio>Bernabeu</estadio>` | Estadio donde se juega. |
| `<equipo_local>` ... `</equipo_local>` | Agrupa los datos del equipo local. |
| `<nombre>Real Madrid</nombre>` | Nombre del equipo local. |
| `<goles>2</goles>` | Goles marcados por el equipo local. |
| `<equipo_visitante>` ... `</equipo_visitante>` | Agrupa los datos del equipo visitante. |
| `</partido>` | Cierra el elemento raíz. |

### Cómo se interpretaría

| MARCADOR | |
|---|---|
| **REAL MADRID** vs **BARCELONA** | **2 — 1** |

### Otro ejemplo: partido de copa sin estadio

El estadio no es obligatorio, así que este partido también es correcto:

```xml
<partido temporada="2026-2027" competicion="Copa">
  <fecha>2026-12-03</fecha>
  <equipo_local>
    <nombre>Athletic Club</nombre>
    <goles>3</goles>
  </equipo_local>
  <equipo_visitante>
    <nombre>Osasuna</nombre>
    <goles>3</goles>
  </equipo_visitante>
</partido>
```

Resultado: **Athletic Club 3 — 3 Osasuna** (empate).

### Ejemplo ampliado: con goleadores

Se pueden añadir elementos opcionales. Aquí cada gol lleva el minuto como atributo:

```xml
<partido temporada="2026-2027" competicion="Liga">
  <fecha>2026-11-08</fecha>
  <estadio>Metropolitano</estadio>
  <equipo_local>
    <nombre>Atletico de Madrid</nombre>
    <goles>2</goles>
    <goleador minuto="23">Jugador A</goleador>
    <goleador minuto="71">Jugador B</goleador>
  </equipo_local>
  <equipo_visitante>
    <nombre>Villarreal</nombre>
    <goles>1</goles>
    <goleador minuto="88">Jugador C</goleador>
  </equipo_visitante>
</partido>
```

### Cómo lo procesaría un programa (en Python)

Como FUTXML es texto con estructura XML, un programa puede leerlo con una librería estándar. Los **elementos** se leen con `find(...).text` y los **metadatos** (atributos) con `get(...)`:

```python
import xml.etree.ElementTree as ET

xml = """<partido temporada="2026-2027" competicion="Liga">
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
</partido>"""

partido = ET.fromstring(xml)

# Metadatos (atributos de <partido>)
temporada = partido.get("temporada")
competicion = partido.get("competicion")

# Elementos
fecha = partido.find("fecha").text
estadio = partido.find("estadio").text
local = partido.find("equipo_local/nombre").text
goles_local = partido.find("equipo_local/goles").text
visitante = partido.find("equipo_visitante/nombre").text
goles_visitante = partido.find("equipo_visitante/goles").text

print("Competición:", competicion)
print("Temporada:", temporada)
print("Fecha:", fecha)
print("Estadio:", estadio)
print(f"Resultado: {local} {goles_local} - {goles_visitante} {visitante}")
```

Salida:

```text
Competición: Liga
Temporada: 2026-2027
Fecha: 2026-10-25
Estadio: Bernabeu
Resultado: Real Madrid 2 - 1 Barcelona
```

Esto demuestra que el lenguaje **facilita el procesamiento automático** de los datos, incluidos los metadatos.

---

## 6. Caso de uso inadecuado

### Crear un videojuego de fútbol en 3D

FUTXML podría guardar **información del partido**, pero **no puede hacerlo todo**.

| Lo que NO hace FUTXML | Por qué |
|---|---|
| **No genera gráficos 3D** | Necesita un motor gráfico. |
| **No anima jugadores** | Se requieren herramientas de animación. |
| **No simula la física** | La lógica del juego debe programarse. |
| **No controla el juego** | No tiene variables, condiciones ni bucles. |

> **FUTXML almacena datos ≠ motor de juego**

**Otros casos en los que tampoco sería lo más adecuado:**

- **Hacer una página web bonita con colores:** para eso están HTML y CSS.
- **Calcular estadísticas complejas** (medias, rankings automáticos): hace falta un lenguaje de programación.
- **Guardar vídeos o imágenes de los partidos:** son archivos binarios, no texto.

**Cómo se solucionaría:** usar FUTXML para guardar los datos y combinarlo con otras tecnologías (un motor como Unity para el juego, o HTML + CSS para mostrar los resultados).

---

## 7. ¿Por qué FUTXML es un lenguaje de marcas?

| N.º | Requisito | Cómo lo cumple FUTXML |
|---|---|---|
| 1 | **Texto plano** | Los datos se pueden leer como texto en cualquier editor. |
| 2 | **Metadatos** | Incluye la temporada y la competición como atributos del `<partido>`. |
| 3 | **Procesamiento automático** | Las etiquetas facilitan la lectura automática por parte de un programa (ver el ejemplo en Python). |
| 4 | **Interpretación / representación** | Cada etiqueta aporta significado al dato (`<goles>`, `<fecha>`...), lo que permite mostrarlos como un marcador o una tabla. |

**FUTXML organiza información futbolística de forma estructurada.**

---

## Conclusión

Con FUTXML hemos creado un lenguaje propio que cumple las cuatro condiciones de un lenguaje de marcas. Sirve para **guardar y consultar datos de partidos**, pero no para ejecutar lógica ni para dar formato visual.

**¡Gracias por vuestra atención!**

---

*LMSGI · Práctica 1 · ASIX*
