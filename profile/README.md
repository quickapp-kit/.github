<div align="center">

# Nyrax · QuickApp Kit

**One core, any platform.**
A full-stack, multi-platform solution for cross-platform quick apps.

*Nyrax is the runtime engine at the heart of QuickApp Kit — the Core is platform-independent and open to any platform; the official engine has already wired in three targets: Android · iOS · embedded LVGL.*

[简体中文](./README.zh-CN.md)

<br/>

<table>
<tr>
<td align="center"><video src="https://github.com/user-attachments/assets/e4f06224-806b-4b5b-87d7-6aba62e84303" width="220" autoplay loop muted playsinline></video><br/><sub>LVGL simulator</sub></td>
<td align="center"><video src="https://github.com/user-attachments/assets/e19887ed-3a6e-4598-9377-4a90ffa645a0" width="220" autoplay loop muted playsinline></video><br/><sub>Android simulator</sub></td>
<td align="center"><video src="https://github.com/user-attachments/assets/3cbea948-f483-423c-86ad-67f1ea944609" width="220" autoplay loop muted playsinline></video><br/><sub>iOS simulator</sub></td>
</tr>
</table>

</div>

---

## What it is

QuickApp Kit is a full-stack, multi-platform quick-app framework:

**JS Runtime + platform-independent C++ Core + three rendering backends (Android / iOS / embedded LVGL) + a build Toolkit + an observability/benchmark suite.**

The Core is platform-independent and open for any platform to attach; the official engine has already wired three backends onto the **same Core**, all running real RPK packages.

- ✅ **Android / iOS** — running on real devices
- ✅ **Embedded** — verified on real hardware (**ESP32-S3-N16R8**)

## Architecture

<div align="center">
  <img src="./assets/架构图-0901.png" width="960" alt="QuickApp Kit layered architecture" />
</div>

## Design Principles

- **Single source of truth, no redundancy** — state has one authoritative representation (a single authoritative Runtime Tree); no dual-tree redundancy, no full diff — information isn't duplicated, actions aren't repeated.
- **Protocols / interfaces define boundaries** — every cross-layer boundary (Core↔Platform, JS↔Core) starts with a protocol and interface, before any implementation.
- **Dependency inversion, swappable** — core parts depend on abstract interfaces, no direct coupling; replaceable and upgradable (the JS engine is implemented this way; other parts to follow).
- **Heavy lifting at compile time, light at runtime** — Page IR, compile-time static dependencies, ID-driven incremental updates; push computation to compile time where possible.
- **Stable kernel + trimmable periphery** — periphery trimmed per target platform (down to feature / component granularity); the build scales small-to-large across resource budgets.
- **Microkernel + plugin extensibility (open-closed)** — features / components extend via protocols on demand; open for extension, closed to kernel modification — no kernel changes needed.

## Design

- **Microkernel + trimmable periphery** — a stable microkernel (bridge / render / event / lifecycle / tree / transaction); the periphery is contract-based, composable and trimmable; **clean, even layering** across boundaries.
- **Platform-independent C++ Core** — core logic **pushed down** and consolidated into the Core, **zero platform leakage**; the Platform Port + Adapter mechanism attaches any platform (LVGL / Android / iOS already wired in as rendering backends).
- **Single authoritative Runtime Tree** — the Core owns the tree and layout (Yoga), NodeID-driven, **no old/new dual-tree full diff**; local-update cost stays independent of tree size.
- **Runtime cost shifted to compile time** — template structure and a stable ID system are finalized at compile time (Page IR); the runtime does pure ID-addressed incremental updates — no tree building, no full-tree diff.
- **JSON-free bridge** — **External function/object** direct calls, no per-call JSON serialization; platform side is Android = JNI / iOS = ObjC++ / LVGL = in-process. Render pipeline: NodeID addressing + transaction-driven.
- **Protocol-driven boundaries** — every boundary (JS↔Core / Core↔Platform) goes through a uniform message protocol, not direct function calls — decoupled, extensible, predictable and composable.
- **Dependency inversion, swappable** — core parts depend on abstract interfaces, no direct coupling; replaceable and upgradable. The JS engine is implemented this way; other parts will follow the same design as time allows.
- **Toolkit** — DSL → Page IR → RPK compile / inspect / run, with a built-in benchmark & observability suite.

## Repositories

| Repo | Role |
|---|---|
| [quickapp-runtime-core](https://github.com/quickapp-kit/quickapp-runtime-core) | Platform-independent C++ kernel |
| [quickapp-runtime-js](https://github.com/quickapp-kit/quickapp-runtime-js) | Framework JS-side runtime |
| [quickapp-runtime-android](https://github.com/quickapp-kit/quickapp-runtime-android) | Android rendering backend |
| [quickapp-runtime-ios](https://github.com/quickapp-kit/quickapp-runtime-ios) | iOS rendering backend |
| [quickapp-runtime-lvgl](https://github.com/quickapp-kit/quickapp-runtime-lvgl) | LVGL rendering backend |
| [quickapp-embedded](https://github.com/quickapp-kit/quickapp-embedded) | Embedded targets by hardware (real-device integration) |
| [quickapp-toolkit](https://github.com/quickapp-kit/quickapp-toolkit) | Build tool (DSL → RPK) |
| [quickapp-benchmark](https://github.com/quickapp-kit/quickapp-benchmark) | Observability & benchmark suite |
| [quickapp-examples](https://github.com/quickapp-kit/quickapp-examples) | Sample apps & fixtures |

---

<div align="center">
<sub>MIT Licensed · Built by <a href="https://github.com/BlueStoneQ">BlueStoneQ</a></sub>
</div>
