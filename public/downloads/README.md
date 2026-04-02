# Carpeta para archivos APK

Coloca aqui tus archivos APK de Factu Lite.

## Estructura recomendada

```
public/downloads/
  factu-lite-v1.0.0.apk    # Version actual
  factu-lite-v1.1.0.apk    # Nueva version (cuando este disponible)
```

## Para agregar una nueva version

1. Agrega la nueva version en `src/data/config.json` en el array `versions`
2. Coloca el archivo APK en esta carpeta
3. Actualiza el campo `apk` con la ruta correcta

Ejemplo en config.json:
```json
{
  "versions": [
    {
      "version": "v1.1.0",
      "date": "2025-06-01",
      "apk": "/downloads/factu-lite-v1.1.0.apk",
      "notes": "Nuevas funcionalidades"
    },
    {
      "version": "v1.0.0",
      "date": "2025-03-01",
      "apk": "/downloads/factu-lite-v1.0.0.apk",
      "notes": "Version inicial"
    }
  ]
}
```
