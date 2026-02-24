# Mechanical Vibrations: Second-Order Systems
## Introduction to Vibrational Systems

In the field of mechanical engineering, we define vibration as any motion that repeats itself after a specific interval of time. As you begin modeling complex machinery, it is vital to recognize that nearly all vibratory systems can be reduced to three essential building blocks:

1. Spring (Elasticity): A component that stores potential energy.
2. Mass (Inertia): A component that stores kinetic energy.
3. Damper: The mechanism through which energy is dissipated.


The fundamental physics of vibration involves the continuous **transfer** of energy between **potential and kinetic states**. When a system's mass is displaced from its equilibrium, the spring exerts a restoration force. The mass then gains momentum, overshooting the equilibrium position due to its inertia, which results in the characteristic oscillatory motion we study.

Practical Application: Note that understanding these building blocks is the foundation of structural stability. By correctly modeling these components, engineers can predict how a structure will react to external forces, ensuring that vibrations remain within safe limits to prevent structural fatigue or catastrophic failure.

## Classification of Vibrational Motion

Before diving into the mathematics, we must classify the motion based on the system components and the predictability of the excitation forces.

|Classification|Definition|
|----|----|
|Undamped Vibration|Occurs when no energy is lost or dissipated through friction or resistance during oscillations.|
|Damped Vibration|Occurs when energy is dissipated through friction or other resistances, eventually bringing the system to rest.|
|Linear Vibration|A system where all components—the spring, mass, and damper—behave linearly.|
|Nonlinear Vibration|A system where any of the basic components behave nonlinearly.|
|Deterministic Vibration|A system where the magnitude of the excitation (force or motion) is known at any given time.|
|Nondeterministic (**Random**) Vibration|A system where the value of the excitation at a given time cannot be predicted and is characterized as irregular and fluctuating.|

<figure>
   <img src="/Robotics/Sensors/semi9_determine.png" alt="determine" width="100%" align="center">
   <figcaption> Figure 1: deterministic and random.</figcaption>
</figure>

Observe the difference in the force-time histories: the deterministic plot shows a clear, periodic pattern, whereas the random excitation plot shows irregular, fluctuating values where no specific magnitude can be predicted for a future time step.

## Modeling the Simple Harmonic Oscillator

To analyze any vibrational system, we must derive its governing Equation of Motion. We rely on Newton’s Second Law: F = ma. In a standard second-order system, we must account for several specific forces.

The Newtonian Sum of Forces:

* Restoration force of the spring: $-kx$
* Damping force: $-c \frac{\mathrm{d}x}{\mathrm{d}t}$
* Gravity (Weight): $W = mg$
* Static restoration force: $-k\delta_{st}$ (The force required to offset gravity at rest)
* External Force: $F(t)$

Synthesized Equation of Motion: When we apply $F = ma$ to a vertical mass, the sum of forces is: $m \frac{\mathrm{d}^2x}{\mathrm{d}t^2} = -k(x + \delta_{st}) - c \frac{\mathrm{d}x}{\mathrm{d}t} + mg + F(t)$

In static equilibrium, the weight of the mass is perfectly balanced by the spring's static deflection force ($mg = k\delta_{st}$). Consequently, these terms cancel out, leaving us with the simplified dynamic equation: $m\ddot{x} + c\dot{x} + kx = F(t)$

## Solving Second-Order Differential Equations

To determine the system response, we solve the homogeneous equation $m\ddot{x} + c\dot{x} + kx = 0$. Engineers simplify this by writing the characteristic equation in terms of a variable $a$: $a^2 + P_1 a + P_0 = 0$

By solving for the roots $a_{1,2}$ using the quadratic formula, we identify 3 distinct physical behaviors:

1. Distinct Real Roots ($P_1^2 \neq 4P_0$): The system is overdamped. The general solution is $y(t) = C_1 e^{a_1 t} + C_2 e^{a_2 t}$.
2. Complex Roots ($z_{1,2} = \alpha \pm i\beta$): The system is underdamped. The solution is oscillatory: $y(t) = C_1 e^{\alpha t} \cos \beta t + C_2 e^{\alpha t} \sin \beta t$.
3. Repeated Roots ($a_1 = a_2$): The system is critically damped. The solution is $y(t) = C_1 e^{a_1 t} + C_2 t e^{a_1 t}$.

## System Responses and Damping Characteristics

The Damping Ratio ($\zeta$) is the ratio of the actual damping coefficient ($c$) to the critical damping coefficient ($c_c$). It dictates the decay of the system:

* **Overdamped** ($\zeta > 1$): High resistance; the mass creeps back to equilibrium without ever crossing it.
* **Critically Damped** ($\zeta = 1$): The threshold state where the system returns to equilibrium in the shortest time possible without oscillation.
* **Underdamped** ($\zeta < 1$): The system oscillates with diminishing amplitude. The response is described by: $x = e^{-\gamma t} a \cos[\omega_1 t - \alpha]$.

<figure>
   <img src="/Robotics/Sensors/semi9_damped.png" alt="damped" width="100%" align="center">
   <figcaption> Figure 2: Simple Harmonic Oscillator.</figcaption>
</figure>

Observe the decay curves. A system with "one-tenth of critical" damping ($\zeta = 0.1$) exhibits many large oscillations. As \zeta increases to "one-half of critical" ($\zeta = 0.5$), the oscillations are suppressed much faster, demonstrating the efficiency of energy dissipation.

Key Takeaway: It is vital to select appropriate damping levels to avoid Aerodynamic Flutter. Without sufficient damping, aerodynamic forces can cause unstable, growing oscillations in structures like aircraft wings or bridges, leading to total structural failure.

## Frequency Domain Analysis: Laplace Transforms

Engineers use the Laplace Transform to convert second-order differential equations from the time domain ($t$) into the frequency domain ($s$). This changes calculus problems into simpler algebraic ones. By defining:
- The operator $s = j\omega$
- Circular natural frequency: $\omega_n=\sqrt{\frac{k}{m}}$
- $\zeta = c/c_c$, actual damping / critical damping
- $c_c=2m\sqrt{\frac{k}{m}} = 2m\omega_n$

We derive the Transfer Function, $H(s)$, representing the ratio of output $X(s)$ to input $F(s): H(s) = \frac{X(s)}{F(s)} = \frac{1}{ms^2 + cs + k}$

To reach the standard engineering form, we normalize this into the Transfer Function $G(s)$: 

$$
G(s) = \frac{\omega_n^2}{s^2 + 2\zeta\omega_n s + \omega_n^2}
$$

The frequency response can be written as
$$
G(j\omega) = \frac{1}{[1-(\omega/\omega_n)^2] + j2\zeta(\omega/\omega_n)}
$$

The magnitude is:
$$
|G(j\omega)| = \frac{1}{\sqrt{[1-(\omega/\omega_n)^2]^2 + (2\zeta(\omega/\omega_n))^2}}
$$

Define the normalized frequency as $\omega_v=\omega/\omega_n$, we have the normalized magnitude $|G(j\omega_v)|$:
$$
|G(j\omega_v)| = \frac{1}{\sqrt{(1-\omega_v^2)^2 + (2\zeta\omega_v)^2}}
$$

In the frequency domain, we analyze the Bandwidth, which is the range of frequencies over which the system responds significantly. This bandwidth varies based on the damping ratio $\zeta$ and natural frequency $\omega_n$.

<figure>
   <img src="/Robotics/Sensors/semi9_zeta.JPG" alt="damped" width="100%" align="center">
   <figcaption> Figure 3: Different zeta.</figcaption>
</figure>

These plots illustrate resonance. As the frequency ratio $\omega/\omega_n$ approaches $1$, the magnitude peaks. Note that as $\zeta$ decreases, the peak magnitude becomes sharper and higher. Conversely, higher damping "flattens" the curve, reducing the peak response.

### Free Vibrations of Undamped Systems

Free vibration occurs when a system oscillates purely under an initial disturbance ($x_0$ or $\dot{x}_0$) with no continuous external force.

Classified by **damp**:
* **Undamped vibrations** result when amplitude of motion remains constant with time (e.g., in a vacuum)
* **Damped vibrations** occur when the amplitude of free vibration diminishes gradually overtime, due to resistance offered by the surrounding medium (e.g., air)

Classified by **system**:
* The **Horizontal System**: Frictionless motion results in:
   $$
   m\ddot{x} + kx = 0
   $$
* The **Vertical System**: As established in Section 3, gravity ($mg$) and static deflection ($k\delta_{st})$ **cancel out**, yielding the same result:
   $$
   m\ddot{x} + kx = 0
   $$

This indicates that when a mass moves in a vertical direction, we can ignore its weight, provided we measure $x$ from its static equilibrium position.

The Euler Bridge to Harmonic Motion: We initially assume a solution in complex exponentials: $x(t) = C_1 e^{i\omega_n t} + C_2 e^{-i\omega_n t}$. By applying Euler’s Formula $(e^{i\phi} = \cos \phi + i \sin \phi)$, we can transition to the more practical trigonometric form:
$$
   x(t) = A_1 \cos \omega_n t + A_2 \sin \omega_n t
$$

Applying Initial Conditions:
$$
x(t=0)=A_1=x_0, \quad \dot{x}(t=0)=\omega_nA_2 = \dot{x}_0
$$

By solving for constants using initial displacement $(x_0)$ and velocity $(\dot{x}_0)$, we find:
$$
x(t) = x_0 \cos \omega_n t + \frac{\dot{x}_0}{\omega_n} \sin \omega_n t
$$

The motion equation and its solution are **harmonic functions of time**.

The motion equation $x(t) = A_1 \cos \omega_n t + A_2 \sin \omega_n t$ can be expressed as:
$$
   x(t) = A_0\sin(\omega_nt+\phi_0)
$$

where $A_0,\omega_0,\phi_0$ are new constants, amplitude and phase angle respectively, and
$$
   A_0 = A = \left[x_0^2+\left(\frac{\dot{x}_0}{\omega_n}\right)^2\right]^{1/2}, \quad \phi_0 = \tan^{-1}\left(\frac{x_0\omega_n}{\dot{x}_0}\right)
$$

1. For vertical system, the spring constant:
$$
   k = \frac{W}{\delta_\text{st}} = \frac{mg}{\delta_\text{st}}
$$

Hence:
$$
   \omega_n = \left(\frac{g}{\delta_\text{st}}\right)^{1/2}
$$

Hence, natural frequency in cycles per second:
$$
   f_n = \frac{1}{2\pi}\left(\frac{g}{\delta_\text{st}}\right)^{1/2}
$$

and, the natural period:
$$
   \tau_n = \frac{1}{f_n} = 2\pi\left(\frac{\delta_\text{st}}{g}\right)^{1/2}
$$

2. Velocity $\dot{x}(t)$ and the acceleration $\ddot{x}_0$ of the mass $m$ at time $t$ can be obtained as:
$$
\begin{aligned}
   &\dot{x}(t) = \frac{\mathrm{d}x}{\mathrm{d}t}(t) = -\omega_nA\sin(\omega_nt-\phi) = \omega_nA\cos(\omega_nt-\phi+\pi/2)\\
   &\ddot{x}(t) = \frac{\mathrm{d}^2x}{\mathrm{d}t^2}(t) = -\omega_n^2A\cos(\omega_nt-\phi) = \omega_n^2A\cos(\omega_nt-\phi+\pi)
\end{aligned}
$$

3. 
- If initial displacement ($x_0$) is zero,
$$
   x(t) = \frac{\dot{x}_0}{\omega_n}\cos(\omega_nt-\pi/2) = \frac{\dot{x}_0}{\omega_n}\sin\omega_nt
$$
- If initial velocity ($\dot{x}_0$) is zero,
$$
   x(t) = x_0\cos\omega_nt
$$

### Free Vibration with Viscous Damping
Damping force: $F_\text{damp} = -c\dot{x}$, where $c$ is the damping constant.

In the vertical system, Newton’s law yields
the equation of motion:
$$
   m\ddot{x} = -c\dot{x}-kx\implies m\ddot{x} +c\dot{x}+kx = 0
$$

Assume a solution in the form: $x(t) = Ce^{st}$, where $C$ and $s$ are undetermined constants

Hence, the characteristic equation is
$$
   ms^2+cs+k=0
$$

The roots of which are:
$$
   s_{1,2} = \frac{-c\pm\sqrt{c^2-4mk}}{2m} = -\frac{c}{2m}\pm\sqrt{\left(\frac{c}{2m}\right)^2 - \frac{k}{m}}
$$

These roots give two solutions to:
$$
   x_1(t) = C_1e^{s_1t}, \quad x_2(t) = C_2e^{s_2t}
$$

Critical Damping Constant and Damping Ratio: The **critical damping** $c_c$ is defined as the value of the damping constant $c$ for which the radical in the prior becomes **zero**:
$$
   \left(\frac{c_c}{2m}\right)^2-\frac{k}{m} = 0\implies c_c = 2m\sqrt{\frac{k}{m}} = 2\sqrt{km} = 2m\omega_n
$$

The damping ratio $\zeta$ is defined as $\zeta = c/c_c$.

Thus, the general solution is
$$
   x(t) = C_1e^{(-\zeta + \sqrt{\zeta^2-1})\omega_nt} + C_2e^{(-\zeta - \sqrt{\zeta^2-1})\omega_nt}
$$

Assuming that $\zeta\neq 0$, consider the following 3 cases:
- Case 1: Underdamped system ($\zeta<1, c<c_c, c/2m<\sqrt{k/m}$):
   For this condition, $(\zeta^2-1)$ is negative and the roots are:
   $$
      \begin{aligned}
         &s_1 = (-\zeta + i\sqrt{1-\zeta^2})\omega_n\\
         &s_2 = (-\zeta - i\sqrt{1-\zeta^2})\omega_n\\
      \end{aligned}
   $$

   and the solution can be written in different forms:
   $$
      \begin{aligned}
        x(t) & =C_1 e^{\left(-\zeta+i \sqrt{1-\zeta^2}\right) \omega_n t}+C_2 e^{\left(-\zeta-i \sqrt{1-\zeta^2}\right) \omega_n t} \\
        & =e^{-\zeta \omega_n t}\left\{C_1 e^{i \sqrt{1-\zeta^2} \omega_n t}+C_2 e^{-i \sqrt{1-\zeta^2} \omega_n t}\right\} \\
        & =e^{-\zeta \omega_n t}\left\{C_1^{\prime} \cos \sqrt{1-\zeta^2} \omega_n t+C_2^{\prime} \sin \sqrt{1-\zeta^2} \omega_n t\right\} \\
        & =X e^{-\zeta \omega_n t} \sin \left(\sqrt{1-\zeta^2} \omega_n t+\phi\right) \\
        & =X_0 e^{-\zeta \omega_n t} \cos \left(\sqrt{1-\zeta^2} \omega_n t-\phi_0\right)
      \end{aligned}
   $$

   For the initial conditions at $t=0$:
   $$
      C_1^\prime = x_0, \quad C_2^\prime = \frac{\dot{x}_0 + \zeta\omega_nx_0}{\sqrt{1-\zeta^2}\omega_n}
   $$

   and hence the solution becomes
   $$
      x(t) = e^{-\zeta\omega_nt}\left\{x_0\cos(\sqrt{1-\zeta^2}\omega_nt) + \frac{\dot{x}_0 + \zeta\omega_nx_0}{\sqrt{1-\zeta^2}\omega_n}\sin(\sqrt{1-\zeta^2}\omega_nt)\right\}
   $$

   The above equation describes a damped harmonic motion. Its amplitude decreases exponentially with time, as shown in the figure below.
   <figure>
     <img src="/Robotics/Sensors/semi9_undamped.png" alt="undamped" width="100%" align="center">
     <figcaption> Figure 4: Undamped system.</figcaption>
  </figure>

  The frequency of **damped vibration** is:
   $$
      \omega_d = \sqrt{1-\zeta^2}\omega_n
   $$
- Case 2: Critically damped system($\zeta=1, c=c_c, c/2m=\sqrt{k/m}$):
   In this case, the two roots are: 
   $$
      s_1=s_2=-\frac{c_c}{2m} = -\omega_n
   $$

   Due to repeated roots, the solution is given by:
   $$
      x(t) = (C_1+C_2t)e^{-\omega_nt}
   $$

   Application of initial conditions gives:
   $$
      C_1 = x_0, \quad C_2 = \dot{x}_0+\omega_nx_0
   $$

   Thus, the solution becomes:
   $$
      x(t) = [x_0+(\dot{x}_0+\omega_nx_0)t]e^{-\omega_nt}.
   $$

   <figure>
     <img src="/Robotics/Sensors/semi9_cri_damped.png" alt="critial damped" width="100%" align="center">
     <figcaption> Figure 5: Critical damped system.</figcaption>
  </figure>

   It can be seen that the motion represented by the above equation is **aperiodic** (i.e., nonperiodic). Since $e^{-\omega_nt}\to 0$ as $t\to\infty$, the motion will eventually diminish to zero.

- Case 3: Overdamped system: ($\zeta>1, c>c_c, c/2m>\sqrt{k/m}$):
   The roots are real and distinct and are given by:
   $$
      \begin{aligned}
         &s_1 = (-\zeta + \sqrt{\zeta^2-1})\omega_n<0\\
         &s_2 = (-\zeta - \sqrt{\zeta^2-1})\omega_n<0\\
      \end{aligned}
   $$

   In this case, the solution is given by:
   $$
      x(t) = C_1 e^{\left(-\zeta+ \sqrt{\zeta^2-1}\right) \omega_n t}+C_2 e^{\left(-\zeta- \sqrt{\zeta^2-1}\right) \omega_n t}
   $$

   For the initial conditions at $t = 0$,
   $$
      \begin{aligned}
         &C_1 = \frac{x_0\omega_n(\zeta+\sqrt{\zeta^2-1})+\dot{x}_0}{2\omega_n\sqrt{\zeta^2-1}}\\
         &C_2 = \frac{-x_0\omega_n(\zeta-\sqrt{\zeta^2-1})-\dot{x}_0}{2\omega_n\sqrt{\zeta^2-1}}\\
      \end{aligned}
   $$

#### Energy dissipated in Viscous Damping
In a viscously damped system, **the rate of change of energy with time** is given by:
$$
   \frac{\mathrm{d}W}{\mathrm{d}t} = \text{force}\times\text{velocity} = Fv = -cv^2 = -c\left(\frac{\mathrm{d}x}{\mathrm{d}t}\right)^2
$$

The energy dissipated in a complete cycle is:
$$
   \Delta W = \int_{t=0}^{(2\pi/\omega_d)}c\left(\frac{\mathrm{d}x}{\mathrm{d}t}\right)^2\mathrm{~d}t = \int_0^{2\pi}cX^2\omega_d\cos^2\omega_dt\cdot\mathrm{d}(\omega_dt) = \pi c\omega_dX^2.
$$

If we assume simple harmonic motion: $x(t) = X\sin\omega_dt$

## Advanced Harmonic Motion Concepts

To fully describe harmonic motion, we use several specific parameters:

* **Natural Frequency** ($\omega_n$): The angular frequency calculated as $\sqrt{k/m}$.
* **Natural Period** ($T$): The time for one cycle, $T = 2\pi\sqrt{m/k}$.
* **Frequency** ($f$): Cycles per second (Hz), $f = \frac{1}{2\pi} \sqrt{k/m}$.
* **Amplitude** ($A_0$): The maximum displacement, $\sqrt{x_0^2 + (\dot{x}_0/\omega_n)^2}$.
* **Phase Angle** ($\phi$): The initial angle of oscillation, $\tan^{-1}(\frac{x_0 \omega_n}{\dot{x}_0})$.