# Log4Gambas3 — README técnico
[English](./README.md)

## Resumen

Log4Gambas3 es una librería pequeña de logging para Gambas3 empaquetada dentro de un proyecto que además incluye una aplicación demo con interfaz gráfica.

La fuente principal exportable está en:

- `.src/Clase/Log4Gambas3.class`

La demo está en:

- `.src/FMain.class`
- `.src/FMain.form`

## Estructura del proyecto

```text
.src/Clase/Log4Gambas3.class   Clase principal exportable
.src/FMain.class               Controlador del formulario demo
.src/FMain.form                Layout de la UI demo
.project                       Metadata del proyecto Gambas
.component                     Metadata del componente
.gambas/                       Artefactos generados/binarios
.desc/                         Descriptores generados
Iconos/                        Recursos visuales
```

## Arquitectura descubierta

### 1. Capa librería

La clase `Log4Gambas3` concentra:

- niveles de logging
- modos de salida
- getters/setters de configuración
- formateo del mensaje
- escritura a archivo
- rotación por cantidad de archivos

### 2. Capa demo/aplicación

`FMain` funciona como banco de pruebas manual para:

- elegir nivel
- elegir salida
- definir cantidad máxima de archivos
- definir tamaño máximo
- enviar texto de prueba

Además guarda preferencias usando `gb.settings`.

## Estado actual

- el nombre del archivo rota por fecha
- la rotación por cantidad de archivos está implementada
- la salida a consola, archivo o ambas está implementada
- `SetMaxFileSize()` ya aplica rotación real por tamaño
- cuando un archivo diario supera el tamaño configurado, la librería crea archivos con sufijos para ese mismo día

## Notas importantes sobre Gambas

- los archivos `.class` y `.form` son **texto plano**
- los `.gambas` y el contenido bajo `.gambas/` son artefactos generados/binarios
- Gambas es **case-insensitive**
- los formularios conviene tocarlos lo mínimo posible y mover lógica a clases o módulos cuando se pueda

## Recomendaciones de desarrollo

- tomar `.src/Clase/Log4Gambas3.class` como fuente real de la librería
- mantener separada la lógica reutilizable de la lógica de demo
- documentar con claridad qué archivos son fuente y cuáles son generados
- evitar convenciones de nombres que dependan de mayúsculas/minúsculas
- agregar una guía simple de validación manual para probar la rotación de logs

## Documentos relacionados

- `README.md` — versión técnica en inglés
- `spec.md` — especificación y hallazgos de arquitectura
- `agent.md` — guía de trabajo para agentes
- `tasks.md` — mejoras detectadas

## Verificación manual

Para probar manualmente la rotación actual de logs:

1. Abre el proyecto en Gambas3.
2. Configura el formulario demo para usar salida a archivo.
3. Define un tamaño máximo muy pequeño.
4. Envía varios mensajes de prueba desde la demo.
5. Verifica que:
   - se creen archivos diarios en la ruta configurada
   - el archivo activo rote a archivos con sufijo cuando supera el tamaño máximo
   - se eliminen archivos antiguos cuando se supera la cantidad máxima configurada

## Contribuir

Las contribuciones son bienvenidas, ya sea reportando bugs, proponiendo mejoras o enviando código.

1. Haz un fork del repositorio
2. Crea una rama (`git checkout -b feature/mi-cambio`)
3. Haz commit de tus cambios
4. Sube tu rama
5. Abre un Pull Request

## Contacto

<p align="center">
  <a href="https://www.linkedin.com/in/sepulvedamarcos">
    <img src="https://img.shields.io/badge/LinkedIn-Marcos%20Sep%C3%BAlveda-blue?logo=linkedin&logoColor=white" />
  </a>
  <a href="mailto:sepulvedamarcos@gmail.com">
    <img src="https://img.shields.io/badge/Email-sepulvedamarcos%40gmail.com-red?logo=gmail&logoColor=white" />
  </a>
  <a href="https://ko-fi.com/sepulvedamarcos">
    <img src="https://img.shields.io/badge/Ko--fi-Apoyar%20con%20un%20caf%C3%A9-ff5e5b?logo=kofi&logoColor=white" />
  </a>
</p>

---

Si te gusta Gacela, considera darle una estrella al repositorio.
