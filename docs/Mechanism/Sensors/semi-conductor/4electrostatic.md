# Introduction to Electrostatic (Capacitive) Sensors

## Introduction to MEMS Transduction Principles

Micro-Electromechanical Systems (MEMS) are fundamentally defined by their ability to perform transduction—the conversion of energy between the physical and electrical domains. For engineers, this necessitates a rigorous understanding of how external physical stimuli are converted into measurable electrical signals (sensors) and how electrical inputs are leveraged to generate controlled mechanical motion (actuators).

In modern micro-scale engineering, 4 primary physical principles dominate:

* **Piezoelectric**: Stress-induced polarization in specific crystal structures.
* **Thermal**: Exploiting differences in thermal expansion coefficients to produce displacement.
* **Magnetic**: Utilizing Lorentz forces or magnetic attraction, often requiring complex integration of coils or permanent magnets.
* **Capacitive** (Electrostatic): Leveraging the interaction between stored charge and electrode geometry.

However, these principles can also be used to transduce external input into electrical output $\to$ **sensors**!

Why it Matters: The Versatility of the Capacitive Method The capacitive method is arguably the most ubiquitous in commercial MEMS. Unlike piezoelectric or thermal methods, it requires no "smart" or exotic materials; it can be implemented using standard structural materials like polysilicon or aluminum. Furthermore, capacitive devices exhibit exceptionally low power consumption (being voltage-driven rather than current-driven) and provide a high-fidelity mechanical-to-electrical response. While the operational distance is limited, the scaling benefits at the micro-level make it the gold standard for high-speed, high-precision sensing and actuation.

## Ferroelectrics and the Piezoelectric Effect

Piezoelectricity is a property of non-centrosymmetric materials where mechanical stress induces electric polarization. To master these materials, one must understand the hierarchy of properties: 

All **ferroelectrics** (铁电材料) are **pyroelectric** (热电) and therefore **piezoelectric**.
- Examples of materials that are piezoelectric but **not** ferroelectric: quartz ($\mathrm{SiO}_2$), ZnO, AlN.
- Examples of Ferroelectric materials (and thus piezoelectric): $\mathrm{BaTiO}_3$, PZT, PVDF (in certain phases).

This nested relationship is critical for material selection in sensor design.

Material Classification

* Piezoelectric (Non-Ferroelectric): Materials such as Quartz ($\mathrm{SiO}_2$), Zinc Oxide (ZnO), and Aluminum Nitride (AlN). These lack switchable domains but are highly stable for frequency control.
* Ferroelectric (and Piezoelectric): Materials like Barium Titanate ($\mathrm{BaTiO}_3$), Lead Zirconate Titanate (PZT), and Polyvinylidene fluoride (PVDF). These possess a spontaneous polarization that can be reversed by an external field.

The Direct and Converse Effects: The Direct Effect involves generating an electric displacement ($D$) from mechanical stress ($T$): $D = dT + \varepsilon E$ Where $d$ is the piezoelectric coefficient and $\varepsilon$ is the permittivity. Conversely, the Converse Effect describes the generation of mechanical strain when an electric field is applied.

Mathematical Modeling of Voltage Generation In a sensing application, the voltage ($V$) generated across a piezoelectric structure of thickness $L$ and cross-section area $A$ when subjected to a force ($F$) is:
$$
V = \frac{d \cdot F \cdot L}{\varepsilon_0 \varepsilon A}
$$

> (Conversely, if a voltage is applied across a structure made of a piezoelectric material, a displacement will occur on the structure due to $F$ generate across the material.)

Technical Note: Dimensionally, the thickness $L$ is critical; a larger thickness, higher stress ($T$), and a higher piezoelectric coefficient lead to a significantly larger generated voltage.

Practical Application: Quartz resonators remain the most common application of this principle, with approximately 10 million units produced daily. These single-crystal devices are vacuum-packaged and valued for their high Q-factor in timing circuits.

## Fundamentals of Electrostatic (Capacitive) Sensing and Actuation

Electrostatic devices operate as variable capacitors. The sensing mechanism relies on the fact that capacitance ($C$) changes when physical parameters are altered by **distance** (gap), **position** (overlap area), or the **dielectric media** (e.g., air vs. liquid).

**Actuation**: electrostatic force (attraction) between moving and fixed plates as a voltage is applied between them.

2 major Configurations:
1. **Parallel Plate capacitor**: Typically used for out-of-plane (vertical) motion.
2. **Interdigitated Fingers / IDT**: Commonly called "comb drives," these are designed for in-plane motion.

Relative Merits

* Pros: Universal sensing/actuation without special materials; ultra-low power; high speed (limited only by mechanical response and charging time).
* Cons: Inverses scaling (force $\propto 1/x^2$), vulnerability to particles in small gaps, and susceptibility to stiction (sticking due to molecular forces).

## Parallel Plate Capacitor
### Mathematical Analysis
For a **parallel plate** with area $A$ and an initial gap $d$, the capacitance is:
$$
C = Q/V = Q/(Ed), \quad E=Q/\varepsilon A \implies C = \frac{Q}{\frac{Q}{\varepsilon A}d} = \frac{\varepsilon A}{d}.
$$

Note:
- Equations without considering **fringe electric field**.
  - The fringe field is frequently ignored in first-order analysis. It is nonetheless important. Its effect can be captured accurately in finite element simulation tools.

- Stored energy:
  $$
    U = \frac12CV^2=\frac12\frac{Q^2}{C}
  $$
- Force is derivative of energy w.r.t. **pertinent dimensional variable**
  $$
    F = \frac{\partial U}{\partial d} = \frac12\frac{\partial C}{\partial d}V^2
  $$
- Plug in the expression for capacitor: $C = \frac{Q}{\frac{Q}{\varepsilon A}d} = \frac{\varepsilon A}{d}.$
- Arrive at the expression for force:
  $$
    F = \frac{\partial U}{\partial d} = -\frac12\frac{\varepsilon A}{d^2}V^2 = -\frac12\frac{CV^2}{d}.
  $$

### Relative Merits 
Relative Merits of Capacitor Actuators:
**Pros**:
- Nearly universal sensing and actuation; no need for special materials.
- Low power. Actuation driven by voltage, not current.
- High speed. Use charging and discharging, therefore realizing full mechanical response speed.

**Cons**:
- Force and distance inversely scaled - to obtain larger force, the distance must be small.
- In some applications, vulnerable to particles as the spacing is small - needs packaging.
- Vulnerable to sticking phenomenon due to molecular forces.



## Analysis of Electrostatic Actuator

What happens to a parallel plate capacitor when the applied **voltage** is gradually **increased**?

### The Electromechanical Model
An electrostatic actuator is a competitive system between non-linear electrical forces and linear mechanical restoring forces.

<figure>
   <img src="/Robotics/Sensors/semi5_mechanic.JPG" alt="Electromechanical Model" width="100%" align="center">
   <div align="center"><figcaption> Figure 1: An Equivalent Electromechanical Model.</figcaption></div>
</figure>

Equilibrium and Hooke’s Law: The suspension acts as a spring with a mechanical spring constant $K_m$. Equilibrium is reached when: $|F_\text{elec}| = |F_\text{mech}| \implies -\frac{1}{2} \frac{\varepsilon A V^2}{d^2} = K_m |x|$

Force Balance Equation at Given Applied Voltage $V$:
$$
-K_mx = \frac{\varepsilon AV^2}{2(x+x_0)^2}
$$

<figure>
   <img src="/Robotics/Sensors/semi5_curves.JPG" alt="Curves" width="100%" align="center">
   <div align="center"><figcaption> Figure 2: Curves for force balance equation. This graph shows the intersection of the linear mechanical restoring force and the family of non-linear electrical force curves for V_1, V_2, V_3. As the voltage reaches the Pull-In Voltage (V_PI), the curves no longer intersect.</figcaption></div>
</figure>

Design Implications: The "First Root" Rule The displacement can be found by solving the third-order equation: $K_m x (x_0 + x)^2 + \frac{1}{2} \varepsilon A V^2 = 0$ When solving this equation, three roots are generated. From a physical perspective, we accept only the first root (the smallest displacement). The other roots represent unstable equilibrium points beyond the pull-in threshold.

Determining Equilibrium Position Graphically:
- At each specific applied voltage, the equilibrium position can be
determined by the intersection of the linear line and the curved
line.
- For certain cases, two equilibrium positions are possible. However, as the plate moves from top to bottom, the first equilibrium position is typically assumed.
- Note that one curve intersects the linear line only at one point.
- As voltage increases, the curve would have no equilibrium position.
- This transition voltage is called **pull-in voltage**.
- The fact that at certain voltage, no equilibrium position can be found, is called **pull-in effect**.

### The "Pull-In" Effect

::: warning Definition: pull-in / snap in effect
As the voltage bias increases from $0$ across a pair of parallel plates, the distance between such plates would decrease until they reach $2/3$ of the original spacing, at which point the 2 plates would be suddenly snapped into contact.
:::

<figure>
   <img src="/Robotics/Sensors/semi5_threshold.JPG" alt="threshold point" width="100%" align="center">
   <div align="center"><figcaption> Figure 3: A threshold point.</figcaption></div>
</figure>

Mathematical Determination of Pull-in Voltage:
Defining Electrical Force Constant
  Let’s define the tangent of the electric force term. It is called electrical force constant, $K_e$:
  $$
    K_e = \frac{\partial F}{\partial x} = \frac{CV^2}{d^2}
  $$

  When voltage is below the pull-in voltage, the magnitude of $K_e$ and $K_m$ are **not** equal at equilibrium.

Key Takeaway:
- Reliable tuning is limited to only $1/3$ of the total gap. Once the plates reach $2/3$ of the original spacing (a displacement of $-x_0/3$), positive feedback causes the plates to "snap" into contact.
- Electrostatic micro mirrors: reduced range of reliable position tuning
- Electrostatic tunable capacitor
  - Reduced range of tuning and reduced tuning range
  - Tuning distance less than $1/3$, tuning capacitance less than $50\%$.

### Example problem
A parallel plate capacitor suspended by 2 fixed-fixed cantilever beams, each with length, width and thickness denoted $l, w$ and $t$, respectively. The material is made of polysilicon, with a Young’s modulus of $120 \mathrm{~GPa}$.
- $L=400 \mathrm{~\mu m}, w=10 \mathrm{~\mu m}, and t=1 \mathrm{~\mu m}$.
- The gap $x_0$ between 2 plates is $2
\mathrm{~\mu m}$.
- The plate area is $400 \mathrm{~\mu m}$ by $400 \mathrm{~\mu m}$.

Calculate the amount of vertical displacement when a voltage of $0.4$ volts is applied.

<figure>
   <img src="/Robotics/Sensors/semi5_example.JPG" alt="example" width="100%" align="center">
   <div align="center"><figcaption> Figure 4: Example image.</figcaption></div>
</figure>

1. Find mechanical force constants
   - Calculate force constant of one beam first: Under force $F$, the max deflection is $d = Fl^3/(12EI)$. The force constant is therefore
    $$
      K_m = \frac{F}{d} = \frac{12EI}{l^3} = \frac{Ewt^3}{l^3} = 0.01875 \mathrm{~N/m}.
    $$
    
    - Total force constant encountered by the parallel plate is $K_m = 0.0375\mathrm{~N/m}$.
2. Find out the Pull-in Voltage: Find out pull-in voltage and compare with the applied voltage.
   1. Find the static capacitance value $C_0$:
    $$
      C_0 = \frac{8.85\times 10^{-12}(\mathrm{F/m})\times(400\times 10^{-6})^2}{2\times 10^{-6}} = 7.083\times 10^{-13}\mathrm{~F}.
    $$

       Find the pull-in voltage value
    $$
      V_p = \frac{2x_0}{3}\sqrt{\frac{k_m}{1.5C_0}} = 0.25(\mathrm{volts}).
    $$

Hence, when the applied voltage is $0.4 \mathrm{~volt}$, the beam has been pulled-in. The displacement is therefore $2 \mathrm{~\mu m}$.

**What if the applied voltage is $0.2 \mathrm{~V}$?**
- Not sufficient to pull-in
- Deformation can be solved by solving the following equation
  $$
    V^2 = \frac{-2k_mx(x+x_0)^2}{\varepsilon A} = \frac{-2k_mx(x+x_0)}{C}.
  $$

  or
  $$
    x^3+2x_0x^2+x_0^2x+\frac{v^2\varepsilon A}{2k_m} = 0
  $$

> Solving Third Order Equation 
> To solve $x^3+ax^2+bx+c=0$:
> Apply $y=x+a/3, p=\frac{-a^2}{3}+b, q=2\left(\frac{a}{3}\right)^3-\frac{ab}{3}+c$, then
>
> $$
  y=A+B, \text{where }A=\sqrt[3]{\frac{-q}{2}+\sqrt{Q}}, B = \sqrt[3]{\frac{-q}{2}-\sqrt{Q}}
> $$
>
> and $x=A+B-a/3$.

### others
Mechanical Spring:
- Cantilever beams with various boundary conditions
- Torsional bars with various boundary conditions

Example of MEMS system: Optical Micro Switches (MEMS Scanning Mirrors)
- Torsional parallel plate capacitor support
- 2 stable positions (+/- 10 degrees w.r.t. rest)
- All aluminum structure
- No process steps entails temperature above $300-
350^\circ \mathrm{C}$



## Interdigitated Comb Drives and Accelerometers

Lateral vs. Transverse Drives

* **Lateral** Comb Drives: Preferred for actuators because force is independent of displacement (as long as overlap is maintained). However, force is a function of finger thickness; thicker fingers yield higher force.
  
  Total capacitance is proportional to the overlap length and depth of the fingers, and inversely proportional to the distance.
  - Pros:
    - Frequently used in actuators for its relatively
  long achievable driving distance.
  - Cons
    - force output is a function of finger thickness. The thicker the fingers, the large force it will be.
    - Relatively large footprint
* **Transverse** Comb Drives: Preferred for sensing due to extreme sensitivity to small displacements, though they have limited travel.
  Direction of finger movement is orthogonal to the direction of fingers.
  - Pros: Frequently used for sensing for the sensitivity and ease of fabrication
  - Cons: not used as actuator because of the physical limit of distance.

Sensing Devices Based on **Transverse** Comb Drive: Analog Devices ADXL Accelerometer The ADXL series utilizes a polysilicon proof mass supported by cantilever beams.

## Summary
Most common MEMS actuators operate with one of the
following physical principles:
- Piezoelectric, Thermal, Magnetic, or Capacitive (Electrostatic)
  - However, these principles can also be used to transduce external input into electrical output è SENSORS!
- **Capacitive Sensing Principle** is one of the most widely used method for commercial MEMS sensors
  - Low current (i.e., low power consumption)
  - Very good mechanical input to electrical output response
  - However, measurable input range is relatively small (due to small operation distance of capacitive plates.)
