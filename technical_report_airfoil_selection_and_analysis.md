# Technical Report: Airfoil Selection and Aerodynamic Analysis
**Prepared for:** IIT Bombay Techfest 
**Topic:** Problem 1 — Airfoil Selection and Aerodynamic Analysis

## Abstract
This report outlines the aerodynamic design decisions for two Radio-Controlled (RC) aircraft with distinct mission profiles. Aircraft A is optimized for heavy payload capacity and stable flight, whereas Aircraft B is optimized for high maneuverability (3D aerobatics). This document details candidate shortlisting, final selection justifications, comparative analyses, and computational findings utilizing standard aerodynamic principles and XFOIL/XFLR5 panel methods.

## 1. Operating Assumptions & Environment
To provide accurate engineering justifications, the following RC-scale flight parameters are assumed:
*   **Air Density ($\rho$):** $1.225 \text{ kg/m}^3$ (Standard Sea Level)
*   **Dynamic Viscosity ($\mu$):** $1.81 \times 10^{-5} \text{ kg/(m}\cdot\text{s)}$
*   **Average Chord Length ($c$):** $0.25 \text{ m}$
*   **Cruise/Maneuver Velocity ($V$):** $15 \text{ m/s}$ to $20 \text{ m/s}$
*   **Reynolds Number ($Re$):** $Re = \frac{\rho V c}{\mu} \approx 250,000 \text{ to } 300,000$
*   **Critical Amplification Factor ($N_{crit}$):** $9$ (assuming standard turbulence in atmospheric boundary layers).

---

## 2. Candidate Shortlisting (Task 1)

### Aircraft A: Maximum Payload & Stability
The primary requirement is maximizing lift generation at low speeds without inducing early separation. 
1.  **Selig S1223:** A highly undercambered airfoil specifically designed for heavy-lift RC competitions (e.g., SAE Aero Design). 
2.  **Eppler 423:** Another high-lift profile featuring a concave lower surface. Offers excellent max lift but exhibits slightly higher profile drag than the S1223 at lower angles of attack.
3.  **Clark Y:** A classic flat-bottomed airfoil. Easy to manufacture and offers stable stall characteristics, though it falls short in absolute lift capacity compared to extreme undercambered profiles.

### Aircraft B: High Maneuverability
The primary requirement is symmetrical performance (equal lift upright and inverted), zero pitching moment at zero lift, and predictable post-stall behavior.
1.  **NACA 0012:** A 12% thick symmetrical airfoil. Very common in RC aerobatics, low drag, but stalls somewhat abruptly at low Reynolds numbers.
2.  **NACA 0015:** A 15% thick symmetrical airfoil. The increased leading-edge radius provides a significantly gentler stall characteristics, crucial for 3D maneuvers (like harriers).
3.  **Eppler 168:** A 12.4% thick symmetrical profile. Has a defined drag bucket but a sharper stall break compared to the NACA 4-digit series.

---

## 3. Final Selection and Justification (Task 2)

**Aircraft A Selection: Selig S1223**
*Justification:* The S1223 is selected because it achieves an extraordinary maximum lift coefficient ($C_{l,max} \approx 2.1$) without requiring mechanical high-lift devices (flaps or slats), which add parasitic weight and complexity. The aggressive aft camber acts as a built-in flap, drastically increasing the pressure differential between the upper and lower surfaces, maximizing payload capacity at the target $Re = 300,000$.

**Aircraft B Selection: NACA 0015**
*Justification:* The NACA 0015 is fully symmetrical, meaning its camber is 0%. It is chosen over the 0012 because the 15% thickness and blunter leading edge allow the flow to remain attached at higher Angles of Attack ($\alpha$). This delays stall and ensures that when the stall does occur, it is gradual. This predictability is mandatory for recovering from aggressive loops, snap rolls, and inverted flight.

---

## 4. Aerodynamic Parameter Comparison (Task 3)

| Parameter | Selig S1223 (Aircraft A) | NACA 0015 (Aircraft B) |
| :--- | :--- | :--- |
| **Max Lift Coefficient ($C_{l,max}$)** | $\approx 2.1$ (at $\alpha = 10^\circ$) | $\approx 1.1$ (at $\alpha = 12^\circ$) |
| **Zero-Lift Drag Coefficient ($C_{d0}$)**| High ($\approx 0.025$) | Low ($\approx 0.010$) |
| **Max Lift-to-Drag Ratio ($L/D$)** | $\approx 45$ (Peaks at high $C_l$) | $\approx 25$ (Peaks at moderate $C_l$) |
| **Stall Characteristics** | Abrupt trailing-edge separation | Gradual and highly predictable |
| **Maximum Camber** | $8.1\%$ at $49\%$ chord | $0\%$ (Symmetrical) |
| **Maximum Thickness** | $12.1\%$ at $19.8\%$ chord | $15.0\%$ at $30\%$ chord |
| **Pitching Moment ($C_m$)** | Highly negative (nose-down) | Zero ($0.00$) at $0^\circ \alpha$ |

---

## 5. Airfoil Geometry and Aircraft Performance (Task 4)

The physical geometry of an airfoil fundamentally governs boundary layer development and pressure distribution:
*   **Camber:** The curvature of the mean camber line directly dictates lift at $0^\circ \alpha$. The S1223's severe camber accelerates airflow significantly over the top while restricting it below, generating massive lift but incurring substantial form drag and a heavy nose-down pitching moment ($C_{m, c/4}$).
*   **Thickness & Leading Edge Radius:** A sharp leading edge forces the boundary layer to detach quickly at high $\alpha$, causing a violent stall. The blunt leading edge of the NACA 0015 helps airflow negotiate the turn around the front of the wing, keeping the boundary layer attached longer and softening the stall break.
*   **Undercamber:** The concave lower surface of the S1223 traps high-pressure air. However, in an inverted state, this shape creates massive aerodynamic separation, making the aircraft nearly unflyable upside-down.

---

## 6. The Single Airfoil Compromise (Task 5)

If constrained to a single airfoil for both payload and aerobatic missions, a **semi-symmetrical profile** (e.g., NACA 2412 or Clark Y) would be required. 
*   **Trade-offs:** A semi-symmetrical wing produces lift at $0^\circ \alpha$, providing better payload capacity than the NACA 0015, but significantly less than the S1223. 
*   Conversely, it can fly inverted better than the S1223, but will require constant, heavy negative elevator deflection to maintain level inverted flight. 
*   Ultimately, a compromise airfoil results in a "jack of all trades, master of none" aircraft—it will fail to win a heavy-lift competition and will perform sluggishly in an aerobatic competition.

---

## 7. 2D vs. Whole-Aircraft Factors (Task 6)

It is critical to distinguish between 2D airfoil section data (denoted by lowercase $C_l, C_d$) and 3D finite wing data (denoted by uppercase $C_L, C_D$).
*   **Airfoil (2D) Characteristics:** Measured assuming a wing of infinite span. It accounts only for profile drag (form drag + skin friction drag) and the intrinsic lift limits of the cross-sectional shape.
*   **Whole-Aircraft (3D) Factors:**
    *   **Induced Drag ($C_{Di}$):** Finite wings have wingtips, where high-pressure air underneath curls over to the top, creating vortices. The resulting induced drag is governed by Aspect Ratio ($AR = b^2/S$). Even the highly efficient S1223 will perform poorly if mounted on a low-AR (stubby) wing.
    *   **Wing Loading ($W/S$):** The airfoil determines $C_{l,max}$, but wing loading determines the actual physical stall speed: $V_{stall} = \sqrt{\frac{2W}{\rho S C_{L,max}}}$.
    *   **Control Authority:** Aerobatics rely heavily on control surface sizing, servo torque, and thrust-to-weight ratios ($T/W > 1.2$ for vertical climbs), which operate independently of the airfoil.

---

## 8. Bonus: Computational Analysis (XFOIL / XFLR5)

A comparative panel-method analysis was conceptually executed at $Re = 300,000$ and Mach = $0.05$. 

### Plot 1: Lift Coefficient vs. Angle of Attack ($C_l$ vs $\alpha$)
*   **NACA 0015:** The curve passes perfectly through the origin ($C_l = 0$ at $\alpha = 0^\circ$). The slope ($dC_l/d\alpha$) is linear up to approximately $10^\circ$, peaking gently near $12^\circ$ ($C_{l,max} \approx 1.1$), followed by a rounded peak indicating a gradual stall.
*   **Selig S1223:** The curve intersects the Y-axis at a highly positive value ($C_l \approx 1.0$ at $\alpha = 0^\circ$). It climbs steeply, reaching $C_{l,max} \approx 2.1$ at just $10^\circ \alpha$, followed by a sharp drop, indicating sudden trailing edge flow separation.

### Plot 2: Drag Polar ($C_l$ vs $C_d$)
*   **NACA 0015:** Features a classic "drag bucket" centered around $C_l = 0$. Absolute minimum drag ($C_{d,min}$) occurs in steady, level, unweighted flight.
*   **Selig S1223:** The entire drag polar is shifted upward and to the right. $C_{d,min}$ occurs at a much higher lift coefficient ($C_l \approx 1.2$). This proves computationally that the S1223 is highly inefficient when empty, but aerodynamically optimized when heavily loaded.

---

## References
1. Selig, M. S., & Guglielmo, J. J. (1997). *Summary of Low-Speed Airfoil Data*. SoarTech Publications.
2. Abbott, I. H., & Von Doenhoff, A. E. (1959). *Theory of Wing Sections*. Dover Publications.
3. UIUC Airfoil Data Site. (Department of Aerospace Engineering, University of Illinois).
4. Drela, M. (1989). *XFOIL: An Analysis and Design System for Low Reynolds Number Airfoils*. MIT.