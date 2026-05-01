# aerobeat-input-gamepad

Future-facing AeroBeat gamepad input package for accessibility, platform exploration, and controller-side experiments.

## Repo stance

AeroBeat v1 gameplay is officially **camera-first**.

This repo remains in the workspace so the broader input architecture can keep a documented gamepad path, but gamepad is **not** an official v1 gameplay input target. Its current role is narrower:

- **Official v1 gameplay path:** camera providers
- **Current gamepad role:** future-facing accessibility and platform exploration
- **Not a current product promise:** equal-status gameplay parity with the camera-first Boxing and Flow path
- **Still useful for:** controller experiments, future platform planning, and accessibility research

In other words: this package stays visible as documented future work without implying that AeroBeat currently ships or endorses gamepad as an official v1 gameplay mode.

## Repository details

- **Type:** Input driver package
- **License:** **Mozilla Public License 2.0 (MPL 2.0)**
- **Primary dependency:** `aerobeat-input-core`
- **Optional future-facing dependencies:** vendor/controller integrations as needed

## GodotEnv development flow

This repo uses the AeroBeat GodotEnv package convention.

- Canonical dev/test manifest: `.testbed/addons.jsonc`
- Installed dev/test addons: `.testbed/addons/`
- GodotEnv cache: `.testbed/.addons/`
- Hidden workbench project: `.testbed/project.godot`
- Repo-local unit tests: `.testbed/tests/`

The repo root remains the package/published boundary for downstream consumers. Day-to-day development, debugging, and validation happen from the hidden `.testbed/` workbench using the pinned OpenClaw toolchain: Godot `4.6.2 stable standard`.

### Restore dev/test dependencies

From the repo root:

```bash
cd .testbed
godotenv addons install
```

That restores this repo's current dev/test manifest into `.testbed/addons/`, including the shared `aerobeat-input-core` contract package plus GUT for validation.

### Open the workbench

From the repo root:

```bash
godot --editor --path .testbed
```

Use this `.testbed/` project as the canonical direct-development and bugfinding surface for future gamepad-driver work.

### Import smoke check

From the repo root:

```bash
godot --headless --path .testbed --import
```

### Run unit tests

From the repo root:

```bash
godot --headless --path .testbed --script addons/gut/gut_cmdln.gd \
  -gdir=res://tests \
  -ginclude_subdirs \
  -gexit
```

### Validation notes

- `.testbed/addons.jsonc` is the committed dev/test dependency contract.
- The manifest should describe the shared contract dependency as `aerobeat-input-core`, matching current lane ownership.
- Repo-local unit tests live under `.testbed/tests/`; this repo's current package payload is rooted at `/`, so the workbench does not ship a `.testbed/src` bridge for this subset.
- Validation for this repo should preserve the downscoped product truth: gamepad remains documented future/accessibility/platform exploration, while official v1 gameplay support stays camera-first.
