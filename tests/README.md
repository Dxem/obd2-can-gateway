# tests

Unit tests for the portable modules in [`../lib`](../lib), built and run on a PC.

Tests use [GoogleTest](https://github.com/google/googletest) (C++) and are run with CTest. GoogleTest is downloaded automatically by CMake (`FetchContent`), so no manual installation is needed.

## Structure

```
tests/
├── CMakeLists.txt         fetches GoogleTest, builds lib/ for the host, registers tests
├── test_can_frame.cpp     frame structure, ring buffer
├── test_slcan.cpp         SLCAN parser and encoder
├── test_isotp.cpp         ISO-TP state machine
└── test_obd.cpp           OBD-II request building and PID decoding
```

There is one test file per module in `lib/`.

## Build and run

From the repository root:

```bash
cmake -S tests -B build/tests
cmake --build build/tests
ctest --test-dir build/tests --output-on-failure
```

The same commands run in CI on every pull request. A pull request with failing tests is not merged.

## What to test

- **Known values.** Reference cases from the standard, for example an engine speed response `41 0C 1A F8` must decode to 1726 rpm.
- **Boundaries.** Empty and full buffers, DLC 0 and 8, the highest 11-bit identifier (`0x7FF`).
- **Invalid input.** Truncated responses, wrong ISO-TP sequence numbers, unknown PIDs. The module must return an error, not crash or read past the buffer.
- **Regressions.** Every bug found on real hardware is first reproduced as a failing test, then fixed.

## Test data

Real frames captured from the vehicle are the most valuable test data. Store short captures in `tests/data/` as CSV and reference them from the tests. Never commit captures that contain the full VIN of a vehicle.

## Conventions

- Test names describe behaviour: `ObdDecode.EngineSpeedFromTwoBytes`, not `Test1`.
- One behaviour per test.
- Tests do not depend on each other or on execution order.