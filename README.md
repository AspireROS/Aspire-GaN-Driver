# Aspire-GaN-Driver
> 基于 **HPM5E3Y** + 氮化镓(GaN)功率器件的 EtherCAT 高速伺服电机驱动器开源项目
> Open-source EtherCAT servo driver based on HPM5E3Y MCU & GaN power device

<p align="center">
  <img src="https://img.shields.io/badge/MCU-HPM5E3Y-0091D5?style=flat-square" alt="MCU">
  <img src="https://img.shields.io/badge/Power-GaN-blue?style=flat-square" alt="GaN">
  <img src="https://img.shields.io/badge/Control-FOC-orange?style=flat-square" alt="FOC">
  <img src="https://img.shields.io/badge/Bus-EtherCAT-green?style=flat-square" alt="EtherCAT">
  <img src="https://img.shields.io/badge/License-Apache%202.0-red?style=flat-square" alt="License">
  <img src="https://img.shields.io/badge/Arch-RISC--V-9D2020?style=flat-square" alt="RISC-V">
  <img src="https://img.shields.io/badge/Status-Developing-yellow?style=flat-square" alt="Status">
</p>

## 📌 项目简介
Aspire-GaN-Driver 是一套面向高性能伺服、FOC 电机控制的开源功率驱动方案，主控采用 **HPM5E3Y** 国产高性能 RISC-V MCU，功率级搭载氮化镓（GaN）开关器件，依托 GaN 高频、低开关损耗优势实现高功率密度、高效率驱动；通信层原生支持 **EtherCAT** 工业实时总线，可对接倍福 TwinCAT、IgH EtherCAT Master 等主站，适用于机器人关节、运动平台、测功机、高性能有感 FOC 伺服等场景。

本项目完整开放硬件原理图、PCB、BOM、底层驱动、FOC 控制算法、EtherCAT 从站协议栈、调试上位机对接示例，可供学习、二次开发与工程原型验证。

## ✨ 核心特性
- 🧠 **主控平台**：HPM5E3Y，基于官方 HPM SDK 开发
- ⚡ **功率器件**：氮化镓 GaN，支持高频开关、低损耗、高功率密度
- 🎛️ **控制算法**：有感 FOC 矢量控制，支持 AS5047P 磁编码器，电流/速度/位置三闭环控制，预留滤波、龙伯格观测器、弱磁控制扩展接口
- 🔗 **实时总线**：EtherCAT 从站，CoE 协议，自定义 PDO 映射，支持 DC 分布式时钟同步，满足微秒级实时控制
- 🛠️ **调试接口**：UART / CAN FD / USB / JTAG，兼容 VOFA 在线波形观测，支持实时参数调参
- 🛡️ **硬件保护**：硬件级过流、过压、欠压、过温、硬件刹车、短路保护、驱动使能互锁
- 📦 **完整开源**：原理图、PCB、BOM、固件源码、配套开发文档、TwinCAT 主站测试工程、上位机调试工具

## 🧰 硬件规格
> 可根据硬件版本自行填充实际参数
- 主控芯片：HPM5E3Y
- 功率器件：GaN 氮化镓功率开关
- 母线供电：____ V DC
- 控制方式：三相有感 FOC 矢量控制
- 编码器：SPI 磁编码器（AS5047P）
- 通信接口：EtherCAT、CAN FD、UART、USB
- PWM 开关频率：最高 ____ kHz
- 适配电机：三相永磁同步电机 PMSM / BLDC

## 📂 仓库目录结构
```bash
Aspire-GaN-Driver
├── Hardware                # 硬件资料
│   ├── SCH                 # 原理图工程
│   ├── PCB                 # PCB 工程文件
│   ├── BOM                 # 物料清单
│   └── Datasheet           # 关键器件手册
├── Firmware                # HPM5E3Y 下位机固件
│   ├── app                 # 应用层：FOC 算法、EtherCAT、电机状态机、保护逻辑
│   ├── drivers             # 底层外设驱动：ADC、PWM、SPI、ETH、GPIO、CANFD
│   ├── lib                 # 第三方库：EtherCAT 从站协议栈、数字滤波、坐标变换
│   ├── cmake               # CMake 编译配置脚本
│   └── HPM_SDK             # HPM 官方 SDK（Git 子模块）
├── Tools                   # 配套调试工具
│   ├── PC_Software         # Qt / Python 上位机调试示例
│   ├── TwinCAT_Demo        # EtherCAT 主站测试工程
│   └── Vofa_Config         # VOFA 示波器波形配置文件
├── Docs                    # 全套开发文档
│   ├── QuickStart.md       # 快速上手教程
│   ├── EtherCAT_Guide.md   # EtherCAT 配置与 PDO 映射说明
│   ├── FOC_Algorithm.md     # FOC 控制算法详解
│   └── Hardware_Manual.md  # 硬件调试、焊接、上电测试手册
├── .gitignore
├── CMakeLists.txt
├── LICENSE
└── README.md
```
## 🚀 编译与烧录
### 环境依赖
```bash
- HPM SDK（适配 HPM5E3Y 芯片版本）
- RISC-V GCC 交叉编译工具链
- CMake + Ninja / Make
- J-Link / DAP-Link 调试下载器
- 可选：TwinCAT / IgH EtherCAT Master（总线功能测试）

# 克隆仓库并拉取所有子模块代码
git clone --recursive https://github.com/xxx/Aspire-GaN-Driver.git
cd Aspire-GaN-Driver

# 创建编译输出目录
mkdir build && cd build

# CMake配置工程
cmake ..

# 编译固件
make -j