# Marea Azul · TP 03 Web Design 3

Landing page estática (HTML + CSS + Bootstrap 5.3) de **Marea Azul**, un recital ficticio para jóvenes de 16 a 20 años.
Sábado 12 de diciembre de 2026, 21 h, Arena Costanera, Buenos Aires. Slogan: _"Dejate llevar."_ · #MareaAzul26

> Evento, artistas y venue ficticios, con fines académicos. La compra es simulada: no se procesan pagos.

## Estructura

```
index.html
css/styles.css      ← estilos propios, cargados después de Bootstrap
img/svg/            ← logo, ola separadora, público, ilustraciones de artistas y merch
```

Para verlo, abrí `index.html` en el navegador (Bootstrap, Bootstrap Icons y las tipografías se cargan por CDN). También se puede publicar con GitHub Pages.

## Cómo cumple la consigna

| Pedido | Dónde |
| --- | --- |
| Sección principal con título, descripción, imagen y CTA | `#inicio`: "MAREA AZUL", bajada, foto en duotono con overlay, "Comprar entradas" y "Ver lineup" |
| Sección informativa (beneficios) | `#show`: franja 3 · 4 · 1 y 4 tarjetas con Bootstrap Icons |
| Sección complementaria con tarjetas | `#lineup` (headliner + 2 soportes) y `#merch` (3 productos) |
| Compra de tickets | `#entradas`: General, Platea (más elegida) y VIP, con modal de compra y modal de confirmación |
| Footer con enlaces e info | Navegación, info/contacto, redes, legales y autores |
| Bootstrap | Grilla, navbar colapsable fija, cards, modales, accordion, badges, formularios, scrollspy |
| Media queries | Mobile first con `min-width` en 576, 768, 992 y 1200 px, más `hover: hover` y `prefers-reduced-motion` |
| Gradients | linear, radial y conic (ver abajo) |
| Animaciones CSS | Entrada del hero, pulso, burbujas, agua, borde VIP, hovers |
| Paleta coherente | Mismos 6 colores (ver tabla) aplicados en todo el CSS |
| Botones de acción | `.btn-ticket` (primario), `.btn-borde` (secundario), `.link-flecha` (texto) |

## Justificación de decisiones

### Paleta
Sale del concepto **"noche bajo el agua"**: todo en la familia del azul, sobre fondo oscuro porque el show es de noche y el azul brilla más sobre negro, como la luz bajo el agua. Para un público joven que escucha pop urbano, trap e indie, la estética de neón azul remite a la noche y a las visuales de los shows en vivo.

| Rol | Color | Uso |
| --- | --- | --- |
| Primario | `#2F6BFF` azul eléctrico | Gradients, separadores, detalles |
| Secundario | `#7B5CFF` violeta | Profundidad en los gradients |
| Acento | `#00D4FF` cian | **Solo** compra y CTA |
| Fondo | `#070B1F` azul noche | Fondo general |
| Superficie | `#111839` | Tarjetas y modales |
| Texto | `#F2F5FF` / `#A5AECF` | Principal / secundario (más de 4.5:1 sobre el fondo) |

La decisión más difícil fue **diferenciar los dos azules**: el cian es bastante más claro que el primario y es el único color de relleno de los botones de compra, así el ojo lo asocia con "comprar".

### Tipografías
- **Unbounded** (títulos): redondeada, ancha y fuerte; se ve joven y tiene presencia en tamaños grandes.
- **Inter** (textos): muy legible en pantallas chicas, que es desde donde entra la mayoría.

Escala: h1 `clamp(2.75rem, 8vw, 6rem)` en 800, h2 de 2 a 3 rem en 700, h3 1.25 rem en 600, párrafos 1 rem en Inter con interlineado 1.6.

### Orden de secciones y jerarquía
Navbar → Hero → El show → Lineup → Entradas → Merch y encuesta → FAQ → Footer.
Primero la emoción (hero), después las razones (beneficios y lineup) y recién ahí el precio. Lo primero que se lee es 1) MAREA AZUL, 2) fecha y lugar, 3) "Comprar entradas". El botón de compra aparece 4 veces: navbar, hero, entradas y footer. El espaciado usa múltiplos de 8 (96 px entre secciones, 64 px en celular).

### Componentes de Bootstrap
- **Grilla**: beneficios `col-12 col-md-6 col-lg-3`, lineup `col-12` + `col-md-6`, entradas `col-md-4`, merch `col-6 col-lg-4`, footer `col-12 col-md-6 col-lg-3`, dentro de `container-xxl` (máx. 1320 px).
- **Navbar** `fixed-top` colapsable, con **scrollspy** para marcar la sección activa.
- **Cards** personalizadas (beneficios, artistas, entradas, merch).
- **Modales**: compra → confirmación, merch, encuesta → gracias. El paso de un modal al otro usa `data-bs-toggle`. La compra es la excepción: el botón "Confirmar compra" envía el formulario, el navegador valida los campos obligatorios (nombre, email, DNI de 7 u 8 números y términos) y recién ahí un script corto abre la confirmación.
- **Accordion** para las preguntas frecuentes.
- **Badges**, **formularios** (`form-control`, `form-select`, `form-check`, `btn-check`) y **botones**.

Los estilos se pisan cargando `css/styles.css` después de Bootstrap, sin variables: colores, fondos, bordes y espaciados están escritos a mano en cada regla. Botones, tarjetas, navbar y modales no se ven "de Bootstrap".

### Media queries
| Query | Qué resuelve |
| --- | --- |
| base (celular) | Hero alineado a la izquierda, botones apilados a ancho completo, fecha y lugar en renglones, "Más elegida" primera (`order-first`), footer centrado |
| `max-width: 767.98px` | Fondo de agua más lento y suave, menos burbujas, modales más compactos |
| `min-width: 576px` | Precio de merch al lado del nombre |
| `min-width: 768px` | Hero centrado, botones en fila, franja de números en 3 columnas, headliner en 2 columnas, encuesta horizontal, footer alineado a la izquierda |
| `min-width: 992px` | Navbar expandida, Platea más grande (`scale`) |
| `min-width: 1200px` | Ajustes de tamaño en pantallas grandes |
| `hover: hover` | Los efectos de hover y el zoom de imágenes solo con mouse; en celular la info se ve siempre |
| `prefers-reduced-motion` | Se desactivan loops y animaciones de entrada |

### Gradients
| Dónde | Tipo | Qué refuerza |
| --- | --- | --- |
| Overlay del hero | linear 180°, noche al 20 % → noche sólida | Legibilidad y fusión con la sección siguiente |
| Fondo de agua del hero | linear + radial, animado (15 s) | Luz que se mueve como agua |
| Título "MAREA AZUL" y números | linear 90°, cian → azul → violeta | Identidad y logo |
| Botón de compra | linear 135°, `#00D4FF` → `#2F6BFF` | Destacar la acción principal |
| Fondos de secciones | radial violeta/azul al ~20 % | Profundidad, separación entre secciones |
| Borde de tarjetas en hover | linear cian → violeta | Feedback |
| Borde de la VIP | **conic**, girando | Exclusividad |
| Ola separadora e ilustraciones | linear (SVG) | Concepto marino |

### Animaciones
| Animación | Qué aporta |
| --- | --- |
| Entrada escalonada del hero (fade + subida, 0.8 s `cubic-bezier(.2,.8,.2,1)`) | Ordena la lectura: título → descripción → botones |
| Pulso del badge "2ª tanda" | Urgencia: lleva la mirada a comprar |
| Burbujas y fondo de agua | Crean el clima de "bajo el agua" |
| Borde cónico giratorio de la VIP | Distingue la entrada premium |
| Hover: tarjetas suben 8 px, botones suben 2 px con glow, links con subrayado que crece (0.25 s ease-out) | Feedback de interacción |

Se animan `transform` y `opacity` (y `box-shadow` en botones) para que sea fluido. Con `prefers-reduced-motion` se apagan.

### Botones
Forma de **píldora** (`border-radius: 999px`), como una burbuja, coherente con el concepto. Tres niveles:
1. **Primario** `.btn-ticket`: gradient cian → azul con texto azul noche en negrita. Es el único elemento con cian de relleno.
2. **Secundario** `.btn-borde`: transparente con borde ("Ver lineup", "Lo quiero", "Responder encuesta").
3. **Link de texto** `.link-flecha`: "Escuchar en Spotify".

Estados: hover sube 2 px con glow cian, active vuelve abajo, focus con contorno cian de 3 px. Alto mínimo de 48 px y ancho completo en celular.

### Un detalle: el total del modal sin JavaScript
El total de la compra ("Total · 2 × Platea — $120.000") se calcula **solo con CSS**: `:has()` detecta el tipo y la cantidad elegidos en los `<select>` y, para cada combinación, un `::after` muestra el texto y el monto correspondientes.

### Qué haríamos distinto
- Una cuenta regresiva real con JavaScript en lugar del badge de urgencia.
- Compra conectada a una plataforma de pagos real.
- Fotos propias del público en lugar de la foto de Unsplash.

## Créditos
- Foto del hero: Unsplash (con filtro duotono por CSS).
- Ilustraciones SVG propias.
- Bootstrap 5.3.8, Bootstrap Icons 1.13.1, Google Fonts (Unbounded, Inter).

TP 03 · Web Design 3 · Teo Moreno y Gabriel Papini
