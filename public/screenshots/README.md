# Carpeta para Screenshots

Coloca aqui las capturas de pantalla reales de la app.

## Requisitos

- Formato: PNG o JPG
- Tamano recomendado: 360x640 px (aspect ratio 9:16 para mobiles)
- Calidad: 80-100%

## Para agregar screenshots

1. Agrega las imagenes en esta carpeta
2. Actualiza `src/data/config.json` en el array `screenshots` con las rutas correctas

Ejemplo en config.json:
```json
{
  "screenshots": [
    {
      "title": "Pantalla Principal",
      "url": "/screenshots/pantalla-principal.png",
      "alt": "Screenshot de la pantalla principal de Factu Lite"
    }
  ]
}
```

## Usando el logo

Para agregar tu logo real:
1. Coloca el archivo SVG o PNG en `public/`
2. Actualiza la referencia en `src/components/Header.astro` y `src/components/Footer.astro`
