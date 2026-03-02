# Sensor Characterization and Noise Analysis

As engineers and researchers in sensor systems, we do not merely collect data; we translate physical phenomena into reliable, actionable electrical signals. This guide serves as a rigorous framework for characterizing sensor performance. We will move beyond simple definitions to explore the mathematical nuances and physical trade-offs that define the limits of modern sensing technology.

## The Anatomy of a "Perfect" Sensor

We often begin with the ideal. A "perfect" sensor is a theoretical benchmark that allows us to quantify the shortcomings of real-world hardware.

A perfect sensor is characterized by 6 essential traits:

* **Negligible Noise**: Total absence of electronic, thermal, and mechanical noise components.
* **Minimal Drift**: Absolute stability over time and through extreme environmental fluctuations.
* **High-End Performance**: Exceptional accuracy, precision, sensitivity, and responsivity.
* **Large Signal-to-Noise Ratio (SNR)**: A maximized ratio of signal power to noise power.
* **Optimal Temporal Response**: Instantaneous rise times and an infinitely wide frequency bandwidth.
* **Economical**: Zero or near-zero manufacturing and operational costs.

In practice, a good sensor is defined by its application-specific fitness, categorized by three criteria:

1. Sensitivity: It must be **highly responsive to the specific property** (measurand) it is designed to detect.
2. Isolation: It must remain **insensitive** to any other environmental interferences (cross-sensitivity) likely to be encountered.
3. Non-invasiveness: It must **not alter the property** it is measuring (e.g., a thermometer that does not change the temperature of the liquid it probes).

Why it Matters: Real-world engineering is the art of the trade-off. We rarely seek theoretical perfection; instead, we optimize a sensor's traits to ensure it provides sufficient reliability for the specific constraints of the project.

## Foundational Performance Metrics

To evaluate sensor reliability, we must distinguish between how "true" a measurement is and how "consistent" the sensor remains.

### Accuracy (Trueness) and Bias

Accuracy is the closeness of a measurement to the true value. It is often a composite metric influenced by both random effects and Bias (systematic error). Bias represents the mean offset relative to a reference value and can often be corrected through calibration.

### Precision: Repeatability and Reproducibility

Precision measures the "scatter" of repeated readings.

* **Repeatability**: Consistency over a **short duration** using the same equipment, operator, and environmental conditions.
* **Reproducibility**: Consistency across **varying conditions**, such as different labs, operators, or days.

### Resolution and Threshold

While often used interchangeably, these are distinct limits:

* Resolution: The smallest change in the input signal that produces a discernible change in the output. This is typically governed by ADC quantization bits or inherent physics.
* Threshold: The smallest amount of input stimulus required to result in a starting output change from zero.

Why it Matters: Understanding the distinction between bias and random scatter allows for targeted error correction. A sensor with high precision but high bias is often easier to calibrate than one with high accuracy but low precision.

### Sensitivity and Responsivity

Sensitivity ($S$), or responsivity, is the output change per unit input: $S = \Delta y / \Delta x$ For linear sensors, $S$ is the constant slope of the transfer function. For non-linear sensors, it is the derivative dy/dx at a specific operating point.

### Range and Dynamic Range

* **Measurement Range** (Span): The span of input values within which the sensor operates at its specified accuracy.
* **Dynamic Range**: The ratio between the largest non-saturating signal and the smallest detectable signal, expressed in decibels (dB).

### Linearity

Linearity measures how closely the sensor's response follows a straight line, usually reported as a percentage of Full Scale (FS).

Why it Matters: Linear sensors simplify the data acquisition chain. Sensitivity is our primary tool for optimizing the SNR, especially in low-power MEMS environments.

### The Impact of Noise and Detection Limits

Noise sets the ultimate physical floor for any sensor. It is quantified via RMS or peak-to-peak measurements.

* **Noise Spectral Density**: The distribution of noise power over frequency.
* **White Noise vs. 1/f (Flicker) Noise**: White noise is constant across frequencies, while flicker noise dominates at lower frequencies.
* **Signal-to-Noise Ratio (SNR)**: The ratio of signal power to noise power for a specific bandwidth.
* **Limit of Detection (LOD)**: The minimum input reliably distinguished from noise (often using a 3\sigma threshold).

### The Sensitivity Paradox

It should be noted that a counter-intuitive definition used in high-precision engineering: $\text{Sensitivity} = \frac{\text{System Output Noise}}{\text{Responsivity}}$. In this specific context, a lower numerical value for sensitivity is actually better, as it represents a smaller minimum detectable signal.

Why it Matters: Noise defines the "floor" of performance. If a signal is below the LOD, no amount of digital resolution (ADC bits) can recover it.

### Offset and Gain Errors (calibration terms)
- **Zero offset**: Output at zero input.
- **Gain error**: Slope deviation from ideal.

### Drift and Temperature Effects

Drift can occur at the zero-point (offset) or in the gain (sensitivity) over time. This is often quantified by the Temperature Coefficient (TC) in ppm/°C.

* **Drift and Stability**
  * Zero drift and sensitivity (gain) drift over time.
  * Long-term stability: Change over weeks/months.
  * Includes aging, hysteresis, creep (notably in strain/load sensors).
* **Temperature Effects**
  * Temperature coefficient (TC) of offset and sensitivity (e.g., ppm/°C).
  * Operating temperature range; thermal shock sensitivity.

### Hysteresis

Hysteresis occurs when the sensor output depends on the "history" of the input—whether the current value was approached from an increasing or decreasing direction. It is prevalent in magnetic (ferromagnetic) and ferroelectric materials.

Why it Matters: Environmental stability determines the required frequency of recalibration. High-drift sensors in critical applications require active temperature compensation.

### Operational Bandwidth and Robustness

* **Response Time**: Characterized by rise time and settling time; usually modeled as a first-order time constant.
* **Bandwidth**: The frequency range where the sensor operates effectively, defined at the $-3\text{~dB}$ point.
* **Selectivity**: The ability to ignore undesired measurands (e.g., a magnetometer ignoring nearby electronics). In addition, there's a cross-axis sensitivity in multi-axis sensors.
* **Repeatability** under varying conditions
  Performance vs humidity, pressure, vibration, EMI/EMC environment, mounting stress, supply voltage variation.
* I**nput/Output loading and impedance**
  * Input impedance / loading (if the sensor is passive or interacts with measured system).
  * Output impedance, drive capability, required termination.
* **Power & Self-heating**: High power consumption in resistive sensors can cause self-heating, which alters the very temperature being measured.
* **Reliability & robustness**
  * MTBF (Mean Time Between Failure), failure rate, calibration interval.
  * Shock/vibration ratings, ingress protection (IP), radiation tolerance (if relevant).
* **Interchangeability & calibration uncertainty**
  * Unit-to-unit variation.
  * Calibration method, traceability, and uncertainty budget (often the most "complete" characterization).

Why it Matters: Matching sensor bandwidth to the phenomenon is critical to avoid signal attenuation or data loss.

## Technical Deep Dive: Comparison of Piezoresistive vs. Capacitive Principles
"Responsivity": **capacitive** or **piezoresistive**?

Should we use capacitive or piezoresistive principle to measure **displacement** of **diaphragm** for a pressure sensor?

We analyze the measurement of displacement ($\delta$) in a diaphragm for a MEMS pressure sensor.

### Mathematical Modeling

Using effective moment arm ($l$), thickness ($t$), width ($w$), and Young's Modulus ($E$):

* Strain ($\varepsilon$): $\varepsilon = \frac{3 \delta t}{2 l^2}$
* Spring constant ($k$): $k = \frac{t^3 w E}{4 l^2}$

For Silicon, the Gauge Factor ($G$) typically ranges from 80 to 200. The responsivity ratio is: $\frac{R_\text{cap}}{R_\text{piezo}} = \frac{2}{3} \frac{l^2}{t} \frac{1}{G} \frac{1}{\delta_0}$ (where $\delta_0$ is the initial gap).

> Details can be seen in [Chapter 3: Comparing piezoresistive and capacitive sensors](./3sensing_principles#comparing-piezoresistive-and-capacitive-sensors)

* Note: Inductive sensors utilize Faraday’s law of induction to convert input energy into electrical energy.

Why it Matters: While capacitive sensors offer higher responsivity in MEMS, they are also more susceptible to environmental noise compared to piezoresistive equivalents.

### Static Transfer Functions and Mathematical Modeling

Relationships between output and input signals of the sensor in conditions of very slow changes (i.e., static) of the input signal determine the static sensor characteristics.

Some important sensor characteristics and properties include:
* **transfer function**, from which a **sensitivity** can be determined
* **span** (input full scale) and **FSO** (full scale output)
* **calibration error**
* **hysteresis**
* **linearity**
* **repeatability**
* **resolution** and **threshold**
* **accuracy**
* **precision**

The Transfer Function is the ideal relationship between stimulus $x$ and output $y$.

While the linear model $y = a + bx$ is ideal, real systems often require:

* Logarithmic: $y = a + b \ln x$
* Exponential: $y = a e^{kx}$
* Power: $y = a_0 + a_1 x^c$
* Higher-order Polynomials: Used when standard approximations fail to fit accurately.

### Sensitivity
- The slope $b$ is called “sensitivity” and $a$ (intercept) – the output at zero input.
- Output signal is mostly of electrical nature, as voltage, current, resistance.

For nonlinear transfer function the "**sensitivity**" (or "responsivity") is defined as $S = \mathrm{d}y/\mathrm{d}x$ and depends on the input value x.

Over a limited range, within specified accuracy limits, the nonlinear transfer function can be modeled by straight lines (piece-wise approximation). For these linear approximations the sensitivity can be calculated by:
$$
S = \Delta y / \Delta x
$$

### Span and Full Scale Output (FSO)
An **input full scale** or **span** is determined by a dynamic range of stimuli which may be converted by a sensor, without unacceptably high inaccuracy. For a very broad range of input stimuli, it can be expressed in **decibels (dB)**, defined by using the logarithmic scale. By using decibel scale the signal amplitudes are represented by much smaller numbers.

Used for broad dynamic ranges:

* Power: $1\text{~dB} = 10 \log(P/P_0)$
* Voltage, Pressure, and Current: $1\text{~dB} = 20 \log(V_2/V_1)$

Full scale output (**FSO**) is the difference between ouput signals for maximum and minimum stimuli, respectively. This must include deviations from the ideal transfer function, specified by $\pm\Delta$.

<figure>
   <img src="/Robotics/Sensors/semi7_FSO.png" alt="FSO" width="100%" align="center">
   <div align="center"><figcaption> Figure 1: FSO.</figcaption></div>
</figure>

### Hysteresis
This is a deviation of the sensor output, when it is approached from **different directions**. It occurs in magnetic materials, ferromagnetic materials and ferroelectric materials, as well as in the elastic, electric, and magnetic behavior of materials.

<figure>
   <img src="/Robotics/Sensors/semi7_hy.JPG" alt="Hysteresis" width="100%" align="center">
   <div align="center"><figcaption> Figure 2: Hysteresis, where Delta is the max. difference at output for specified input.</figcaption></div>
</figure>

### Aliasing
Output signal due to sampling frequency of the sensing devices: **Aliasing** occurs when an oscilloscope does not sample the signal fast enough to construct an accurate waveform record. The signal frequency is misidentified, and the waveforms displayed on an oscilloscope become indistinguishable. Aliasing is basically a form of undersampling.

<figure>
   <img src="/Robotics/Sensors/semi7_aliasing.png" alt="Aliasing" width="100%" align="center">
   <div align="center"><figcaption> Figure 3: Aliasing</figcaption></div>
</figure>


### Nonlinearity
This error is specified for sensors, when the nonlinear transfer function is **approximated by a straight line**. It is a maximum deviation of a real transfer function from the straight line and can be specified in % of FSO.

The approximated line can be drawn as the so called "best straight line" which is a line midway between two parallel lines envelpoing output values of a real transfer function.

Another method is based on the least squares procedure.

<figure>
   <img src="/Robotics/Sensors/semi7_nonlinear.JPG" alt="Nonlinearity" width="100%" align="center">
   <div align="center"><figcaption> Figure 4: Nonlinearity.</figcaption></div>
</figure>

### Repeatability
This error is caused by sensor **instability** and can be expressed as the maximum difference between output readings as determined by two calibration
cycles, given in % of FSO.
$$
\delta_r = \Delta / \mathrm{FSO}
$$

<figure>
   <img src="/Robotics/Sensors/semi7_repeat.JPG" alt="Repeatibility" width="100%" align="center">
   <div align="center"><figcaption> Figure 5: Repeatability.</figcaption></div>
</figure>

### Resolution and Threshold
**Threshold** is the smallest increment of stimulus which gives noticeable change in output. **Resolution** is the step change at output during continuous change of input.

<figure>
   <img src="/Robotics/Sensors/semi7_resolution.JPG" alt="Resolution" width="100%" align="center">
   <div align="center"><figcaption> Figure 6: Resolution and threshold.</figcaption></div>
</figure>

### Calibration Error
**Calibration error** is determined by innacuracy permitted by a manufacturer after calibration of a sensor in the factory.

To determine the slope and intercept of the function one applies two stimuli $x_1$ and $x_2$ and the sensor responds with $A_1$ and $A_2$. The higher signal is measured with error – $\Delta$. This results in the error in intercept (new intercept $a_1$, real $a$)
$$
\delta_a = a_a-a = \Delta / (x_2-x_1)
$$

and in the error of the slope
$$
\delta_b = \Delta / (x_2-x_1)
$$

<figure>
   <img src="/Robotics/Sensors/semi7_calibration.png" alt="Calibration" width="100%" align="center">
   <div align="center"><figcaption> Figure 7: Calibration error.</figcaption></div>
</figure>

## Noise
- **Electronic noise**
  A random fluctuation in an **electrical signal**, a characteristic of all electronic circuits. Noise generated by electronic devices varies greatly, as it can be produced by several different effects.
- **Johnson–Nyquist noise** (thermal noise, Johnson noise, or Nyquist noise)
  The electronic noise generated by the **thermal agitation of the charge carriers** (usually the electrons) inside an electrical conductor at equilibrium, which happens regardless of any applied voltage.
  - "**White Noise**", i.e., it cannot be filtered because it is spread out through the entire spectrum
- **Shot noise**
  It's in electronic devices consists of random fluctuations of the electric current in many electrical conductors, due to the **current being carried by discrete charges** (electrons) whose number per unit time fluctuates. This is often an issue in **p-n junctions**. In metal wires this is not an issue, as correlations between individual electrons remove these random fluctuations
- **Flicker noise**
  Also known as $1/f$ noise, is a signal or process with a frequency spectrum that **falls off steadily into the higher frequencies**. It occurs in almost all electronic devices, and results from a variety of effects, though always related to a direct current.
  - Results from a variety of effects, such as **impurities in a conductive channel, generation and recombination noise in a transistor due to base current**, etc. Its origin is not well-known. In electronic devices, it is a low-frequency phenomenon, as the higher frequencies are overshadowed by white noise from other sources
- **Burst noise**
  It's a type of electronic noise that occurs in **semiconductors**. It is also called popcorn noise, impulse noise, bistable noise, or random telegraph signal(RTS) noise.
  - Consists of sudden step-like transitions between two or more levels (non-Gaussian), as high as several hundred millivolts, at random and unpredictable times. Each shift in offset voltage or current lasts for several milliseconds, and the intervals between pulses tend to be in the audio range (less than 100 Hz), leading to the term popcorn noise for the popping or crackling sounds it produces in audio circuits.
- **Avalanche noise**
  A junction phenomenon in a semiconductor in which **carriers in a high-voltage gradient develop sufficient energy to dislodge additional carriers through physical impact**; this agitation creates ragged current flows which are indicated by noise. This is the noise produced when a junction diode is operated at the onset of avalanche breakdown.

## Sensor Calibration
Why calibrate? Because measurements drive decisions. Calibration characterizes error relative to a reference; adjustment applies corrections

Calibration: choose the model that matches physics + required accuracy

### Example of calibration

Calibrating a Temperature Sensor
* **Define requirements**: sensor type (RTD/thermistor/TC), range, target uncertainty, pass/fail criteria.
* **Select traceable reference(s)**: calibrated reference thermometer + readout, certificate, uncertainties.
* **Stabilize**: warm up instruments; wait for thermal equilibrium (set stability rule, e.g., drift < threshold over N minutes).
* **Plan calibration points**: choose 3–10 points across the as-used range; include endpoints; add points near critical temps.
* **Run up/down sequence**: increasing then decreasing temperatures to assess hysteresis (when applicable).
* **Acquire data correctly**: log reference + DUT simultaneously; specify sampling rate, averaging window, bandwidth/filtering; record time stamps.
* **Apply corrections**: compensate for known effects (lead-wire resistance for RTDs, cold-junction compensation for thermocouples, self-heating checks).
* **Compute calibration**: error at each point (DUT − reference); fit model (offset/gain, polynomial,
or lookup table); check residuals.
* **Estimate uncertainty**: include reference, bath stability/uniformity, repeatability, resolution, drift, fit residuals; report expanded uncertainty UUU with kkk.
* **Document & label**: conditions (ambient, immersion, medium), results, coefficients/table, validity range, date, traceability; apply calibration label.

Calibrating a Force Sensor (page 1)
* **Define scope & criteria**: sensor type (load cell/force transducer), range,
tension/compression, accuracy target, pass/fail limits.
* **Select traceable reference**: deadweights or force standard machine with valid certificate; confirm uncertainty and capacity margin.
* **Mounting & alignment**: proper fixturing, centered load line, minimize side-load/moment; use correct adapters; torque per spec.
* **Warm-up & stabilization**: power on instrumentation; precondition sensor; ensure thermal/mechanical equilibrium.
* **Zero & tare procedure**: establish zero under no-load with mounting in place; define zeroing frequency.
* **Preloading / cycling**: apply several load cycles to reduce seating effects; document number of cycles.
* **Choose calibration points**: 5–10 points across range (incl. 0 and near full-scale); include denser points where used most.
* **Loading sequence**: run ascending and descending loads to capture hysteresis; include holds at each step for stabilization.
* **Data acquisition**: record reference force and sensor output simultaneously; specify sampling
rate, averaging window, and settling time.
* **Evaluate key errors**: sensitivity (slope), nonlinearity, hysteresis, repeatability; check for creep during hold periods.
* **Fit calibration curve**: linear (mV/V vs N) or polynomial/lookup; generate coefficients and input/output units clearly.
* **Uncertainty budget**: reference uncertainty, alignment/fixtures, resolution, repeatability, creep, temperature effects, fit residuals; report expanded UUU (with kkk).
* **Document & label**: conditions (orientation, adapters, excitation, temperature), results, validity range, traceability; set recalibration interval.

## Ultimate Sensitivity of a Mechanical Sensor
"**Thermal Equivalent Noise**"
* Molecular movements due to temperature variations within a mechanical structures may cause random **vibrations** of the mechanical structure – this random mechanical movement may be picked up by the **mechanical-to-electrical energy transducer** (i.e., piezoresistive, piezoelectric, or capacitive) of your sensing system, which results in **noise due to molecular movement**.

<figure>
   <img src="/Robotics/Sensors/semi7_handwriting.png" alt="Overall" width="100%" align="center">
   <div align="center"><figcaption> Figure 8: Overall system noise.</figcaption></div>
</figure>

### Error Sources: Thermal Noise

The **Equipartition Theorem** says that: **noise** is associated with any phenomena which convert mechanical or electric energy into heat. Thermal noise is equally distributed in frequency.

For the cantilever beam, the thermal energy os $\frac12K_BT$ (Some says $\frac32K_BT$), where $K_B$ is Boltzmann constant=$1.38064852 \times 10^{-23} \mathrm{~m^2 kg s^{-2}K^{-1}}$, $T$ is the absolute temperature.

$$
\frac12K_BT=\frac12kx^2 \to x=\sqrt{\frac{K_BT}{k}}
$$

Assume this is a second order system;
The thermal mechanical energy is $\frac{1}{2} K_{B} T$.
The output Xr and input acceleration $\ddot{{X}}_{i}$ has the following relationship:
(i.e., a $\mathbf{2}^{\text {nd }}$ order mass-spring-damper response system)

$$
\frac{X_r}{\ddot{X}_i}=\sqrt{\frac{1}{\left(\omega_{0}^{2}-\omega^{2}\right)^{2}+\left(\frac{\omega \omega_{0}}{Q}\right)^{2}}} \longleftrightarrow\left|X_{r T}\right|^{2}=\frac{\left(F_{T} / m\right)^{2}}{\left(\omega_{0}^{2}-\omega^{2}\right)^{2}+\left(\frac{\omega \omega_{0}}{Q}\right)^{2}}
$$

Where, ${Q}=\frac{{m} \omega_{0}}{{R}}$ is the quality factor, and R is the viscous dissipation factor. ${F}_{\mathrm{T}}$ is the thermal equivalent force. ${X}_{\mathrm{rT}}$ is the thermal equivalent displacement.

The root mean square of thermal equivalent displacement is:

$$
\begin{aligned}
\left(X_{r T}\right)_\text{rms}^{2}=&\int_{0}^{\infty} \frac{\left(F_{T} / m\right)^{2}}{\left(\omega_{0}^{2}-\omega^{2}\right)^{2}+\left(\frac{\omega \omega_{0}}{Q}\right)^{2}} \mathrm{~d} \omega\\
=&\int_{0}^{\infty} \frac{\left(F_{T} / k\right)^{2}}{\left(\frac{m}{k}\right)^{2} \omega^{4}+\frac{R^{2}-2 m k}{k^{2}} \omega^{2}+1} \mathrm{~d} \omega  
\end{aligned}
$$

Consider:

$$
\int_{0}^{\infty} \frac{a^{2}-b^{2}}{a^{2} b^{2} x^{4}+\left(a^{2}+b^{2}\right) x^{2}+1} d x=a \cdot \tan (a x)-\left.b \cdot \tan (b x)\right|_{0} ^{\infty}=\frac{\pi}{2}(a-b)
$$

Let:

$$
a b=\frac{m}{k}, \text { and } a^{2}+b^{2}=\frac{R^{2}-2 m k}{k^{2}}
$$

We can get:

$$
\left(X_{r T}\right)_\text{rms}^{2}=\left(F_{T} / k\right)^{2} \frac{\pi}{2(a+b)}=\frac{\pi F_{T}^{2}}{2 R k}
$$

Let the thermal energy equal the mechanical energy:

$$
\frac{1}{2} K_{B} T=\frac{1}{2} k\left(x_{r T}\right)_\text{rms}^{2}=\frac{1}{2} k \frac{\pi F_{T}^{2}}{2 R k}
$$

The thermal equivalent force (TEF) is:

$$
F_{T}=\sqrt{\frac{2 R {K}_{B} {T}}{\pi}}
$$

The thermal equivalent acceleration (TEA) is:

$$
\ddot{X}_{T}=\frac{F_{T}}{m}=\sqrt{\frac{2 R K_{B} {T}}{m^{2} \pi}}
$$


Example: Thermal Noise in **AFM**
* Thermal noise of the AFM (atomic force microscope) cantilever is a significant sources of noise when trying to detect forces between nano-scale entities.
* Thermal noise is caused by random thermal excitations that result in positional fluctuations of the cantilever, thereby setting a lower limit on the force resolution in AFM measurements

Thermal noise equivalent acceleration
$$
\sqrt{4K_BT\frac{\omega_0m}{Q}}
$$

AFM Sensor Transduction Principle
* Relationship between force and the probe distance from sample
  * $r < r_0$, repulsive force
  * $r > r_0$, attractive force

### Derivation of Thermal Equivalent Displacement
Given that

$$
\frac{\left|x_{\gamma}\right|}{\left|\ddot{x}_{i}\right|}=\left[\frac{1}{\left(\omega_{o}-\omega^{2}\right)^{2}+\frac{\omega^{2} \omega_{0}^{2}}{Q^{2}}}\right]^{1 / 2}
$$

Let $X_{\gamma T}=$ thermal equivalent displacement, then,

$$
\left|x_{\gamma T}\right|^{2}=\frac{\left|F_{T}\right|^{2} \frac{1}{m^{2}}}{\left(\omega_{o}-\omega^{2}\right)^{2}+\frac{\omega^{2} \omega_{0}^{2}}{Q^{2}}}
$$

where $F_{T}=$ thermal equivalent force
Then, $\left(x_{\gamma T}\right)_{r m s}^{2}=\int_{0}^{\infty} d w\left[\frac{\left|F_{T}\right|^{2} \frac{1}{m^{2}}}{\left(\omega_{o}-\omega^{2}\right)^{2}+\frac{\omega^{2} \omega_{0}^{2}}{Q^{2}}}\right]$
$Q=\frac{\omega_{o} m}{D}$ as the damping coefficient and D as the viscous dissipation factor

$$
\frac{\left|F_{T}\right|^{2}}{\left[\left(\omega_{o}-\omega^{2}\right) m\right]^{2}+\frac{\omega^{2} \omega_{0}^{2} m^{2}}{Q^{2}}}=\frac{\left|F_{T}\right|^{2}}{\left(k_{s}-m \omega^{2}\right)^{2}+R^{2} \omega^{2}}
$$

where $k_{s}=m \omega_{o}^{2}$ is the spring constant as we have defined before.
Then,

$$
\begin{aligned}
\left(x_{\gamma T}\right)_{r m s}^{2} & =\left|F_{T}\right|^{2} \int_{0}^{\infty} \frac{d w}{\left(k_{s}-m \omega^{2}\right)^{2}+R^{2} \omega^{2}} \\
& =\left|F_{T}\right|^{2}\left(\frac{1}{4 R k_{s}}\right)
\end{aligned}
$$

so, $\frac{1}{2} k_{B} T=\frac{1}{2} \frac{k_{s}\left|F_{T}\right|^{2}}{4 R k_{s}} \rightarrow\left|F_{T}\right|=\sqrt{4 R k_{B} T}$ Thermal Noise Equivalent Force
Now, with $\left|X_{\gamma T}\right|=\frac{\left|F_{T}\right|^{2}}{\left(k_{s}-m \omega^{2}\right)^{2}+R^{2} \omega^{2}},\left|X_{\gamma}\right|=\frac{m\left|\ddot{X}_{i}\right|^{2}}{\left(k_{s}-m \omega^{2}\right)^{2}+R^{2} \omega^{2}}$
Thermal Noise Equivalent acceleration
$T_{N E A}=\frac{\left|X_{\gamma T}\right|}{\left|X_{\gamma}\right|}=\sqrt{4 R k_{B} T}=\sqrt{4 k_{B} T \frac{\omega_{o} m}{Q}}$
with sensitivity $=\frac{\left|X_{T}\right|}{\left|X_{\gamma}\right| /\left|m \ddot{X}_{i}\right|}, T_{\text {NEA }}$ puts a lower limit on sensitivity.

$$
\begin{gathered}
\text { Sensitivity }=\frac{\left|X_{T}\right|}{\left|X_{\gamma}\right| /\left|m \ddot{X}_{i}\right|} \text { where } \frac{\left|X_{\gamma}\right|}{\left|m \ddot{X}_{i}\right|}=\frac{1}{\alpha} \\
\left|F_{T}\right|=\sqrt{4 R K_{B} T}=m\left|X_{T}\right| \\
\frac{\left|X_{T}\right|}{\left|F_{T}\right|}=\frac{1}{\alpha} \Rightarrow\left|X_{T}\right|=\frac{\left|F_{T}\right|}{\alpha}=\frac{\sqrt{4 R K_{B} T}}{\alpha} \\
\therefore \text { Sensitivity }=\sqrt{4 R K_{B} T}
\end{gathered}
$$

Example of Application: Atomic Force Microscope (AFM)

<figure>
   <img src="/Robotics/Sensors/semi7_flow.JPG" alt="flow" width="100%" align="center">
   <div align="center"><figcaption> Figure 9: Input-to-Output Signal Flow.</figcaption></div>
</figure>

- Error 1: from the beam structure geometric design and thermal noise
  For example, shape error of the beam and tip, deflection due to weight, AFM tip into pierce specimen surface, thermal noise, frequency shift, complicated interaction forces, etc.
- Error 2: from electronics components
  For example, Johnson noise, shot noise, 1/f (flicker) noise, and burst (popcorn) noise, avalanche noise, etc.

## Glossary of Technical Terms
* Accuracy: Closeness to true value.
* Bandwidth: Frequency range within $-3\text{~dB}$ limits.
* Bias: Systematic offset error.
* Calibration: Establishing the input-output relationship.
* Drift: Deviation in output over time for constant input.
* FSO: Difference between outputs at maximum and minimum stimuli.
* Hysteresis: Deviation based on the direction of input change.
* LOD: Limit of Detection; minimum detectable input.
* Precision: Measurement consistency (scatter).
* Quantization: Resolution limit from digital processing.
* Repeatability: Precision under identical short-term conditions.
* Selectivity: Sensitivity to desired vs. undesired measurands.
* Span: Input full scale range.
* Threshold: Smallest input causing a non-zero output change.

## Question
### What are the basic concepts used to describe quantitatively what is a good sensor?

To describe quantitatively what constitutes a **good sensor**, several key performance metrics and characterization parameters are used to evaluate its accuracy, precision, and operational limits.

#### **Core Accuracy and Precision Concepts**
*   **Accuracy (Trueness):** This is the **degree of closeness** of a measurement to the actual or "true" value of the quantity being measured. It often accounts for both bias (systematic error) and random effects.
*   **Precision (Repeatability/Reproducibility):** This refers to the **consistency or scatter of repeated readings** under unchanged conditions. It is often reported as a standard deviation.
*   **Bias (Offset):** This represents the **mean error** relative to a reference or true value, often referred to as a systematic error.

#### **Sensitivity and Responsivity**
*   **Responsivity:** Defined as the **input-output gain** of a detector system, it represents the change in output per unit change in input. For linear systems, this is a unique value (the slope of the transfer function); for nonlinear systems, it is the local derivative ($dy/dx$).
*   **Sensitivity:** While sometimes used interchangeably with responsivity, in engineering it specifically refers to the **minimum magnitude of input signal** required to produce a specified output with a target **Signal-to-Noise Ratio (SNR)**. A "good" sensor typically has **small sensitivity**, meaning it requires a very small input to be reliably detected against noise.

#### **Detection Limits and Resolution**
*   **Resolution:** This is the **smallest change in input** that produces a discernible change in the output signal. It is often limited by the bits in an Analog-to-Digital Converter (ADC) or the inherent physics of the sensor.
*   **Threshold:** This is the **smallest increment of stimulus** that results in a noticeable change in output starting from zero.
*   **Limit of Detection (LOD):** This is the smallest input that can be **reliably distinguished from noise** based on specific criteria like a 3$\sigma$ false-alarm rate.

#### **Operational Range and Linearity**
*   **Span (Measurement Range):** The range between the **minimum and maximum** measurable input stimulus within which the sensor meets its accuracy specifications.
*   **Full Scale Output (FSO):** The **difference between output signals** for the maximum and minimum stimuli.
*   **Linearity (Nonlinearity):** This quantifies how closely the sensor's transfer function follows a **straight line**. It is typically reported as a percentage of the FSO.
*   **Dynamic Range:** The **ratio of the largest non-saturating signal** to the smallest detectable signal, often expressed in decibels (dB).

#### **Stability and Reliability**
*   **Hysteresis:** A phenomenon where a sensor provides **different outputs for the same input** depending on whether the stimulus is increasing or decreasing.
*   **Drift:** The change in **zero offset or sensitivity** over time due to aging or environmental changes.
*   **Stability:** The sensor's ability to maintain its characteristics over a **long term** (weeks or months).

#### **Dynamic Performance**
*   **Bandwidth (Frequency Response):** The range of frequencies over which the sensor can accurately track the input, often defined by the **-3 dB point**.
*   **Response Time:** Measured by parameters like **rise time, settling time, and the time constant**, this defines how quickly a sensor reacts to a step change in the measurand.

#### **The "Perfect" Sensor Profile**
According to the sources, a **"perfect" sensor** is one that has **extremely low noise** (electronic, thermal, and mechanical), **large SNR**, **low cost**, and is **highly selective**, meaning it is sensitive only to the target property and insensitive to all others.

### How to estimated “Responsivity” for piezoresistive, capacitive, and piezoelectric MEMS sensors, i.e., what is the electrical output versus mechanical input relationship?

To estimate the **responsivity** of MEMS sensors, you must determine the **input-output gain**, which is the ratio of the change in electrical output ($\Delta y$) to the change in mechanical input ($\Delta x$). For linear systems, this is a unique value; for nonlinear systems, it is the local slope or derivative ($dy/dx$).

In the context of mechanical sensors, the input is typically **force ($F$)** and the output is a fractional change in an electrical property. Based on the sources, here is how to estimate responsivity for the three sensor types:

**1. Piezoresistive MEMS Sensors**
Responsivity for a piezoresistive sensor is measured as the fractional change in resistance per unit force ($dR/R$ per $dF$).
*   ** Transduction Principle:** The change in resistance relates to strain ($\epsilon$) through the gauge factor ($G$): $dR/R = G d\epsilon$.
*   **Estimation Formula:** By deriving the relationship between strain and force using the beam’s dimensions (length $l$, thickness $t$, width $W$) and Young's modulus ($E$), the responsivity is calculated as:
    $$\text{Responsivity (Piezoresistive)} = \frac{dR/R}{dF} = G \cdot \frac{6l}{t^2 W E}$$.

**2. Capacitive MEMS Sensors**
Responsivity for a capacitive sensor is measured as the fractional change in capacitance per unit force ($dC/C$ per $dF$).
*   **Transduction Principle:** Capacitance is defined as $C = \epsilon A / \delta$, where $\delta$ is the initial gap. A change in displacement ($d\delta$) results in a fractional change of $dC/C = -d\delta/\delta$.
*   **Estimation Formula:** Assuming small displacements where the current gap $\delta$ is approximately the initial gap $\delta_0$, the responsivity is:
    $$\text{Responsivity (Capacitive)} = \frac{dC/C}{dF} = \frac{1}{\delta_0} \cdot \frac{4l^3}{t^3 W E}$$.
*   **Comparison:** Capacitive sensors are generally much more sensitive than piezoresistive ones (often by a factor of **~3000/$G$**), though they are more susceptible to noise.

**3. Piezoelectric MEMS Sensors**
The sources characterize piezoelectric sensors as having the highest **strain sensitivity** among common MEMS principles. 
*   **Transduction Principle:** They convert mechanical energy directly into electrical energy (voltage or charge).
*   **Performance Value:** According to the provided comparison table, piezoelectric sensors have a typical **strain sensitivity of 5.0 V/$\mu$***, which is significantly higher than capacitive (0.005) or piezoresistive (0.0001) principles.

**Summary Table of Responsivity Principles**
| Sensor Principle | Electrical Output | Typical Strain Sensitivity [V/$\mu$*] |
| :--- | :--- | :--- |
| **Piezoelectric** | Voltage/Charge | **5.0** |
| **Capacitive** | $dC/C$ | **0.005** |
| **Piezoresistive**| $dR/R$ | **0.0001** |


### What is the ultimate “Sensitivity” of a MEMS mechanical sensor?

The **ultimate sensitivity** of a MEMS mechanical sensor is defined by its **Thermal Equivalent Noise Limit**. This limit represents the fundamental floor of what a sensor can detect, beyond which signal information is lost to background noise.

Based on the provided sources, here are the key concepts and quantitative measures for this limit:

**1. The Physical Origin: Thermal Equivalent Noise**
The ultimate limit is governed by **molecular movements** caused by temperature variations within the mechanical structure. These movements cause random **vibrations** in the mechanical sensing element (such as a cantilever beam), which are then picked up by the mechanical-to-electrical transducer (capacitive, piezoelectric, or piezoresistive) and converted into electrical noise.

**2. The Equipartition Theorem**
The sources use the **Equipartition Theorem** to describe how energy is distributed. It states that noise is associated with any phenomenon that converts mechanical or electrical energy into heat. For a mechanical structure like a cantilever beam, the thermal energy ($\frac{1}{2}K_BT$) is equated to the mechanical energy ($\frac{1}{2}kx^2$) to derive the **Thermal Equivalent Displacement (TED)**:
*   $$x = \sqrt{\frac{K_BT}{k}}$$ 
*(Where $K_B$ is the Boltzmann constant, $T$ is absolute temperature, and $k$ is the spring constant)*.

**3. Quantitative Estimation of Ultimate Sensitivity**
In engineering, "Sensitivity" is defined as the minimum magnitude of input signal required to produce a specified output with a target signal-to-noise ratio. Quantitatively, the sources derive the ultimate sensitivity of a system as:
*   $$\text{Sensitivity} = \sqrt{4RK_BT}$$

In this relationship:
*   **$R$** represents the **viscous dissipation factor** (related to the quality factor $Q$).
*   **$K_B$** is the Boltzmann constant ($1.38 \times 10^{-23}$).
*   **$T$** is the absolute temperature.

**4. Impact on Sensor Design**
*   **Lower is Better:** A "good" sensor has a **small sensitivity value**, meaning it has a lower system output noise or a higher responsivity, allowing it to detect smaller input changes reliably.
*   **Detection Limits:** This thermal limit sets the **lower boundary** for force resolution in high-precision instruments like the **Atomic Force Microscope (AFM)**.
*   **Bandwidth Dependencies:** Sensitivity is also dependent on **bandwidth** or sampling rate, as these factors influence how much noise is integrated into the final signal.
