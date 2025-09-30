# 📝 Log4Gambas3
*Logging simple y efectivo para tus proyectos Gambas3*

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Made with Gambas](https://img.shields.io/badge/Made%20with-Gambas3-green.svg)](http://gambas.sourceforge.net/)
[![Platform](https://img.shields.io/badge/Platform-Linux-orange.svg)](https://www.linux.org/)

## 🎯 ¿Qué es Log4Gambas3?

Una librería de logging ligera y simple para Gambas3 que te permite registrar eventos de tu aplicación con los niveles estándar de logging, rotación automática de archivos y configuración flexible.

**¿Por qué otra librería de logging?** Aunque existe una librería oficial, este proyecto nace como ejercicio de aprendizaje y alternativa minimalista para quienes buscan algo directo y sin complicaciones.

## ✨ Características

- 📊 **Niveles estándar**: Debug, Info, Warning, Error, Fatal
- 🎯 **Múltiples destinos**: Consola, archivo de texto, o ambos simultáneamente
- 🔄 **Rotación automática**: Por fecha, tamaño de archivo o cantidad máxima
- ⚙️ **Configuración sencilla**: Define una vez al inicio y olvídate
- 🪶 **Súper liviana**: Un solo archivo, cero dependencias adicionales
- ⚡ **Sin overhead**: Mínimo impacto en el rendimiento de tu aplicación

## 🚀 Instalación rápida

### Opción 1: Agregar directamente al proyecto

```bash
cd tu-proyecto-gambas
wget https://raw.githubusercontent.com/sepulvedamarcos/Log4Gambas3/main/Log4Gambas3.class
# O simplemente copia el archivo .class a tu proyecto
```

Luego actualiza tu proyecto en el IDE de Gambas (F5).

### Opción 2: Clonar el repositorio

```bash
git clone https://github.com/sepulvedamarcos/Log4Gambas3.git
cp Log4Gambas3/Log4Gambas3.class ~/tu-proyecto/
```

## 📖 Uso básico

### Inicio rápido

```gambas
' En el inicio de tu aplicación (Main.module)
Public logger As Log4Gambas3

Public Sub Main()
  
  ' Crear instancia del logger
  logger = New Log4Gambas3
  
  ' Configuración mínima - salida a consola
  logger.SetOutput(Log4Gambas3.OUTPUT_CONSOLE)
  
  ' ¡Listo! Ahora puedes usar el logger
  logger.Info("¡Aplicación iniciada!")
  
End
```

### Los cinco niveles de logging

```gambas
' 🐛 DEBUG - Información detallada para depuración
logger.Debug("Valor de la variable usuarios: " & usuarios.Count)

' ℹ️ INFO - Eventos generales e informativos
logger.Info("Conexión establecida con la base de datos")

' ⚠️ WARNING - Situaciones inesperadas pero manejables
logger.Warning("Archivo de configuración no encontrado, usando defaults")

' ❌ ERROR - Errores que permiten continuar la ejecución
logger.Error("No se pudo guardar el archivo: " & Error.Text)

' 💀 FATAL - Errores críticos que impiden continuar
logger.Fatal("Base de datos inaccesible, cerrando aplicación")
```

## ⚙️ Configuración avanzada

### Logging a archivo

```gambas
' Configurar salida a archivo
logger.SetOutput(Log4Gambas3.OUTPUT_FILE)
logger.SetLogFile(User.Home &/ ".miapp/logs/aplicacion.log")
```

### Rotación por tamaño

```gambas
' Rotar cuando el archivo supere 10MB
logger.SetMaxFileSize(10 * 1024 * 1024)
' Resultado: aplicacion.log, aplicacion.log.1, aplicacion.log.2, etc.
```

### Rotación por cantidad de archivos

```gambas
' Mantener solo los últimos 5 archivos de log
logger.SetMaxFiles(5)
' Se elimina el más antiguo al crear uno nuevo
```

### Rotación por fecha

```gambas
' Crear un archivo nuevo cada día
logger.SetRotateByDate(True)
' Resultado: aplicacion-2025-09-30.log, aplicacion-2025-10-01.log, etc.
```

### Nivel mínimo de logging

```gambas
' En producción: solo INFO hacia arriba (oculta DEBUG)
logger.SetMinLevel(Log4Gambas3.LEVEL_INFO)

' En desarrollo: mostrar TODO incluyendo DEBUG
logger.SetMinLevel(Log4Gambas3.LEVEL_DEBUG)
```

### Salida dual (consola + archivo)

```gambas
' Lo mejor de ambos mundos
logger.SetOutput(Log4Gambas3.OUTPUT_BOTH)
logger.SetLogFile("/var/log/miapp/miapp.log")
```

## 💡 Ejemplo completo de producción

```gambas
' Main.module
Public logger As Log4Gambas3

Public Sub Main()
  
  ' Inicializar el logger
  logger = New Log4Gambas3
  
  ' Configuración para producción
  logger.SetOutput(Log4Gambas3.OUTPUT_FILE)
  logger.SetLogFile(User.Home &/ ".miapp/logs/miapp.log")
  logger.SetMaxFileSize(50 * 1024 * 1024)  ' 50MB máximo por archivo
  logger.SetMaxFiles(10)                    ' Mantener 10 archivos históricos
  logger.SetRotateByDate(True)              ' Archivo nuevo cada día
  logger.SetMinLevel(Log4Gambas3.LEVEL_INFO) ' Solo INFO y superiores
  
  logger.Info("=== Aplicación MiApp v1.0 iniciada ===")
  logger.Info("Usuario: " & User.Name)
  logger.Info("Sistema: " & System.Host)
  
  Try
    InicializarAplicacion()
  Catch
    logger.Fatal("Error crítico al iniciar: " & Error.Text)
    logger.Fatal("Ubicación: " & Error.Where)
    Quit
  End Try
  
End

Public Sub InicializarAplicacion()
  
  logger.Debug("Iniciando carga de configuración...")
  
  If Not Exist(User.Home &/ ".miapp") Then
    logger.Warning("Directorio de configuración no existe, creándolo")
    Mkdir User.Home &/ ".miapp"
  Endif
  
  logger.Info("Configuración cargada correctamente")
  logger.Debug("Total de plugins cargados: 5")
  
End
```

## 📊 Configuraciones recomendadas

### 🔧 Entorno de desarrollo

```gambas
logger.SetOutput(Log4Gambas3.OUTPUT_CONSOLE)
logger.SetMinLevel(Log4Gambas3.LEVEL_DEBUG)
' Ventaja: Ver todo en tiempo real mientras desarrollas
```

### 🚀 Entorno de producción

```gambas
logger.SetOutput(Log4Gambas3.OUTPUT_FILE)
logger.SetLogFile("/var/log/miapp/miapp.log")
logger.SetMaxFileSize(50 * 1024 * 1024)
logger.SetMaxFiles(20)
logger.SetMinLevel(Log4Gambas3.LEVEL_INFO)
logger.SetRotateByDate(True)
' Ventaja: Logs organizados, sin llenar el disco
```

### 🧪 Entorno de testing

```gambas
logger.SetOutput(Log4Gambas3.OUTPUT_BOTH)
logger.SetLogFile("/tmp/miapp-test.log")
logger.SetMinLevel(Log4Gambas3.LEVEL_DEBUG)
' Ventaja: Ver en consola Y guardar para análisis posterior
```

### 🏠 Aplicación de escritorio

```gambas
logger.SetOutput(Log4Gambas3.OUTPUT_FILE)
logger.SetLogFile(User.Home &/ ".local/share/miapp/logs/miapp.log")
logger.SetMaxFileSize(10 * 1024 * 1024)
logger.SetMaxFiles(3)
logger.SetMinLevel(Log4Gambas3.LEVEL_WARNING)
' Ventaja: No molesta al usuario, solo registra problemas
```

## 📚 Referencia API

### Constantes de nivel

| Constante | Uso | Descripción |
|-----------|-----|-------------|
| `LEVEL_DEBUG` | Desarrollo | Información detallada de depuración |
| `LEVEL_INFO` | General | Eventos informativos normales |
| `LEVEL_WARNING` | Atención | Advertencias que no impiden continuar |
| `LEVEL_ERROR` | Problema | Errores recuperables |
| `LEVEL_FATAL` | Crítico | Errores irrecuperables |

### Constantes de salida

| Constante | Comportamiento |
|-----------|----------------|
| `OUTPUT_CONSOLE` | Solo escribe en la terminal |
| `OUTPUT_FILE` | Solo escribe en archivo |
| `OUTPUT_BOTH` | Escribe en terminal Y archivo |

### Métodos de logging

```gambas
logger.Debug(mensaje As String)    ' Nivel DEBUG
logger.Info(mensaje As String)     ' Nivel INFO
logger.Warning(mensaje As String)  ' Nivel WARNING
logger.Error(mensaje As String)    ' Nivel ERROR
logger.Fatal(mensaje As String)    ' Nivel FATAL
```

### Métodos de configuración

```gambas
' Configurar destino de salida
logger.SetOutput(modo As Integer)

' Definir archivo de log
logger.SetLogFile(ruta As String)

' Configurar rotación por tamaño (en bytes)
logger.SetMaxFileSize(tamaño As Long)

' Configurar cantidad máxima de archivos
logger.SetMaxFiles(cantidad As Integer)

' Activar/desactivar rotación por fecha
logger.SetRotateByDate(activar As Boolean)

' Definir nivel mínimo a registrar
logger.SetMinLevel(nivel As Integer)

' Personalizar formato de línea (avanzado)
logger.SetFormat(formato As String)
```

## 🎯 Buenas prácticas

### ✅ Hazlo así

```gambas
' Contextualiza tus mensajes
logger.Error("Error al cargar usuario ID " & userId & ": " & Error.Text)

' Usa el nivel apropiado
logger.Debug("Query SQL: " & sqlQuery)  ' Solo en desarrollo
logger.Info("Usuario autenticado: " & username)  ' Eventos importantes
logger.Error("Falló conexión: " & Error.Text)  ' Errores

' Incluye información para diagnóstico
logger.Warning("Cache expirado después de " & timeout & " segundos")
```

### ❌ Evita esto

```gambas
' No registres en bucles intensivos
For i = 0 To 1000000
  logger.Debug("Procesando item " & i)  ' ¡MAL! Archivo gigante
Next

' No registres información sensible
logger.Info("Password: " & userPassword)  ' ¡NUNCA!
logger.Debug("Token de sesión: " & token)  ' ¡PELIGROSO!

' No abuses del nivel FATAL
logger.Fatal("El usuario cerró la ventana")  ' No es fatal
```

### 💡 Tips profesionales

1. **Inicializa temprano**: Configura el logger antes de cualquier otra operación
2. **Un logger por aplicación**: Usa una instancia global, no múltiples loggers
3. **Verifica permisos**: Asegúrate de tener permisos de escritura en la ruta de logs
4. **Monitorea el tamaño**: Configura rotación para evitar logs de GB
5. **Niveles en producción**: Usa INFO o WARNING en producción, DEBUG solo en desarrollo

## 🏆 Casos de uso reales

Log4Gambas3 está siendo utilizado en:

### 📸 Gacela
*Gestor de galería multiusuario para Linux*
- Tracking de importaciones de fotos
- Monitoreo de errores de base de datos
- Auditoría de accesos multiusuario

### 🎮 Tu proyecto aquí
*¿Usas Log4Gambas3?*  
[Abre un issue](https://github.com/sepulvedamarcos/Log4Gambas3/issues) para agregarte a esta lista

## 🆚 Comparación con alternativas

| Característica | Log4Gambas3 | Librería oficial | gb.util.Log |
|----------------|-------------|------------------|-------------|
| **Instalación** | 1 archivo | Varios archivos | Incluida |
| **Complejidad** | Muy baja | Media | Baja |
| **Rotación** | Sí (múltiples modos) | Sí | Limitada |
| **Configuración** | Programática | Archivo config | Programática |
| **Tamaño** | ~15KB | ~50KB | Variable |
| **Curva aprendizaje** | 5 minutos | 30 minutos | 10 minutos |
| **Ideal para** | Proyectos pequeños/medianos | Enterprise | Proyectos simples |

## 🛣️ Roadmap

- [x] Niveles de logging estándar
- [x] Rotación por tamaño y fecha
- [x] Salida múltiple (consola + archivo)
- [ ] Tests automatizados
- [ ] Formato JSON para logs estructurados
- [ ] Envío a syslog
- [ ] Compresión automática de logs antiguos
- [ ] Filtros personalizables por módulo
- [ ] Colores en salida de consola
- [ ] Integración con servicios de monitoreo externos

## 🤝 Contribuir

¡Las contribuciones son bienvenidas! Este es un proyecto de aprendizaje y toda ayuda suma.

**Formas de contribuir:**
- 🐛 Reportar bugs en [Issues](https://github.com/sepulvedamarcos/Log4Gambas3/issues)
- 💡 Sugerir mejoras o nuevas características
- 📝 Mejorar la documentación
- 🔧 Enviar Pull Requests con código

**Proceso:**
1. Fork el proyecto
2. Crea tu branch: `git checkout -b feature/mi-mejora`
3. Commit tus cambios: `git commit -m 'Agrega característica X'`
4. Push: `git push origin feature/mi-mejora`
5. Abre un Pull Request

## 📄 Licencia

GPL v3 - Software libre para siempre.

Eres libre de usar, modificar y distribuir este código. Si creas algo basado en Log4Gambas3, debe ser también GPL v3.

## 👨‍💻 Autor

**Marcos Sepúlveda**  
GitHub: [@sepulvedamarcos](https://github.com/sepulvedamarcos)

## 🙏 Agradecimientos

- Comunidad de **Gambas3** por crear un entorno fantástico
- Inspiración en **Log4j**, **Winston** y otras librerías clásicas
- Todos los que reportan bugs y sugieren mejoras

## 📖 Recursos adicionales

- [Documentación oficial de Gambas3](http://gambaswiki.org/)
- [Foro de Gambas](https://www.gambas-es.org/)
- [Repositorio oficial de Gambas](https://gitlab.com/gambas/gambas)

---

<div align="center">

**¿Te resultó útil Log4Gambas3?**  
⭐ Dale una estrella al repositorio

**¿Quieres apoyar el desarrollo?**  
☕ [Invítame un café](https://ko-fi.com/sepulvedamarcos)

*Proyecto creado con fines educativos y de aprendizaje*

</div>
