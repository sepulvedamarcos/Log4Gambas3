# Log4Gambas3

Logging simple para proyectos Gambas3.

## Propuesta de valor

Log4Gambas3 busca ofrecer una librería de logging chica, directa y fácil de integrar en proyectos Gambas3:

- niveles clásicos: `Debug`, `Info`, `Warning`, `Error`, `Fatal`
- salida a consola, archivo o ambas
- rotación simple por fecha y límite de archivos
- API corta, orientada a uso práctico

## Por qué usarlo

- evita montar una solución de logging más pesada
- sirve como base entendible para aprender Gambas3 y empaquetado de componentes
- trae una app/demo para probar comportamiento y configuración

## Instalación

### Requisitos

- Gambas3
- Componentes usados por el proyecto:
  - `gb.image`
  - `gb.gui`
  - `gb.form`
  - `gb.settings`

### Consideraciones importantes

- Este repositorio contiene **código fuente de la librería** y una **aplicación demo**.
- Los archivos `.class` y `.form` de Gambas son **texto plano**, aunque algunas herramientas los traten como binarios.
- Los archivos `.gambas` sí corresponden a artefactos binarios/generados.
- El proyecto tiene archivos del IDE que no siempre conviene versionar como fuente estable: `.gambas/`, `.desc/`, `.info`, `.startup`, `.settings`, imágenes generadas, etc.

### Formas de usarlo

1. Abrir este proyecto en Gambas3 y compilar/instalar el componente.
2. Reutilizar la clase exportada ubicada en `.src/Clase/Log4Gambas3.class`.
3. Tomar la demo incluida como referencia de integración.

## Estado del repositorio

Este `README.md` queda intencionalmente como versión corta/comercial.

Para documentación técnica y de trabajo con agentes:

- inglés: `rearme.md`
- español: `readme-es.md`
- arquitectura: `spec.md`
- guía para agentes: `agent.md`
- backlog técnico: `tasks.md`
