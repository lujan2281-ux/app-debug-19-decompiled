# app-debug-19 — Decompilación para revisión en GitHub

Este repositorio contiene:
- `original_apk/app-debug-19.apk`: el APK original.
- `extracted_apk/`: contenido del APK (zip descomprimido).
- `docs/classes.dex.strings.txt`: strings crudas extraídas del `classes.dex` (útil para buscar endpoints/paquetes rápidamente).
- `sources/`: carpeta vacía donde volcar el código Java/Kotlin generado por **JADX** (o smali con **apktool**).

> **Importante:** asegurate de tener derechos para publicar el código derivado de este APK. Si el app no es tuyo o incluye dependencias con licencias restrictivas, podría no ser legal subirlo a GitHub.

## Cómo obtener el código fuente (Java/Kotlin) con JADX

1. **Descargá JADX** (GUI o CLI) desde su página oficial.
2. Abrí el APK directamente con jadx-gui **o** desde consola:
   ```bash
   jadx -d sources original_apk/app-debug-19.apk
   ```
3. Confirmá que en `sources/` se generaron paquetes/clases (`.java`). Si la app usa Kotlin, verás `.java` descompilado desde bytecode DEX igualmente.
4. Revisá el `AndroidManifest.xml` **legible** en la vista de JADX. (El del APK está en binario AXML).

## Alternativa: obtener smali con apktool

```bash
apktool d -o sources_smali original_apk/app-debug-19.apk
```

Esto produce:
- `sources_smali/smali*/...`: código **smali** (nível DEX), muy fiel al binario.
- `AndroidManifest.xml`: decodificado a texto.

## Subir a GitHub

1. Si todavía no iniciás git:
   ```bash
   git init
   git add .
   git commit -m "Estructura inicial + APK y extracción"
   ```
2. Ejecutá jadx (o apktool) y verificá el resultado en `sources/` (o `sources_smali/`).
3. Agregá y commiteá los nuevos archivos:
   ```bash
   git add sources
   git commit -m "Decompilación con JADX"
   ```
4. Conectá tu repo remoto y subí:
   ```bash
   git remote add origin <URL-de-tu-repo>
   git branch -M main
   git push -u origin main
   ```

## .gitignore

Se incluye un `.gitignore` tipo Android/Java para evitar binarios pesados. Ajustalo según tu caso.

## Notas de licencia y privacidad
- Eliminá o anonimiza claves/API/secretos que puedan aparecer en el código descompilado.
- Respetá licencias de terceros (bibliotecas embebidas).
- Si la app es de un tercero, pedí permiso antes de publicar el código derivado.