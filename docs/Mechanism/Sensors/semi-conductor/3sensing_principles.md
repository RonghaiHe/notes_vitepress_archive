# Introduction to Micro and Nano Sensing Principles

## About Sensors
### Defining the Sensor and Transducer

In the realm of Micro-Nano systems, we must first establish a rigorous vocabulary. According to the American National Standards Institute (ANSI), **a sensor is a device that provides a usable output in response to a specified measurand (the physical quantity, property, or condition being measured).**

While a sensor acquires a physical parameter and converts it into a signal suitable for processing (optical, electrical, or mechanical), a transducer is a broader functional classification. A transducer converts energy from one domain to another. Familiar examples include:

* Microphones: Transducing sound pressure into electrical signals.
* Loudspeakers: Transducing electrical signals into sound pressure.
* Biological Senses: Our senses of touch or sight transduce environmental stimuli into neural impulses.

Sensor technology is the essential bridge between the stochastic physical world and our deterministic digital systems. Without these interfaces, the "Libelium Smart World" or the Internet of Things (IoT)—ranging from smart roads and radiation monitoring to wine quality enhancement—would have no data to process. Sensors provide the "nervous system" for modern automation.

### Criteria for Sensor Selection

Selecting a sensor is never a "plug-and-play" decision; it is an exercise in managing engineering trade-offs. We categorize these constraints into three primary domains:

- Environmental Factors:
  - Temperature range
  - Humidity effects
  - Corrosion
  - Size
  - Overrange protection
  - Susceptibility to EM interferences
  - Ruggedness
  - Power consumption
  - Self-test capability
- Economic Factors
  - Cost
  - Availability
  - Lifetime
- Sensor Characteristics
  - Sensitivity
  - Range
  - Stability
  - Repeatability
  - Linearity
  - Error
  - Response time
  - Frequency response

## Examples of Sensing Principles
### Quantifying Sensor Performance: What Makes a "Good" Sensor?

Confuse resolution, sensitivity, and responsivity? Let us clarify:

* **Resolution** (分辨率): The **smallest** detectable change in the measurand. It is the absolute floor of what the sensor can "see."
* **Responsivity** (响应度): This is the input-output gain. For linear systems, it is a constant ratio; for nonlinear systems, it is the local **slope** (the derivative) of the response curve.
> Example: Photodetector (optical signal is converted into an electric current)
> 
> Responsivity = electrical output per optical input.
* **Sensitivity** (灵敏度): the **minimum magnitude** of input signal required to produce a specified output signal having a specified signal-to-noise ratio, or other specified criteria.
  > **Responsivity** and **Sensitivity** have very different definitions in Engineering and Science disciplines!
* **Signal-to-Noise Ratio (SNR)**: The ratio of signal power to noise power. Even a high-responsivity sensor is useless if the SNR is below 1:1, as the information is lost in the noise.
* **Accuracy** vs. **Precision**:
  * **Accuracy** (准确度) is closeness to the true value (hitting the bullseye).
  * **Precision** (Repeatability 精密度) is hitting the same spot consistently, even if it is not the bullseye.
* **Hysteresis**: The difference in output when an input is approached from an increasing vs. decreasing direction.

<figure>
   <img src="/Robotics/Sensors/semi4_hyster.JPG" alt="Hysteresis" width="100%" align="center">
   <div align="center"><figcaption> Figure 1: Example of Hysteresis.</figcaption></div>
</figure>


In this graph, Force (Y-axis) is plotted against Extension (X-axis). You will notice two distinct paths for Loading and Unloading. This lag indicates that the material "remembers" its previous state, a critical factor for engineers to compensate for during calibration.

## Micro Force Sensing Principle
### Piezoresistive Sensors

**Piezoresistivity** (压阻效应) is the change in electrical resistivity ($\rho$) of a material when subjected to mechanical stress.
> Crucial Note: Unlike the piezoelectric effect (压电效应), this does not produce a voltage; it only **changes the resistance**.

The Physics of Scale:

In Metals, the change in resistance is primarily due to **geometry changes** ($\Delta L/L$). However, in Semiconductors (like Silicon), the effect is dominated by changes in resistivity ($\Delta \rho/\rho$). At the atomic level, strain alters the inter-atomic spacing, which shifts the material's bandgaps, making it easier or harder for electrons to reach the conduction band.

Mechanical Context & Placement:

Mechanical stress ($\sigma$) and strain ($\varepsilon$) follow Hooke's Law: $\sigma = E\varepsilon$.

<figure>
   <img src="/Robotics/Sensors/semi4_piezoresist.JPG" alt="piezoresist" width="100%" align="center">
   <div align="center"><figcaption> Figure 2: Piezoresistive.</figcaption></div>
</figure>

In a cantilever, stress is distributed around a neutral plane. One side of the plane undergoes tensile stress (positive strain), while the other undergoes compressive stress (negative strain).

Pedagogical Note on Placement: If we are designing a diaphragm-based pressure sensor, where do we place our silicon $n$-well piezoresistors? Engineering intuition suggests the center, and the math backs this up: stress at the center ($\sigma_C \approx 45.0 \text{ MPa}$) is double that of the boundary ($\sigma_B \approx 22.5 \text{ MPa}$). A higher $\sigma_C$ yields a higher $\Delta R/R$, which maximizes our SNR.

<figure>
   <img src="/Robotics/Sensors/semi4_strain-stress.png" alt="strain-stress" width="100%" align="center">
   <div align="center"><figcaption> Figure 3: Strain-stress relationship.</figcaption></div>
</figure>

<figure>
   <img src="/Robotics/Sensors/semi4_strain-stress-materials.png" alt="strain-stress-materials" width="100%" align="center">
   <div align="center"><figcaption> Figure 4: Strain-stress relationship for different materials.</figcaption></div>
</figure>

<figure>
   <img src="/Robotics/Sensors/semi4_beam-stress.png" alt="beam deflection" width="100%" align="center">
   <div align="center"><figcaption> Figure 6: Beam deflection.</figcaption></div>
</figure>

To calculate the **stress** and **strain**:
$$
\begin{aligned}
  &\text{Stress} = \frac{\text{Force / Load}}{\text{Area}}, \quad \sigma = \frac{F}{A}\\
  &\text{Strain} = \frac{\text{Length of Stretch}}{\text{Original Length}}, \quad \varepsilon = \frac{\delta}{L}
\end{aligned}
$$

If a constant force $F$ is applied to the free end of the beam, then its maximum (static) deflection is given by standard equation for a maximum deflection of a cantilever beam of constant cross section :
$$
D=\frac{F L^3}{3 E I}
$$

where $D$ is the deflection of the free end of the beam, $F$ is the force applied to the free end, $L$ is the length of the beam, and EI is the flexural rigidity of the beam ( $E=$ Young's modulus).

**Gage factors**: the relation between deformation and resistance
$$
F = \frac{\Delta R/R}{\varepsilon_L}
$$

and
$$
R=\frac{\rho L}{A}
$$

- Metals: changes in **geometry** dominate
  $$
  \frac{\Delta R}{R}=\frac{\Delta L}{L} - \frac{\Delta A}{A}
  $$
- Semiconductors: changes in **resistivity** dominate (strain causes differences in atomic spacing, which in turn causes changes in band gaps and thus $\rho$)
  $$
  \frac{\Delta R}{R}=\frac{\Delta \rho}{\rho}
  $$

**Piezoresistors** are resistors made from a piezoresistive material and are usually used for measurement of mechanical stress.

location of piezoresistors

bridge balancing

### Piezoelectric Sensors

Derived from the Greek piezo ("to squeeze"), Piezoelectricity is the charge which **accumulates in certain solid materials** (crystals, ceramics, bone) under strain.

When a neutral molecule is stressed, its internal charge distribution is disrupted, causing charge to accumulate on the surface. Unlike the resistive type, these generate a voltage ($V_m$) directly:
$$
\begin{aligned}
  &V_m = d_{31} \frac{F}{\varepsilon L}\\
  &V_m = d_{31} \frac{F}{\varepsilon W}\\
  &V_m = d_{31} \frac{Ft}{\varepsilon LW}\\
\end{aligned}
$$

Above equations are valid when force is applied in the length $(L)$, width $(W)$ or thickness $(t)$ directions respectively.

(Note: Here, $d_{31}$ is the piezoelectric coefficient, $31$ denotes the crystal axis and $\varepsilon$ is the material permittivity).

#### Piezoelectric Effect
$$
\begin{gathered}
  D_i=e_{ij}^\sigma E^j + d_{im}^d\sigma_m\\
  \varepsilon_k = d_{jk}^cE_j + S_{km}^E\sigma_m
\end{gathered}
$$

where: 
- $D_i$: dielectric displacement
- $\varepsilon_k$: mechanical strain vector
- $E_j$: applied electric field vector
- $\sigma_m$: mechanical stress vector
- $d_{im}^d, d_{jk}^c$: piezoelectric coefficients
- $e_{ij}^\sigma$: dielectric permittivity
- $S_{km}^E$: elastic compliance matrix

Frequency dependent output of Piezoelectric Sensors
- A piezoelectric sensor has very high DC output impedance and can be modeled as a proportional voltage source and filter network. The voltage V at the source is directly proportional to the applied force, pressure, or strain. The output signal is then related to this mechanical force as if it had passed through the equivalent circuit.


#### Transverse Effect

Beyond simple longitudinal sensing, we often utilize the **Transverse Effect**. This allows us to decouple the charge-generating axis from the neutral axis. This is vital for designers because it provides a mechanism to fine-tune sensitivity by adjusting the b/a ratio (the ratio of the dimension in line with the charge generating axis to the dimension in line with the neutral axis).
$$
C_x=d_{xy}F_yb/a
$$

where $d$ is the corresponding piezoelectric coefficient.

#### Longitudinal Effect
The amount of charge produced is strictly proportional to the applied force and is independent of size and shape of the piezoelectric element. Using several elements that are **mechanically in series and electrically in parallel** is the only way to increase the charge output. The resulting charge is:
$$
C_x=d_{xx}F_xn
$$

where:
- $d_{xx}$ is the piezoelectric coefficient for a charge in xdirection released by forces applied along $x$-direction (in pC/N)
- $F_x$ is the applied Force in $x$-direction (in N)
- $n$ corresponds to the number of stacked elements

#### Shear Effect
The charges produced are strictly proportional to the applied forces and are independent of the element’s size and shape. For $n$ elements mechanically in series and electrically in parallel the charge is
$$
C_x=2d_{xx}F_xn
$$

In contrast to the longitudinal and shear effects, the transverse effect opens the possibility to fine-tune sensitivity on the force applied and the element dimension.

## Comparative Analysis: Sensing Principles

When choosing a principle, we look at the Threshold (minimum detectable input) and the Span to threshold ratio.

"Responsivity": capacitive or piezoresistive?

Should we use **capacitive** or **piezoresistive** principle to measure **displacement of diaphragm** for a pressure sensor?

### Comparing piezoresistive and capacitive sensors
<figure>
   <img src="/Robotics/Sensors/semi3_compare.JPG" alt="Compare" width="100%" align="center">
   <div align="center"><figcaption> Figure 7: Force in beams.</figcaption></div>
</figure>

- **Assume**: $\ell$: effective moment arm (the moment on the fixed end by $F$)
- **Given** (From the previous chapters):
  $$
  \begin{gathered}
    \varepsilon = \frac{3\delta t}{2\ell^2}\\
    k = \frac{t^3wE}{4\ell^2}
  \end{gathered}
  $$

$$
\text{Responsivity}\equiv\frac{\text{Change  in output}}{\text{Change  in input}}
$$

- Piezoresistive sensor: $\frac{\mathrm{d}R/R}{\mathrm{d}F}$
- Capacitive sensor: $\frac{\mathrm{d}C/C}{\mathrm{d}F}$

Now, for **piezoresistive sensors**:
$$
\frac{\Delta R}{R} = G\varepsilon\implies \frac{\mathrm{d}R}{R} = G\mathrm{~d}\varepsilon, \quad (\text{Note: }\Delta R=0 \text{ if }\varepsilon=0)
$$

find $\mathrm{d}\varepsilon$:
$$
\begin{aligned}
  &\frac{\mathrm{d}\varepsilon}{\mathrm{d}F} &&= \frac{\mathrm{d}\varepsilon}{\mathrm{d}\delta}\frac{\mathrm{d}\delta}{\mathrm{d}F} = \frac{3t}{2\ell^2}\left(\frac{1}{k}\right), \quad F=k\delta\\
  &&&= \frac{3t}{2\ell^2}\frac{4\ell^3}{t^3wE} = \frac{6\ell}{t^2wE}\\
  \implies& \frac{\mathrm{d}R/R}{\mathrm{d}F} &&=G\frac{6\ell}{t^2wE}
\end{aligned}
$$

For capacitive sensors:
$$
\begin{aligned}
  C = \frac{\varepsilon A}{\delta}&\implies \mathrm{d}C = -\frac{\varepsilon A}{\delta^2}\mathrm{~d}\delta = -C\frac{\mathrm{d}\delta}{\delta}\\
  &\implies \frac{\mathrm{d}C}{C} = -\frac{\mathrm{d}\delta}{\delta}
\end{aligned}
$$

Then,
$$
\frac{\mathrm{d}C/C}{\mathrm{d}F} = \frac{1}{\delta_0}\frac{\mathrm{d}\delta}{\mathrm{d}F}
$$

> - Assume the "-" sign can be eliminated by circuit design.
> - Assume $\mathrm{d}\delta$ is small comparing to $\delta$, so $\delta\approx\delta_0$. (This's convenient for 1st order approximations)

Hence,
$$
\frac{\mathrm{d}C/C}{\mathrm{d}F} = \frac{1}{\delta_0}\frac{4\ell^3}{t^3wE}
$$

> Note:
> $$
  \frac{\mathrm{d}C/C}{\mathrm{d}a} = \frac{1}{C}\frac{\mathrm{d}C}{\mathrm{d}\delta}\frac{\mathrm{d}\delta}{\mathrm{d}F}\frac{\mathrm{d}F}{\mathrm{d}a} = \frac{M}{\delta_0k}
> $$

So,
$$
  \frac{R_\text{cap}}{R_\text{piezo}} = \frac{2}{3}\frac{\ell^2}{t}\frac{1}{G}\frac{1}{\delta_0}
$$

For $\ell\sim 500\mathrm{~\mu m}, t\sim 5\mathrm{~\mu m}, \delta_0\sim 10\mathrm{~\mu m}$, the advanatge of capacitice over piezoresistive is $\sim 3000/G$.

As we have learned, $G_\text{Si}\sim 80-200$, so,in MEMS, capacitive sensors are more **sensitive**. However, they are **more susceptible to noise**.

Note:
$$
\text{Sensitivity}\equiv\frac{\text{System output noise}}{\text{responsivity}}
$$

- This is contrast to our understanding that the greater the "sensitivity", the better a sensor is. From the above definition, a sensor with lower sensitivity is better because it'll have lower system output noise or higher responsivity
- Think of "sensitivity" as the smallest quantity of signal that you can detect with your sensor that you're sure is not a noise signal

### Conclusion
* **Piezoelectric**: Offers the highest Span-to-threshold ratio (100,000,000), making it ideal for high-dynamic-range applications, though it has a relatively high threshold (5.0).
* **Piezoresistive**: Boasts an incredibly low threshold (0.0001) and a high span ratio (2,500,000), perfect for high-precision micro-sensing.
* **Inductive** & **Capacitive**: These provide moderate thresholds (0.001 - 0.005) and lower span ratios, often used where non-contact sensing is required.

## Signal Conditioning and The Wheatstone Bridge

In MEMS, $\Delta R$ is typically less than 1% of the total resistance. Measuring such a tiny change directly is nearly impossible due to noise. We use a Wheatstone Bridge to convert this $\Delta R$ into a differential voltage.

The bridge output $(e_o)$ relative to input $(e_i)$ is: $\frac{\Delta e_o}{e_i} = \frac{1}{4} \left( \frac{\Delta \epsilon_1}{\varepsilon} - \frac{\Delta \epsilon_2}{\varepsilon} + \frac{\Delta \epsilon_3}{\varepsilon} - \frac{\Delta \epsilon_4}{\varepsilon} \right)$

Engineering Intuition: Why the subtractions? This math enables Common Mode Cancellation. If the temperature changes, all resistors change equally; because the bridge subtracts the changes in adjacent arms, the temperature noise cancels out. Furthermore, because the center and boundary of a diaphragm have opposite signs of strain, we place them in adjacent arms so the negative signs cancel out, making the final signal additive and significantly enhancing sensitivity.

## Comprehensive Glossary of Technical Jargon and Formulas

* Measurand: The physical quantity being measured.
* Transducer: A device converting energy between domains.
* Piezoresistivity Formula: $(\Delta\rho/\rho) = \pi\sigma$ (where $\pi$ is the piezoresistive coefficient).
* Gage Factor ($F$): $(\Delta R/R) / \varepsilon_L$. A measure of the sensitivity of a strain gage.
* Cantilever Deflection ($D$): $FL^3 / 3EI$.
* Flexural Rigidity ($EI$): The stiffness of a beam; the product of Young's Modulus and the area moment of inertia.
* Young's Modulus ($E$): The ratio of stress to strain in the elastic region.
* Piezoelectric Coefficient ($d_{31}$): The ratio of electric charge generated per unit of applied force.
* Permittivity ($\varepsilon$): The measure of a material's ability to store an electric field.
* Span: The range between the minimum and maximum limits of a sensor's measurement capability.
* SNR: Signal-to-Noise Ratio (Power Signal / Power Noise).
* Hysteresis: Output lag behind the input during loading/unloading.

## Conclusion: Characteristics of an Ideal Sensor

As you progress in your design careers, aim for these "Ideal" metrics:

1. High responsivity, i.e., give a large output voltage when the input is a small quantity
2. Stability & Low Drift: Reliable over time and temperature.
3. Repeatable output
4. Linearity
5. Low Hysteresis
6. Fast frequency response, wide Bandwidth: Fast, consistent response to dynamic inputs.
7. Low power consumption
8. Small volume and weight

## Question
### What are the basic concepts used to describe quantitatively what is a good sensor?

To describe quantitatively what constitutes a "good" sensor, several key performance concepts and parameters are used to measure its effectiveness, reliability, and precision:

Core Measurement Concepts
- **Resolution**: This is defined as the smallest change the sensor can detect in the quantity it is measuring. It is distinct from responsivity and sensitivity, though the terms are often confused.
- **Responsivity**: This measures the input-output relationship (the gain or ratio) of a detector system. For linear systems, this is a unique value; for nonlinear systems, it is the local slope or derivative of the response curve. In MEMS design, responsivity is calculated as the Change in Output / Change in Input.
- **Sensitivity**: In the context of detection devices, sensitivity is the minimum magnitude of input signal required to produce a specified output signal that meets a specific Signal-to-Noise Ratio (SNR) or other criteria.
- **Signal-to-Noise Ratio** (SNR): This is the electrical power ratio between the meaningful information (the signal) and the unwanted background noise. A higher ratio indicates less corruption by noise.
- **Threshold**: This is the minimum value of the input signal required to elicit any change in output or to start from zero.
Accuracy and Precision
- **Accuracy**: This refers to the degree of closeness of the measurements to the actual or "true" value of the quantity being measured.
- Precision (Repeatability/Reproducibility): This is the degree to which repeated measurements under unchanged conditions show the same results. A sensor can be precise (repeatable) without being accurate (close to the true value).
Behavioral and Dynamic Characteristics
- **Linearity**: This describes how well the sensor's output maintains a consistent ratio to the input across its entire range.
- **Hysteresis**: This is the phenomenon where a lag occurs between the application and removal of a stimulus, resulting in different outputs depending on whether the input is increasing or decreasing.
- **Stability** and **Drift**: Stability refers to the sensor's ability to maintain a repeatable output over time, while low drift indicates minimal unintended change in output when the input is constant.
- **Response Time** and **Frequency Response**: These quantify the sensor's dynamic response, specifically how quickly it reacts to changes (response time) and its effective operating range across different frequencies (bandwidth).
Characteristics of an "Ideal" Sensor
According to the sources, an ideal sensor should possess the following quantitative and qualitative traits:
- **Large responsivity** (providing a large output for a small input).
- **Linearity** and **low hysteresis**.
- **Fast frequency response** and **wide bandwidth**.
- **Low power consumption**, **small volume**, and **low cost**

### How to estimate “Responsivity” for piezoresistive, capacitive, and piezoelectric MEMS sensors, i.e., what is the electrical output versus mechanical input relationship?

**Responsivity** is defined as the measure of the **input-output relationship** (gain or ratio) of a detector system. In the context of MEMS mechanical sensors, it is calculated as the **Change in Output divided by the Change in Input**.

The following sections detail how to estimate this relationship for different transduction principles based on the sources.

### 1. Piezoresistive MEMS Sensors
For a piezoresistive sensor, the mechanical input is typically **force ($F$)**, and the electrical output is the **fractional change in resistance ($dR/R$)**. 

*   **Transduction Relationship:** The change in resistivity is defined by the gauge factor ($G$) and strain ($\epsilon$): $\frac{\Delta R}{R} = G\epsilon$.
*   **Estimation Formula:** By combining the relationship for strain on a cantilever beam ($\epsilon = \frac{3 \delta t}{2 l^2}$) and the spring constant ($k = \frac{t^3 W E}{4 l^3}$), the responsivity is derived as:
    $$\text{Responsivity} = \frac{dR/R}{dF} = G \cdot \frac{6l}{t^2 W E}$$
    *(Where $l$ is the length, $t$ is thickness, $W$ is width, and $E$ is Young's modulus)*.

### 2. Capacitive MEMS Sensors
In capacitive sensors (such as a diaphragm or comb-drive), the input is **force ($F$)** and the output is the **fractional change in capacitance ($dC/C$)**.

*   **Transduction Relationship:** Capacitance is defined as $C = \frac{\epsilon A}{d}$, where $d$ is the gap (or displacement $\delta$). A change in displacement results in $\frac{dC}{C} = -\frac{d\delta}{\delta}$.
*   **Estimation Formula:** Using the mechanical stiffness relationship where displacement change per unit force is $\frac{1}{k}$, and assuming a small displacement compared to the initial gap ($\delta_0$), the responsivity is:
    $$\text{Responsivity} = \frac{dC/C}{dF} = \frac{1}{\delta_0} \cdot \frac{4l^3}{t^3 W E}$$
*   **Comparison Note:** In typical MEMS dimensions, **capacitive sensors are significantly more sensitive** (often by a factor of ~3000/$G$) than piezoresistive ones, though they are more susceptible to noise.

### 3. Piezoelectric MEMS Sensors
Piezoelectric sensors generate an **electrical charge ($C_x$)** or **voltage ($V_m$)** directly proportional to the applied **mechanical force ($F$)**. The responsivity depends on how the force is applied to the crystal axis:

*   **Longitudinal Effect:** The charge is produced in the same direction as the force. 
    $$\text{Output Charge } (C_x) = d_{xx} F_x n$$ 
    *(Where $d_{xx}$ is the piezoelectric coefficient and $n$ is the number of stacked elements)*.
*   **Transverse Effect:** Force is applied along a neutral axis, and charge is generated perpendicularly. This allows for **fine-tuning sensitivity** by adjusting the element's dimensions ($a$ and $b$):
    $$\text{Output Charge } (C_x) = d_{xy} F_y \frac{b}{a}$$
*   **Shear Effect:** For $n$ elements in series, the charge is $C_x = 2d_{xx} F_x n$.
*   **Voltage Output:** The generated voltage ($V_m$) is also proportional to force. For example, when force is applied in the direction of thickness ($t$), the relationship is $V_m = d_{33} F \frac{t}{\epsilon L W}$.

### Summary of "Good" Sensor Quantitative Traits
When estimating these relationships, an **ideal sensor** is characterized by **large responsivity** (high output for small input), **linearity**, and **low hysteresis** (minimal lag between application and removal of force).

### What is an “ideal sensor”?
An **ideal sensor** is a device optimized across technical, physical, and economic dimensions to provide the most effective measurement of a physical parameter. According to the sources, an ideal sensor possesses the following key characteristics:

*   **Large Responsivity:** It should provide a **large output signal** (such as voltage) even when the **input is a very small quantity**. Responsivity represents the "gain" or unique input-output relationship of the system.
*   **Linearity:** The sensor's response should be **linear** across its operating range. In a linear system, the responsivity remains constant rather than varying as a local slope or derivative.
*   **Stability and Repeatability:** It must provide a **stable output with low drift** over time. Additionally, it should be highly **precise (repeatable)**, meaning it shows the same results consistently when measurements are repeated under unchanged conditions.
*   **Low Hysteresis:** There should be **minimal lag** between the application and removal of a stimulus. An ideal sensor does not show different responses based on whether the input is increasing or decreasing.
*   **Dynamic Performance:** The sensor should feature a **fast frequency response** and a **wide bandwidth**, allowing it to react quickly to rapid environmental changes.
*   **Physical and Economic Efficiency:** Beyond measurement accuracy, an ideal sensor is designed for practical implementation, featuring **low power consumption**, **small volume and weight**, and a **low cost** for manufacturing.

In contrast to these ideal traits, real-world sensors are often evaluated by their **threshold**—the minimum input signal required to start a change from zero—and their **signal-to-noise ratio (SNR)**, which quantifies how much the meaningful signal has been corrupted by background noise.