# Aspire-GaN-Driver

> 基于 HPM5E3Y 系列 MCU 与 GaN 功率器件的 EtherCAT 电机驱动器项目。
>
> An EtherCAT motor-drive project based on HPM5E3Y-series MCUs and GaN power devices.

<p align="center">
  <a href="https://github.com/AspireROS/Aspire-GaN-Driver/tree/Hardware">
    <img src="https://img.shields.io/badge/Hardware-branch-1f6feb?style=flat-square" alt="Hardware branch">
  </a>
  <a href="https://github.com/AspireROS/Aspire-GaN-Driver/tree/Software">
    <img src="https://img.shields.io/badge/Software-branch-2da44e?style=flat-square" alt="Software branch">
  </a>
  <img src="https://img.shields.io/badge/MCU-HPM5E3Y-0091D5?style=flat-square" alt="MCU">
  <img src="https://img.shields.io/badge/Power-GaN-2563eb?style=flat-square" alt="GaN">
  <img src="https://img.shields.io/badge/Control-FOC-f97316?style=flat-square" alt="FOC">
  <img src="https://img.shields.io/badge/Bus-EtherCAT-16a34a?style=flat-square" alt="EtherCAT">
  <img src="https://img.shields.io/badge/License-Apache%202.0-dc2626?style=flat-square" alt="Apache 2.0">
</p>

## 📌 项目简介

Aspire-GaN-Driver 面向高性能电机控制与 EtherCAT 实时通信场景，目标是构建一套基于 HPM5E3Y 系列 RISC-V MCU 和 GaN 功率器件的开放式电机驱动方案。

项目当前采用分支管理硬件与软件资料：

- **`main`**：项目总览、许可协议与仓库导航。
- **[`Hardware`](https://github.com/AspireROS/Aspire-GaN-Driver/tree/Hardware)**：HPM5E3YIVK1 核心板的原理图、PCB 工程、引脚分配和器件资料。
- **[`Software`](https://github.com/AspireROS/Aspire-GaN-Driver/tree/Software)**：基于 HPM5E00 平台的软件、板级支持包和外设示例，包含电机控制及 EtherCAT 相关配置。

> 当前项目仍处于开发阶段。硬件版本、软件功能覆盖范围和可用接口请以对应分支中的实际文件为准。

## 📂 当前内容

### 🔧 硬件分支

硬件资料位于 [`Hardware`](https://github.com/AspireROS/Aspire-GaN-Driver/tree/Hardware) 分支，主要包括：

- `Hardware/Introduction.md`：硬件资料说明。
- `Hardware/PCB Schematic/JLC/`：嘉立创 EDA 工程文件。
- `Hardware/Pin Assignment/Pin Assignment.csv`：MCU 与外设引脚分配表。
- `Hardware/Component Selection & Requirements/`：主控、电源、以太网、CAN、USB 及接口保护等器件资料。

### 💻 软件分支

软件资料位于 [`Software`](https://github.com/AspireROS/Aspire-GaN-Driver/tree/Software) 分支，当前可见内容包括：

- `Software/app/`：应用与外设示例。
- `Software/boards/hpm5e00evk/`：HPM5E00EVK 板级支持、引脚复用、PWM、ADC、QEI 和 EtherCAT 相关配置。
- `Software/boards/hpm5e00evk/README_zh.rst`：开发板说明和接口信息。

## ✨ 主要方向

- 🧠 HPM5E3Y 系列 RISC-V MCU 平台
- ⚡ GaN 功率级与高频电机驱动
- 🎛️ 三相 BLDC/PMSM 电机控制
- 📈 FOC 矢量控制与电流、速度、位置控制环
- 🔌 PWM、ADC、QEI 等电机控制外设协同
- 🔗 EtherCAT 实时通信与从站接口支持
- 🤖 面向机器人关节、运动平台和其他高动态电机系统的原型验证

以上内容描述项目方向；尚未在当前仓库中明确实现或验证的功能，不应视为稳定产品特性。

## 🚀 快速开始

### 获取仓库

克隆主分支：

```bash
git clone https://github.com/AspireROS/Aspire-GaN-Driver.git
cd Aspire-GaN-Driver
```

按需获取硬件或软件分支：

```bash
git fetch origin Hardware Software

# 查看硬件资料
git switch Hardware

# 查看软件资料
git switch Software
```

也可以直接克隆指定分支：

```bash
git clone --branch Hardware https://github.com/AspireROS/Aspire-GaN-Driver.git Aspire-GaN-Driver-Hardware
git clone --branch Software https://github.com/AspireROS/Aspire-GaN-Driver.git Aspire-GaN-Driver-Software
```

### 🧰 软件开发环境

软件分支使用 HPM5E00 系列板级支持和 HPM SDK 生态。开始编译前，请根据软件分支中的板级说明准备：

- HPM SDK 及其依赖
- RISC-V 交叉编译工具链
- 对应版本的 CMake、Ninja 或 Make
- J-Link、CMSIS-DAP 或其他兼容调试器
- EtherCAT 主站环境（进行 EtherCAT 联调时）

由于当前 `main` 分支不包含构建工程，具体的配置、编译和烧录命令应以 [`Software`](https://github.com/AspireROS/Aspire-GaN-Driver/tree/Software) 分支的实际构建文件为准。

## ⚠️ 硬件安全

本项目涉及电机功率驱动和 GaN 开关器件，调试时可能存在高压、触电、短路、器件损坏和机械运动风险：

- 上电前确认电源极性、母线电压、接地和限流设置。
- 初次上电使用隔离电源或限流方案，并从较低母线电压开始验证。
- 上电后不要触碰功率器件、母线端子或裸露导体。
- 焊接和调试过程中采取 ESD 防护措施。
- 连接电机前先确认 PWM 默认状态、硬件使能和故障保护逻辑。
- 任何实际应用都必须根据目标系统完成电气安全、EMC、热设计、可靠性和机械安全验证。

本项目仅供学习、研究和原型验证使用，不构成可直接用于量产设备的安全保证。

## 🤝 贡献指南

欢迎通过 Issue 和 Pull Request 参与改进。提交问题时请尽量提供：

- 使用的分支、硬件版本和软件 commit
- 芯片、调试器、工具链及构建环境
- 最小复现步骤和完整错误日志
- 必要时附上原理图位置、波形或现场照片

提交代码前，请完成与改动相关的编译、基础功能验证和文档更新。

## 📜 开源协议

本项目采用 [Apache License 2.0](./LICENSE) 开源协议。使用、修改或分发本项目时，请遵守许可证中的版权、专利和免责声明条款。

## 🙏 致谢

- HPMicro HPM SDK 及相关开发工具
- EtherCAT 生态与开源社区
- GaN 器件及电机控制领域的技术资料与社区贡献
