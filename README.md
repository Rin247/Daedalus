# Daedalus — OEM Hardware Command Center & System Tuning Suite

Daedalus is an open-source, lightweight Windows hardware command center built with C++20 and Qt 6 / QML (`Daedalus.exe`). Designed as an all-in-one, bloat-free replacement for OEM utility suites (Razer Synapse, ASUS Armoury Crate, Lenovo Vantage/Legion Zone, Acer PredatorSense, MSI Center, Alienware CC), Daedalus combines ThrottleStop & MSI Afterburner tuning parity, BIOS unlocking, driver slimming, custom fan curves, RGB peripheral lighting controls, native HWiNFO-grade telemetry, and a native Vulkan/DX 9/10/11/12 in-game OSD via a privileged service daemon (`DaedalusHwService`).

---

## ⚡ Core Subsystems & Status Matrix

| Subsystem | Features & Capabilities | Status / Roadmap |
|---|---|---|
| **Graphics Engine** | **Vulkan 1.3 & DirectX 12_1** desktop viewport | Active |
| **OEM Command Center** | Razer, ASUS, Lenovo, Acer, MSI, Corsair, Logitech peripheral HID & ACPI control | Active / Expanding |
| **CPU/GPU Overclocking** | Native **ThrottleStop & MSI Afterburner feature parity**: MSR Vcore/Uncore ratio/offsets, PL1/PL2 power, GPU offsets | Active |
| **UI/UX Overhaul & Auto-Tuner** | Modern M3 UI/UX preset controls, automated undervolt stability tester, per-app profiles | Active / Roadmap |
| **Native Telemetry Engine** | Clean-room HWiNFO-grade sensor polling (clocks, package power, die/hotspot/VRM temps) | Active / Expanding |
| **Native In-Game OSD** | Clean-room Vulkan & DX 9/10/11/12 in-game overlay engine, RTSS feature parity, 1% low FPS stats | Active / Expanding |
| **BIOS Kitchen** | UEFI/AMI BIOS image parser, hidden menu unlocker, NVRAM editor, microcode/GOP updates | Active / Expanding |
| **Driver Kitchen & Slimmer** | NVIDIA/AMD driver debloater, telemetry stripper, bare INF repackager, DDU wipe | Active / Expanding |
| **Fan Supervisor** | Custom multi-point fan curves, EC fan polling, OEM laptop thermal tables | Active / Expanding |
| **System Cleaner** | Windows temp/cache cleanup, bloatware service disabler, registry key cleaner | Active |
| **Audio & System Tweaks** | Bluetooth A2DP LDAC/aptX HD codec tuner, battery charge cap, telemetry disabler | Active |

---

## ⚡ Key Features & Subsystem Breakdown

### 🎛️ OEM Command Center & Peripheral Control (`hardware` & `daemon`)
- **Current**: Direct USB HID lighting control for Razer and third-party peripherals, embedded controller (EC) access, embedded matrix lighting grid editor, and background service IPC over named pipes (`DaedalusHwService`).
- **Planned / Roadmap**: Native hardware & peripheral protocol support for **ASUS** (ROG / TUF Armoury Crate replacement), **Lenovo** (Legion Vantage replacement), **Acer** (PredatorSense replacement), **MSI** (Center / Dragon Center replacement), Corsair, and Logitech; unified cross-brand lighting sync profiles and game-reactive ambient lighting.

### ⚡ CPU/GPU Overclocking, Undervolting & Tuning (`views/OcView` & `views/TuningView`)
- **Current**: Native **ThrottleStop and MSI Afterburner feature parity**: MSR-based CPU ratio and voltage offset tuning (Vcore, Uncore/Cache), package power limits adjustment (PL1, PL2, Tau), GPU core/memory clock offsets, and BIOS/MSR safety write guards (`TuningToolGuard`).
- **Planned / Roadmap**: Streamlined Material 3 UI/UX refinement for intuitive tuning controls, one-click preset cards, automated curve optimizer (undervolting stability stress test), per-application tuning profiles, advanced memory timing adjustments, and OEM ACPI WMI mode switching.

### 📊 Native Hardware Telemetry Engine (`core/telemetry`)
- **Current**: Clean-room C++ sensor engine reading low-overhead hardware telemetry (CPU package power, core/bus clocks, die/hotspot/VRM temperatures, VRAM utilization) with full HWiNFO feature parity.
- **Planned / Roadmap**: Custom sensor alert thresholds, historical logging to CSV/JSON, and multi-GPU telemetry tracking.

### 🎮 Native In-Game OSD Overlay Engine (`osd`)
- **Current**: Native Vulkan and DX 9/10/11/12 in-game OSD rendering engine with complete RivaTuner Statistics Server (RTSS) feature parity, custom font rendering, and RTSS IPC fallback compatibility.
- **Planned / Roadmap**: Customizable multi-column OSD layout editor, real-time 1% low / 0.1% low FPS metrics, frame time histogram graphs, and benchmark recording.

### 🔓 BIOS Kitchen & Tweaker/Unlocker (`bios-kitchen`)
- **Current**: UEFI / AMI BIOS image structure parser, NVRAM variable editor, ACPI table reader, and safety BIOS backup flasher.
- **Planned / Roadmap**: Hidden BIOS menu unlocking (exposing hidden AMD CBS/PBS and Intel Advanced overclocking menus), CPU microcode updates, GOP / Option ROM updates, VBIOS / power table limit modifier, and SPI flasher integration.

### ✂️ Driver Kitchen & Slimmer (`driver-kitchen`)
- **Current**: Windows Driver Store inspector (`DriverStoreEnumerator`) for removing stale/duplicate OEM drivers, DDU-style graphics driver wipe, and INF driver package analyzer.
- **Planned / Roadmap**: Automated NVIDIA & AMD graphics driver debloater (stripping GeForce Experience, NvContainer, Telemetry, and AMD bloatware), bare INF driver repackager, clean driver installer builder, and Windows Update driver override blocker.

### 🌀 Fan Supervisor & Thermal Curve Engine (`core/fan`)
- **Current**: Custom multi-point fan curves for CPU, GPU, and chassis fans; EC fan polling; hysteresis and step-delay smoothing.
- **Planned / Roadmap**: OEM laptop fan control support (ASUS ROG/TUF fan tables, Lenovo Legion fan modes, Acer Predator turbo fan toggle, MSI Cooler Boost), acoustic noise vs cooling optimizer, and zero-RPM fan mode toggle.

### 🧹 System Cleaner (`cleaner`)
- **Current**: System temp/cache cleaner, recycle bin management, and junk file scanner.
- **Planned / Roadmap**: OEM background service disabler/bloatware remover, leftover registry key cleaner, and privacy cleaner.

### 🎧 System Tweaks & Bluetooth Audio (`tweaks`)
- **Current**: Windows Bluetooth A2DP audio codec selector (LDAC, aptX HD, AAC, SBC bitrate tuning) and system tweaks manager.
- **Planned / Roadmap**: Windows telemetry disabler, gaming performance mode toggles, battery charge threshold limiter (e.g. 80% charge cap for laptops), and process priority manager.

---

## 🏗️ Architecture & Technology Stack

- **Graphics APIs**: Vulkan 1.3 & DirectX 12_1.
- **UI Shell**: C++20, Qt 6.12, QML, Custom Material 3 dark dashboard layout.
- **Hardware Daemon**: Elevated Windows Service (`DaedalusHwService`) using direct MSR assembly, Win32 kernel APIs, and OEM ACPI WMI interfaces.
- **IPC Protocol**: Secure local Named Pipe communication with input validation write gates.
- **Licensing**: AGPL-3.0.

---

## 🛠️ Building & Running

### Prerequisites
- **Visual Studio 2022** (C++20 MSVC compiler)
- **Qt 6.12** (`msvc2022_64`)

### Build Commands

```bat
:: Build Release binary (Daedalus.exe & DaedalusHwService.exe)
build.bat Release

:: Launch Daedalus
run.bat
```

---

## 📜 License

Daedalus is released under the **GNU Affero General Public License v3.0** (AGPL-3.0). See [`LICENSE`](LICENSE) for details.
