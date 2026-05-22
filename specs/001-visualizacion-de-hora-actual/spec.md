# 001 - Visualización de Hora Actual

## Introducción

Este componente implementa un archivo HTML estático que muestra la hora actual en formato de 24 horas (`HH:MM:SS`) y se actualiza automáticamente cada segundo mediante JavaScript vanilla. El objetivo es permitir a los usuarios visualizar la hora del servidor de manera sencilla y en tiempo real.

## Criterios de Aceptación

### Escenario 1: Renderizado básico de la página
- **Dado** que el usuario abre el archivo `index.html` en cualquier navegador moderno,
- **Cuando** la página se carga por completo,
- **Entonces** debe mostrar un diseño limpio con un título centralizado llamado "Hora Actual".

### Escenario 2: Formato de la hora
- **Dado** que la página se visualiza en el navegador,
- **Cuando** se muestra el texto del reloj,
- **Entonces** la hora debe estar en formato `HH:MM:SS` (ejemplo: `14:35:08`).

### Escenario 3: Actualización en tiempo real
- **Dado** que el usuario permanece en la página sin recargar,
- **Cuando** cambia el tiempo del sistema,
- **Entonces** la hora debe actualizarse automáticamente cada segundo.

## Especificaciones Técnicas

### Tecnologías
- **Lenguajes:** HTML5, CSS3, JavaScript vanilla.

### Estructura del archivo
- **Archivo principal:** `index.html` (autónomo y autodescargable).

### Diseño visual
- **Fuente:** Legible (Arial, Helvetica o sans-serif).
- **Contraste:** Alto para facilitar la lectura.
- **Contenedor:** Centrado vertical y horizontal.

## Diagrama de Flujo (Opcional)

```mermaid
flowchart TD
    A[Inicializar página] --> B[Mostrar título: "Hora Actual"]
    B --> C[Obtener hora actual con JavaScript]
    C --> D[Actualizar hora cada segundo]
    D -->|Tiempo pasa| D
```

El flujo comienza con la carga de la página, muestra el título, captura la hora actual y actualiza el contenido cada segundo.