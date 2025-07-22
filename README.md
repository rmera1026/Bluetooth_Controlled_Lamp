# 🔌 STM32 Bluetooth Relay Controller

<div align="center">

![STM32](https://img.shields.io/badge/STM32-03234B?style=for-the-badge&logo=stmicroelectronics&logoColor=white)
![C](https://img.shields.io/badge/C-00599C?style=for-the-badge&logo=c&logoColor=white)
![Bluetooth](https://img.shields.io/badge/Bluetooth-0082FC?style=for-the-badge&logo=bluetooth&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)

*A sophisticated wireless relay control system featuring STM32 microcontroller, Bluetooth connectivity, and real-time OLED feedback*

[Features](#-features) •
[Hardware](#-hardware-components) •
[Installation](#-installation) •
[Usage](#-usage) •
[Technical Details](#-technical-details) •
[Contributing](#-contributing)

</div>

---

## 🌟 Overview

This project implements a **professional-grade Bluetooth-controlled relay system** using the STM32F103RBT6 microcontroller. The system allows wireless control of electrical devices through Bluetooth communication while providing real-time visual feedback via an integrated OLED display. Perfect for home automation, IoT applications, or remote device control scenarios.

### 🎯 Key Highlights
- **Wireless Control**: Seamless Bluetooth communication at 9600 baud
- **Real-time Feedback**: SSD1306 OLED display with status indicators
- **Professional Hardware**: Built on STM32F103RBT6 ARM Cortex-M3 platform
- **Robust Design**: DMA-enabled UART communication for reliable data transfer
- **Clean Architecture**: HAL library implementation with modular design

---

## ✨ Features

### 🔧 Core Functionality
- **Bluetooth Command Interface**: Receive '1' and '0' commands wirelessly
- **Relay Control**: Precise GPIO-based relay switching (PA1)
- **Visual Status Display**: Real-time status updates on 128x64 OLED screen
- **Professional Typography**: Multiple font sizes for optimal readability

### 📡 Communication Features
- **UART1 Interface**: 9600 baud rate with DMA support
- **I2C Display Interface**: Fast and reliable OLED communication
- **Command Processing**: Robust command parsing and execution
- **Error Handling**: Comprehensive error management system

### 🎨 User Experience
- **Intuitive Display**: Clear "Light On" and "Light Off" status messages
- **Responsive Design**: Immediate visual feedback for all commands
- **Clean Interface**: Minimalist display design for easy reading

---

## 🔧 Hardware Components

| Component | Specification | Purpose |
|-----------|--------------|---------|
| **Microcontroller** | STM32F103RBT6 | Main processing unit (ARM Cortex-M3) |
| **Display** | SSD1306 OLED (128x64) | Status visualization |
| **Communication** | Bluetooth Module (HC-05/HC-06) | Wireless command interface |
| **Output Control** | Relay Module | Device switching capability |
| **Interface** | UART + I2C | Communication protocols |

### 📊 Pin Configuration
```
STM32F103RBT6 Pinout:
├── PA1  → Relay Control (GPIO Output)
├── PA5  → Debug LED (GPIO Output)
├── PA9  → UART1 TX (Bluetooth)
├── PA10 → UART1 RX (Bluetooth)
├── PB6  → I2C1 SCL (OLED)
└── PB7  → I2C1 SDA (OLED)
```

---

## 🚀 Installation

### Prerequisites
- **STM32CubeIDE** or compatible ARM development environment
- **STM32CubeMX** for configuration management
- **ARM GCC Toolchain** for compilation
- **ST-Link** or compatible programmer/debugger

### Quick Start
1. **Clone the Repository**
   ```bash
   git clone https://github.com/rmera1026/Bluetooth_Controlled_Lamp.git
   cd Relay_Control
   ```

2. **Open in STM32CubeIDE**
   - Import existing project
   - Select the `Relay_Control` folder

3. **Build the Project**
   ```bash
   # Using command line
   make all
   
   # Or use IDE build (Ctrl+B)
   ```

4. **Flash to STM32**
   - Connect ST-Link debugger
   - Click "Run" or use Flash & Run configuration

### Hardware Setup
1. **Connect Components**:
   - Wire OLED display to I2C1 (PB6, PB7)
   - Connect Bluetooth module to UART1 (PA9, PA10)
   - Attach relay module to PA1
   - Power all components appropriately

2. **Bluetooth Pairing**:
   - Power on the system
   - Pair with Bluetooth module (default: HC-05)
   - Default PIN: `1234` or `0000`

---

## 💡 Usage

### Basic Operation
1. **Power On**: System initializes and displays "Light controller"
2. **Bluetooth Connection**: Connect your device to the Bluetooth module
3. **Send Commands**:
   - Send `'1'` → Turn relay ON → Display shows "Light off"
   - Send `'0'` → Turn relay OFF → Display shows "Light on"

### Command Interface
```c
Commands:
'1' → Relay ON  (GPIO PA1 = HIGH)
'0' → Relay OFF (GPIO PA1 = LOW)
```

### Mobile App Integration
This system can be controlled by any Bluetooth terminal app:
- **Android**: Bluetooth Terminal, Serial Bluetooth Terminal
- **iOS**: BLE Terminal, LightBlue Explorer
- **Custom Apps**: Integrate using Bluetooth Serial protocols

---

## 🔬 Technical Details

### Architecture Overview
```
┌─────────────────┐    ┌──────────────┐    ┌─────────────┐
│   Bluetooth     │───▶│   STM32F103  │───▶│    Relay    │
│     Module      │    │      MCU     │    │   Module    │
└─────────────────┘    └──────┬───────┘    └─────────────┘
                              │
                              ▼
                       ┌─────────────┐
                       │ SSD1306 OLED│
                       │   Display   │
                       └─────────────┘
```

### Software Architecture
- **HAL Driver Layer**: STM32 Hardware Abstraction Layer
- **Peripheral Drivers**: UART, I2C, GPIO, DMA configuration
- **Application Layer**: Command processing and display management
- **OLED Driver**: Custom SSD1306 library integration

### Performance Specifications
- **MCU Frequency**: 8 MHz (HSI oscillator)
- **UART Baud Rate**: 9600 bps
- **I2C Clock Speed**: 100 kHz
- **Response Time**: < 10ms for command execution
- **Display Update**: Real-time status reflection

### Memory Usage
```
Flash Memory: ~15KB used (STM32F103RBT6 has 128KB)
SRAM: ~2KB used (STM32F103RBT6 has 20KB)
```

---

## 📁 Project Structure

```
Relay_Control/
├── 📁 Core/
│   ├── 📁 Inc/                 # Header files
│   │   ├── main.h             # Main application header
│   │   ├── stm32f1xx_hal_conf.h
│   │   └── stm32f1xx_it.h     # Interrupt handlers
│   ├── 📁 Src/                 # Source files
│   │   ├── main.c             # Main application logic
│   │   ├── stm32f1xx_it.c     # Interrupt implementations
│   │   └── system_stm32f1xx.c # System configuration
│   └── 📁 Startup/             # Startup assembly files
├── 📁 Drivers/
│   ├── 📁 STM32F1xx_HAL_Driver/ # STM32 HAL library
│   ├── 📁 CMSIS/               # ARM CMSIS library
│   └── 📁 OLED/                # SSD1306 OLED driver
│       ├── ssd1306.c          # OLED main driver
│       ├── ssd1306.h          # OLED header
│       ├── ssd1306_fonts.c    # Font definitions
│       └── ssd1306_conf.h     # OLED configuration
├── 📁 Debug/                   # Build output directory
├── Relay_Control.ioc          # STM32CubeMX configuration
└── README.md                  # This file
```

---

## 🛠️ Development

### Building from Source
```bash
# Clean build
make clean

# Build project
make all

# Flash to device
make flash

# Debug build
make debug
```

### Customization Options
- **Baud Rate**: Modify `huart1.Init.BaudRate` in `main.c`
- **Display Messages**: Update text strings in main function
- **Pin Configuration**: Adjust GPIO settings in `MX_GPIO_Init()`
- **Additional Commands**: Extend command processing in main loop

### Adding Features
1. **Multiple Relays**: Add more GPIO outputs
2. **Sensor Integration**: Include temperature, humidity sensors
3. **WiFi Connectivity**: Replace Bluetooth with ESP32 module
4. **Mobile App**: Develop custom Android/iOS application

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

### Development Guidelines
- Follow STM32 HAL coding standards
- Comment code thoroughly
- Test on actual hardware
- Update documentation for new features

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- **STMicroelectronics** for the comprehensive HAL library
- **Olivier Van den Eede & Aleksander Alekseev** for the SSD1306 OLED driver
- **ARM** for the CMSIS library and Cortex-M3 architecture

---

## 📞 Contact

**Ronald Mera** - rmera1026@gmail.com

Project Link: [https://github.com/rmera1026/Bluetooth_Controlled_Lamp](https://github.com/rmera1026/Bluetooth_Controlled_Lamp)

---

<div align="center">

**⭐ Star this repository if you found it helpful! ⭐**

*Built with ❤️ and STM32*

</div>
