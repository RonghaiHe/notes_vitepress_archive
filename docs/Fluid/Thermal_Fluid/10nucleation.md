# Modeling of Active Nucleation Site Density*
## Significance of active nucleation site density for simulation
partition of heat flux
$$
Q_w = Q_c+Q_q+Q_e
$$

- $Q_c$: convective heat flux (sub-cooled liquid)
- $Q_q$: quenching heat flux (sub-cooled liquid)
- $Q_e$: evaporation heat flux

Wall nucleation source depends on Key models to estimate wall nucleation source term:
- Active nucleation site density
- Bubble departure diameter
- Bubble departure frequency

## Difficulty of active nucleation site density modeling
Three factors to be considered in modeling
- Flow dynamics
- Heat transfer
- **Surface condition**

## Fundamentals of bubble nucleation
No non-condensable gas contained:
$$
\Delta P = P_g - P_f = \frac{2\sigma}{r} 
$$

According to Clausius-Claypeyron's Eq.
$$
\frac{\mathrm{d}P}{\mathrm{d}T} = \frac{h_{fg}}{T(\nu_g-\nu_f)}
$$

where:
- $\frac{\mathrm{d}P}{\mathrm{d}T}$: Vapor pressure at the equilibrium b/w vapor & liquid
- $h_{fg}$: latent heat
- $\nu_g-\nu_f$: Volume change due to evaporation


Integration from $P_{{f}}$ to $P_{{g}}$, corresponding to $T_{{s}}$ to $T_{{g}}\left(=T_{{f}}\right)$
$$
\Delta {T}_s\left(\equiv T_g-T_{\text {sat }}\right) \approx \frac{T_{\text {sat }} v_g}{i_{f g}} \cdot \frac{2 \sigma}{r} \begin{aligned}
& \text { If } r \text { is very small, } \Delta T_{\mathrm{s}} \\
& \text { becomes very large. }
\end{aligned}
$$

Some non-condensable gas contained
$$
\begin{aligned}
& P_g+P_a=P_f+\frac{2 \sigma}{r} \\
& \Delta T_\text{sat} \approx \frac{T_\text{sat} v_g}{h_{f g}} \cdot\left(\frac{2 \sigma}{r}-P_a\right)
\end{aligned}
$$

Non-condensable gas → Lower superheat


DT=... used in the exam

## Dependence of [Active nucleation site density] on experimental parameters

Dependence of active nucleation site density on exponent to wall superheat from $2.0$ to $6.0$

maybe it's the **exponential function**

## Assumed distributions for cavity size and cone angle
Use different distribution

Hibiki & Ishii (2003)
$$
N_n\approx \overline{N}_n \left\{1-\exp\left(-\frac{\theta^2}{8\mu^2}\right)\right\}\left\{\exp\left(-\frac{\lambda'}{R_c}\right)-1\right\}
$$