Declaración uso IA: SI

A continuación se detallará las instancias en las que se hizo uso de IA en la realización de este proyecto, declarando las entradas y salidas además de una reflexión sobre que cambios realizar.

En todos los casos se utilizó la IA DeepSeek-V4-Flash

1.  Input: 
        Indicame el bloque de código con los 3 breakpoints necesarios para un documento css de una página web.

    Output:
        # Bloques de código con breakpoints para CSS

        Aquí tienes el bloque de código con los **3 breakpoints** más comunes y necesarios para una página web responsive:

        ```css
        /* ============================================
        BREAKPOINTS RESPONSIVE
        ============================================ */

        /* 1. MÓVIL / TABLET PEQUEÑA (hasta 767px) */
        @media (max-width: 767px) {
        /* Estilos para móviles */
        .container {
            width: 100%;
            padding: 0 15px;
        }

        .header {
            flex-direction: column;
        }

        .nav-menu {
            display: none; /* Se suele usar menú hamburguesa */
        }

        .grid {
            grid-template-columns: 1fr;
        }
        }

        /* 2. TABLET / ESCRITORIO PEQUEÑO (768px - 1023px) */
        @media (min-width: 768px) and (max-width: 1023px) {
        /* Estilos para tablets */
        .container {
            width: 720px;
            margin: 0 auto;
        }

        .grid {
            grid-template-columns: repeat(2, 1fr);
        }
        }

        /* 3. ESCRITORIO / DESKTOP (desde 1024px) */
        @media (min-width: 1024px) {
        /* Estilos para escritorio */
        .container {
            width: 960px;
            margin: 0 auto;
        }

        .grid {
            grid-template-columns: repeat(3, 1fr);
        }
        }
        ```

        ## 📌 Explicación de los 3 breakpoints

        | # | Rango | Dispositivo | Uso típico |
        |---|-------|-------------|------------|
        | **1** | `max-width: 767px` | Móviles | 1 columna, menú hamburguesa |
        | **2** | `768px – 1023px` | Tablets | 2 columnas, layout intermedio |
        | **3** | `min-width: 1024px` | Escritorio | 3+ columnas, layout completo |

        ## 💡 Recomendaciones

        - **Mobile First**: si trabajas con esta filosofía, invierte el orden usando `min-width` en lugar de `max-width`:
        ```css
        @media (min-width: 768px) { /* tablet */ }
        @media (min-width: 1024px) { /* desktop */ }
        @media (min-width: 1280px) { /* desktop grande */ }
        ```

        - **Breakpoints habituales en frameworks** (Bootstrap 5): `576px`, `768px`, `992px`, `1200px`, `1400px`.

        - Usa **unidades `rem`** en lugar de `px` si quieres respetar el zoom del usuario:
        ```css
        @media (min-width: 48rem) { /* equivale a 768px */ }
        ```

        ¿Quieres que te lo adapte a **Mobile First** o a algún framework específico (Tailwind, Bootstrap, etc.)?

    Reflexión y cambios a realizar:
        La IA indicó lo que se le pidió además de explicación y recomendaciones extra. Recuerda mi idea previa de usar unidades rem en vez de px pero durante las presentaciones se dejó en claro que debían usarse, en el caso de las especificaciones de las medidas mínimas para los distintos dispositivos, unidades en px.
        Siguiendo los consejos del profesor se ha utilizado de base el bloque indicado por la IA usando unidades en px y se ha resuelto no quedar con la duda. A continuación la consulta respecto al uso de px por sobre rem en este caso. 

_________________________________________________________________________

2.  Input:
        Recomiendas usar medidas rem en lugar de px pero ¿porqué en el código que entregaste están todas las medidas especificadas en px en lugar de rem?

    Output:
        # Tienes toda la razón — buena observación 👏

        Es una **inconsistencia real** en mi respuesta anterior. Me expliqué mal. Vamos a aclararlo:

        ## 🔍 ¿Qué pasó?

        En el bloque de código usé `px` en los breakpoints (`max-width: 767px`, etc.) pero luego **recomendé** usar `rem`. Eso es contradictorio y confuso. La recomendación de `rem` aplica principalmente a los **media queries**, no a todas las medidas del layout.

        ## ✅ Aclaración correcta

        ### 1. En los **media queries** → sí conviene `rem`

        **Motivo:** los `rem` en media queries respetan el **tamaño de fuente configurado por el usuario** en su navegador (accesibilidad). Si alguien aumentó el texto base a 20px, un breakpoint en `rem` se ajusta; uno en `px` no.

        ```css
        /* ❌ No respeta zoom de fuente del usuario */
        @media (max-width: 767px) { ... }

        /* ✅ Sí lo respeta (16px base → 48rem = 768px) */
        @media (max-width: 47.9375rem) { ... }
        ```

        > ⚠️ **Matiz importante:** los `rem` en media queries dependen del tamaño de fuente **inicial del navegador** (normalmente 16px), **no** del `font-size` del `html` que definas en tu CSS. Es un detalle que suele confundir.

        ### 2. En **anchos de contenedores y layout** → `px`, `%`, `vw` o `ch` están bien

        ```css
        .container {
        width: 960px;   /* ✅ Perfectamente válido */
        max-width: 100%;
        }
        ```

        Aquí `px` es correcto porque son medidas de **layout**, no de tipografía.

        ### 3. En **tipografía y espaciados** → ahí sí `rem` es la norma

        ```css
        body { font-size: 1rem; }        /* ✅ */
        h1   { font-size: 2rem; }        /* ✅ */
        .card { padding: 1.5rem; }       /* ✅ */
        ```

        ## 🔁 Código corregido (coherente con la recomendación)

        ```css
        /* ============================================
        BREAKPOINTS EN rem (base 16px)
        48rem  = 768px
        64rem  = 1024px
        ============================================ */

        /* 1. MÓVIL */
        @media (max-width: 47.9375rem) {
        .container { width: 100%; padding: 0 1rem; }
        .grid { grid-template-columns: 1fr; }
        }

        /* 2. TABLET */
        @media (min-width: 48rem) and (max-width: 63.9375rem) {
        .container { width: 45rem; margin: 0 auto; }
        .grid { grid-template-columns: repeat(2, 1fr); }
        }

        /* 3. ESCRITORIO */
        @media (min-width: 64rem) {
        .container { width: 60rem; margin: 0 auto; }
        .grid { grid-template-columns: repeat(3, 1fr); }
        }
        ```

        ## 📌 Resumen

        | Dónde | Unidad recomendada | Por qué |
        |-------|-------------------|---------|
        | Media queries | `rem` | Respeta accesibilidad del usuario |
        | Tipografía | `rem` | Escala con preferencias del usuario |
        | Espaciados (padding/margin) | `rem` | Consistencia con tipografía |
        | Anchos de contenedor | `px` / `%` / `ch` | Son medidas de layout, no de texto |
        | Bordes, sombras finas | `px` | Precisión de 1px real |

        Gracias por señalarlo — mi código anterior no era coherente con la recomendación. ¿Quieres que te pase una **guía de conversión px → rem** rápida o el bloque ya adaptado a **Mobile First**?

    Reflexión y cambios a realizar:
        Se entiende que es mejor utilizar rem en lugar de px incluso en este contexto específico. 
        No se aplican cambios pero se hace otra consulta respecto al tema. 
_________________________________________________________________________

3.  Input: 
        Responde brevemente si acaso es realmente mejor utilizar medidas rem en este contexto o mantener el uso de px para para los breakpoints.

    Output:
        En este contexto, **usar `rem` (o `em`) es realmente mejor que `px`**, principalmente por accesibilidad.

        La razón es simple: si el usuario aumenta el tamaño de fuente predeterminado del navegador (no solo el zoom de la página), los breakpoints definidos con `rem`/`em` se ajustarán junto con el tamaño de fuente del usuario, haciendo que el diseño se adapte mejor a la legibilidad; mientras que los breakpoints en `px` permanecen fijos, pudiendo provocar que el contenido se apriete o se desborde en pantallas pequeñas .

        **Pero hay un detalle**: en el contexto de media queries, `rem` y `em` son básicamente equivalentes, y algunos desarrolladores incluso recomiendan usar `em` para evitar bugs históricos de Safari . Por lo tanto, si buscas la máxima compatibilidad, `em` es una opción segura; si prefieres mantener la coherencia con la unidad tipográfica, `rem` también es completamente válido.

    Reflexión y cambios a realizar:
        Debido a las razones dadas se decide cambiar el esqueleto de los breakpoints en el css, cambiandolo por un uso de medidas en rem (bloque indicado en el punto 2.)
