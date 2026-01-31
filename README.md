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
Bronchoscopy is critical for diagnosing lung diseases, but traditional navigation faces three core challenges:
1.  **Visual Blindness:** Lens occlusion by blood/secretions causes immediate loss of localization.
2.  **Catheter Deformation:** Non-linear deformation of flexible catheters leads to model drift.
3.  **High Cost:** Commercial solutions (e.g., Ion, Monarch) rely on expensive EM/FOSS sensors, limiting accessibility.

### Our Solution: ViSA-Nav
We propose a **Bionic Embodied Intelligence** approach inspired by human hand-eye coordination. The system integrates two modalities:
* **Visual Stream:** Self-supervised Visual Odometry (VO) for global perception.
* **Action Stream:** Kinematic priors from operator movements (push/rotate) for local constraints.

---

## 🚀 System Architecture

[cite_start]The core framework consists of three coupled modules :

### 1. Visual Self-Supervised Odometry (Visual-VO)
* **Backbone:** Lightweight networks suitable for edge deployment.
* **Method:** Unsupervised learning using photometric consistency loss to estimate relative pose from endoscopic video streams.
* **Goal:** Provide accurate localization when visual features are rich.

### 2. Action Weak Labeling Network (Action-Net)
* **Input:** Operator action sequences (insertion, rotation, bending).
* **Model:** LSTM / MLP based temporal modeling to predict catheter tip trends.
* **Function:** Acts as a "blind state compensation" mechanism when vision fails.

### 3. Uncertainty-Driven Fusion
* **Mechanism:** An Extended Kalman Filter (EKF) that dynamically adjusts weights based on **Uncertainty Quantification**.
* **Behavior:**
    * *Clear Vision:* Trust Visual-VO.
    * *Lens Occluded:* Smoothly switch to Action-Net predictions.
    * *Deviation Alert:* Trigger warnings when visual-action inconsistency exceeds a threshold.

---

## 🛠️ Tech Stack & Hardware

* **Software:**
    * **OS:** Ubuntu 20.04 / ROS Noetic 
    * **Deep Learning:** PyTorch (Visual backbone & Action sequence modeling)
    * **Simulation:** OpenSim / Custom Virtual Data Factory
* **Hardware (Validation):**
    * Bronchoscopy Simulator (Preclinic PLHX1002-B / PLHXNJ101BX) 
    * Respiratory Motion Simulation System (PLHXNJ001) 

---



## 📥 Installation (Preliminary)

*Current status: Research Prototype. Full release pending.*

```bash
# 1. Clone the repository
git clone [https://github.com/RodimusMeng/ViSA-broncho-nav.git](https://github.com/RodimusMeng/ViSA-broncho-nav.git)
cd visa-broncho-nav

# 2. Install Python dependencies
pip install -r requirements.txt

# 3. Build ROS workspace (if applicable)
catkin_make
source devel/setup.bash
