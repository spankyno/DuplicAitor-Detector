# DuplicAitor Detector

Aplicación de escritorio de **solo análisis** para detectar archivos duplicados y similares.

**Importante:** Esta aplicación **nunca** copia, mueve, borra, renombra ni modifica ningún archivo. Es estrictamente de lectura.

## Requisitos

- .NET 8 SDK
- Windows, macOS o Linux

```bash
dotnet restore
dotnet build
dotnet run
```

## Funcionalidades

### Análisis
- Carpetas: ruta manual, diálogo nativo 📁, **Drag & Drop**
- Subcarpetas, modo comparación de 2 ubicaciones
- Filtros por nombre y tamaño (`1MB`, `500KB`…)
- **Hash SHA-256** en paralelo → duplicados **exactos**
- **Duplicados probables**: mismo tamaño + nombre normalizado similar (quita “copia”, “(1)”, “_v2”…) o similitud ≥ 85 % y tamaño ±2 %
- Relacionados: mismo nombre de archivo, distinto contenido
- **Caché de hashes** (JSON en AppData) para reescaneos rápidos
- Progreso, logs, Pausar / Reanudar / Cancelar

### Resultados
- Pestañas: Exactos · **Probables** · Relacionados · Únicos
- Panel de ahorro potencial (exactos + probables)

### Exportación
- **HTML** — informe visual oscuro
- **JSON** — datos estructurados
- **PDF** — informe A4 (QuestPDF)

### Perfiles
- Guardar / Cargar configuración (carpetas + filtros)

## Criterios de “probable”

1. Mismo tamaño exacto y nombre normalizado igual (sin sufijos de copia/versión).
2. O bien: similitud de nombre ≥ 85 % (Levenshtein) y diferencia de tamaño ≤ 2 %.

No incluye archivos que ya forman parte de un grupo exacto (mismo hash).

## Caché

`%LOCALAPPDATA%/DuplicAitorDetector/hash-cache.json` (o equivalente en Linux/macOS).  
Clave: ruta + tamaño + fecha de modificación.

## Licencia

Código de ejemplo. Úsalo y modifícalo libremente.
