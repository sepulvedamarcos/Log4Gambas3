# Log4Gambas3

[Español](./readme-es.md)

Simple logging library for Gambas3.

*A practical way to add traces and log files to your applications without overcomplicating things.*

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Made with Gambas](https://img.shields.io/badge/Made%20with-Gambas-green.svg)](http://gambas.sourceforge.net/)
[![Platform](https://img.shields.io/badge/Platform-Linux-orange.svg)](https://www.linux.org/)

## What is Log4Gambas3?

**Log4Gambas3** is a small library for recording events, errors, and debug messages in applications built with Gambas3.

It can write logs to the console, to files, or to both at the same time with a simple and direct configuration.  
The project also includes a demo application so you can quickly test how it works.

## Why use it?

As an application grows, having clear traces helps you understand what happened, detect errors faster, and follow the execution flow more easily.

Log4Gambas3 is built to solve that in a simple way:

- easy-to-use log levels,
- flexible output options,
- date-based log files,
- and automatic rotation to avoid uncontrolled log accumulation.

## What does it offer?

- **Log levels**: Fatal, Error, Warning, Info, and Debug.
- **Flexible output**: console, file, or both.
- **Date-based files**: logs are organized automatically.
- **File rotation**: control how many log files to keep.
- **Size-based rotation**: create new files when the configured size is exceeded.
- **Included demo**: test the library quickly.

## Use cases

Log4Gambas3 can be useful for:

- Gambas3 desktop applications,
- internal utilities,
- administration tools,
- systems that need basic traceability,
- projects where you want debugging support without a complex setup.

## Usage example

```gambas
Dim log As New Log4Gambas3

log.SetAppName("MyApplication")
log.SetLogFile(User.Home &/ "logs")
log.SetMinLevel(Log4Gambas3.LEVEL_INFO)
log.SetOutput(Log4Gambas3.OUTPUT_BOTH)
log.SetMaxFiles(5)
log.SetMaxFileSize(1024 * 1024)

log.Info("Application started")
log.Warning("This is a warning")
log.Error("A test error occurred")
```

## Included demo

The project includes a test interface where you can:

- choose the log level,
- select the output type,
- define the maximum number of files,
- adjust the maximum file size,
- and send test messages.

It is a quick way to see how the library behaves before integrating it into another project.

## Project status

The library currently supports:

- writing messages with date, application name, and level,
- generating daily log files,
- rotating files by count,
- and rotating by size when a file exceeds the configured limit.

## License

This project is distributed under the GPL v3 license.

## Contact

<p align="center">
  <a href="https://www.linkedin.com/in/sepulvedamarcos">
    <img src="https://img.shields.io/badge/LinkedIn-Marcos%20Sep%C3%BAlveda-blue?logo=linkedin&logoColor=white" />
  </a>
  <a href="mailto:sepulvedamarcos@gmail.com">
    <img src="https://img.shields.io/badge/Email-sepulvedamarcos%40gmail.com-red?logo=gmail&logoColor=white" />
  </a>
  <a href="https://ko-fi.com/sepulvedamarcos">
    <img src="https://img.shields.io/badge/Ko--fi-Buy%20me%20a%20coffee-ff5e5b?logo=kofi&logoColor=white" />
  </a>
</p>

---

If you like the project, consider giving the repository a star.
