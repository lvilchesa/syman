# SYMAN.md — Registro del sitio syman.cl
**Cliente:** Syman SPA (Constructora & Montaje), Cabrero, Biobío  
**Sitio actual:** https://syman.cl (Bluehost, cuenta `vilchesc`, carpeta `public_html/syman/`)  
**Repo:** `D:\DEV\Web\ClaudeCode\GitHub\lvilchesa\syman\` → **github.com/lvilchesa/syman** (público)  
**Revisión:** https://lvilchesa.github.io/syman/ (GitHub Pages habilitado el 25-sep-2026, sin dominio propio todavía)  
**Última actualización:** 2026-09-25 (v1.1)

---

## ▶ Punto de retomada (leer primero)

**Estado:** sitio **limpio, subido y publicado** en https://lvilchesa.github.io/syman/ (probado: 21 fotos, sin errores). Falta migrar el dominio con `D:\DEV\Web\ClaudeCode\PROTOCOLO-MIGRACION-GHPAGES.md`.

**Sobre el cliente:** después de enviar la información original, **nunca más mandó nada**; solo paga para mantener el sitio en línea. **No contar con que entregue datos nuevos**: se trabaja con lo que hay.

**Decisiones tomadas:**
- **Se mantiene el diseño original** (plantilla "Landigoo building", Bootstrap 3 + jQuery). Solo se limpió, no se rediseñó.
- **Sin formulario de contacto.** Contacto solo con teléfono (enlace `tel:`) y correo (`mailto:`). El PHP no entra al repo (`.gitignore`).
- **Galería sin ampliación ni enlaces** (pedido textual del cliente: "sin 'ampliación' al tocar la foto. Así no más. Son imágenes grandes. Sin link"). Son imágenes simples en recuadros de 350 px, sin ventana, sin lupa y sin títulos visibles. Los títulos que existían (Casa 48 m², Piscina…) quedan solo en el `alt`. Las 6 fotos de oct-2022 tienen `alt` genérico.
- **Logo sin el texto "Syman" al lado** (era redundante, pedido del cliente).
- **Sin Facebook ni WhatsApp**: no hay datos confirmados.
- **Pie de página VyASA** (el mismo de El Mundo de Rafa): "Desarrollo y Soporte Vyasa SpA - Hosting SomosWeb". El año se actualiza solo.

✅ `enviaemail.php` **borrado del hosting** (comprobado: 404, 25-sep-2026).

**Correo: Email Routing POSTERGADO a propósito** (25-sep-2026). El cliente usa más su correo personal que `contacto@syman.cl`, y se activará cuando pueda hacer clic en la verificación de Cloudflare. Mientras tanto, el MX en Cloudflare sigue apuntando a `mail.syman.cl` (Bluehost, DNS only), así que el reenvío de Bluehost sigue funcionando. ⚠ **No cancelar Bluehost hasta activar Email Routing.**

**Migración (protocolo):** fase 1 ✅ (Pages publicado) · **fase 2 ✅ molde en Cloudflare calza con Bluehost** (27 registros importados, 16 pasados de Proxied a DNS only, respaldo en `MigracionDNS/respaldos/syman.cl_20260925-152141.json`) · **fase 3 en curso:** NS cambiados en NIC.cl por Gonzalo el 25-sep-2026 (a `venkat` / `vita.ns.cloudflare.com`), esperando que NIC los publique y la zona pase a *active*.
Después, cuando la zona esté activa: Email Routing (`contacto@` → wcconstruccionesyman@gmail.com, **el cliente debe hacer clic en la verificación**), TXT de verificación de GitHub, `aplicar-github` y dominio + HTTPS en Pages.

---

## Datos para la migración (fase 0 del protocolo, 25-sep-2026)
- DNS: **Bluehost** (`ns1/ns2.bluehost.com`), **sin DNSSEC**. IP 162.241.216.59, **el mismo servidor que el hotel y Licahue** (cuenta `vilchesc`).
- **Correo:** `contacto@syman.cl` es **solo un reenvío** en Bluehost → **wcconstruccionesyman@gmail.com** (confirmado en cPanel el 25-sep-2026). Se reemplaza con Cloudflare Email Routing, igual que en Licahue. ⚠ Cloudflare exige que el dueño de esa casilla **haga clic en un correo de verificación**: es lo único que habría que pedirle al cliente, y conviene hacerlo antes del cambio de DNS.
- SPF actual: `v=spf1 a mx include:websitewelcome.com ~all` (de Bluehost). Sin DMARC.

---

## Historial

### v1.0 — Limpieza para GitHub Pages (2026-09-25)
**Seguridad:**
- `enviaemail.php` estaba **copiado de otro cliente** (rectimaquinas.cl) y **activo en producción**: cualquiera podía usarlo para enviar correos a direcciones arbitrarias con texto arbitrario desde el servidor de Bluehost (relay de spam), y elegir el destinatario `@rectimaquinas.cl`. El `error_log` muestra visitas de bots en ago y sep-2026. Nunca funcionó como formulario (los nombres de los campos no coincidían con el HTML). **Se sacó del repo; falta borrarlo del hosting.**

**Código (`index.html` reescrito con la misma estructura y el mismo diseño):**
- **Galería:** las 7 primeras fotos abrían todas la misma ventana (`id="tcasa36"` repetido). Se corrigió, y después (v1.1) se quitaron las ventanas por completo.
- `lang="es"`, meta descripción, sin bloqueo de zoom en celulares, ícono de pestaña (`images/favicon.png`, la grúa amarilla).
- Teléfono con enlace `tel:` (antes `#` abriendo una pestaña nueva), correo con `mailto:`, sin el Facebook que apuntaba a `#`.
- Se quitaron el cargador (su GIF no existía), el formulario comentado, párrafos vacíos, `</footer>` huérfano, `src` duplicado y la clase `co-xs-12` (errata).
- Ortografía: estaquedad→estanqueidad, Conózca→Conozca, Porton→Portón, mantencion→mantención, "personal … comprometidos"→comprometido, "que satisfagan"→satisfaga, espacios después de coma, Biobio→Biobío.
- `js/all.js`: se quitó **retina.js**, que tiraba `exports is not defined` y nunca funcionó.
- `style.css`: fuera las referencias a `images/bg.png` (no existía) y los `@import` de flaticon, owl.carousel y prettyPhoto (no se usaban). Al final hay un bloque "AJUSTES 2026" con los tres paneles oscuros de servicios a la misma altura (antes se igualaban con `</br></br>`).
- Contacto **en horizontal**: dirección, teléfono y correo lado a lado con el ícono arriba (en celular, uno bajo otro). Antes quedaba una columna angosta a la izquierda, junto al hueco del formulario comentado. CSS en el bloque "AJUSTES 2026" de `style.css`, con selectores `.contant-info.contact-horizontal` porque `building.css` se carga después y si no ganaría.

**Archivos:** de **184 archivos / 61 MB a 59 / 7,9 MB**.
- Borrados los que no se usaban: fotos de la plantilla en `uploads/building/` (solo se usa `c18.jpg`), duplicados en `images/obras/`, CSS y JS de plugins sin uso, `Thumbs.db`, `index-suspendido.html`, `underco.jpg`, `error_log`. **Todo sigue en `../syman.zip`** (copia íntegra del hosting).
- Recomprimidas sin cambiar tamaño: portada `c18.jpg` 2,1 MB→237 KB, y 4 fotos de la galería de más de 550 KB.
- Íconos de servicios: PNG de 800×800 (~1 MB c/u) mostrados a 90–120 px → JPG de 240×240 (~15 KB c/u).
- **Fotos sin usar del cliente:** 28 fotos de WhatsApp (dic-2019/ene-2020) + `Photos.zip` (21 fotos) movidas a `../syman-material/fotos-whatsapp-2019-2020/`. **Parecen fotos reales de sus trabajos: sirven para ampliar la galería si se quiere.**

### v1.1 — Pedidos del cliente (2026-09-25)
- Logo del menú sin el texto "Syman" al lado.
- Galería: fuera enlaces, ventanas y lupa; las fotos se muestran tal cual (21 probadas, sin errores).
- Contacto en horizontal (ver v1.0).

---

## Notas técnicas
- **Probar localmente:** `python -m http.server 8766` en la carpeta. Las fotos de la galería van **sin** `loading="lazy"`: con lazy quedaban invisibles en la plantilla.
- **Cuenta de git:** este repo usa el correo global (lvilchesa), que es correcto porque el destino es lvilchesa. Para hacer push hace falta el login de lvilchesa (el Administrador de credenciales de Windows tiene YN-TGS). Se puede usar GitHub Desktop con esa cuenta.
- **GitHub Pages gratis exige repo público.**
