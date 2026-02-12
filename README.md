# 🎧 Fewer Samples, Same Security?
## Evaluating Raw Audio Deepfake Detection Under Compressive Sensing

---

## 📖 Overview

This project investigates the robustness of raw waveform-based audio deepfake detection models under **Compressive Sensing (CS)** constraints.

Most anti-spoofing systems assume access to fully observed, high-resolution audio signals. However, practical deployment environments may involve bandwidth limitations, compressed acquisition hardware, or sub-Nyquist sampling conditions. Under such constraints, detection models must operate with incomplete signal information.

This work studies how much discriminative information for deepfake detection survives when the waveform is dimensionally reduced before being processed by neural networks.

---

## 🎯 Motivation

Deepfake detection models are typically trained and evaluated under ideal signal conditions. In real-world systems, however, signals may be:

- Acquired under hardware constraints  
- Compressed during transmission  
- Limited by bandwidth restrictions  
- Processed on edge devices with reduced sensing capability  

This raises a critical question:

> Can audio deepfake detection systems maintain reliability when only a fraction of the original waveform measurements is available?

---

## 🧠 Core Idea

Instead of feeding the full waveform to the model, we apply **frame-wise Compressive Sensing (CS)** to reduce signal dimensionality.


Each compressed measurement is a linear combination of the original samples. Unlike simple downsampling or masking, compressive sensing preserves distributed information through random projections while reducing dimensionality.

Importantly, **no reconstruction step is performed**. The compressed waveform is directly provided to the model, allowing us to evaluate robustness under true information loss.

---

## 🔬 Experimental Setup

### Audio Configuration

- Sample Rate: 16 kHz  
- Segment Length: 4 seconds (64000 samples)  
- Frame Size: 160 samples  

Each audio segment is divided into frames, and compressive sensing is applied independently to each frame.

### Compression Ratios Evaluated

- 0.75 (25% reduction)
- 0.50 (50% reduction)
- 0.25 (75% reduction)

This enables controlled analysis of performance degradation as signal dimensionality decreases.

---

## 🧠 Models Evaluated

All models operate directly on raw waveform input:

- **AASIST-style architecture** (Convolution + Attention + GRU)
- **RawNet2 Anti-Spoof**
- **RawTFNet**
- **RawFormerL** (Convolution + Transformer Encoder)

These architectures represent different modeling paradigms:

- Convolutional feature extraction  
- Attention-based temporal modeling  
- Recurrent sequence modeling  
- Transformer-based global context modeling  

This diversity allows structured analysis of how architectural design influences robustness under compression.

---

## 📊 Evaluation Focus

Performance is measured using:

- Accuracy  
- F1-score  
- Equal Error Rate (EER)  
- Minimum Tandem Detection Cost Function (min-tDCF)  

Beyond raw performance numbers, this study investigates:

- How detection reliability degrades with dimensional reduction  
- Whether spoofed and bonafide signals exhibit different sparsity behavior  
- Architectural sensitivity to compressed inputs  
- Information redundancy in raw waveform representations  

---

## 🔎 Research Contribution

This work provides:

- A systematic robustness benchmark for waveform-based anti-spoofing models  
- Insight into detection performance under constrained acquisition conditions  
- Comparative analysis across CNN, RNN, attention, and transformer architectures  
- A foundation for deploying secure audio deepfake detection in bandwidth-limited systems  

---

## 🔮 Future Directions

Potential extensions include:

- Learned sensing matrices  
- Reconstruction-based comparison pipelines  
- Adaptive or task-aware compression  
- Cross-dataset generalization studies  
- Theoretical sparsity analysis of spoof versus bonafide signals  