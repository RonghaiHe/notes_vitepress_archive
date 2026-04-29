# AI-enabled MEMS Sensors and Applications
Why do we need ‘AI’ algorithms for MEMS sensors?

- Measurement Limitations of MEMS sensors?
  - Response to Physical Input
  - Signal to Noise Ratio
  - Drift over Time
- Examples of AI-enabled Sensor Applications
  - Introduction to AI-enabled Sensor Signal Processing and Classification
  - Examples of Applications

## Limitation

Key **Noise** Sources in Electronic Circuits:
- Thermal noise
- Shot noise
- Flicker noise
- Amplifier noise
- Power-supply noise
- Quantization+sampling noise

Why Wearable IMU Position Tracking **Drifts**?
Orientation can be tracked well; absolute position drifts fast because acceleration is integrated twice and bias accumulates as $t^2$.

Even with excellent noise density, bias and gravity-leakage dominate long-term drift. External references(GPS, ZUPT, map matching, UWB, vision) are needed for stable position

## Application: behavior classification
Data Processing for Behavior Classification:
1. **Raw data**
2. **Preprocessing**: filter, normalization, Fourier transform...
3. **Segmentation**: sliding window, ...
4. **Feature Extraction**: time domain, frequency domain, heuristic domain, ...
5. **Dimension Reduction**: PCA, UMAP, ...
6. **Classification**: Naive bayes, Neural network, kNN, SVM, ...

## Conclusion
- **Cyber Physical Human Systems** (CPHS): connections between physical world, cyber world, and humans/animals to create innovative systems and applications.
- Combining MEMS, Nanotechnology, and AI are fundamentally important to the development of human-centric, low power, ubiquitous, mobile, and intelligent sensing platforms:
  - **Healthcare**: Flexible, skin-like sensors for TCM-based diagnosis
  - **Drug discovery**: Injectable Motion Sensor for animal motion tracking and recognition
  - **Sports**: An IoT framework for next-generation sports training
