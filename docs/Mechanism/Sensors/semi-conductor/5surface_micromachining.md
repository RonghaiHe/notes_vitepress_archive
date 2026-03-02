# Surface Micromachining

## Understanding the Micro-Scale

In the field of Micro-Electro-Mechanical Systems (MEMS), precision is dictated by our mastery of the microscopic world. To engineer effectively at this level, we must first establish a rigorous definition of the scales involved.

Definition and Scales:

The "micro" scale is anchored by the micrometer ($\mathrm{~\mu m}$), the primary unit of distance in MEMS design.

* meso scale: $1 \mathrm{~mm}$ or $10^{-3} \mathrm{~m}$.
* Micrometer ($\mathrm{~\mu m}$): $1/1,000 \mathrm{~mm}$ or $10^{-6} \mathrm{~m}$.
* Nanometer ($\mathrm{~nm}$): $1/1,000 \mathrm{~\mu m}$ or $10^{-9} \mathrm{~m}$.
* Angstrom (Å): $1/10 \mathrm{~nm}$ or $10^{-10} \mathrm{~m}$.

Size Comparison Analysis:

To contextualize these dimensions, consider how common entities compare to the standard MEMS device range of 1 to 1,000 $\mathrm{~\mu m}$:

* Human hair: $\sim 100 \mathrm{~\mu m}$
* Bacteria: $\sim 5 \mathrm{~\mu m}$
* Tobacco smoke: $\sim 0.5 \mathrm{~\mu m}$
* Integrated Circuit (IC) elements: $\sim 0.2 \mathrm{~\mu m}$
* Viruses: $> 0.1 \mathrm{~\mu m}$
* MEMS/micromachines: $1\sim 1000\mathrm{~\mu m}$

The "Why it Matters" Summary Understanding these scale differences is critical because physical constraints change as we move from the meso (millimeter) scale to the micro and nano scales. At these dimensions, a single speck of dust is a mountain. Manufacturing precision requires specialized techniques to manage the physical properties of thin films and the extreme environmental factors that can lead to device failure.

## The Controlled Environment: Clean Room Standards

Micro-fabrication cannot occur in a standard laboratory. Microscopic debris, such as skin cells or lint, is often larger than the mechanical elements of a MEMS device, leading to catastrophic structural interference.

Environmental Control Fabrication requires a "**Clean Room**" where air quality, humidity, and temperature are strictly regulated. Standards typically require a constant humidity of 45% and a temperature of 70°F.

Class Definitions Clean rooms are categorized by "Class," defined by the maximum number of particles larger than $0.5 \mathrm{~\mu m}$ permitted per cubic foot of air.

Clean Room Class	Max Particles ($> 0.5 \mathrm{~\mu m}$) per ft^3
- Class 100:	< 100 particles (size $> 0.5 \mathrm{~\mu m}$)
- Modern VLSI:	Class 10 to Class 1

Practical Application:

These environmental controls ensure that microscopic particles do not contaminate thin films during deposition or interfere with the pattern transfer during lithography, preventing structural defects in the final micromachines.

## The Core Methodology: Add, Lithograph, Subtract

- The foundation of both IC and MEMS technology
- Allows parallel "manufacturing" of millions of parts simultaneous and consistently.

Process Overview The cycle consists of three repeating stages:

**Add** Thin Film $\rightarrow$ Photolithography (光刻) $\rightarrow$ **Subtract** Thin Film.

- Add: Add by deposition, oxidation, electroplating etc.
- Subtract: Etch by ions, gas, or chemicals, etc.


### Photolithography

<figure>
   <img src="/Robotics/Sensors/semi6_lithography.JPG" alt="steps for lithography" width="100%" align="center">
   <div align="center"><figcaption> Figure 1: Steps for UV lithography</figcaption></div>
</figure>

Deep-Dive ultra violet(UV) Lithography is the process used to transfer a pattern from a mask to the substrate. 

The process follows six technical steps:

1. Bulk Substrate: Begin with the base material (typically a Silicon wafer).
2. Coating: Apply a thin film of Photoresist (PR), a photosensitive polymer.
3. Masking: Cover the PR with a pre-patterned mask.
4. Developing: Expose to UV light and place in a developing solution to reveal the pattern.
5. Etching: Subtract the thin film in areas not protected by the PR.
6. Stripping: Remove the remaining PR to conclude the subtraction phase.

<figure>
   <img src="/Robotics/Sensors/semi6_photolithography.png" alt="photolithography" width="100%" align="center">
   <div align="center"><figcaption> Figure 2: A schematic illustrating the optical path where a UV light source passes through reduction optics and a patterned mask. The optics focus the light onto the wafer surface, ensuring the pattern is "in focus" for precise transfer onto the photoresist.</figcaption></div>
</figure>

Technical Limits The resolution (minimum width $w$) of a device is limited by the wavelength ($\lambda$) of the light source (used to make the image transfer from a mask to a target material), expressed by the formula:
$$
w \approx \sqrt{\lambda}
$$

- Typical light source: UV light; wave length $\sim 0.3$ to $0.5\mathrm{~\mu m}$ ($300$ to $500\mathrm{~nm}$)

As technology has progressed, the limit of photolithography size reduction has moved from $10 \mathrm{~\mu m}$ in 1971 to approximately $11 \mathrm{~nm}$ in 2015, utilizing light sources like Hg lamps ($~400 \mathrm{~nm}$), KrF lasers ($248 \mathrm{~nm}$), and ArF lasers ($193 \mathrm{~nm}$).

PR thickness $t$ can be expressed by the equation:
$$
t\sim ks^2/\sqrt{\omega}
$$

where $k$ is a constant related to viscosity, $s$ is the solid content in the solution expressed in percent by weight, and $\omega$ is the angular velocity of the spinning wafer.

### Thin Film Addition: Growth and Deposition

Adding materials to a substrate is achieved through two distinct philosophies: growth and deposition.

Growth vs. Deposition

* **Growth**: Requires a **"seed" material** from the substrate (基材). For example, Silicon Dioxide ($\mathrm{SiO}_2$) can be grown from a Silicon (Si) substrate.

  Thermal Oxidation: $\mathrm{SiO}_2$ is grown by heating Si to $900–1200^\circ\mathrm{C}$ in either pure oxygen or water.
  * **Dry Oxidation**: $\mathrm{Si} + \mathrm{O}_2 \rightarrow \mathrm{SiO}_2$
  * **Wet Oxidation**: $\mathrm{Si} + 2\mathrm{H}_2\mathrm{O} \rightarrow \mathrm{SiO}_2+ 2\mathrm{H}_2$
  * Deal-Grove Model: 
    $$
      X_{\mathrm{SiO}_2}(t) = .5A\left[\sqrt{1+\frac{4B}{A^2}t}-1\right]
    $$
    * For short durations, specifically when $t \ll A^2/4B$, the oxide thickness is calculated as $X_{\mathrm{SiO}_2}(t) = (B/A)t$.
* **Deposition**: Material is placed on top of a substrate. This does not require a chemical relationship with the base material (e.g., depositing Gold on Silicon).
  * **Thermal Evaporation** (Physical Vapor Deposition)
  * **E-Beam Evaporation** (Physical Vapor Deposition)
  * **Sputtering** (Physical Vapor Deposition)
  * **Chemical Vapor "Deposition"**

#### Thermal Evaporation
Evaporation of thin films take place in a vacuum environment.

Note:
- Physical Vapor Deposition (PVD) PVD occurs in a vacuum to prevent oxidation and ensure uniform coverage.
-  A vacuum system can be classified based on its chamber pressure
   - High vacuum: $10^{-3}$ to $10^{-6} \mathrm{~Torr}$
   - Very high vacuum: $10^{-6}$ to $10^{-9} \mathrm{~Torr}$
   - Ultrahigh vacuum: below $10^{-9} \mathrm{~Torr}$
- $1 \mathrm{~micron} = 1 \mathrm{~mTorr}; 1 \mathrm{~mTorr} = 1 \mathrm{~mm} Hg; 1 \mathrm{~Pa}=1 \mathrm{~N}/\mathrm{~m}^2 = 7.5 \mathrm{~mTorr} (1 \mathrm{~mTorr} = 0.133 \mathrm{~Pa})$
  - This is a unit of pressure, NOT a unit of distance.

The mean-free-path of gas particles is about
$$
  \lambda=5/P_m [\mathrm{cm}]
$$

where $P_m$ is the pressure in $\mathrm{mTorr}$. Thus at a pressure of $10^{-4}\mathrm{~Torr}$, $\lambda$ is of the order of $50\mathrm{~cm}$, which is about the size of a typical vacuum chamber.

The rate at which atoms pass into vacuum from a heated source is given by the Hertz-Knudsen equation:
$$
  W = 3.5\times 10^{22}\alpha P^*/(MT)^{1/2} \mathrm{~atoms/cm^2-sec}
$$

where $P^*$ is the vapor pressure in $\mathrm{Torr}$, $T$ is the temperature in $^\circ K$, and $M$ is the molecular weight in grams. The parameter $\alpha$ is the evaporation coefficient and is dependent on the cleanliness of the evaporation surface and range from $1$ (clean surface) to $10^{-3}$ (dirty surface).

Thus, the evaporated flux from a small source of area $A_e$ and evaporation rate $W$, which is incident on an elemental substrate surface area located in an angle $f$ off the perpendicular axis of the source (as shown below) yields a deposition flux per unit area of the substrate that is given by
$$
  W_d = (WA_e/pr^2)\cos\phi\cos\theta
$$

where $r$ is the distance from the source to the substrate. The cosq term accounts for the fact that the substrate may not be perpendicular to the line of centers connecting the source and substrate.

The **thickness growth rate** of the film is given by:
$$
  D=MW_d/rN_A
$$

Where $N_A$ is Avogadro’s number, $M$ is the molecular weight, and $r$ is the mass density of the deposit.

Summary of Thermal Evaporation
- Source materials: aluminum ($\mathrm{Al}$), copper ($\mathrm{Cu}$), nickel ($\mathrm{Ni}$), chromium ($\mathrm{Cr}$), titanium ($\mathrm{Ti}$), gold ($\mathrm{Au}$), $\mathrm{SiO}_2$, …etc.
- Chamber condition: high vacuum to control composition of the deposited materials ($10^{-5}$ to $10^{-6} \mathrm{~Torr}$)
- Prevents oxidation (low moisture in a vacuum chamber)
- Allows uniform coverage

#### E-Beam Evaporation
- Basically same as Thermal Evaporation, except that **an electron-beam is used to melt source materials** (instead of a **resistive coil** (电阻线圈) that is used in thermal evaporation systems)
- Source materials: same as thermal evaporation, i.e., $\mathrm{Al, Cu, Ni, Cr, Ti, Au, SiO}_2$, …etc.
- The source material is **not in direct contact** with a filament as in the case of thermal evaporation. This non-contact evaporation will allow **cleaner** materials to be deposited.

<figure>
   <img src="/Robotics/Sensors/semi5_e-beam.png" alt="e-beam" width="100%" align="center">
   <div align="center"><figcaption> Figure 3: Schematics of E-Beam Evaporator.</figcaption></div>
</figure>

Melting Temperatures  of various commonly used MEMS materials

| Target | Melting Pt (°C) | Temp at 10^{-2} Torr (°C) |
| ---- | ---- | ----|
| Aluminum (Al) | 659 | 1220 |
| Chromium (Cr) | ~1900 | 1400 |
| Copper (Cu) | 1084 | 1260 |
| Gold (Au) | 1063 | 1400 |
| Nickel (Ni) | 1450 | 1530 |
| Platinum (Pt) | 1770 | 2100 |
| Silicon (Si) | 1410 | 1350 |
| Titanium (Ti) | 1700 | 1750 |
| Tungsten (W) | 3380 | 3230 |

#### Sputtering
A **momentum transfer** process * no chemical or composition change of material.

- Source material: almost anything.
- Atoms for molecules at source (target) surface are "knocked off" by energized gas ions (e.g., $\mathrm{Ar}^+$) and deposit on the wafer.
- More expensive than evaporation

<figure>
   <img src="/Robotics/Sensors/semi5_sputtering.JPG" alt="sputtering" width="100%" align="center">
   <div align="center"><figcaption> Figure 4: Schematics of Sputtering.</figcaption></div>
</figure>

Sputtering "Yields":
- However, Sigmund’s linear cascade theory correlates well with experimental values in the near-linear energy range and has become widely used:
$$
S = K(M_iM_t/(M_i+M_t)^2)(E/U_o) a(M_t/M_i)$$

where $K$ is a constant in the range from .1 to .3, $M_i$ and $M_t$ are the masses of the incident ion and target atom, respectively, $E$ is the energy of the incident ion, and $U_o$ is the binding energy of the target atom (usually taken as the sublimation energy). $a(M_t/M_i)$ is a monotomically increasing function of $M_t/M_i$; at typical mass ratios of $M_t/M_i \sim 2$, $a$ is $\sim 0.3$.


Chemical Vapor Deposition (CVD) CVD involves chemical interactions between gas precursors and the substrate.

Ion energy and sputtering yield for various MEMS related materials

|Target|Ion Energy (eV)|Yield (atoms/ion)|
|----|----|----|
|Au|600|2.8|
|Cr|600|1.3|
|Pt|600|1.6|
|Al|500|1.0|
|Si|500|0.5|
|Cu|500|2.4|

#### Chemical Vapor "Deposition"
Chemical interaction between vapor and substrate

#### CVD
Example:
- Silicon Nitride: $\mathrm{SiH}_4 + \mathrm{NH}_3 + \mathrm{H}_2 \to \mathrm{Si}_x\mathrm{N}_y$ ($\mathrm{Si}_3\mathrm{N}_4$ + gas by products)
- Silicon Nitride: $\mathrm{SiH}_2\mathrm{Cl}_2 + \mathrm{NH}_3 + \mathrm{H}_2 \to \mathrm{Si}_x\mathrm{N}_y$ ($\mathrm{Si}_3\mathrm{N}_4$ + gas by products)
- Polysilicon: $\mathrm{SiH}_4 \to \mathrm{Si} + 2\mathrm{H}_2$
- Silicon Dioxide: $\mathrm{SiH}_4 + \mathrm{O}_2 \to \mathrm{SiO}_2 + 2\mathrm{H}_2$

Various types:
* LPCVD (Low Pressure):
  * Operates at ~0.5 Torr;
  * Long gas mean-free-path
  * Excellent step coverage.
* PECVD (Plasma Enhanced)
  * Same as LPCVD, but grows discharge plasma during deposition
  * Lower deposition temperature than LPCVD
  * Film quality worst than LPCVC

<figure>
   <img src="/Robotics/Sensors/semi6_cvd.png" alt="cvd" width="100%" align="center">
   <div align="center"><figcaption> Figure 5: Plasma-Enhanced CVD.</figcaption></div>
</figure>


#### Electroplating 电镀
* A classical method to “grow” metals
* Requires a seed layer
* The term electroplating means the coating of an object with a thin layer of metal by use of electricity. The metals most often used are **gold, silver, chromium, copper, nickel, tin and zinc**, but many others are used also. The object to be plated is usually a different metal, but can be the same metal or a non-metal.
* Useful for **"LIGA"** micromachining process.

#### Spin-on coating
Thickness:
$$
t\sim ks^2/\sqrt{\omega}
$$

* Materials such as photoresist and polyimide (widely used as a passivation layer for IC chips and as a structural material for MEMS devices)
* Polyimid (survives up to $\sim 300 ^\circ\mathrm{C}$) used to build MEMS devices has the following disadvantage:
  * May be unstable over time mechanically
  * Attracts moisture
* Generally, materials which are in viscous-fluidic form at room temperature can be spin-coated, i.e., liquid polymers.

### Thin Film Subtraction: Etching Fundamentals

#### Etching Metrics

* A process is selective if it etches the desired material at a high rate and all other exposed surfaces at lower rates.
* Selectivity ($S_\text{AB}$): The ratio of the etch rate of material A to material B. High selectivity is required to ensure the etchant removes the target film without destroying the mask or substrate.
* Isotropy/Anisotropy: **Isotropic** etches are non-directional (**rounded sidewalls**), while **anisotropic** etches are directional (**vertical sidewalls**).

#### Wet Etching
Completely based on chemical reactions

<figure>
   <img src="/Robotics/Sensors/semi6_wet.png" alt="wet" width="100%" align="center">
   <div align="center"><figcaption> Figure 6: Wet Etching.</figcaption></div>
</figure>

* **Polysilicon Etch**
  * Etched with Nitric and Hydrofluoric (HF) acid at room temperature.
  * $\mathrm{Si+HNO}_3 + 6\mathrm{HF}\to \mathrm{H}_2\mathrm{SiF}_6 + \mathrm{HNO}_2 + \mathrm{H}_2 + \mathrm{H}_2\mathrm{O}$
  * Mask: Nitride or photoresist (not for too long)
  * Etchrate at ~400 Å/min for $n^+$ doped polysilicon
  * ~1500 Å/min for undoped polysilicon
* **Nitride Etch**
  * Nitride is very hard to etch, so it's a good mask for many processes
  * Use hot Phosphoric Acid ($\mathrm{H}_3\mathrm{PO}_4$)
  * Etchrate: ~80 Å/min at 180°C. The etch rate is strongly dependent on film composition, i.e., the stoichiometry ($x$ and $y$ values for $\mathrm{Si}_x\mathrm{N}_y$).
  * Mask: $\mathrm{SiO}_2$ ~1 Å/min
* Oxide Etch ($\mathrm{SiO}_2$)
  * Use HF at room temperature.
  * $\mathrm{SiO}_2 + 6\mathrm{HF} \to \mathrm{SiF}_6 + \mathrm{H}_2 + 2\mathrm{H}_2\mathrm{O}$
  * Mask: photoresist, polysilicon, nitride
  * Etchrate: dry oxide < wet oxide < CVD oxide
  * With 49% HF ==> 23,000 Å /min for wet oxide; 36,000 Å /min for phosphosilicate glass(PSG)
  * With 5:1 of $\mathrm{H}_2\mathrm{O}$: HF mixture ==> 1,000 Å /min for wet oxide; 7,000 Å /min for PSG

The advantage of wet etching is that it gives good **selectivity** but its **resolution limit** is only $\sim 3 \mathrm{~\mu m}$.

#### Dry Etching and Plasma

**Plasma** (等离子体) is a highly ionized gas with local electric charges that produce physical and chemical etching effects.

* Doping Effects: In plasma etching, heavily n-type doped Polysilicon etches much faster than p-type or undoped versions.
* Gas Profiles: Fluorine-based gases ($\mathrm{CF}_4, \mathrm{SF}_6$) generally etch isotropically, while Chlorine-based gases ($\mathrm{Cl}_2$) provide anisotropic profiles.

* Polysilicon
  * Poly-Si can be etched by $\mathrm{Cl}$ and $\mathrm{F}$ based gases such as $\mathrm{Cl}_2, \mathrm{CF}_4$, and $\mathrm{SF}_6$.
  * $\mathrm{F}$ based gases generally etch isotropically while $\mathrm{Cl}$ based gases can yield anisotropic profiles.
  * For heavily n-type doped poly-Si, the etch rate is >> undoped poly-Si
  * For p-type doped poly-Si, the etch rate is indistinguishable from undoped poly-Si.
* Thermal and LPCVD Oxide
  * $S\mathrm{iO}_2$ can be etched by $\mathrm{CHF}_3, \mathrm{C}_2\mathrm{F}_6, \mathrm{CCl}_4, \mathrm{CF}_4$ and $\mathrm{NF}_3$.
  * $\mathrm{CHF}_3, \mathrm{C}_2\mathrm{F}_6$, and $\mathrm{CCl}_4$ etch $\mathrm{SiO}_2$ ansiotropically under most operating conditions.
  * $\mathrm{CF}_4$ and $\mathrm{NF}_3$ can etch $\mathrm{SiO}_2$ ansiotropically
  only under specific operating conditions.
  * Etch rate: PSG > LPCVD $\mathrm{SiO}_2$ > thermal $\mathrm{SiO}_2$. (Rate of psg can be $2R$ (thermal-$\mathrm{SiO}_2$))


**Sputtering** yields are generally determined experimentally. However, Sigmund’s linear cascade theory correlates well with experimental values in the near-linear energy range and has become widely used.


## Example: Micro Hinge

The "Pister Hinge" demonstrates how surface micromachining creates moving mechanical parts through the use of sacrificial layers.

Fabrication Sequence

1. Grow a sacrificial SiO_2 layer on a Silicon substrate.
2. Apply Photoresist (PR).
3. Expose and develop the PR to define a "bar" pattern.
4. Etch the SiO_2 to create the sacrificial support.
5. Deposit a structural Polysilicon layer over the SiO_2 bar.
6. Apply a second PR layer.
7. Expose and develop to define the hinge beam.
8. Etch the Polysilicon structural layer.
9. Strip the PR.
10. Final Release: Remove the SiO_2 sacrificial layer with HF, leaving a free-standing, movable Polysilicon beam.

## Summary
* Surface Micromachining
  * Thin film addition
  * UV Photolithography
  * Thin film subtraction

### Q: What are the common Si-based materials used to build MEMS devices?

Common silicon-based materials used in the construction of MEMS devices include:

*   **Single Crystalline Silicon (Si):** This is typically used as the **bulk substrate** or base material for the devices.
*   **Polysilicon (Poly-Si):** This is a primary **structural material** used to build components like beams and hinges. It is often deposited using Chemical Vapor Deposition (CVD).
*   **Silicon Dioxide ($\mathrm{SiO}_2$):** This material is pervasive in MEMS for **electrical insulation**, as a **masking material**, or as a **sacrificial layer** that is later removed to release moving parts. It can be "grown" through thermal oxidation or deposited via CVD.
*   **Silicon Nitride ($\mathrm{Si}_3\mathrm{N}_4$ or $\mathrm{Si}_x\mathrm{N}_y$):** It is frequently used as a **masking material** because it is very hard to etch, but it can also serve as a structural layer. 
*   **Amorphous Silicon:** This form of silicon is specifically mentioned as a material used in Plasma-Enhanced Chemical Vapor Deposition (PECVD) processes.
*   **Phosphosilicate Glass (PSG):** Often categorized with oxides, PSG is used in thin-film addition and is sometimes referred to as **Low Temperature Oxide (LTO)**.

These materials are typically applied to a substrate through a process of **adding thin films**, patterning them via **photolithography**, and then **subtracting** (etching) them to create complex microscopic structures.

### Q: What are the key techniques to add thin films?

Key techniques for adding thin films in micro-fabrication and MEMS technology include **growth**, **deposition**, **electroplating**, and **spin-on coating**.

1. **Thin Film Growth (Thermal Oxidation)**
Growth requires a proper "seed" material to initiate the process. The most common example is **thermal oxidation**, where silicon ($\mathrm{Si}$) is heated to temperatures between **900 and 1200 °C** in either pure oxygen (dry oxidation) or water vapor (wet oxidation) to grow **silicon dioxide ($\mathrm{SiO}_2$)**. This material is widely used for electrical insulation or as a masking layer.

2. **Deposition Techniques**
Deposition is categorized into two main physical and chemical processes:
   * **Physical Vapor Deposition (PVD):**
       * **Thermal Evaporation:** Uses a resistive coil to heat and evaporate source materials (like $\mathrm{Al, Cu, Au}$, or $\mathrm{SiO}_2$) in a high vacuum environment.
       * **E-Beam Evaporation:** Similar to thermal evaporation, but utilizes an **electron beam** to melt the source material. Because the material is not in direct contact with a filament, it allows for cleaner deposited films.
       * **Sputtering:** A **momentum transfer process** where energized gas ions (typically $Ar^+$) "knock off" atoms from a target material, which then deposit onto the wafer. This process is more expensive than evaporation but can be used for almost any material.
   * **Chemical Vapor Deposition (CVD):** This involves a **chemical interaction** between a vapor and the substrate. 
       * **LPCVD (Low Pressure CVD):** Performed at low pressure (~0.5 torr) to ensure a long gas mean-free-path and **excellent step coverage**.
       * **PECVD (Plasma Enhanced CVD):** Uses discharge plasma to allow for **lower deposition temperatures** than LPCVD, though the film quality is generally lower.

3. **Electroplating**
This is a classical method used to **grow metals** (such as gold, silver, copper, and nickel) by using electricity. It requires a **seed layer** and is particularly useful for the "LIGA" micromachining process.
4. **Spin-on Coating**
This technique is used for materials that are in **viscous-fluidic form** at room temperature, such as liquid polymers. A uniform layer is achieved by spinning the wafer at high speeds.
   * **Common Materials:** **Photoresist (PR)** and **polyimide**.
   * **Thickness Control:** The thickness ($t$) is controlled by the angular velocity ($w$), viscosity, and solid content of the solution.

### Q: What are the key techniques to subtract thin films?

The key techniques to subtract thin films, also known as **etching**, are categorized into two primary methods: **wet etching** and **dry etching**.

1. **Wet Etching**
This technique is **completely based on chemical reactions** between an etching solution and the thin film material.
   *   **Mechanism:** The wafer is immersed in a liquid chemicals that attack the targeted material but ideally not the masking layer (like photoresist).
   *   **Advantages:** It typically offers **good selectivity**, meaning it can etch one material much faster than others.
   *   **Disadvantages:** It has a **resolution limit of approximately 3 µm** and often suffers from **under-cutting** (under-etching), where the chemicals etch horizontally beneath the mask.
   *   **Common Examples:** 
       *   **Polysilicon:** Etched using Nitric acid ($HNO_3$) and Hydrofluoric acid (HF).
       *   **Silicon Dioxide ($SiO_2$):** Etched using HF or Buffered Oxide Etch (BOE).
       *   **Silicon Nitride ($Si_3N_4$):** Etched using hot phosphoric acid ($H_3PO_3$) at 180°C.

2. **Dry Etching**
Dry etching uses gases, ions, or plasma to remove material rather than liquid chemicals.
   *   **Plasma Etching:** This involves using a highly ionized gas, or **plasma**, to produce chemical or physical effects on the target layer. It can be **isotropic** (producing round sidewalls) or **anisotropic** (producing vertical sidewalls) depending on the gases used.
       *   *Fluorine-based gases* (like $CF_4$ or $SF_6$) generally etch isotropically.
       *   *Chlorine-based gases* (like $Cl_2$) can yield anisotropic profiles.
   *   **Sputtering:** This is a physical momentum transfer process where energized ions "knock off" atoms from the target surface.
   *   **Reactive Ion Etching (RIE):** A common form of dry etching mentioned for materials like Parylene using $O_2$ plasma to achieve specific etch rates.

**Key Concepts in Subtraction**
*   **Selectivity:** A process is considered selective if it etches the desired material at a high rate while leaving other exposed surfaces (like the substrate or mask) relatively untouched.
*   **Isotropy vs. Anisotropy:** **Isotropic** etches progress in all directions equally (round sidewalls), while **anisotropic** etches are directional (vertical sidewalls), which is often preferred for high-precision micro-structures.
