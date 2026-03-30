# Log4Gambas3 — Tasks

## High priority

- [x] Fix message formatting in `.src/Clase/Log4Gambas3.class` so timestamp, app name, level and message are all preserved.
- [x] Remove the trailing space in generated log filenames.
- [ ] Define and enforce a clear policy for source vs generated Gambas files in the repository.
- [ ] Review current tracked changes in `.project`, `.component`, `.version`, `.src/FMain.class`, `.src/FMain.form`, `.app.png`, `.icon.png`.

## Medium priority

- [ ] Implement real max-size rotation or rename `SetMaxFileSize()` to reflect current behavior.
- [x] Filter rotation by current app prefix, not only by `*.log`.
- [ ] Decide whether the demo app should stay in the same repo/package as the reusable class.
- [ ] Remove or ignore backup files such as `.src/FMain.class~`.
- [ ] Improve nomenclature consistency in code and docs (`logger`, `log output`, `max files`, `app name`, etc.).

## Documentation

- [ ] Add an explicit packaging/install workflow for producing the `.gambas` library artifact.
- [ ] Document release/versioning strategy.
- [ ] Add a small “how to test manually” section for the demo form.
- [ ] Add examples for console-only, file-only and both outputs.

## Gambas-specific housekeeping

- [ ] Document clearly that `.class` and `.form` are plain text, even if some tools mis-detect them.
- [ ] Document clearly that `.gambas` artifacts are binary/generated.
- [ ] Revisit `.gitignore` to ensure it matches the desired source-control policy.
- [ ] Decide which IDE-generated metadata should remain tracked and which should not.

## Future improvements

- [ ] Consider splitting internal formatting, file writing and rotation into smaller private helpers.
- [ ] Add automated verification if a practical Gambas test workflow is defined.
- [ ] Consider adding localization/documentation consistency for English and Spanish docs.
