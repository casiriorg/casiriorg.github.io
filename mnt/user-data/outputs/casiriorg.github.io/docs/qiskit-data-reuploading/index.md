# QDR — Qiskit Data Reuploading

**La primera librería pip-instalable y sklearn-compatible para clasificadores cuánticos con Data Re-Uploading, construida sobre Qiskit 2.x.**

[![CI](https://github.com/Carlosandp/qiskit-data-reuploading/actions/workflows/ci.yml/badge.svg)](https://github.com/Carlosandp/qiskit-data-reuploading/actions)
[![PyPI](https://img.shields.io/pypi/v/qiskit-data-reuploading?color=blue)](https://pypi.org/project/qiskit-data-reuploading/)
[![Python](https://img.shields.io/pypi/pyversions/qiskit-data-reuploading)](https://pypi.org/project/qiskit-data-reuploading/)
[![Code License: MIT](https://img.shields.io/badge/Code%20License-MIT-yellow.svg)](https://github.com/Carlosandp/qiskit-data-reuploading/blob/main/LICENSE)

---

## ¿Qué es Data Re-Uploading?

El machine learning clásico codifica los datos **una sola vez** antes de procesarlos. Data Re-Uploading rompe esta suposición: las features de entrada se inyectan en **cada capa** del circuito cuántico, intercaladas con puertas de rotación entrenables.

```
Capa 1:  [ Encode(x) → Train(θ) ]
Capa 2:  [ Encode(x) → Train(θ) ]  ← mismo x, nuevos θ
Capa N:  [ Encode(x) → Train(θ) ]
               ↓
          Medición → clasificación
```

Un solo qubit con suficientes capas puede aproximar cualquier función continua — el análogo cuántico del teorema de aproximación universal. Esto lo convierte en un modelo variacional excepcionalmente compacto para hardware NISQ.

> Implementa la arquitectura de Pérez-Salinas et al. (2020), *"Data re-uploading for a universal quantum classifier"*, Quantum, 4, 226.

---

## Instalación

```bash
# Estándar
pip install qiskit-data-reuploading

# Con soporte para hardware IBM Quantum
pip install "qiskit-data-reuploading[hardware]"
```

**Requisitos:** Python ≥ 3.10 · Qiskit ≥ 2.0 · qiskit-machine-learning ≥ 0.9.0

---

## Quick Start

```python
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import MinMaxScaler
from qdr.models import DataReuploadingClassifier

X, y = load_iris(return_X_y=True)
X = MinMaxScaler().fit_transform(X)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

model = DataReuploadingClassifier(
    n_qubits=2,
    n_layers=5,
    encoding="rx_ry_rz",
    entanglement="full",
    optimizer="COBYLA",
    max_iter=150,
)

model.fit(X_train, y_train)
print(f"Accuracy: {model.score(X_test, y_test):.4f}")
```

---

## Lo que resuelve esta librería

Antes de QDR, no existía en el ecosistema Qiskit:

- Un `DataReuploadingClassifier` instalable vía pip con API sklearn-compatible
- Soporte nativo de data re-uploading en `qiskit-machine-learning`
- Un feature map dedicado en `circuit.library`
- Benchmarks reproducibles (DR vs. MLP/SVM) sobre Qiskit 2.x con primitivas V2

---

## Repositorio

[github.com/Carlosandp/qiskit-data-reuploading](https://github.com/Carlosandp/qiskit-data-reuploading){ .md-button }
[API Reference](api.md){ .md-button .md-button--primary }
