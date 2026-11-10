# Cafetea

**Cuaderno de extracción para espresso y café de filtro.**

Cafetea te ayuda a ajustar una receta (*dial-in*): anotas el café y la receta, cronometras la extracción, catas y la app calcula el ratio y la extracción y te dice qué cambiar en la siguiente. Cada extracción se guarda en un diario, puedes guardar la receta patrón de cada tostador y los gráficos muestran en qué tiempos y ratios te salen las tazas equilibradas.

🔗 **App publicada:** https://jlopez-i.github.io/cafetea/

---

## Índice

- [Funcionalidades](#funcionalidades)
- [Cómo se usa](#cómo-se-usa)
- [Cálculos y rangos de referencia](#cálculos-y-rangos-de-referencia)
- [Datos y privacidad](#datos-y-privacidad)
- [Ejecutar en local](#ejecutar-en-local)
- [Publicar en GitHub Pages](#publicar-en-github-pages)
- [Estructura del proyecto](#estructura-del-proyecto)
- [Detalles técnicos](#detalles-técnicos)

---

## Funcionalidades

### Dial-in
- **Selector Espresso / Filtro.** Cada modo tiene sus propios valores por defecto, unidades y rangos, y recuerda lo último que escribiste al cambiar de uno a otro.
- **Ficha del café**, con los mismos datos que traen las tarjetas de los tostadores:
  - *Café:* tostador, nombre del café, nivel de tueste, perfil de tueste (espresso, filtro, omni), fecha de tueste, puntuación SCA y notas del tostador.
  - *Origen:* país, región, finca, productor, altitud, variedad (con sugerencias al escribir; admite varias), proceso (lavado, natural, honey, semi-lavado, anaeróbico, maceración carbónica) y criba. Calcula los **días de reposo** desde la fecha de tueste.
- **Receta:** dosis, ratio, bebida o agua (si cambias el ratio se recalcula la cantidad, y al revés), temperatura, punto de molienda y TDS opcional.
- **Método de filtro:** V60, Kalita Wave, Chemex, Origami, AeroPress, prensa francesa u otro.
- **Cronómetro integrado:** al pararlo, el tiempo pasa directamente a la receta. En espresso se muestra en segundos y en filtro en minutos.
- **Cata:** perfil obtenido (ácido / equilibrado / amargo), dulzor, acidez, cuerpo y amargor de 1 a 5, valoración de 1 a 10 y notas libres.
- **Lectura en vivo:** ratio, estilo (ristretto/normale/lungo o intenso/estándar/suave), tiempo, caudal o TDS y extracción (% EY), con una barra que sitúa el ratio en su rango.
- **Receta patrón:** al escribir un tostador que tiene receta patrón, aparece encima de la receta con las diferencias respecto a la tuya (dosis, ratio, tiempo, temperatura) y el botón **Aplicar patrón**.
- **Diagnóstico:** propone el siguiente ajuste según el perfil de cata, el tiempo, el ratio y la temperatura, y te avisa si el café es demasiado fresco o lleva mucho tiempo tostado.

### Recetas patrón
La receta de partida que recomienda cada tostador, normalmente en la bolsa o en su web.
- Una receta por tostador y método (espresso o filtro). Puede servir para todos sus cafés o solo para uno concreto; si hay una para ese café, tiene prioridad sobre la general.
- Campos: tostador, café (opcional), método de filtro, dosis, ratio y bebida o agua (enlazados), rango de tiempo, temperatura, molienda y notas.
- **Ficha del café opcional** (país, región, finca, productor, altitud, variedad, proceso, tueste, puntuación SCA, criba y notas). Al usar la receta en Dial-in, la ficha se copia con ella.
- Agrupadas por tostador, con botones **Usar en Dial-in**, **Editar** y **Borrar**.

### Diario
- Historial de todas las extracciones, de la más reciente a la más antigua.
- Búsqueda por tostador, café, país, región, finca, productor, variedad, proceso, método o notas.
- Filtros por perfil de cata y por método (espresso / filtro).
- **Repetir** carga una receta guardada en Dial-in; **Borrar** pide confirmación.

### Análisis
Cuatro gráficos interactivos, cada uno con datos de espresso o de filtro y filtrables por café:

| Gráfico | Qué muestra |
|---|---|
| Perfil según tiempo y ratio | Cada extracción como un punto, con su forma y su color según el perfil de cata, sobre la ventana ideal del método |
| Carta de control de extracción | TDS frente a % EY con la zona objetivo y diagonales de ratio constante |
| Perfil por franja de tiempo | Porcentaje de tazas ácidas, equilibradas y amargas en cada franja de duración |
| Valoración | Evolución de tu nota en orden cronológico |

También muestra cuatro cifras: número de extracciones, % de acierto, tu ventana de tiempo para tazas equilibradas y tu ratio de referencia. Mientras no tengas datos de un método, los gráficos muestran **datos de ejemplo**, marcados como tales y sin guardarse.

### Guía técnica
Tablas de referencia: estilos de espresso, métodos de filtro, fórmulas de extracción, diagnóstico en taza, reposo del grano según el tueste, limpieza de la máquina y composición del agua.

---

## Cómo se usa

1. *(Una vez por tostador)* En **Recetas**, guarda la receta que recomienda.
2. En **Dial-in**, elige *Espresso* o *Filtro*.
3. Rellena la ficha del café y la receta. Si el tostador tiene receta patrón, pulsa **Aplicar patrón** para partir de ella. Si tienes refractómetro, añade el TDS.
4. Pulsa **Iniciar** en el cronómetro al empezar la extracción y **Parar** al terminar.
5. Cata y marca el perfil, los atributos y la valoración.
6. Lee el diagnóstico, pulsa **Guardar** y aplica el ajuste propuesto en la siguiente extracción. Cambia una sola variable cada vez.
7. Consulta **Análisis** cuando tengas varias extracciones para ver tu ventana de tiempo y ratio.

> **Consejo:** *Partir del último* carga la receta de tu última extracción del método activo, para iterar sin volver a escribir todo.

---

## Cálculos y rangos de referencia

### Fórmulas

| Concepto | Espresso | Filtro |
|---|---|---|
| Ratio | bebida ÷ dosis | agua ÷ dosis |
| Bebida en taza | peso de la bebida | ≈ agua − 2 × dosis (el poso retiene unos 2 g de agua por gramo de café) |
| Extracción (EY %) | TDS % × bebida ÷ dosis | TDS % × (agua − 2 × dosis) ÷ dosis |
| Caudal | bebida ÷ tiempo (g/s) | — |

### Rangos que usa la app

| Parámetro | Espresso | Filtro |
|---|---|---|
| Ventana de tiempo | 25–32 s | 2:30–4:00 min |
| Ventana de ratio | 1:1,8 – 1:2,4 | 1:15 – 1:17 |
| Estilos por ratio | Ristretto < 1:1,6 · Normale 1:1,6–2,4 · Lungo > 1:2,4 | Intenso < 1:15 · Estándar 1:15–17 · Suave > 1:17 |
| Extracción objetivo | 18–22 % | 18–22 % |
| TDS objetivo | 8–12 % | 1,15–1,35 % (caja de la SCA) |

Son puntos de partida habituales en café de especialidad, no reglas fijas: el café y tu paladar mandan.

---

## Datos y privacidad

- La app **no tiene servidor ni cuentas**. En GitHub Pages todo se guarda en el `localStorage` de tu navegador: las extracciones en `cafetea_shots` y las recetas patrón en `cafetea_recipes`.
- Los datos **no se sincronizan entre dispositivos ni navegadores**, y se pierden si borras los datos del sitio.
- Si usaste la versión anterior (*Barista Lab*) en el mismo origen, sus registros se importan automáticamente la primera vez.
- No se envía nada a terceros. La única petición externa es la carga de tipografías desde Google Fonts.

---

## Ejecutar en local

No necesita instalación ni compilación: abre `index.html` en el navegador.

Si prefieres servirlo por HTTP:

```bash
python3 -m http.server 8000
# y abre http://localhost:8000
```

---

## Publicar en GitHub Pages

1. **Settings → Pages**.
2. En *Source* elige **Deploy from a branch**.
3. En *Branch* elige `main` y la carpeta `/ (root)`, y pulsa **Save**.
4. En uno o dos minutos la app queda publicada en `https://<usuario>.github.io/cafetea/`.

El archivo `.nojekyll` hace que GitHub sirva los archivos tal cual, sin procesarlos con Jekyll. En planes gratuitos, Pages solo funciona con repositorios públicos.

---

## Estructura del proyecto

```
cafetea/
├── index.html   # La aplicación completa: HTML, CSS y JavaScript
├── .nojekyll    # Hace que GitHub Pages sirva los archivos tal cual
└── README.md
```

---

## Detalles técnicos

- **Una sola página** en HTML, CSS y JavaScript sin frameworks, librerías ni proceso de build.
- **Gráficos en SVG** dibujados a mano, con tooltips, sensibles al tamaño de pantalla y redundancia de forma y color (triángulo, círculo, cuadrado) para que se lean con daltonismo.
- **Tema claro y oscuro** automático según el sistema.
- **Diseño adaptable** a escritorio y móvil. Añadida a la pantalla de inicio del móvil, funciona como una app.
- **Navegación por ancla**: `#dial-in`, `#recetas`, `#diario`, `#analisis` y `#guia` se pueden enlazar directamente.
- **Tipografías:** Big Shoulders Display (títulos y cifras), Schibsted Grotesk (texto) y JetBrains Mono (datos), desde Google Fonts, con tipografías del sistema como respaldo.
