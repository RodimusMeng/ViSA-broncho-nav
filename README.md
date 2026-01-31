# ViSA-broncho-nav
ViSA-Nav: Bronchoscopic Intelligent Navigation via Visual Self-Supervised Learning and Action Weak Labeling.

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![ROS](https://img.shields.io/badge/ROS-Noetic-green.svg)](http://wiki.ros.org/noetic)
[![Framework](https://img.shields.io/badge/PyTorch-1.10%2B-orange.svg)](https://pytorch.org/)

**ViSA-Nav** (Visual Self-supervised & Action-labeled Navigation) is a robust, low-cost bronchoscopic navigation system designed to address clinical challenges such as visual blindness and high hardware costs. By fusing **Visual Self-Supervised Learning** with **Action Weak Labeling**, this system provides real-time position estimation and deviation alerts without relying on expensive electromagnetic sensors.

> **Project Context:** Tongji University SITP Project

---

## 📖 Introduction

### The Clinical Problem
[cite_start]Bronchoscopy is critical for diagnosing lung cancer[cite: 16], but traditional navigation faces three core challenges:
1.  [cite_start]**Visual Blindness:** Lens occlusion by blood/secretions causes immediate loss of localization[cite: 25].
2.  [cite_start]**Catheter Deformation:** Non-linear deformation of flexible catheters leads to model drift[cite: 29].
3.  [cite_start]**High Cost:** Commercial solutions (e.g., Ion, Monarch) rely on expensive EM/FOSS sensors, limiting accessibility[cite: 33, 36].

### Our Solution: ViSA-Nav
[cite_start]We propose a **Bionic Embodied Intelligence** approach inspired by human hand-eye coordination[cite: 41, 43]. The system integrates two modalities:
* [cite_start]**Visual Stream:** Self-supervised Visual Odometry (VO) for global perception[cite: 45].
* [cite_start]**Action Stream:** Kinematic priors from operator movements (push/rotate) for local constraints[cite: 49].

---

## 🚀 System Architecture

[cite_start]The core framework consists of three coupled modules [cite: 44-52]:

### 1. Visual Self-Supervised Odometry (Visual-VO)
* [cite_start]**Backbone:** Lightweight networks (MobileNetV3 / ResNet-18) suitable for edge deployment[cite: 46, 81].
* [cite_start]**Method:** Unsupervised learning using photometric consistency loss to estimate relative pose from endoscopic video streams[cite: 46].
* **Goal:** Provide accurate localization when visual features are rich.

### 2. Action Weak Labeling Network (Action-Net)
* [cite_start]**Input:** Operator action sequences (insertion, rotation, bending)[cite: 49].
* [cite_start]**Model:** LSTM / MLP based temporal modeling to predict catheter tip trends[cite: 49, 87].
* [cite_start]**Function:** Acts as a "blind state compensation" mechanism when vision fails[cite: 49].

### 3. Uncertainty-Driven Fusion
* [cite_start]**Mechanism:** An Extended Kalman Filter (EKF) that dynamically adjusts weights based on **Uncertainty Quantification**[cite: 51, 92].
* **Behavior:**
    * *Clear Vision:* Trust Visual-VO.
    * [cite_start]*Lens Occluded:* Smoothly switch to Action-Net predictions[cite: 52].
    * [cite_start]*Deviation Alert:* Trigger warnings when visual-action inconsistency exceeds a threshold[cite: 70].

---

## 🛠️ Tech Stack & Hardware

* **Software:**
    * [cite_start]**OS:** Ubuntu 20.04 / ROS Noetic [cite: 46, 96]
    * **Deep Learning:** PyTorch (Visual backbone & Action sequence modeling)
    * [cite_start]**Simulation:** OpenSim / Custom Virtual Data Factory [cite: 107]
* **Hardware (Validation):**
    * [cite_start]Bronchoscopy Simulator (Preclinic PLHX1002-B / PLHXNJ101BX) [cite: 116]
    * [cite_start]Respiratory Motion Simulation System (PLHXNJ001) [cite: 116]

---

## 📅 Roadmap (12-Month Plan)

[cite_start]This project follows the SITP timeline[cite: 99].

- [ ] **Phase I (Month 1-3):** Foundation & VO Setup
    - [ ] [cite_start]复现基于光度一致性的 Visual VO (MobileNetV3)[cite: 81, 103].
    - [ ] [cite_start]搭建虚拟数据生成方案[cite: 103].
- [ ] **Phase II (Month 4-6):** Modeling & Simulation
    - [ ] [cite_start]训练动作趋势预测模型 (Action-Net)[cite: 107].
    - [ ] [cite_start]开发视觉质量评估 (VQA) 模块[cite: 107].
- [ ] **Phase III (Month 7-9):** Integration
    - [ ] [cite_start]ROS 系统集成与双模态融合算法 (EKF) 实现[cite: 111].
    - [ ] [cite_start]医疗机器人平台联调与数据采集[cite: 111].
- [ ] **Phase IV (Month 10-12):** Validation
    - [ ] [cite_start]鲁棒性对比实验与消融研究[cite: 115].
    - [ ] [cite_start]偏差预警机制阈值优化[cite: 115].

---

## 📥 Installation (Preliminary)

*Current status: Research Prototype. Full release pending.*

```bash
# 1. Clone the repository
git clone [https://github.com/YourUsername/visa-broncho-nav.git](https://github.com/YourUsername/visa-broncho-nav.git)
cd visa-broncho-nav

# 2. Install Python dependencies
pip install -r requirements.txt

# 3. Build ROS workspace (if applicable)
catkin_make
source devel/setup.bash
