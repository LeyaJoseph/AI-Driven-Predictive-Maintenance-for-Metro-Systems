# AI Driven Predictive Maintenance for Metro Systems
Unsupervised anomaly detection using an autoencoder to identify early failure patterns in high-frequency sensor data from a metro train Air Production Unit (APU), enabling predictive maintenance in a safety-critical system.

---

## Overview
This project applies an unsupervised machine learning approach to predictive maintenance for metro systems.  
An autoencoder-based anomaly detection model is developed to detect failure patterns in sensor data from an Air Production Unit (APU), a critical subsystem with no redundancy.

The model successfully detects documented failure events in advance, demonstrating how machine learning can support proactive maintenance decisions and reduce operational disruptions in real-world transportation systems.

---

## Problem Context: Predictive Maintenance of APU

### The Need for Predictive Maintenance
The Air Production Unit (APU) is a highly demanded component on a metro vehicle and operates continuously throughout the day. It supplies compressed air to multiple subsystems, including:

- Secondary suspension system (maintains vehicle height regardless of passenger load)
- Other pneumatic control systems

Key challenges:
- **No redundancy**: APU failure leads to immediate train removal from service
- **Traditional threshold-based monitoring fails** to detect early degradation
- Failures are often sudden and difficult to anticipate

---

## Objective
The objectives of predictive maintenance for the APU are to:

- Reduce operational problems
- Reduce unforeseen stops and downtime
- Shift maintenance strategy from **reactive** to **predictive**
- Enable early fault detection using data-driven methods

---

## Machine Learning Approach: Autoencoder

### Why Autoencoders?
Autoencoders are well-suited for predictive maintenance because they can learn normal operating behavior from sensor data and detect deviations without requiring labeled failure data.

This project leverages autoencoders for:
- **Anomaly detection**: Identify deviations from normal operating patterns
- **Condition monitoring**: Continuous assessment of system health
- **Predictive maintenance**: Early warning of potential failures

---

## Model Architecture & Hyperparameters

### Model Description
- **Encoder**:
  - 3 hidden layers: 128 → 64 → 32 neurons
- **Bottleneck layer**:
  - 12 neurons
- **Decoder**:
  - Mirrors encoder architecture: 32 → 64 → 128 neurons

### Activation Functions
- **ReLU** for hidden layers
  - Computationally efficient
  - Reduces vanishing gradient issues
  - Provided strong performance without requiring alternative activations
- **Linear activation** for output layer
  - Suitable for continuous-valued sensor data

### Optimization
- **Optimizer**: Adam
  - Adaptive learning rate
  - Efficient convergence for large datasets and deep models

---

## Data
- **Dataset**: MetroPT Dataset for Predictive Maintenance  
- **Source**: Public dataset hosted on Zenodo  
- **Link**: https://zenodo.org/record/6854240

### Description
The dataset contains high-frequency multivariate sensor measurements from a metro train Air Production Unit (APU), including normal operation and documented failure events.

-**Training period**:  
  February 1, 2022 – February 27, 2022
- **Test period**:  
  February 28, 2022 – March 2, 2022
- **Data type**: Multivariate time-series sensor data
- **Targets**: Reconstruction error (Mean Squared Error) between autoencoder input and output

The dataset is included in the `data/` directory for reproducibility.

---

## Methodology
1. Train the autoencoder using data representing normal operating conditions
2. Compute reconstruction error (MSE) for each time step
3. Establish anomaly thresholds based on training data distribution
4. Flag anomalies when reconstruction error exceeds thresholds

### Anomaly Thresholds
- **MSE > 10⁻³** → Warning for probable failure  
- **MSE > 10⁻²** → Confirmed failure  

Thresholds were selected using boxplot analysis of reconstruction errors from the training dataset.

---

## Results

- One documented APU failure occurred on **February 28, 2022 at 21:53**
- The autoencoder detected a significant anomaly when:
  - MSE exceeded **10⁻³ at 22:12**
- This corresponds to a **21-minute detection lag**, successfully identifying the failure using an unsupervised approach, where traditional threshold-based methods failed

Additional observations:
- An earlier MSE peak above the warning threshold was observed on February 28, indicating potential early degradation
- The model detected **all documented failure cases** provided in the test timeframe of the dataset

---

## Impact
- Demonstrated effective **early fault detection** in a safety-critical metro system
- Showed the advantage of transitioning from threshold-based monitoring to **data-driven predictive maintenance**, reducing the risk of unplanned downtime and service disruptions
- Validated the applicability of unsupervised ML models in real-world engineering systems

---

## Limitations & Future Work
- Reduce detection latency by:
  - Fine-tuning network depth and neuron count
  - Using finer temporal segmentation instead of aggregated intervals
- Extend approach to:
  - Additional subsystems
  - Real-time or online deployment
- Explore uncertainty quantification and adaptive anomaly thresholds

---

## Repository Structure
├── Autoencoder.ipynb # Model training and evaluation

├── results/

└── README.md

---

## Key Learnings
- Autoencoders are effective for anomaly detection when labeled failure data is scarce
- Reconstruction error provides a reliable indicator of system health
- Domain knowledge is critical for threshold selection and interpretation
- ML can meaningfully support decision-making in safety-critical systems

---

## References
- Veloso, B. R. (2022). *The MetroPT dataset for predictive maintenance*. Scientific Data, 9, 764.

---

