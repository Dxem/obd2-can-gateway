# lib

Portable C modules that hold the core logic of the gateway.

Code in this directory has **no dependency on the STM32 HAL or any hardware**. Every module must compile with a regular host compiler (gcc, clang, MSVC). This is what makes the logic unit-testable on a PC (see [`../tests`](../tests)).

## Modules

| Module | Purpose | Status |
|---|---|---|
| `can_frame/` | CAN frame structure (ID, DLC, data, 11/29-bit flag) and a ring buffer for frames | planned |
| `slcan/` | Lawicel / SLCAN protocol: text commands to CAN frames and back | planned |
| `isotp/` | ISO 15765-2 transport protocol: segmentation, reassembly, flow control | planned |
| `obd/` | OBD-II requests (modes 01, 09) and decoding of responses into physical values | planned |

## Module layout

Every module follows the same structure:

```
lib/<module>/
├── CMakeLists.txt         add_library(<module> ...)
├── include/<module>/      public headers
│   └── <module>.h
└── src/                   implementation
    └── <module>.c
```

Headers are included with the module prefix to avoid name clashes:

```c
#include "obd/obd.h"
```

## Rules

1. **No hardware access.** No HAL includes, no registers, no interrupts. A module receives data as function arguments and returns results to the caller. Sending a frame on the real bus is the job of `firmware/bsp/`.
2. **No dynamic memory.** No `malloc` / `free`. Buffers are statically sized or provided by the caller.
3. **Explicit error handling.** Functions that can fail return a status code. Truncated or malformed input must be rejected, never trusted.
4. **C++ compatible headers.** Every public header is wrapped so it can be used from the C++ test suite:

   ```c
   #ifdef __cplusplus
   extern "C" {
   #endif

   /* declarations */

   #ifdef __cplusplus
   }
   #endif
   ```

5. **Fixed-width types.** Use `uint8_t`, `uint16_t`, `uint32_t` from `<stdint.h>` instead of `int` or `char` for protocol data.
6. **Every module has tests.** A new module is not merged without a matching test file in `../tests`.

## Adding a new module

1. Create the directory structure shown above.
2. Add `add_library(<module> src/<module>.c)` and `target_include_directories(<module> PUBLIC include)` to its `CMakeLists.txt`.
3. Register the module in the firmware build (`firmware/CMakeLists.txt`) and in the test build (`tests/CMakeLists.txt`).
4. Write tests before or together with the implementation.