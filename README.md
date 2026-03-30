# Log4Gambas3
[Español](./readme-es.md)

## Overview

Log4Gambas3 is a small Gambas3 logging library packaged as a project that also includes a demo GUI application.

Its main exported source lives in:

- `.src/Clase/Log4Gambas3.class`

The project also includes a form-based demo:

- `.src/FMain.class`
- `.src/FMain.form`

## Project structure

```text
.src/Clase/Log4Gambas3.class   Main exported logging class
.src/FMain.class               Demo form controller
.src/FMain.form                Demo UI layout
.project                       Gambas project metadata
.component                     Component metadata
.gambas/                       Generated/binary artifacts
.desc/                         Generated descriptors/call metadata
Iconos/                        Project icons
```

## Architecture discovered

### 1. Library layer

`Log4Gambas3.class` exposes:

- log levels
- output modes
- getters/setters for configuration
- message formatting
- file writing
- file rotation by count

### 2. Demo/application layer

`FMain` is a manual test harness for:

- level selection
- output selection
- max files
- max file size
- test message emission

It persists some UI settings through `gb.settings`.

## Current behavior

- date-based file naming is implemented
- file count rotation is implemented
- console/file/both outputs are implemented
- max file size rotation is implemented
- when a daily log file exceeds the configured size, the library creates suffixed files for the same day

## Gambas-specific notes

- `.class` and `.form` files are plain text source files
- `.gambas` files and content under `.gambas/` are generated/binary artifacts
- Gambas is case-insensitive, so naming collisions are easier to introduce than in many other languages
- form files should be changed carefully; moving logic out of forms is usually safer than deep UI edits

## Development recommendations

- treat `.src/Clase/Log4Gambas3.class` as the source of truth for the reusable library
- keep demo concerns out of the reusable logging class
- document generated files vs source files clearly for contributors and agents
- prefer stable naming conventions that do not rely on case differences
- add a practical manual verification flow for log file rotation behavior

## Related docs

- `readme-es.md` — Spanish technical version
- `spec.md` — architecture and technical findings
- `agent.md` — agent operating guide
- `tasks.md` — prioritized improvements

## Manual verification

To verify the current log rotation behavior manually:

1. Open the project in Gambas3.
2. Configure the demo form to use file output.
3. Set a very small max file size.
4. Send multiple test messages from the demo.
5. Confirm that:
   - daily log files are created in the configured path
   - the active file rolls over to suffixed files when size is exceeded
   - old files are removed when the configured max-file count is exceeded
