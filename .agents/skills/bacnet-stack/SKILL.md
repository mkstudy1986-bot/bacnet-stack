```markdown
# bacnet-stack Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches you how to contribute to the `bacnet-stack` codebase, a Python project (with C/C++ integration) for BACnet protocol support. It covers the project's coding conventions, commit patterns, and the main workflows for adding features, fixing bugs, updating changelogs, extending BACnet objects, and supporting new ports or backends. You'll learn how to structure code, write tests, and follow the team's established processes for high-quality, maintainable contributions.

---

## Coding Conventions

**File Naming**
- Uses `camelCase` for file names.
  - Example: `bacnetDevice.py`, `objectPropertyHandler.py`

**Import Style**
- Uses relative imports.
  - Example:
    ```python
    from .utils import encode_apdu
    from ..common import constants
    ```

**Export Style**
- Uses named exports (explicitly listing what is exported).
  - Example:
    ```python
    __all__ = ['BacnetDevice', 'ObjectPropertyHandler']
    ```

**Commit Patterns**
- Freeform commit messages, sometimes with `docs` prefix.
- Average message length: ~79 characters.
  - Example:
    ```
    docs: update README with new object property example
    Add support for Modbus gateway backend and update tests
    ```

---

## Workflows

### Feature Development with Tests

**Trigger:** When you want to add a new feature or extend functionality in the codebase.  
**Command:** `/new-feature`

1. Implement feature logic in one or more source files (e.g., `src/bacnet/basic/object/*.c`, `src/bacnet/basic/sys/*.c`).
2. Update or add header files as needed (e.g., `src/bacnet/basic/object/*.h`, `src/bacnet/basic/sys/*.h`).
3. Add or update unit/regression tests (e.g., `test/bacnet/basic/object/*/src/main.c`, `test/bacnet/basic/sys/*/src/main.c`, `test/bacnet/basic/server/*/src/main.c`).
4. Update build/test files (`CMakeLists.txt` or `Makefile`) if new test or source files are added.

**Example:**
```c
// src/bacnet/basic/object/new_object.c
void NewObject_Init(void) {
    // Feature logic here
}
```
```c
// test/bacnet/basic/object/new_object/src/main.c
int main(void) {
    // Regression test for the new feature
}
```

---

### Bugfix with Regression Test

**Trigger:** When you need to fix a bug and ensure it does not regress in the future.  
**Command:** `/bugfix`

1. Identify and fix the bug in the relevant source file(s) (e.g., `src/bacnet/basic/object/*.c`, `src/bacnet/basic/sys/*.c`, `src/bacnet/*.c`).
2. Add or update a test that covers the bug scenario (e.g., `test/bacnet/basic/object/*/src/main.c`, `test/bacnet/basic/sys/*/src/main.c`).
3. Update test build files if necessary (e.g., `test/bacnet/basic/object/*/CMakeLists.txt`).

**Example:**
```c
// src/bacnet/basic/object/device.c
// Fix for property read bug
```
```c
// test/bacnet/basic/object/device/src/main.c
// Test that triggers the bug and verifies the fix
```

---

### Changelog Update for Release or Fix

**Trigger:** When a new feature, bugfix, or security fix is added and needs to be documented for users.  
**Command:** `/update-changelog`

1. Edit `CHANGELOG.md` to add a new entry describing the change.
2. Commit `CHANGELOG.md` with a message referencing the update.

**Example:**
```markdown
## [Unreleased]
### Added
- Support for new Modbus gateway backend

### Fixed
- Device object property read bug
```

---

### Object Property Addition with Tests

**Trigger:** When you want to extend a BACnet object with new properties or API functions.  
**Command:** `/add-object-property`

1. Add or update property logic in the object source file (e.g., `src/bacnet/basic/object/device.c`, `src/bacnet/basic/object/lo.c`).
2. Update the corresponding header file (e.g., `src/bacnet/basic/object/device.h`, `src/bacnet/basic/object/lo.h`).
3. Update or add server logic if needed (e.g., `src/bacnet/basic/server/bacnet_device.c`).
4. Add or update unit tests for the new property (e.g., `test/bacnet/basic/object/device/src/main.c`, `test/bacnet/basic/object/lo/src/main.c`, `test/bacnet/basic/server/bacnet_device/src/main.c`).

**Example:**
```c
// src/bacnet/basic/object/device.c
bool Device_Read_Property(...) {
    // New property logic
}
```
```c
// test/bacnet/basic/object/device/src/main.c
// Test for new device property
```

---

### Port or Backend Support Extension

**Trigger:** When you want to add or update support for a new hardware platform, datalink, or backend system.  
**Command:** `/add-port-backend`

1. Add or modify source files for the new port/backend (e.g., `ports/*/*.c`, `src/bacnet/basic/bzll/*`, `src/bacnet/basic/sys/*`).
2. Update or add Makefiles/CMakeLists.txt for build integration.
3. Add or update documentation (e.g., `README.md` in relevant folder).
4. Add or update tests for the new backend/port (e.g., `test/bacnet/basic/bzll/src/main.c`).

**Example:**
```c
// ports/zigbee/zigbee_port.c
// Implementation for Zigbee datalink
```
```markdown
# README.md (in ports/zigbee/)
Describes how to use the Zigbee port
```

---

## Testing Patterns

- Test files are typically C source files (e.g., `main.c`) under `test/bacnet/basic/*/src/`.
- Test build files: `CMakeLists.txt` or `Makefile` in the relevant test directory.
- Test naming: mirrors the object or feature being tested.
- Testing framework: not explicitly specified; tests are likely custom or minimal C test harnesses.
- For Python code, if present, standard unittest or pytest patterns can be followed.

**Example Test File:**
```c
// test/bacnet/basic/object/device/src/main.c
int main(void) {
    // Setup
    // Run test cases
    // Assert results
    return 0;
}
```

---

## Commands

| Command              | Purpose                                                        |
|----------------------|----------------------------------------------------------------|
| /new-feature         | Start a new feature or API addition with corresponding tests   |
| /bugfix              | Fix a bug and add a regression/unit test                      |
| /update-changelog    | Add an entry to the changelog for a release or fix            |
| /add-object-property | Add new properties or API functions to a BACnet object        |
| /add-port-backend    | Add or update support for a new port, datalink, or backend    |
```
