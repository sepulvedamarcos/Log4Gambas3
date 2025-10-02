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

Luego actualiza tu proyecto en el IDE de Gambas.

### Opción 2: Clonar el repositorio crear la aplicación y agregala al proyecto una vez compilada

```bash
git clone https://github.com/sepulvedamarcos/Log4Gambas3.git
cp Log4Gambas3/Log4Gambas3.class ~/tu-proyecto/
```

### Opción 3: Bajar el release desde la pagina de github

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

  ' Configurar nombre de la aplicación
  logger.SetAppName("MiApp")

  ' Configuración mínima - salida a consola
  logger.SetOutput(Log4Gambas3.OUTPUT_CONSOLE)

  ' ¡Listo! Ahora puedes usar el logger
  logger.Info("¡Aplicación iniciada!")

End
```

**Nota importante sobre `SetAppName()`:** Este método define el nombre que aparecerá en cada línea de log y también se usará como prefijo en los nombres de archivo (ejemplo: `MiApp-2025-09-30.log`). Si no lo configuras, se usará "app" por defecto.

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
logger.SetLogFile(User.Home &/ ".miapp/logs")
logger.SetAppName("MiApp")
' El archivo será: MiApp-2025-09-30.log (se crea automáticamente por fecha)
```

**Importante:** `SetLogFile()` define el **directorio** donde se guardarán los logs, no el nombre del archivo. Los archivos se crean automáticamente con el formato: `nombreapp-YYYY-MM-DD.log`

### Rotación por tamaño

```gambas
' Configurar tamaño máximo por archivo
logger.SetMaxFileSize(10 * 1024 * 1024)  ' 10MB
```

### Rotación por cantidad de archivos

```gambas
' Mantener solo los últimos 5 archivos de log
logger.SetMaxFiles(5)
' Cuando se supera este límite, se elimina automáticamente el archivo más antiguo
' Los archivos tienen formato: miapp-2025-09-28.log, miapp-2025-09-29.log, etc.
```

**Cómo funciona:** Log4Gambas3 revisa automáticamente la cantidad de archivos `.log` en el directorio que coincidan con el nombre de tu aplicación. Si hay más archivos que el máximo configurado, elimina los más antiguos basándose en el nombre del archivo (orden alfabético = orden cronológico).

### Rotación automática por fecha

```gambas
' Log4Gambas3 implementa rotación automática por fecha
' NO necesitas activarla, está siempre activa
' Formato automático: nombreapp-YYYY-MM-DD.log
' Ejemplos:
'   MiApp-2025-09-30.log
'   MiApp-2025-10-01.log
'   MiApp-2025-10-02.log
```

**Ventajas de la rotación por fecha:**
- Archivos organizados cronológicamente
- Fácil identificar logs de un día específico
- No necesitas configurar nada extra
- Se combina con `SetMaxFiles()` para limitar la cantidad total

### Nivel mínimo de logging

```gambas
' En producción: solo INFO hacia arriba (oculta DEBUG)
logger.SetMinLevel(Log4Gambas3.LEVEL_INFO)

' En desarrollo: mostrar TODO incluyendo DEBUG
logger.SetMinLevel(Log4Gambas3.LEVEL_DEBUG)

' Solo advertencias y errores
logger.SetMinLevel(Log4Gambas3.LEVEL_WARNING)
```

**Jerarquía de niveles:**
```
LEVEL_DEBUG   (5) - Más detallado
LEVEL_INFO    (4)
LEVEL_WARNING (3)
LEVEL_ERROR   (2)
LEVEL_FATAL   (1) - Menos detallado
LEVEL_NONE    (0) - Sin logging
```

Si configuras `LEVEL_WARNING`, solo se registrarán mensajes de tipo Warning, Error y Fatal. Los mensajes Debug e Info serán ignorados.

### Salida dual (consola + archivo)

```gambas
' Lo mejor de ambos mundos: ver en tiempo real Y guardar historial
logger.SetOutput(Log4Gambas3.OUTPUT_BOTH)
logger.SetLogFile("/tmp/miapp/logs")
logger.SetAppName("MiApp")

' Ahora cada mensaje aparecerá en:
' 1. La consola (terminal)
' 2. El archivo de log correspondiente
```

**Ideal para:** Debugging, testing, o cuando necesitas monitorear en tiempo real pero también quieres guardar un registro permanente.

## 💡 Ejemplo completo de producción

```gambas
' Main.module
Public logger As Log4Gambas3

Public Sub Main()

  ' Inicializar el logger
  logger = New Log4Gambas3

  ' Configurar nombre de la aplicación
  logger.SetAppName("MiApp")

  ' Configuración para producción
  logger.SetOutput(Log4Gambas3.OUTPUT_FILE)
  logger.SetLogFile(User.Home &/ ".miapp/logs")
  logger.SetMaxFiles(10)                     ' Mantener 10 días de logs
  logger.SetMinLevel(Log4Gambas3.LEVEL_INFO) ' Solo INFO y superiores

  logger.Info("=== Aplicación MiApp v1.0 iniciada ===")
  logger.Info("Usuario: " & User.Name)
  logger.Info("Sistema: " & System.Host)


    InicializarAplicacion()

  Catch
    logger.Fatal("Error crítico al iniciar: " & Error.Text)
    logger.Fatal("Ubicación: " & Error.Where)
    Quit


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

**Resultado:** Esta configuración creará archivos como:
- `~/.miapp/logs/MiApp-2025-09-30.log`
- `~/.miapp/logs/MiApp-2025-10-01.log`
- etc.

Y mantendrá solo los últimos 10 archivos automáticamente.

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
logger.SetLogFile("/var/log/miapp")
logger.SetAppName("MiApp")
logger.SetMaxFiles(20)
logger.SetMinLevel(Log4Gambas3.LEVEL_INFO)
' Ventaja: Logs organizados por fecha, sin llenar el disco
' Archivos: MiApp-2025-09-30.log, MiApp-2025-10-01.log, etc.
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
logger.SetLogFile(User.Home &/ ".local/share/miapp/logs")
logger.SetAppName("MiApp")
logger.SetMaxFiles(3)
logger.SetMinLevel(Log4Gambas3.LEVEL_WARNING)
' Ventaja: No molesta al usuario, solo registra problemas
' Archivos automáticos por fecha
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
' Configurar destino de salida (OUTPUT_NONE, OUTPUT_FILE, OUTPUT_CONSOLE, OUTPUT_BOTH)
logger.SetOutput(modo As Integer)

' Definir directorio para archivos de log
logger.SetLogFile(directorio As String)

' Definir nombre de la aplicación (prefijo de archivos y aparece en cada línea)
logger.SetAppName(nombre As String)

' Configurar cantidad máxima de archivos a mantener
logger.SetMaxFiles(cantidad As Integer)

' Configurar tamaño máximo de archivo (funcionalidad en desarrollo)
logger.SetMaxFileSize(tamaño As Long)

' Definir nivel mínimo a registrar
logger.SetMinLevel(nivel As Integer)
```

**Nota importante sobre `SetLogFile()`:** Este método define el **directorio** donde se guardarán los logs, NO el nombre del archivo. Los archivos se crean automáticamente con el formato: `nombreapp-YYYY-MM-DD.log`

### Métodos getter

```gambas
' Obtener configuración actual
Dim nivel As Integer = logger.GetMinLevel()
Dim salida As Integer = logger.GetOutput()
Dim maxArchivos As Integer = logger.GetMaxFiles()
Dim directorio As String = logger.GetLogFile()
Dim nombre As String = logger.GetAppName()
Dim tamañoMax As Long = logger.GetMaxFileSize()
```
## 🧪 Formulario de prueba

El proyecto incluye un formulario de ejemplo (`FMain.form`) que demuestra todas las funcionalidades de Log4Gambas3.

**Componentes requeridos para el formulario de prueba:**
- gb.qt5 (o gb.gtk3)
- gb.settings

**Nota:** Si solo quieres usar la librería en tu proyecto, únicamente necesitas copiar el archivo `Log4Gambas3.class`. El formulario de prueba es opcional.

## 🎯 Buenas prácticas

### ✅ Hazlo así

```gambas
' 1. Configura el nombre de app al inicio
logger.SetAppName("MiSuperApp")  ' Archivos: MiSuperApp-2025-09-30.log

' 2. Contextualiza tus mensajes
logger.Error("Error al cargar usuario ID " & userId & ": " & Error.Text)

' 3. Usa el nivel apropiado según el entorno
logger.Debug("Query SQL: " & sqlQuery)  ' Solo en desarrollo
logger.Info("Usuario autenticado: " & username)  ' Eventos importantes
logger.Error("Falló conexión: " & Error.Text)  ' Errores recuperables

' 4. Incluye información útil para diagnóstico
logger.Warning("Cache expirado después de " & timeout & " segundos")

' 5. Usa Try/Catch con logging

  ConexionBD()
Catch
  logger.Error("Error en BD: " & Error.Text & " en " & Error.Where)

```

### ❌ Evita esto

```gambas
' NO registres en bucles intensivos
For i = 0 To 1000000
  logger.Debug("Procesando item " & i)  ' ¡MAL! Archivo gigante
Next

' NO registres información sensible
logger.Info("Password: " & userPassword)  ' ¡NUNCA!
logger.Debug("Token de sesión: " & token)  ' ¡PELIGROSO!
logger.Info("Tarjeta de crédito: " & cardNumber)  ' ¡CRÍTICO!

' NO abuses del nivel FATAL
logger.Fatal("El usuario cerró la ventana")  ' No es fatal
logger.Fatal("Usuario escribió mal el password")  ' No es fatal

' NO olvides configurar el nombre de app
' Si no usas SetAppName(), todos tus logs se llamarán "app-2025-09-30.log"
```

### 💡 Tips profesionales

1. **Configura al inicio**: Llama a `SetAppName()` antes que cualquier otro método de configuración
2. **Un logger global**: Declara `Public logger As Log4Gambas3` en Main para usarlo en toda la app
3. **Ruta con permisos**: Asegúrate de tener permisos de escritura (usa User.Home para apps de usuario)
4. **Limita archivos**: Usa `SetMaxFiles()` para que no se llene el disco (recomendado: 5-20 archivos)
5. **Niveles por entorno**: 
   - Desarrollo: `LEVEL_DEBUG`
   - Testing: `LEVEL_INFO`
   - Producción: `LEVEL_WARNING` o `LEVEL_INFO`

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
- [x] Rotación automática por fecha
- [x] Rotación por cantidad de archivos
- [ ] Salida múltiple (consola + archivo)
- [x] Rotación por tamaño de archivo (completar implementación)
- [ ] Envío a syslog
- [ ] Filtros personalizables por módulo
- [ ] Colores en salida de consola
- [ ] Formato de mensaje personalizable
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