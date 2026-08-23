# Aspire-GaN-Driver

> 基于 HPM5E3Y 系列 MCU 与 GaN 功率器件的 EtherCAT 电机驱动器硬件设计项目。
>
> Hardware design for an EtherCAT motor driver based on HPM5E3Y-series MCUs and GaN power devices.

<p align="center">
  <a href="https://github.com/AspireROS/Aspire-GaN-Driver/tree/main">
    <img src="https://img.shields.io/badge/Main-overview-6f42c1?style=flat-square" alt="Main branch">
  </a>
  <a href="https://github.com/AspireROS/Aspire-GaN-Driver/tree/Hardware">
    <img src="https://img.shields.io/badge/Hardware-branch-1f6feb?style=flat-square" alt="Hardware branch">
  </a>
  <a href="https://github.com/AspireROS/Aspire-GaN-Driver/tree/Software">
    <img src="https://img.shields.io/badge/Software-branch-2da44e?style=flat-square" alt="Software branch">
  </a>
  <img src="https://img.shields.io/badge/MCU-HPM5E3Y-0091D5?style=flat-square" alt="MCU">
  <img src="https://img.shields.io/badge/Power-GaN-2563eb?style=flat-square" alt="GaN">
  <img src="https://img.shields.io/badge/Bus-EtherCAT-16a34a?style=flat-square" alt="EtherCAT">
  <img src="https://img.shields.io/badge/Design-Hardware-0ea5e9?style=flat-square" alt="Hardware design">
  <img src="https://img.shields.io/badge/Docs-Specs-64748b?style=flat-square" alt="Specifications">
  <img src="https://img.shields.io/badge/Status-Developing-f59e0b?style=flat-square" alt="Developing">
</p>

## 📌 项目简介

本分支用于维护 Aspire-GaN-Driver 项目的硬件设计资料，当前目标硬件为 `HPM5E3YIVK1` 核心板。

硬件以 HPM5E3Y 系列 RISC-V MCU 为核心，围绕 EtherCAT/以太网、CAN、UART、SPI、JTAG、PWM、ADC 和 QEI 等资源进行设计，为 GaN 功率驱动和电机控制应用提供硬件基础。

项目分支职责如下：

- 🏠 `main`：项目总览、仓库导航和通用说明。
- 🔧 `Hardware`：原理图、器件资料、引脚分配、硬件规格和 PCB 工程。
- 💻 `Software`：固件、板级支持包、电机控制和 EtherCAT 软件配置。

当前项目仍处于开发阶段，具体硬件能力、接口定义和电气参数以本分支中的最新设计文件为准。

## 📂 硬件资料

### 🗂️ 目录结构

| 路径 | 内容 |
| --- | --- |
| [`Hardware/BOM/`](./Hardware/BOM/) | 物料及器件相关资料。 |
| [`Hardware/Doc/Datasheet/`](./Hardware/Doc/Datasheet/) | MCU、电源、CAN 和接口保护器件数据手册。 |
| [`Hardware/Doc/Images/`](./Hardware/Doc/Images/) | 硬件设计相关图片或参考资料。 |
| [`Hardware/Doc/Pin Assignment/`](./Hardware/Doc/Pin%20Assignment/) | MCU 引脚分配和信号复用表。 |
| [`Hardware/Doc/Specs/`](./Hardware/Doc/Specs/) | 硬件设计规格、接口要求、设计约束和验收标准。 |
| [`Hardware/PCB Schematic/`](./Hardware/PCB%20Schematic/) | 原理图工程、导出文件和其他 PCB 设计资料。 |

### 📚 关键资料

- 🧱 [HPM5E3YIVK1 硬件设计规格](./Hardware/Doc/Specs/Hardware%20Design%20Specification.md)
- 🔌 [接口定义要求](./Hardware/Doc/Specs/Interface%20Definition%20Requirements.md)
- 📐 [设计约束](./Hardware/Doc/Specs/Constraint%20Design.md)
- 🧪 [验收测试标准](./Hardware/Doc/Specs/Acceptance%20Test%20Criteria.md)
- 🧭 [Pin Assignment.csv](./Hardware/Doc/Pin%20Assignment/Pin%20Assignment.csv)
- 🧠 [HPM5E00 数据手册](./Hardware/Doc/Datasheet/HPM5E00.pdf)

## 🔌 当前硬件资源

根据当前引脚分配表，设计涉及以下主要 MCU 资源：

- 🌐 `ESC0`、`ETH0` 和 `ENET_PHY`：EtherCAT/以太网接口。
- 🚌 `MCAN0`：CAN 接口。
- 🖥️ `UART0.A`：调试串口。
- 🛠️ `JTAG.A`：程序下载和硬件调试。
- 🔄 `SPI1.B`：SPI 扩展接口。
- ⚡ `PWM0`：电机控制 PWM 输出。
- 📈 `ADC0`：模拟量采样。
- 🧭 `QEI1`：编码器 A/B/Z 输入。

上述资源的最终连接关系应同时核对原理图、`Pin Assignment.csv`、软件引脚初始化和接口规格文档。

## 🧩 器件资料

当前数据手册目录包含：

- 🧠 主控：`HPM5E00.pdf`
- 🔋 电源：`AP63205WU-7.pdf`、`LMR38020FDDAR.pdf`、`RT9013-33GB.pdf`、`TPS62A02DRLR.pdf`
- 🚌 CAN/通信：`SIT1042AQTK3.pdf`
- 🛡️ 接口保护：`PRTR5V0U2X.pdf`

器件替代或新增器件时，应同步更新数据手册、BOM、原理图、设计约束和验收测试标准。

## 🚀 建议使用流程

1. 🧱 阅读 [硬件设计规格](./Hardware/Doc/Specs/Hardware%20Design%20Specification.md)，了解系统组成和设计目标。
2. 🔌 阅读 [接口定义要求](./Hardware/Doc/Specs/Interface%20Definition%20Requirements.md)，确认接口、信号和复用资源。
3. 📐 阅读 [设计约束](./Hardware/Doc/Specs/Constraint%20Design.md)，落实电源、Layout、EMC、热和制造要求。
4. 🧭 对照 [Pin Assignment.csv](./Hardware/Doc/Pin%20Assignment/Pin%20Assignment.csv) 和数据手册检查引脚及电气连接。
5. 🧪 根据 [验收测试标准](./Hardware/Doc/Specs/Acceptance%20Test%20Criteria.md) 完成样板检查和功能验证。

## ⚠️ 硬件安全

本项目涉及电机功率驱动和 GaN 开关器件，调试时可能存在高压、触电、短路、器件损坏和机械运动风险：

- 上电前确认电源极性、母线电压、接地和限流设置。
- 初次上电使用隔离电源或限流方案，并从较低母线电压开始验证。
- 上电后不要触碰功率器件、母线端子或裸露导体。
- 焊接和调试过程中采取 ESD 防护措施。
- 连接电机前先确认 PWM 默认状态、硬件使能和故障保护逻辑。
- 实际应用前必须完成电气安全、EMC、热设计、可靠性和机械安全验证。

本项目仅供学习、研究和原型验证使用，不构成可直接用于量产设备的安全保证。

## 📝 文档维护

- 🔄 设计变更必须同步更新原理图、PCB、BOM、引脚分配和相关规格文档。
- 📏 文档中的具体电压、电流、阻抗、时序和温度参数应以经评审的设计文件和器件数据手册为准。
- 🏷️ 发布新的硬件版本时，应在文档中记录版本号、变更内容、测试结果和遗留问题。
- ✅ 未经验证的功能或参数不得作为已实现的产品特性对外使用。
