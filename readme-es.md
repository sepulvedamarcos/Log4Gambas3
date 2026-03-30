# Log4Gambas3

[English](./README.md)

Librería simple de logging para Gambas3.

*Una forma práctica de agregar trazas y archivos de log a tus aplicaciones sin complicarte.*

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Made with Gambas](https://img.shields.io/badge/Made%20with-Gambas-green.svg)](http://gambas.sourceforge.net/)
[![Platform](https://img.shields.io/badge/Platform-Linux-orange.svg)](https://www.linux.org/)

## ¿Qué es Log4Gambas3?

**Log4Gambas3** es una librería pequeña para registrar eventos, errores y mensajes de depuración en aplicaciones hechas con Gambas3.

Permite escribir logs en consola, en archivos o en ambas salidas al mismo tiempo, con una configuración simple y directa.  
El proyecto también incluye una aplicación demo para probar su funcionamiento.

## ¿Por qué usarla?

Cuando una aplicación empieza a crecer, tener trazas claras ayuda a entender qué pasó, detectar errores y seguir mejor el flujo de ejecución.

Log4Gambas3 busca resolver eso con una propuesta simple:

- niveles de log fáciles de usar,
- salida flexible,
- archivos organizados por fecha,
- y rotación automática para no acumular logs sin control.

## ¿Qué ofrece?

- **Niveles de log**: Fatal, Error, Warning, Info y Debug.
- **Salida flexible**: consola, archivo o ambas.
- **Archivos por fecha**: los logs se organizan automáticamente.
- **Rotación de archivos**: controla cuántos logs conservar.
- **Rotación por tamaño**: crea archivos nuevos cuando se supera el tamaño definido.
- **Demo incluida**: para probar la librería fácilmente.

## Casos de uso

Log4Gambas3 puede servirte si estás haciendo:

- aplicaciones de escritorio en Gambas3,
- utilidades internas,
- herramientas de administración,
- sistemas que necesiten trazabilidad básica,
- proyectos donde quieras depurar sin montar una solución compleja.

## Ejemplo de uso

```gambas
Dim log As New Log4Gambas3

log.SetAppName("MiAplicacion")
log.SetLogFile(User.Home &/ "logs")
log.SetMinLevel(Log4Gambas3.LEVEL_INFO)
log.SetOutput(Log4Gambas3.OUTPUT_BOTH)
log.SetMaxFiles(5)
log.SetMaxFileSize(1024 * 1024)

log.Info("Aplicación iniciada")
log.Warning("Esta es una advertencia")
log.Error("Ocurrió un error de prueba")
```

## Demo incluida

El proyecto incluye una interfaz de prueba desde donde puedes:

- seleccionar el nivel de log,
- elegir el tipo de salida,
- definir cantidad máxima de archivos,
- ajustar el tamaño máximo,
- y enviar mensajes de prueba.

Es una forma rápida de ver cómo funciona la librería antes de integrarla en otro proyecto.

## Estado del proyecto

Actualmente la librería permite:

- escribir mensajes con fecha, aplicación y nivel,
- generar archivos diarios de log,
- rotar archivos por cantidad,
- y rotar por tamaño cuando el archivo supera el límite configurado.

## Licencia

Este proyecto se distribuye bajo licencia GPL v3.

## Contacto

<p align="center">
  <a href="https://www.linkedin.com/in/sepulvedamarcos">
    <img src="https://img.shields.io/badge/LinkedIn-Marcos%20Sep%C3%BAlveda-blue?logo=linkedin&logoColor=white" />
  </a>
  <a href="mailto:sepulvedamarcos@gmail.com">
    <img src="https://img.shields.io/badge/Email-sepulvedamarcos%40gmail.com-red?logo=gmail&logoColor=white" />
  </a>
  <a href="https://ko-fi.com/sepulvedamarcos">
    <img src="https://img.shields.io/badge/Ko--fi-Invítame%20un%20café-ff5e5b?logo=kofi&logoColor=white" />
  </a>
</p>

---

Si te gustó el proyecto, considera darle una estrella al repositorio.
