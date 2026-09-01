<div align="center">

# Nyrax · QuickApp Kit

**一套内核，接入任意平台。**
面向跨端快应用的多平台全链路解决方案。

*Nyrax 是 QuickApp Kit 的运行时引擎代号 —— Core 基座平台无关、面向任意平台开放接入；官方引擎已接入 Android · iOS · 嵌入式 LVGL 三端。*

[English](./README.md)

</div>

---

## 这是什么

QuickApp Kit 是一套多平台全链路快应用框架解决方案：

**JS Runtime + 平台无关 C++ Core + 三端渲染后端（Android / iOS / 嵌入式 LVGL）+ 构建 Toolkit + 可观测 / Benchmark 体系。**

Core 平台无关、面向任意平台开放接入；官方引擎已将三端接入**同一个 Core**，并跑通真实 RPK。

- ✅ **Android / iOS** —— 真机可运行
- ✅ **嵌入式** —— 真机验证通过（**ESP32-S3-N16R8**）

## 架构

<div align="center">
  <img src="./assets/架构图-0901.png" width="960" alt="QuickApp Kit 分层架构" />
</div>

## 设计

- **微内核 + 外围扩展** —— 稳定微内核（bridge / 渲染 / 事件 / 生命周期 / Tree / 事务）；外围基于 Contract 可扩展、可裁剪；分层边界 clean 平整。
- **平台无关 C++ Core** —— 核心能力下沉收敛到 Core，零平台泄漏；Platform Port 与 Adapter 机制可接入多平台（已接入 LVGL / Android / iOS 作为渲染后端）。
- **唯一权威 Runtime Tree** —— Core 独占树与 Layout（Yoga），NodeID 驱动，无新旧双树全量 Diff；局部更新复杂度与树规模无关。
- **免 JSON 序列化 bridge** —— 基于 external function 直调，平台侧 Android = JNI / iOS = ObjC++ 桥接 / LVGL = 同进程直调；渲染管线：NodeID 寻址 + 事务驱动。
- **核心部件可替换** —— 关键部件（QuickJS / Yoga）依赖抽象接口（依赖倒置）。
- **核心工具链 Toolkit** —— DSL → Page IR → RPK 编译 / inspect / run + 内置 Benchmark 可观测体系。

## 仓库

| 仓库 | 定位 |
|---|---|
| [quickapp-runtime-core](https://github.com/quickapp-kit/quickapp-runtime-core) | 平台无关 C++ 内核 |
| [quickapp-runtime-js](https://github.com/quickapp-kit/quickapp-runtime-js) | 框架 JS 侧运行时 |
| [quickapp-runtime-android](https://github.com/quickapp-kit/quickapp-runtime-android) | Android 渲染后端 |
| [quickapp-runtime-ios](https://github.com/quickapp-kit/quickapp-runtime-ios) | iOS 渲染后端 |
| [quickapp-runtime-lvgl](https://github.com/quickapp-kit/quickapp-runtime-lvgl) | LVGL 渲染后端 |
| [quickapp-embedded](https://github.com/quickapp-kit/quickapp-embedded) | 按硬件分类的嵌入式真机集成 |
| [quickapp-toolkit](https://github.com/quickapp-kit/quickapp-toolkit) | 编译构建工具（DSL → RPK） |
| [quickapp-benchmark](https://github.com/quickapp-kit/quickapp-benchmark) | 可观测与 Benchmark 体系 |
| [quickapp-examples](https://github.com/quickapp-kit/quickapp-examples) | 示例应用与 fixture |

---

<div align="center">
<sub>MIT Licensed · Built by <a href="https://github.com/BlueStoneQ">BlueStoneQ</a></sub>
</div>
