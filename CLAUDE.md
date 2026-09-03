# CLAUDE.md — Luchito Maranatha

Catálogo digital para **Luchito Maranatha**, marca ecuatoriana de alimentos tradicionales y productos empacados.

## Tecnología

HTML/CSS/JS vanilla, sin build, sobre `craft-catalog-engine`.

```
index.html          # UI
config.json         # config tienda (tema, whatsapp, mapa, category_order) — sync solo pisa `categories`
productos.json      # generado por catalogsync (no editar a mano)
theme.css           # identidad visual bespoke
logo.png            # logo horizontal con fondo transparente
media/favicon.png   # favicon — lo sube el cliente
```

Imágenes de productos: las mapea catalogsync en el push (no se versionan a mano).

## Fuente de verdad de los productos

**craft-crm** (nodo core, producción). Los productos viven en la DB por `business_id`.
`catalogsync` regenera `productos.json` + la clave `categories` de `config.json` desde la DB y hace push a este repo → Cloudflare Pages despliega.

Todo lo demás de `config.json` (tema, tipografías, WhatsApp, ubicación, redes) lo controla este repo y **se preserva** en cada sync. No editar `productos.json` a mano.

## Datos del cliente

- **WhatsApp consultas**: +593 96 995 9995
- **Cloudflare Pages**: `luchito-maranatha.pages.dev`
- **Business ID**: `b05e53ce-1194-49c4-9890-93d8d00060ac`

## Branding

- **Paleta**: borgoña `#741915`, dorado `#C18A2E`, pergamino suave y fondo blanco.
- **Tipografías**: Marcellus (títulos) + DM Sans (interfaz).
- **Dirección visual**: minimalista, clara y profesional, inspirada en una app de supermercado premium.

## Modelo del catálogo

- Los productos no publican precios por decisión comercial; las acciones abren una consulta por WhatsApp.
- `Humitas` y `Promo Morocho + Colada Morada` tienen tipo `promocion` y aparecen en el slider.
- Las imágenes se cargaron mediante la API de Craft CRM y catalogsync las materializa en `producto/<slug>/images/`.

## Deploy

```bash
git add . && git commit -m "descripción" && git push
```

Cloudflare Pages despliega automáticamente en push a `main` (workflow en `.github/workflows/deploy.yml`).
