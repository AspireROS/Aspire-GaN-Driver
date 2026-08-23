# 🧱 HPM5E3YIVK1 硬件设计规格

## 🎯 1. 文档目的

本文档定义 HPM5E3YIVK1 核心板的总体硬件组成、功能边界和设计基线，作为原理图设计、PCB Layout、器件选型和硬件验收的依据。

本文档描述设计要求，不替代器件数据手册、原理图和 PCB 工程文件。涉及具体电压、电流、阻抗、时序和封装参数时，应以最新数据手册和经评审的原理图为准。

## 🧭 2. 设计目标

- 以 HPM5E3Y 系列 MCU 为核心，提供电机控制所需的 PWM、ADC、QEI 和调试资源。
- 提供 EtherCAT 相关控制器、PHY 和差分接口资源。
- 提供 CAN、UART、SPI 和 JTAG 等调试或扩展接口。
- 建立可验证的电源、复位、时钟、保护和状态指示电路。
- 满足原理图、PCB 制造、调试和后续版本迭代的可维护性要求。

## 🧩 3. 系统组成

| 子系统 | 设计内容 | 主要参考资料 |
| --- | --- | --- |
| 主控 | HPM5E3Y 系列 MCU、启动配置、复位、时钟和调试连接 | `../Datasheet/HPM5E00.pdf` |
| 电源 | 输入电源转换、MCU 电源、接口电源和必要的滤波去耦 | `../Datasheet/AP63205WU-7.pdf`、`../Datasheet/LMR38020FDDAR.pdf`、`../Datasheet/RT9013-33GB.pdf`、`../Datasheet/TPS62A02DRLR.pdf` |
| EtherCAT/以太网 | ESC、PHY、差分收发、复位、参考时钟和管理接口 | `../Pin Assignment/Pin Assignment.csv` |
| CAN | MCAN 信号、收发器、终端匹配和保护 | `../Datasheet/SIT1042AQTK3.pdf` |
| 接口保护 | 外部接口的 ESD/浪涌保护和连接器防护 | `../Datasheet/PRTR5V0U2X.pdf` |
| 调试与扩展 | JTAG、UART、SPI、QEI、PWM 和 ADC 信号 | `../Pin Assignment/Pin Assignment.csv` |

## 🔌 4. MCU 资源基线

当前引脚分配文件中已出现以下关键资源：

- `PWM0.P[2:7]`：电机控制 PWM 输出。
- `ADC0.IN00`、`ADC0.IN01`、`ADC0.IN02`、`ADC0.IN03`、`ADC0.IN08`、`ADC0.IN10`、`ADC0.IN11`、`ADC0.IN13`、`ADC0.IN14`、`ADC0.IN15`：模拟采样资源。
- `QEI1.A/B/Z`：编码器输入。
- `ESC0`、`ETH0` 和 `ENET_PHY`：EtherCAT/以太网相关资源。
- `MCAN0.TXD/RXD`：CAN 接口资源。
- `UART0.TXD/RXD/RTS/CTS`：串口资源。
- `SPI1`：SPI 扩展资源。
- `JTAG.TDO/TDI/TCK/TMS/TRST`：调试资源。

最终功能复用必须与原理图、软件引脚初始化和 `Pin Assignment.csv` 三方保持一致。

## 📐 5. 设计要求

### 🔋 5.1 电源与复位

- 各电源轨应具备明确的输入范围、输出电压、最大负载、电源时序和容差要求。
- MCU、PHY、收发器和外部接口电源应根据数据手册配置去耦、滤波和上电时序。
- 复位信号应具备明确的有效电平、保持时间和异常恢复行为。
- 关键电源轨应预留测试点，便于上电前检查和运行状态测量。
- 具体电压和电流值须在原理图评审时补充并冻结。

### 🌐 5.2 高速接口

- EtherCAT/以太网差分信号应保持连续参考平面，按照 PCB 叠层和 PHY 要求控制差分阻抗。
- 差分对长度、间距、过孔、回流路径和连接器区域应满足 Layout 约束。
- PHY 参考时钟、复位、MDIO/MDC 和 LED/状态信号应按器件时序连接。
- 外部接口保护器件应靠近连接器放置，并避免影响高速信号完整性。

### ⚡ 5.3 电机控制信号

- PWM 输出应具备明确的默认状态和硬件使能关系，异常或复位期间不得产生非预期驱动脉冲。
- ADC 输入应根据被测信号范围配置分压、滤波和输入保护，避免超过 MCU 输入范围。
- QEI 输入应明确 A/B/Z 相逻辑、电平、滤波和连接器定义。
- PWM、ADC 和 QEI 信号的命名应与软件配置和测试记录一致。

### 🏭 5.4 可制造性与可维护性

- 器件封装、极性、丝印、测试点和连接器方向应便于生产检查和现场维护。
- 原理图中应标注关键器件型号、替代料限制和未装配选项。
- 版本变更应同步更新 BOM、引脚分配、原理图、规格文档和验收记录。

## 📦 6. 设计输出

- 原理图和 PCB 工程：`Hardware/PCB Schematic/`
- 器件数据手册：`Hardware/Doc/Datasheet/`
- 引脚分配：`Hardware/Doc/Pin Assignment/Pin Assignment.csv`
- 设计约束：`Constraint Design.md`
- 接口定义：`Interface Definition Requirements.md`
- 验收标准：`Acceptance Test Criteria.md`

## 📝 7. 待确认项目

- 母线输入范围、各路电源额定值和最大负载。
- MCU、PHY、收发器和接口的具体电源时序。
- EtherCAT 差分阻抗、时钟方案和连接器定义。
- PWM 频率、ADC 采样率、QEI 输入频率和保护阈值。
- 结构尺寸、散热方式、工作温度和 EMC 等级。
