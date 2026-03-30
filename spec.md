# Log4Gambas3 — Architecture Spec

## Goal

Provide a lightweight Gambas3 logging component with a simple API and a small demo application to validate behavior.

## Scope discovered

### Reusable library

- File: `.src/Clase/Log4Gambas3.class`
- Responsibility: expose the logging API and implement output/rotation behavior

### Demo application

- Files:
  - `.src/FMain.class`
  - `.src/FMain.form`
- Responsibility: provide a visual/manual test surface for the library

## Dependencies

From `.project`:

- `gb.image`
- `gb.gui`
- `gb.form`
- `gb.settings`

## Public API discovered

### Logging methods

- `Debug(m As String)`
- `Info(m As String)`
- `Warning(m As String)`
- `Error(m As String)`
- `Fatal(m As String)`

### Configuration methods

- `SetMinLevel(level As Integer)`
- `GetMinLevel() As Integer`
- `SetOutput(out As Integer)`
- `GetOutput() As Integer`
- `SetMaxFiles(max As Integer)`
- `GetMaxFiles() As Integer`
- `SetMaxFileSize(size As Long)`
- `GetMaxFileSize() As Long`
- `SetLogFile(path As String)`
- `GetLogFile() As String`
- `SetAppName(name As String)`
- `GetAppName() As String`

### Read properties

- `Levels As String[]`
- `Outputs As String[]`

## Runtime flow

1. Consumer creates `New Log4Gambas3`
2. Consumer configures app name, output mode and path
3. Public methods delegate to `SendMessage()`
4. `SendMessage()` checks minimum log level
5. Output is sent to console, file, both or none
6. File path uses daily naming and cleanup by max-file count

## Technical findings

### Strengths

- API is intentionally small
- defaults are easy to understand
- demo makes manual verification easy
- packaging already points to a Gambas library/component model

### Issues discovered

1. `SendMessage()` overwrites the timestamp because the second assignment uses `=` instead of concatenation.
2. `WriteToFile()` builds the filename with a trailing space after `.log`.
3. `SetMaxFileSize()` stores a value but size-based rotation is not implemented.
4. `CheckFileRotator()` deletes by alphabetical order of `*.log`, not strictly filtered by app prefix.
5. Demo and library source are mixed in the same repository without a dedicated docs map for contributors.
6. Existing repo state already contains local modifications in project metadata and IDE-generated assets.

## Source vs generated artifacts

### Source of truth

- `.src/**/*.class`
- `.src/**/*.form`
- `.project`
- `.component`
- documentation files `*.md`

### Generated or environment-specific

- `.gambas/`
- `*.gambas`
- `.desc/`
- `.info`
- `.startup`
- `.settings`
- `.app.png`
- `.icon.png`
- backup files like `*~`

## Gambas-specific agent rules

1. Treat `.class` and `.form` as text files.
2. Treat `.gambas` as binary/generated artifacts.
3. Remember Gambas is case-insensitive.
4. Avoid deep `.form` edits unless necessary.
5. Prefer extracting logic from forms into reusable classes/modules.

## Suggested skills / MCP usage

### Skills

- `gambas3-modern-dev`: architecture review, naming, safe refactors
- `project-documentation`: docs structure and doc separation
- `clean-code`: when extracting logic or simplifying API internals
- `solid-architect-advisor`: if the project grows beyond a single class

### MCP / tooling

- Engram memory: useful for preserving conventions, discoveries and pending work
- No project-specific MCP resources/templates are currently registered in this environment

## Documentation split decided

- `README.md`: short, persuasive, installation-focused
- `rearme.md`: English technical readme
- `readme-es.md`: Spanish technical readme
- `agent.md`: operational guidance for agents
- `tasks.md`: backlog and improvements
