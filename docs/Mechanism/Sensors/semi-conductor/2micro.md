# 2 Physics in the Micro and Nano Worlds
## Micro/Nano Scale Physics
### Surface Force Domination
- For **conventional macro** manipulation, **gravitational force** is dominate over surface forces, i.e., we can pick and place objects as desired
- For **micro/nano** manipulations, **surfaces forces** are dominate over gravity or inertia forces, i.e., **adhesion** force is a problem.

In micro/nano scales:
- Electrostatic / 静电力
- Surface Tension (capillary) 表面张力（毛细管）
- van der Waals / 范德华力

## Why Make Things Small?
- Higher Frequency Response
- Faster time response
- Faster diffusion times

## Quiz
### In the micro world, which force is more important: body force or surface force? Why?
In the micro world, **surface force** is significantly more important than body force. 

The reasons for this shift in importance are rooted in the physics of **scaling** and the **surface-to-volume ratio**:

**1. Scaling Laws**
The importance of a force is determined by how it scales as dimensions decrease:
*   **Body Forces (e.g., Gravity and Inertia):** These are proportional to **volume**, which scales at **$L^3$** (where $L$ is a characteristic length). As an object gets smaller, its volume and weight drop extremely rapidly.
*   **Surface Forces (e.g., Adhesion, Surface Tension, Electrostatics):** These are proportional to **surface area**, which scales at **$L^2$**. 

**2. Surface-to-Volume Ratio**
Because area ($L^2$) decreases more slowly than volume ($L^3$) during miniaturization, **smaller bodies have a much larger surface area relative to their volume** compared to larger bodies of the same shape. Consequently, as you move from the macro world to the micro world, surface-related phenomena begin to overwhelm volume-related ones.

**3. Physical Consequences**
This shift, known as **Surface Force Domination**, has several critical effects:
*   **Adhesion Problems:** In macro-scale manipulation, gravity is the dominant force, allowing us to pick and place objects easily. In the micro/nano world, **surface forces (like van der Waals and electrostatics)** are much stronger than gravity, making "stiction" or adhesion a major problem—objects tend to "stick" to surfaces and are difficult to release.
*   **Faster Thermal and Chemical Response:** Because heat exchange and diffusion are governed by the surface-to-volume ratio, micro-scale devices can exchange heat and allow molecules to diffuse significantly faster than macro-scale devices. For example, a molecule in a 10µm volume diffuses **1,000,000 times faster** than one in a 1cm volume.
*   **Dominant Forces:** In the micro world, forces that are typically neglected in the macro world—such as **electrostatic forces**, **surface tension (capillary forces)**, and **van der Waals forces**—must be given much more attention.

### Q: Do you know which forces we should pay much more attention to in the micro world (i.e., we normally neglect these forces in the macro world)?
In the micro world, you must pay much more attention to **surface forces**, which are often neglected in the macro world because **body forces** (like gravity and inertia) are usually dominant at larger scales.

According to the sources, the specific forces that become dominant and require careful consideration in micro-scale engineering include:

*   **Electrostatic Forces:** These are caused by contact charges between uncharged bodies, interactions between a charged body and an uncharged wall, or forces between multiple charged bodies.
*   **van der Waals Forces:** These arise from the **instantaneous polarization** of atoms and molecules due to quantum mechanical effects. While they are temporary and weak at a macro level, they contribute significantly to **adhesion problems** (stiction) in the micro world.
*   **Surface Tension (Capillary Forces):** These forces depend on the liquid-air interfacial tension, contact angles, and the radius of liquid drops. In micro-fluidics, surface tension can become a primary driver of motion or a significant obstacle.
*   **Viscous Forces:** In micro-fluidic domains, the **Reynolds number** is typically very low, meaning that **viscous forces dominate over inertia forces**. This makes mixing in microchannels extremely difficult because the flow remains laminar rather than turbulent.

**Why these forces dominate**
This shift in importance is due to **scaling laws** and the **surface-to-volume ratio**. Body forces like gravity scale with volume ($L^3$), while surface forces scale with area ($L^2$). As dimensions ($L$) decrease, the volume drops much faster than the surface area, meaning **smaller bodies have larger surface areas relative to their volumes**. Consequently, surface-related phenomena like adhesion, surface tension, and electrostatics overwhelm the effects of weight and inertia that we are accustomed to in daily life.

### Q: Allometric or Isometric scaling?
The choice between **allometric** and **isometric scaling** depends on whether proportional relationships and shapes are preserved as an object or organism changes in size. 

Here is the breakdown of these two concepts:

**1. Isometric Scaling (Shape-Proportional)**
Isometric scaling occurs when the **proportional relationships** between different dimensions are preserved as size changes. 
*   **Geometric Expectation:** It follows the rule where the scaling exponent ($b$) matches geometric expectations: Length $\propto L$, Area $\propto L^2$, and Volume $\propto L^3$.
*   **Constant Ratios:** In this type of scaling, **ratios remain constant** with size, and the overall shape is preserved.
*   **Micro-Scale Consequence:** Even when scaling is isometric (preserving shape), the **surface-to-volume ratio** changes. Smaller bodies have significantly larger surface areas relative to their volumes than larger bodies of the same shape. This is why surface forces dominate in the micro world.

**2. Allometric Scaling (Non-Proportional)**
Allometry describes how characteristics change with size in a **non-proportional** way ($b \neq$ geometric expectation).
*   **Biological Context:** It originally described the relationship between the size of a body part and the whole body as they grow, but it now encompasses morphological, physiological, and ecological traits.
*   **Functional Adaptation:** Allometric patterns often reflect **functional and adaptive factors**. For example:
    *   **Metabolic Rate:** Scales as the $3/4$-power of mass across 27 orders of magnitude.
    *   **Heart Rate:** Scales with a negative exponent of $-1/4$ (smaller animals have faster heart rates).
    *   **Lifespan:** Generally increases with body mass.
*   **Types of Allometry:** It is categorized as **Positive Allometry** ($b > 1$) or **Negative Allometry** ($b < 1$).

**Comparison Summary**
| Feature | Isometric Scaling | Allometric Scaling |
| :--- | :--- | :--- |
| **Proportions** | Preserved (constant) | Changed (non-proportional) |
| **Shape** | Preserved | Changed |
| **Exponent ($b$)** | Matches geometric expectation ($b=1$) | Deviates from geometric expectation |
| **Drivers** | Pure geometry/physics | Function, adaptation, and evolution |

In engineering and MEMS, we often use **isometric scaling** to predict how physical forces (like gravity vs. electrostatics) will shift as we miniaturize a design. In biology, **allometric scaling** is more common, as it accounts for how real organisms must adapt their physiology (like bone strength or metabolic rate) to survive at different sizes.

### Q: Why do we want to make things small? 
We want to make things small because miniaturization provides fundamental advantages in speed, efficiency, and structural integrity that are not possible at the macro scale. According to the sources, the primary reasons for making things small include:

*   **Higher Frequency Response:** In mechanical sensing, reducing the size of components like a proof mass decreases its inertia. A **smaller mass results in a higher natural frequency ($w_n$)**, which allows sensors to respond much more quickly to rapid physical changes.
*   **Faster Thermal Response:** Heat exchange is governed by the **surface-to-volume ratio**. Because micro-structures have a much larger surface area relative to their volume, they can exchange heat at significantly higher frequencies. For example, a nickel rod with a diameter of 50µm has a thermal time constant of approximately **0.039 seconds**, whereas a rod with a 1.27cm diameter takes **1.24 seconds** to respond.
*   **Rapid Chemical and Biological Analysis:** Diffusion time is drastically reduced at smaller scales. A molecule in a bulk liquid diffuses **1,000,000 times faster** over a distance of 10µm than it does over 1cm. This phenomenon is capitalized on in **Lab-on-a-Chip (LOC)** technology, which integrates multiple laboratory functions onto a single chip to handle picoliters of fluid for near-instantaneous analysis.
*   **Increased Structural Strength:** Smaller objects are relatively **stronger compared to their own weight**. Scaling laws show that axial stress is proportional to length ($L$); therefore, as dimensions decrease, an object is much **less likely to collapse under its own gravity**. This allows micro-structures to survive impacts and forces that would destroy macro-scale versions of the same design.
*   **Integration and Market Efficiency:** Miniaturization allows for the creation of complex, multi-functional systems—such as **MEMS** (Microelectromechanical Systems)—that can be mass-produced at low cost. This has led to a massive global market for small devices like crash sensors, microphones, and micro-fuel cells.


<!-- ## Introduction
::: warning Definition: sensors
A device which provides a usable output in response to a specified measurand
:::

- A sensor acquires a physical parameter and converts it into a signal suitable for processing (e.g.,xs optical, electrical, mechanical)
- A transducer
  - Microphone, Loud Speaker, Biological Senses (e.g., touch, sight,…etc.)

### Good sensors -->
