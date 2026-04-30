# 🧠 Symmetry-Constrained PINN for Graphene Band Structure

> Forked from [weishanlee/pinnGraphene](https://github.com/weishanlee/pinnGraphene)
> Research collaboration — arXiv preprint published 2025

📄 **arXiv:2508.10718** · [Read the paper](https://arxiv.org/abs/2508.10718)

---

## ⚠️ Fork & Contribution Notice

This repository is a fork of the original project. The core methodology, model architecture, mathematical formulation, and training strategy were developed and led by the original authors at Pui Ching Middle School Macau.

**My contributions as a collaborator:**
- Implementation support and code testing
- Documentation assistance
- Technical discussions and review

---

## 📌 About the Project

This project implements **Symmetry-Constrained Multi-Scale Physics-Informed Neural Networks (SCMS-PINNs)** for predicting the electronic band structure of graphene with <2% error across the entire Brillouin zone.

The key idea: instead of letting a neural network learn symmetry implicitly, the model *enforces* graphene's D6h crystallographic symmetry directly through group averaging — guaranteeing exact C₆ᵥ symmetry regardless of network architecture.

**Key results:**
- Band structure error: < 2% across entire Brillouin zone
- Dirac point accuracy: < 0.01 eV deviation
- Fermi velocity: 1.06 × 10⁶ m/s (matches experimental value)
- Training time: ~1 hour on NVIDIA V100

---

## 🏗️ Architecture Highlights

**Multi-Head ResNet** with three specialised heads:
- *K-Head* — captures linear dispersion near Dirac points
- *M-Head* — models saddle point behaviour at M point
- *General Head* — smooth interpolation across the Brillouin zone

**Exact Symmetry Enforcement** via group averaging over all 12 C₆ᵥ operations:
`E_sym(k) = (1/12) Σ_{g∈C₆ᵥ} E_NN(R_g·k)`

**Progressive Training Schedule:**
- Epochs 0–50: mild Dirac constraint (ω_K = 5)
- Epochs 50–150: head specialisation (ω_K = 12)
- Epochs 150+: strong physics enforcement (ω_K = 25)

---

## 🗂️ Repository Structure

```
/codes
  scms_pinn_graphene_v35.py       # Main SCMS-PINN implementation
  train_scms_pinn_v35.py          # Training script
  physics_validation_graphene_v35.py
  comprehensive_visualization_v35.py
  comprehensive_v35_run.sh        # Full pipeline script
/figures                          # Band structure plots, heatmaps, convergence curves
/output                           # Trained models, logs, validation reports
```

---

## 🚀 Quick Start

```bash
git clone https://github.com/weishanlee/pinnGraphene.git
cd pinnGraphene
pip install -r requirements.txt
cd codes
./comprehensive_v35_run.sh
```

Requires: Python 3.8+ · PyTorch 2.3+ · CUDA-enabled GPU (recommended)

---

## 📖 Citation

```bibtex
@article{lee2025scmspinn,
  title={Symmetry-Constrained Multi-Scale Physics-Informed Neural Networks
         for Graphene Electronic Band Structure Prediction},
  author={Lee, Wei Shan and Kwok, I Hang and Leong, Kam Ian
          and Chau, Chi Kiu Althina and Sio, Kei Chon},
  journal={arXiv preprint arXiv:2508.10718},
  year={2025}
}
```

---

## 👥 Authors

| Name | Affiliation |
|------|-------------|
| Wei Shan Lee (corresponding) | Pui Ching Middle School Macau |
| I Hang Kwok | Pui Ching Middle School Macau |
| Kam Ian Leong | Pui Ching Middle School Macau |
| Chi Kiu Althina Chau | Pui Ching Middle School Macau |
| **Kei Chon Sio (Vasco)** | **University of Toronto Mississauga** |

📜 MIT License
