# Geometric Standardisation, Hydraulic Context and CAD/BIM Reconstruction of Concrete Antifer Cubes

**Ricardo Carvalho (2026)**

**Suggested citation**

> Carvalho, R. (2026). *Geometric Standardisation, Hydraulic Context and CAD/BIM Reconstruction of Concrete Antifer Cubes*.

---

## Abstract

Concrete Antifer cubes are massive grooved unreinforced concrete artificial armour units used in rubble-mound breakwaters and related maritime protection works. They were developed in connection with the Port of Antifer, in Normandy, after hydraulic investigations indicated that plain concrete cubes did not provide the required armour-layer stability for the intended exposure. The adopted unit retained the robustness of a compact concrete block, but introduced lateral grooves and moderate tapering to improve hydraulic behaviour, reduce smooth face-to-face rearrangement and preserve large resistant concrete sections.

This paper provides a technical synthesis of Antifer cubes from the viewpoints of historical development, hydraulic stability, placement effects, structural integrity, manufacture, quality control and reproducible geometric reconstruction. It also formalises the algebraic volume calculation used for the adopted Pita Antifer geometry and the volume-normalised Carvalho dimensional convention implemented in the associated production script. The script generates one closed vectorial Antifer armour-unit solid from input unit weight $W$ and concrete unit weight $W_c$, with exports to IFC, STL, OBJ and DXF from the same validated boundary-representation. It is a geometric CAD/BIM production and documentation tool, not a hydraulic stability design program.

The geometric core of the paper is intentionally concentrated in Section 5 to avoid mixing dimensional conventions, volume normalisation and hydraulic design assumptions. In that section, the Pita convention is defined as the historical dimensional reference with $K_V=V/H^3=1.0247$, while the Carvalho convention is defined as a volume-normalised reference with $K_V=1.$. Both use the same vectorial topology: a square frustum, four lateral plan chamfers and four single circular-arc grooves. The Carvalho convention applies a common horizontal normalisation factor to the Pita-derived plan and groove coefficients so that the reference height coincides with the volume-equivalent nominal diameter $D_n=H=V^{1/3}$.

The main engineering conclusion is that Antifer hydraulic performance is not governed by geometric coefficients alone. Armour-layer stability depends primarily on placement pattern, packing density, slope, wave climate, storm duration, damage criterion, toe and crest details and construction tolerances. Van der Meer-type concrete-unit stability formulae provide direct preliminary design relations for regular two-layer cubes and a consistent stability-number framework for Antifer sizing when Antifer-calibrated coefficients are used; Hudson-type coefficients should be interpreted as system-dependent comparative values, not intrinsic constants of the concrete shape.

**Keywords:** Antifer cube; concrete armour unit; rubble-mound breakwater; hydraulic stability; Hudson formula; Van der Meer stability number; Antifer stability formula; circular groove; Pita 1986; Carvalho 2026; CAD/BIM; IFC; STL; OBJ; DXF; volume coefficient; concrete armour geometry.

---

## Highlights

- Antifer cubes are best interpreted as **improved massive concrete cubes**, not as slender high-interlock units.
- The documented morphology comprises a slightly tapered concrete body with one circular-arc groove on each of the four lateral sides.
- The adopted Pita geometry has no top bevel: the upper face is a single horizontal plane at $z=H$.
- $B$ is the top bounding width at $z=H$, and $D$ is a lateral corner-chamfer offset in plan.
- The full geometric definition is consolidated in Section 5, where all Pita and Carvalho coefficients are given once in a single reference table.
- The volume coefficient is obtained algebraically as a square frustum minus four plan-corner chamfers minus four circular-groove segments.
- The square-frustum formula is demonstrated by integrating the linearly varying square cross-section through the height.
- Carvalho (2026) is a volume-normalised dimensional convention with $V/H^3=1.$; it is not a second historical drawing standard.
- Hydraulic performance is governed mainly by placement method, packing density, damage definition and wave climate.
- Van der Meer concrete-unit formulae and Antifer-calibrated stability-number relations are direct preliminary stability tools, subject to their empirical validity range.
- The production script is a geometric CAD/BIM generator for IFC, STL, OBJ and DXF; it does not perform complete hydraulic design.

---

## 1. Introduction

Artificial concrete armour units are used where natural armourstone cannot be obtained in the required size, quantity, durability or cost envelope. They are particularly relevant in exposed deep-water breakwaters, port entrances and emergency repair works where armourstone of adequate nominal diameter would be difficult to quarry, handle or transport.

Within this family of solutions, the Antifer cube occupies a specific technical position. It is more hydraulically refined than a plain cube, but more structurally robust and concrete-intensive than slender units that rely strongly on interlock. Its stability is derived from submerged weight, friction, limited mechanical engagement and the architecture of the armour layer.

The Antifer cube was developed in the early 1970s in connection with the Port of Antifer, Normandy, France. International manuals describe it as a development of the simple cube with one groove on each of the four lateral sides. The grooves improve hydraulic behaviour and reduce the tendency for smooth face-to-face packing. Frens reports that the prototype Antifer harbour breakwater was built between 1976 and 1978 and that simple cubic blocks did not provide sufficient stability in the hydraulic tests, leading to the adoption of grooved blocks.

The unit became technically attractive after the structural-integrity difficulties experienced by several slender concrete armour units in the late 1970s and early 1980s. The broader lesson from structures such as Sines, Arzew El Djedid and Crescent City was that hydraulic stability and structural integrity must be assessed together. A shape may be hydraulically efficient in model tests, but if prototype units fracture under rocking, impact, fatigue, handling loads or thermal cracking, the armour layer loses both mass and engagement. The Antifer cube responded to that risk profile by retaining a compact massive body and avoiding slender arms.

This paper addresses a recurring limitation in the public technical literature: the Antifer cube is widely recognised, but its geometry is not governed by one universally available public CAD standard. Manuals describe the unit and its general construction logic; project documents and academic studies provide dimensional ratios; however, exact digital reconstruction requires a fully explicit convention.

The objective of this paper is therefore twofold:

1. to summarise the engineering context of Antifer cubes as hydraulic and structural armour units; and
2. to give a complete, reproducible algebraic definition of the Pita Antifer geometry and the Carvalho volume-normalised dimensional convention used by the production CAD/BIM generator.

The intended readership is coastal, port and maritime engineers involved in armour-unit selection, physical modelling, rehabilitation design, construction quality control or geometric reconstruction of concrete armour units.

---

## 2. Sources, Evidence Classes and Method

This paper is a documentary synthesis and geometric standardisation study. It does not report new physical model tests, prototype monitoring or finite-element structural-integrity simulations.

The source base comprises historical design references, international manuals, laboratory studies, thesis work, peer-reviewed papers, project records and the associated geometry-generation implementation. The interpretation follows a conservative hierarchy of evidence.

| Evidence class | Meaning in this paper | Examples of use |
|---|---|---|
| Primary technical reference | Manual, standard, thesis, physical-model report or peer-reviewed paper with direct technical content | geometry, stability formulae, structural-integrity interpretation, manufacture and quality control |
| Project or prototype record | Named structure, quantities, construction record, official communication or prototype monitoring paper | adoption cases and project context |
| Derived geometric evidence | Vectorial reconstruction, algebraic volume balance, IFC/STL/OBJ/DXF exports and dimensional consistency checks | CAD/BIM reconstruction and geometric standardisation |
| Contextual evidence | Review literature or related armour-unit research that informs interpretation but does not define the geometry | broader discussion of concrete armour-unit evolution and structural robustness |

The paper separates three levels of analysis.

| Level | Scope | Main risk if confused |
|---|---|---|
| Hydraulic design level | armour-layer stability under wave action | treating $K_D$ as an intrinsic property of the block |
| Geometric reference level | published or historical dimensional coefficients | mixing incompatible definitions of $B$, $C$, $D$ or $R$ |
| CAD/BIM production level | IFC/STL/OBJ/DXF geometry generated from explicit coefficients | producing visually plausible but algebraically inconsistent geometry |

This separation is essential because a historical coefficient such as $V/H^3$ is meaningful only when the corresponding geometric construction is stated.

---

## 3. Nomenclature

| Symbol | Meaning | Typical unit |
|---|---|---:|
| $A$ | lower external width of the Antifer body at $z=0$ | m |
| $B$ | upper external width at $z=H$ in the adopted drawing convention | m |
| $C$ | groove inset / characteristic maximum groove depth | m |
| $D$ | lateral corner-chamfer offset in plan | m |
| $D_n$ | Van der Meer nominal diameter, $D_n=V^{1/3}$ | m |
| $H$ | total Antifer cube height or convention reference height | m |
| $H_D$ | design wave height used in Hudson-type sizing | m |
| $H_s$ | significant wave height | m |
| $H_{1/10}$ | mean of the highest one-tenth of wave heights | m |
| $K_D$ | Hudson stability coefficient | - |
| $K_V$ | non-dimensional volume coefficient, $V/H^3$ | - |
| $A_g$ | non-dimensional area of one circular groove segment | - |
| $R$ | absolute circular-groove radius | m |
| $r$ | non-dimensional groove radius, $r=R/H$ | - |
| $E$ | outside offset of the circular-arc centre from the side face | m |
| $e$ | non-dimensional outside centre offset, $e=E/H$ | - |
| $q$ | non-dimensional groove half-opening | - |
| $V$ | armour-unit volume | m$^3$ |
| $W$ | unit weight in force units | kN or N |
| $W_c$ | concrete unit weight in practical notation | kN/m$^3$ |
| $a$ | non-dimensional bottom width, $a=A/H$ | - |
| $b$ | non-dimensional top width, $b=B/H$ | - |
| $c$ | non-dimensional groove inset, $c=C/H$ | - |
| $d$ | non-dimensional chamfer offset, $d=D/H$ | - |
| $\theta$ | main lateral taper angle from vertical | degrees |
| $\tan^{-1}$ | inverse tangent function | - |
| $\rho_c$, $\rho_w$ | concrete and water mass density | kg/m$^3$ |
| $\rho_\nabla$ | relative density, $\rho_c/\rho_w$ | - |
| $\rho'_\nabla$ | relative submerged density, $\rho_\nabla-1$ | - |
| $\rho_\nabla$ or $\rho'_\nabla$ notation | notation varies by reference; definitions must be checked | - |
| $\nu$ | kinematic viscosity where used in hydraulic formulae | m$^2$/s |
| $\beta$ | wave angle of attack | degrees |
| $\beta_m$ | maximum allowable wave angle in some formulae | degrees |
| $\tau$ | storm duration parameter where used | s or dimensionless |
| $N$ or $N_z$ | number of waves in stability formulae | - |
| $N_{od}$ | damage number / number of displaced units per equivalent width | - |
| $s_{0m}$ | deep-water wave steepness based on mean wave period | - |
| $\tan\theta_\beta$ | armour slope factor corrected for wave attack in some relations | - |
| $\tan\theta_h$ | hydraulic slope term in some stability relations | - |
| $\tan\theta_s$ | structure slope term in some stability relations | - |
| $\tan\theta$ | tangent of armour slope angle | - |
| $\theta_h$, $\theta_s$ | slope angles used in some stability formulae | degrees |
| $\theta_b$ | bottom/main lateral angle of the Antifer side | degrees |
| $\beta$ | wave obliquity where used in stability formulae | degrees |
| $\rho'_\nabla$ | relative submerged density where used in cited Antifer relations | - |

---

## 4. Historical and Technical Development of the Antifer Cube

### 4.1 From simple cube to grooved cube

The plain concrete cube is the simplest substitute for natural armourstone. Its stability arises mainly from submerged weight and friction. It is easy to fabricate, easy to handle and structurally robust, but it is vulnerable to hydraulic inefficiencies associated with regularisation, low roughness, reduced permeability and smooth face-to-face arrangements.

The Antifer cube modifies the simple cube by adding one groove on each of the four lateral faces. The resulting unit remains massive, but the lateral recesses:

- interrupt broad flat contact planes;
- reduce the probability of smooth face-to-face packing;
- increase roughness and local turbulence at the armour surface;
- improve mechanical engagement between adjacent units;
- preserve thick concrete webs and large resistant sections.

The lack of one universally enforced public geometry is central to the present paper. Digital reconstruction must therefore state the coefficient family, the meaning of each symbol and the exact geometric construction used to generate the drawing or solid.

### 4.2 Position within the evolution of concrete armour units

Concrete armour units may be interpreted through four broad families.

| Family | Typical examples | Dominant stabilising mechanism | Structural implication |
|---|---|---|---|
| Massive or blocky units | cube, Antifer cube, modified cube | own weight, friction and limited interlock | low slenderness, high robustness, high concrete consumption |
| Double-layer interlocking units | Tetrapod, Dolos, Akmon | own weight plus interlock | higher hydraulic efficiency but greater sensitivity to breakage |
| Single-layer interlocking units | Accropode, Core-Loc, Xbloc | high interlock in one layer | efficient, but dependent on strict placement and no-damage design |
| Regular pattern or hollow units | Seabee, Haro, Cob, Shed, Diode | frictional restraint and/or high porosity | high performance when placement tolerances are achieved |

The Antifer cube belongs to the massive/blocky family, but with enhanced surface geometry. It should therefore not be reduced to a plain cube in digital representation. Conversely, it should not be treated as a slender high-interlock unit; its structural value lies in avoiding slender arms and high tensile-stress concentrations.

### 4.3 Structural-integrity context after major breakwater failures

The period after the Sines, Arzew El Djedid and Crescent City failures created a paradigm shift in concrete armour-unit design. These failures highlighted the risk of relying on hydraulic model stability while underestimating prototype structural behaviour. Unit selection cannot be based on hydraulic stability alone. A stable armour layer requires:

- adequate hydraulic resistance to displacement;
- acceptable rocking and impact levels;
- sufficient tensile strength and fatigue resistance;
- adequate thermal control during curing;
- correct placement and packing;
- tolerance-compatible underlayer and toe construction;
- post-storm inspection where movement is expected.

This is why Antifer cubes remain relevant even when more concrete-efficient alternatives exist. Their robust geometry may be preferable where wave-climate uncertainty, construction-tolerance limitations, emergency repairs, foundation deformation or structural-integrity concerns dominate the design problem.

---

## 5. Geometric Definition and Algebraic Volume

This section is the single reference location for the Pita and Carvalho dimensional conventions used in the production implementation. Later sections refer back to this section rather than repeating the same coefficient tables.

### 5.1 Adopted coefficient table

The Pita convention preserves the historical dimensional reference. The Carvalho convention uses the same vectorial topology and circular-arc groove construction, but it is horizontally normalised so that $V/H^3=1.$.

| Quantity | Pita convention | Carvalho convention | Meaning |
|---|---:|---:|---|
| $K_V=V/H^3$ | 1.02470 | 1. | non-dimensional volume coefficient |
| $f$ | 1. | 0.987874174182 | common plan/groove normalisation factor |
| $a=A/H$ | 1.086 | 1.072831353161 | bottom bounding width at $z=0$ |
| $b=B/H$ | 1.005 | 0.992813545052 | top bounding width at $z=H$ |
| $d=D/H$ | 0.024 | 0.023708980180 | lateral corner-chamfer offset in plan |
| $r=R/H$ | 0.1215 | 0.120026712163 | circular-groove radius |
| $e=E/H$ | 0.02590645961 | 0.025592322393 | outside centre offset of groove circle |
| $c=C/H=r-e$ | 0.09559354039 | 0.09443438977 | exact circular-arc groove inset |
| historical $C/H$ notation | 0.0956 | not applicable | rounded historical Pita notation |
| $q/H$ | 0.118705961731 | 0.117266553915 | groove half-opening |
| $2q/H$ | 0.237411923462 | 0.234533107831 | full groove opening |

### 5.2 Shared geometric interpretation

Both conventions use the following geometric interpretation.

| Geometric item | Adopted production interpretation |
|---|---|
| Top face | single horizontal plane at $z=H$ |
| Top bevel | none |
| $B$ | top bounding width measured at $z=H$ |
| $D$ | lateral plan-chamfer offset at the four corners |
| Side grooves | four identical single circular arcs |
| Groove radius | absolute radius $R=rH$ |
| Groove centre | outside the corresponding side face by $E=eH$ |
| Auxiliary straight inner groove segment | none |
| Horizontal sections | two homologous square sections: lower width $A$ at $z=0$ and upper width $B$ at $z=H$ |

The word "homologous" is important. The lower and upper plan shapes have the same topology and are connected through the height by straight ruled faces before groove and chamfer subtractions are introduced.

### 5.3 Demonstration of the square-frustum volume formula

Let a square frustum have height $H$, lower width $A$ and upper width $B$. At a vertical coordinate $z$, measured from the bottom, the linearly interpolated side length is:


$$
s(z)=A+\frac{B-A}{H}z.
$$


The horizontal area at level $z$ is:


$$
S(z)=s(z)^2.
$$


The frustum volume is therefore:


$$
V_{\mathrm{frustum}}
=
\int_0^H
\left(A+\frac{B-A}{H}z\right)^2
\,dz.
$$


Expanding and integrating:


$$
V_{\mathrm{frustum}}
=
\int_0^H
\left[
A^2
+
2A\frac{B-A}{H}z
+
\left(\frac{B-A}{H}\right)^2z^2
\right]dz,
$$



$$
V_{\mathrm{frustum}}
=
A^2H
+
A(B-A)H
+
\frac{(B-A)^2}{3}H.
$$


Collecting terms gives:


$$
V_{\mathrm{frustum}}
=
\frac{H}{3}
\left(A^2+AB+B^2\right).
$$


Using $a=A/H$ and $b=B/H$:


$$
\frac{V_{\mathrm{frustum}}}{H^3}
=
\frac{a^2+ab+b^2}{3}.
$$


This is the gross body used before subtracting the four lateral corner chamfers and the four circular side grooves.

### 5.4 Complete non-dimensional volume model

After the gross square frustum is defined, the adopted Antifer geometry subtracts four plan-corner chamfers and four lateral circular-groove segments.

| Component | Non-dimensional expression | Role in volume balance |
|---|---:|---|
| Gross square frustum | $K_{\mathrm{frustum}}=(a^2+ab+b^2)/3$ | starting body between widths $A=aH$ and $B=bH$ |
| Four corner chamfers | $K_{\mathrm{corners}}=2d^2$ | plan-corner volume removed through the height |
| One circular groove | $A_g=r^2\cos^{-1}(e/r)-e\sqrt{r^2-e^2}$ | area removed by one lateral groove in $H^2$ units |
| Four circular grooves | $K_{\mathrm{grooves}}=4A_g$ | total groove-volume subtraction |
| Final coefficient | $K_V=K_{\mathrm{frustum}}-K_{\mathrm{corners}}-K_{\mathrm{grooves}}$ | resulting $V/H^3$ |

The groove half-opening and inset are derived from the circular arc:

\[
q=\sqrt{r^2-e^2},
\qquad
c=r-e.
\]

The Pita balance is closed by imposing $K_V=1.02470$ and solving the circular-arc centre offset $e$ for the corresponding one-groove area. The Carvalho balance is then obtained by the common horizontal factor described in Section 5.6.

### 5.5 Numerical volume balances

The following table gives the complete volume balance without repeating the full coefficient table.

| Convention | Gross frustum | Chamfer subtraction | Groove subtraction | Final $V/H^3$ |
|---|---:|---:|---:|---:|
| Pita | 1.093617 | 0.001152 | 0.067765 | 1.0247 |
| Carvalho | 1.067255782180 | 0.001124231482 | 0.066131550698 | 1. |

For the Pita convention, the one-groove area required by the balance is:

\[
A_g=\frac{1.093617-0.001152-1.0247}{4}
=0.01694125.
\]

Solving

\[
A_g=r^2\cos^{-1}(e/r)-e\sqrt{r^2-e^2}
\]

with the Pita radius from the coefficient table gives the exact circular-arc centre offset and consequently the exact groove inset and groove opening reported in Section 5.1.

### 5.6 Carvalho volume normalisation

The Carvalho convention is obtained by applying a common horizontal normalisation factor to the Pita plan and groove coefficients:

\[
f=\sqrt{\frac{K_{V,C}}{K_{V,P}}}
=\sqrt{\frac{1.}{1.0247}}
=0.987874174182.
\]

The reason for the square root is that the vertical reference height is kept as $H$, while the horizontal dimensions that control plan areas are multiplied by $f$. Consequently, all area-type contributions to $V/H^3$ scale with $f^2$.

Thus:

\[
K_{V,C}=f^2K_{V,P}=1..
\]

This convention preserves the Pita construction logic and topology, but not the numerical values of the Pita ratios. It should therefore be treated as a volume-normalised reference system, not as an alternative historical drawing.

### 5.7 Dimensional scaling and nominal diameter

For an input unit weight $W$ and concrete unit weight $W_c$:

\[
V=\frac{W}{W_c}.
\]

The reference height for any convention is:

\[
H=\left(\frac{V}{K_V}\right)^{1/3}.
\]

All remaining dimensions are obtained by multiplying $H$ by the corresponding coefficient in Section 5.1.

The Van der Meer nominal diameter is:

\[
D_n=V^{1/3}.
\]

Therefore:

| Convention | Volume relation | Nominal diameter relation | Interpretation |
|---|---:|---:|---|
| Pita | $V=1.0247H^3$ | $D_n=1.008166460709H$ | historical drawing height is slightly smaller than $D_n$ |
| Carvalho | $V=H^3$ | $D_n=H$ | reference height equals the volume-equivalent nominal diameter |

With no top bevel, the main lateral taper is controlled by $A$ and $B$ over the full height:

\[
\theta=\tan^{-1}\left(\frac{a-b}{2}\right),
\qquad
\theta_b=90^\circ-\theta.
\]

Using the coefficients in Section 5.1 gives a main lateral angle from vertical of approximately $2.32^\circ$ for the Pita convention and $2.29^\circ$ for the Carvalho convention.

---

## 6. Hydraulic Stability Framework

### 6.1 Hudson-type sizing

The Hudson formula remains a common preliminary sizing tool for concrete armour units:

\[
W=
\frac{\gamma_c H_D^3}{K_D\Delta^3\cot\alpha},
\]

where:

\[
\Delta=\frac{\gamma_c}{\gamma_w}-1.
\]

For concrete armour units, the formula must be used cautiously. Hudson-type sizing is valuable for preliminary comparisons, but final design depends on physical model testing, placement method, construction tolerance and acceptable damage.

A $K_D$ value compresses many physical mechanisms into one empirical coefficient:

- unit shape;
- placement method;
- packing density;
- armour-layer porosity;
- slope;
- wave breaking and wave spectrum;
- storm duration;
- damage definition;
- underlayer and core permeability;
- wave obliquity;
- allowable rocking or displacement;
- prototype structural strength.

A $K_D$ value without these associated conditions is not a complete design parameter.

### 6.2 Stability number

For comparison across density and volume, the stability number is often preferable:

\[
N_s=\frac{H_s}{\Delta D_n},
\qquad
D_n=V^{1/3}.
\]

The distinction between drawing height and nominal diameter matters when transferring hydraulic sizing to CAD/BIM geometry. Section 5.7 gives the relation between $D_n$ and $H$ for the two conventions used here.

### 6.3 Van der Meer and Antifer stability formulae

Van der Meer should not be treated only as conceptual background for Antifer design. In this paper, the hydraulic framework is interpreted in three complementary levels: Hudson-type coefficients for preliminary comparison, Van der Meer stability-number formulae for two-layer regular concrete cubes, and Antifer-specific stability-number formulae using the same empirical design structure with Antifer-calibrated coefficients.

| Formula family | Typical use | Governing quantity | Interpretation for Antifer work |
|---|---|---|---|
| Hudson | preliminary sizing and comparison | $K_D$ | useful as an equivalent stability index, but strongly dependent on placement and damage definition |
| Van der Meer regular-cube formula | direct preliminary design of two-layer regular cubes | $N_s=H_s/(\Delta D_n)$ | relevant reference because Antifer belongs to the massive cube-derived family |
| Antifer-calibrated stability-number formulae | direct preliminary sizing of Antifer blocks where the coefficient set is applicable | $N_s=H_s/(\Delta D_n)$ | preferred formula-based route when Antifer-specific coefficients are available |
| Physical modelling | final verification for important works | measured damage, rocking, displacement and overtopping | required when exposure, layout or placement differs materially from the tested basis |

For double-layer regular cubes, the Van der Meer concrete-unit relation may be written as:

\[
\frac{H_s}{\Delta D_n}
=
\left(
6.7\frac{N_{od}^{0.4}}{N^{0.3}}+1.0
\right)s_{om}^{-0.1}.
\]

The same stability-number form is also convenient for software implementation and comparison:

\[
N_s
=
\left(
k_1\frac{N_{od}^{k_2}}{N_z^{k_3}}+k_4
\right)s_{0m}^{-k_5}.
\]

In this form, the coefficients define the armour-unit family and the tested slope condition.

| Armour unit and slope | $k_1$ | $k_2$ | $k_3$ | $k_4$ | $k_5$ | Comment |
|---|---:|---:|---:|---:|---:|---|
| Regular cube, $\cot\alpha=1.5$ | 6.7 | 0.400 | 0.300 | 1. | 0.100 | Van der Meer two-layer regular-cube relation |
| Regular cube, $\cot\alpha=2.0$ | 7.374304 | 0.400 | 0.300 | 1.100642 | 0.100 | slope-adjusted regular-cube coefficient form |
| Antifer, $\cot\alpha=1.5$ | 6.951 | 0.443 | 0.291 | 1.082 | 0.082 | Antifer-calibrated coefficient set |
| Antifer, $\cot\alpha=2.0$ | 6.138 | 0.443 | 0.276 | 1.164 | 0.070 | Antifer-calibrated coefficient set |

The corresponding computational chain is:

| Step | Expression | Meaning |
|---|---:|---|
| 1 | $s_{0m}=2\pi H_s/(gT_m^2)$ | deep-water wave steepness based on mean period |
| 2 | $\Delta=W_c/W_w-1$ | relative submerged density expressed with specific weights |
| 3 | $N_s=\left(k_1N_{od}^{k_2}/N_z^{k_3}+k_4\right)s_{0m}^{-k_5}$ | empirical stability number for the selected unit and slope |
| 4 | $D_n=H_s/(\Delta N_s)$ | nominal armour-unit dimension |
| 5 | $V=D_n^3$ | armour-unit volume by nominal diameter |
| 6 | $W=W_cD_n^3$ | required concrete-unit weight |

Formula-based Antifer sizing remains empirical. The selected coefficient set is valid only within the intended range of slope, placement, damage level, wave steepness and storm length. For important or atypical works, physical modelling remains the governing verification step.

---

## 7. Placement Method, Packing Density and Damage

### 7.1 Why placement dominates Antifer behaviour

Antifer cubes are not independent hydraulic objects once placed in an armour layer. Their behaviour depends on the architecture of the layer. The same concrete unit may perform differently when placed:

- regularly in a square or pyramid-like pattern;
- irregularly with greater porosity and roughness;
- in a dense arrangement with reduced voids;
- in a low-density arrangement with higher roughness but reduced support;
- on a smooth or irregular underlayer;
- near the still-water level, where first displacements often initiate;
- on trunk, head, transition or roundhead sections.

The engineering variable is therefore not the Antifer cube alone, but the **Antifer armour system**.

### 7.2 Evidence from irregular placement studies

Irregular placement studies show that Antifer stability depends strongly on damage definition. Conservative definitions including rocking and turning tend to produce lower $K_D$ values than definitions based only on rolling or extraction. This is important because rocking may precede fatigue, concrete damage or progressive instability.

Representative conclusions from the published irregular-placement evidence include:

- significant wave height is often a better stability descriptor than maximum wave height alone;
- average porosity around 0.47 has been reported for modified irregular placement;
- damage may increase approximately parabolically with significant wave height;
- conservative low-damage criteria can lead to $K_D$ values of approximately 2.7 to 3.5;
- $K_D\cot\alpha$ may give a more physically consistent slope ranking than $K_D$ alone.

### 7.3 Evidence from placement-pattern studies

Placement-pattern studies show that regular or semi-regular arrangements can greatly increase apparent stability. However, high packing density and high regularity may also increase reflection and overtopping. The practical issue is not simply to maximise $K_D$, but to find a robust compromise between stability, overtopping, reflection, construction accuracy and failure mode.

Reported Antifer coefficients across different placement methods may range from values near 4 to values above 20. This range should not be interpreted as uncertainty in the concrete geometry. It is evidence that placement architecture controls the response.

### 7.4 Regular versus irregular placement

| Placement tendency | Main advantage | Main disadvantage |
|---|---|---|
| regular / accurately controlled | higher displacement stability | potentially higher reflection and overtopping |
| irregular / rougher layer | reduced overtopping and greater roughness | lower displacement stability |
| denser placement | greater contact restraint | lower porosity and potentially higher reflection |
| lower-density placement | greater porosity and roughness | greater risk of movement |

For roundheads and other three-dimensional exposure zones, stability usually dominates and irregular placement may be inappropriate unless supported by specific physical-model evidence.

### 7.5 Consolidated stability interpretation

| Source type | Main result | Use in design |
|---|---|---|
| historical Pita-type guidance | Antifer $K_D$ values depend on slope and admissible damage | useful historical reference |
| British and international preliminary guidance | Antifer values generally treated cautiously for preliminary sizing | not a substitute for model testing |
| irregular-placement experiments | low-damage $K_D$ values can be conservative | relevant for damage-sensitive projects |
| Frens-type placement studies | $K_D$ strongly depends on placement and packing | demonstrates placement dominance |
| regular/irregular comparative tests | regular placement improves stability; irregular placement can reduce overtopping | shows the functional trade-off |

The defensible conclusion is that Antifer stability is not governed by a single coefficient. Any final design should be tested with the intended placement method, underlayer geometry, toe detail, crest arrangement, wave spectrum, water levels and damage criteria.

---

## 8. Structural Integrity and Failure Mechanisms

### 8.1 Why massive geometry matters

Unreinforced concrete has relatively low tensile strength compared with compressive strength. Breakage of concrete armour units is usually governed by tensile stress, fatigue, impact and cracking rather than compressive crushing. The Antifer cube reduces structural-integrity risk by avoiding slender arms. Its main resistant sections remain large, and its grooves do not create the same lever-arm vulnerability as Dolos or Tetrapod members.

Nevertheless, Antifer units are not immune to damage. They may still suffer:

- thermal cracking during curing of massive concrete;
- handling and lifting damage;
- impact damage during placement;
- abrasion and corner wear under wave action;
- rocking-induced fatigue;
- fracture caused by poor concrete quality;
- damage due to settlement or jamming in the armour layer.

### 8.2 Hydraulic failure versus structural failure

A design may fail by several mechanisms.

| Mechanism | Description | Antifer relevance |
|---|---|---|
| Hydraulic displacement | unit moves out of its stable position | controlled by $K_D$, $N_s$, placement, slope and wave climate |
| Rocking | repeated angular movement without complete extraction | may precede fatigue or impact damage |
| Progressive extraction | displacement of outer units exposes lower layer or underlayer | depends on layer architecture and toe/crest confinement |
| Underlayer erosion | armour openings allow filter or core material loss | critical if both layers are disturbed |
| Structural breakage | unit fractures and loses mass or engagement | lower risk than slender units but not negligible |
| Overtopping-induced rear damage | crest/rear armour affected by transmitted water | depends on crest level, roughness and porosity |
| Roundhead instability | 3D exposure and oblique attack increase movements | generally requires conservative detailing |

A complete Antifer assessment therefore requires both hydraulic and structural criteria.

### 8.3 Unit size and structural caution

Large Antifer blocks should be accompanied by:

- thermal control in mix design and curing;
- tensile-strength specification, not compressive strength alone;
- documented lifting and turning procedures;
- inspection for deep cracks;
- unit identification and traceability;
- mass and density control;
- post-placement survey and post-storm inspection.

---

## 9. Manufacture, Materials and Quality Control

### 9.1 Concrete and formwork

Antifer cubes are normally manufactured as unreinforced concrete units. Practical requirements include:

- formwork dimensions consistent with the volume specification;
- adequate stripping angles;
- no cold joints;
- layer-by-layer vibration during casting;
- immediate curing after stripping;
- thermal protection where required;
- avoidance of honeycombing and deep cracking;
- unique identification of each unit from stripping to placement.

### 9.2 Volume and mass control

For an armour unit whose stability is strongly mass-dependent, quality control must verify:

\[
M=\rho_cV
\]

or in weight notation:

\[
W=W_cV.
\]

A dimensional error becomes a stability error. A density error becomes a stability error. A drawing or CAD volume error becomes a procurement and construction-control error when digital models are used for quantities.

The direct practical relation is:

\[
H=\left(\frac{W/W_c}{K_V}\right)^{1/3},
\]

where $K_V$ is taken from the selected convention in Section 5.1.

### 9.3 Rejection and defect logic

Defects should be evaluated by structural significance, not appearance alone.

| Defect type | Typical interpretation | Recommended logic |
|---|---|---|
| Surface bubbles or minor bleeding | often cosmetic but may indicate poor production practice | record and improve production control |
| Honeycombing or mass voids | may reduce mass and local strength | evaluate, reject if significant |
| Shallow hairline cracking | may be tolerable depending on depth and location | inspect and monitor |
| Deep cracking | potential fracture plane under impact/fatigue | reject or restrict to low-exposure use if allowed |
| Corner loss | affects mass and contact behaviour | quantify mass loss and location |
| Cold joint | unacceptable in unreinforced massive units | reject |

---

## 10. CAD/BIM Reconstruction and Digital Metrology

### 10.1 Requirements for scientific digital reconstruction

A technical reconstruction of an Antifer cube should satisfy the following conditions:

1. all dimensions are derived from named coefficients;
2. the meaning of $A$, $B$, $C$, $D$, $R$ and $E$ is explicit;
3. the top and bottom sections are generated from the same vectorial construction;
4. the lateral grooves are generated from the stated circular-arc equation;
5. the volume coefficient is derived from the same coefficients used in the geometry;
6. no hidden template geometry is inserted;
7. all export formats are generated from the same validated boundary-representation;
8. all non-dimensional values are reported with sufficient precision for verification.

### 10.2 Active production script

The associated production script is a Tkinter-based **Vectorial Antifer IFC + STL + OBJ + DXF Generator**. It generates one closed Antifer armour-unit solid from input unit weight $W$ and concrete unit weight $W_c$.

| Item | Script behaviour |
|---|---|
| Script type | Tkinter graphical production application |
| Geometry source | pure vectorial generation; no embedded CAD, SAT, ACIS, IFC, DXF or mesh template |
| Selectable conventions | Pita and Carvalho, as defined in Section 5 |
| Input parameters | unit weight $W$ [kN] and concrete unit weight $W_c$ [kN/m$^3$] |
| Volume formula | $V=W/W_c$ |
| Height formula | $H=(V/K_V)^{1/3}$ |
| Top convention | $B$ is the top width at construction level $z=H$ |
| Top bevel | none |
| Corner chamfers | lateral plan chamfers |
| Groove profile | one circular arc per side, with radius $R$ and centre offset $E$ |
| Groove sampling | `GROOVE_ARC_POINTS = 144` |
| IFC output | IFC4 `IfcFacetedBrep` with property and quantity data |
| STL output | closed triangular mesh in metres |
| OBJ output | indexed triangular mesh in metres |
| DXF output | AutoCAD 2018 / AC1032 ACIS-backed `3DSOLID` |
| Text output | `output.txt` calculation and validation report |

The two conventions use the same vectorial topology, the same two homologous horizontal sections, the same four lateral plan chamfers and the same single circular-arc groove construction. The distinction is the dimensional reference system used for $H$ and for the corresponding non-dimensional coefficients.

### 10.3 Verification workflow

A scientifically auditable workflow should check at least:

| Check | Required result |
|---|---|
| dimensional inputs | the selected convention coefficients match Section 5.1 |
| no top bevel | the top face is at $z=H$ and uses $B$ as the top width |
| corner chamfers | four lateral plan chamfers with coefficient $D/H$ |
| groove construction | one circular arc per side, radius $R$ and centre offset $E$ |
| closed shell | every B-rep edge is shared by exactly two faces |
| volume relation | geometric and B-rep volumes match the selected convention |
| centroid convention | exported $X=0$ and $Y=0$ pass through the homogeneous centre of mass |
| bottom datum | exported $Z=0$ remains the physical bottom level |
| IFC output | exact cap loops are written as IFC4 `IfcFacetedBrep` faces |
| STL/OBJ output | triangular meshes are closed and volume-consistent |
| DXF output | ACIS-backed `3DSOLID` is suitable for CAD inspection and mass-property checks |
| report output | `output.txt` records the same calculation and validation values shown in the GUI |

This workflow prevents the most common digital error: producing a visually plausible Antifer geometry whose volume coefficient is not traceable to the same dimensional definitions.

---

## 11. Applications and Example Uses

Antifer cubes have been used or studied in several breakwater and maritime-protection contexts. The following examples are included as engineering context, not as direct design precedents. For any new project, the relevant parameters remain the local wave climate, water levels, slope, toe, crest, underlayer, placement pattern, unit mass, concrete density and allowable damage.

| Country / region | Works / context | Role of Antifer units |
|---|---|---|
| France | Port of Antifer | development context and prototype application of the grooved cube concept |
| Portugal | Sines West Breakwater | repair and rehabilitation context under severe Atlantic exposure |
| Portugal | Leixões outer breakwater extension | modern rubble-mound protection using Antifer concrete blocks |
| Portugal | Douro Bar / Cabedelo do Douro | Antifer cube monitoring, tracking and stability assessment |
| Portugal / Azores | Lajes das Flores | exposed Atlantic island port protection and reconstruction context |
| Belgium | Zeebrugge rubble-mound breakwater | prototype-scale overtopping and run-up context on grooved cube armour |
| Morocco | Mohammedia | historical exposed-breakwater application context |
| Brunei | breakwater manufacturing / placement context | production, curing and placement references for large concrete armour units |

The examples show the range of uses for massive grooved concrete cubes. They do not define a universal stability coefficient. The governing design value must be selected for the intended armour system and verified against the project-specific hydraulic and construction conditions.

---

## 12. Design Implications

### 12.1 Geometry is not the controlling hydraulic uncertainty

The algebraic geometry is important for technical drawings, digital consistency and correct volume interpretation. It should not, however, be interpreted as a substitute for hydraulic stability verification.

The dominant uncertainties are:

- placement method;
- packing density;
- armour slope;
- toe stability;
- underlayer permeability;
- wave climate;
- water levels;
- storm duration;
- accepted damage;
- overtopping and crest response;
- construction tolerances.

Changing or refining a geometric drawing coefficient does not justify adopting a higher $K_D$. The hydraulic coefficient must come from literature values applicable to the same placement system or from project-specific physical modelling.

### 12.2 Antifer selection is a system decision

Antifer cubes may be technically attractive when:

- quarry rock is unavailable in sufficient size or quality;
- structural robustness is more important than minimum concrete volume;
- construction conditions make strict single-layer interlocking placement difficult;
- uncertainty exists in wave climate, foundation behaviour or post-storm access;
- repair works require a conservative and familiar unit;
- high-density concrete is being considered for massive block-type units;
- the client values simple fabrication, traceability and inspection.

They may be less attractive when:

- concrete volume minimisation is the dominant criterion;
- very low overtopping is required without increasing crest height;
- the project can reliably implement strict monolayer placement;
- environmental or carbon constraints penalise high concrete consumption;
- hydraulic model testing shows unacceptable reflection or overtopping for the required layout.

### 12.3 Placement recommendations from the evidence

| Design objective | More favourable tendency | Technical caveat |
|---|---|---|
| maximise displacement stability on trunk | regular or accurately controlled placement | may increase reflection and overtopping |
| reduce overtopping | irregular or more porous/rough layer | may reduce displacement resistance |
| protect roundheads | regular / high-stability arrangement | irregular placement generally not recommended where stability is critical |
| reduce unit breakage risk | robust massive units and marginal-displacement design | thermal and handling damage still require control |
| reduce construction cost | depends on unit size, placement rate and concrete volume | high-stability arrangements may require high placement accuracy |
| improve drawing quantity control | algebraically consistent volume coefficient | does not replace hydraulic validation |

---

## 13. Limitations

The limitations of this paper are explicit:

- no new hydraulic model tests were performed;
- no new prototype monitoring was performed;
- no finite-element structural-integrity model was produced;
- the production script is a geometric CAD/BIM generator; it is not a complete hydraulic design tool;
- the adoption table is not an exhaustive global catalogue;
- project-specific design still requires wave climate, water levels, toe, underlayer, crest, overtopping, transmission, construction sequence, geotechnics and damage criteria;
- critical works should be verified by physical modelling or equivalent project-specific evidence.

---

## 14. Conclusions

The geometric conclusions are summarised separately from the design conclusions because the two topics are often confused.

| Topic | Conclusion |
|---|---|
| Unit type | Antifer cubes are massive grooved unreinforced concrete armour units developed in France in connection with the Port of Antifer. |
| Engineering role | The unit is best described as an improved massive cube: the grooves improve hydraulic interaction and reduce face-to-face rearrangement, while the thick body preserves structural robustness. |
| Structural classification | The Antifer cube should not be classified as a slender high-interlock unit; its advantage is conservative robustness, not minimum concrete consumption. |
| Geometric convention | The production geometry has no top bevel; $B$ is the top bounding width at $z=H$, and $D$ is a lateral plan-chamfer offset. |
| Groove convention | Each lateral groove is one circular arc of radius $R$, with centre offset $E$ and no auxiliary straight inner segment. |
| Volume balance | The unit volume is obtained as a square frustum minus four corner chamfers minus four circular-groove segments. |
| Pita convention | Pita preserves the historical dimensional reference with $K_V=1.02470$. |
| Carvalho convention | Carvalho applies a common horizontal factor so that $K_V=1.$ and $H=D_n$. |
| Stability coefficient | Reported Antifer $K_D$ values vary widely because $K_D$ is controlled by placement pattern, packing density, wave conditions, slope and damage definition. |
| Van der Meer framework | Van der Meer concrete-unit formulae and Antifer-calibrated stability-number relations are direct preliminary stability tools within their empirical validity range. |
| Project verification | Final design must be verified against the actual armour-layer arrangement, wave climate, allowable damage and construction tolerances. |

A defensible Antifer workflow must distinguish historical dimensional references, volume-normalised dimensional references, generated digital geometry and hydraulic design assumptions.

---

## 15. Data and Code Availability

The digital implementation associated with this paper is the **Vectorial Antifer IFC + STL + OBJ + DXF Generator** by Ricardo Carvalho (2026).

| Output | Description |
|---|---|
| IFC | IFC4 `IfcFacetedBrep` model with property and quantity data |
| STL | closed triangular surface mesh in metres |
| OBJ | indexed triangular surface mesh in metres |
| DXF | AutoCAD 2018 / AC1032 file with an ACIS-backed `3DSOLID` |
| TXT | `output.txt` calculation and validation report |

The selectable dimensional conventions are defined in Section 5.1 and are not repeated here. The implementation principles are:

| Implementation principle | Adopted value or behaviour |
|---|---|
| Geometry source | pure vectorial B-rep generation |
| Embedded templates | none |
| Top face | single horizontal plane at $z=H$ |
| Lateral grooves | single circular arc per side |
| Shared export source | same validated geometric source for IFC, STL, OBJ and DXF |
| Pita reference | historical dimensional coefficient set with $V/H^3=1.0247$ |
| Carvalho reference | volume-normalised coefficient set with $V/H^3=1.$ |
| Carvalho normalisation | horizontal plan/groove factor $f=0.987874174182$ |

---

## 16. Acknowledgement and Dedication

This work is respectfully dedicated to the memory of **Carlos Alberto Roldão Maia Pita** (1950-2002), Portuguese civil engineer and specialist in maritime hydraulics and rubble-mound breakwater design. His LNEC *Memória n.º 670 — Dimensionamento Hidráulico do Manto Resistente de Quebra-Mares de Talude* remains an important technical reference for Portuguese maritime engineering and provides a key historical basis for the geometric interpretation of Antifer cubes.

---

## 17. References

1. Pita, C. A. R. M. *Dimensionamento Hidráulico do Manto Resistente de Quebra-Mares de Talude*. Laboratório Nacional de Engenharia Civil, Memória n.º 670, Lisboa, 1986.
2. BSI. *BS 6349-7:1991 Maritime structures — Part 7: Guide to the design and construction of breakwaters*, with 2010 corrigenda.
3. CIRIA; CUR; CETMEF. *The Rock Manual: The use of rock in hydraulic engineering*, 2nd ed., 2007.
4. U.S. Army Corps of Engineers. *Coastal Engineering Manual*. Engineer Manual EM 1110-2-1100, U.S. Army Corps of Engineers, Washington, D.C., 6 volumes, 2002. Official USACE Publications repository.
5. Yagci, O.; Kapdasli, S.; Cigizoglu, H. K. “The stability of the antifer units used on breakwaters in case of irregular placement”, *Ocean Engineering*, 31, 1111-1127, 2004.
6. Frens, A. B. *The Impact of Placement Method on Antifer-block Stability*. MSc thesis, Delft University of Technology, 2007.
7. Neves, M. G.; Silva, L. G.; Reither, S. *Stability and overtopping of rubble-mound breakwaters: influence of the placement method and density of cubic blocks*. LNEC / PIANC Portugal.
8. Chegini, V.; Aghtouman, P. Hydraulic stability formulae for Antifer blocks, 2006.
9. Freitas, P. M. G. *Hydraulic Stability of Antifer Cubes: Physical Model Study*. MSc dissertation, Instituto Superior Técnico, 2013.
10. Scaravaglione, G.; Latham, J.-P.; Xiang, J.; Francone, A.; Tomasicchio, G. R. “Historical overview of the structural integrity of Concrete Armour Units”, 2022.
11. Edge, B. L.; Magoon, O. T.; et al. / ASCE-ICCE documentation on the rehabilitation of the West Breakwater of Sines and the use of high-density Antifer cubes.
12. Reis, M. T.; Fortes, C. J. E. M.; Neves, M. G.; et al. “Rehabilitation of Sines west breakwater: wave overtopping study”, *Proceedings of the Institution of Civil Engineers - Maritime Engineering*, 2011.
13. Troch, P.; De Rouck, J.; Van Damme, L. “Full-scale wave-overtopping measurements on the Zeebrugge rubble mound breakwater”, *Coastal Engineering*, 2004.
14. Geeraerts, J.; De Rouck, J.; Troch, P.; et al. “Effects of new variables on the overtopping discharge at steep rubble mound breakwaters: the Zeebrugge prototype case”, 2009.
15. Jensen, O. J. Historical syntheses on the evolution of armour units and recent observations on Antifer behaviour on highly exposed breakwaters, including references to Antifer, Mohammedia and Zeebrugge.
16. Luís, L.; Freire, S.; Barros, J.; Lopes, H.; Lemos, R.; Fortes, C.; Neves, G. “Estudos e projetos do prolongamento do quebra-mar exterior e das acessibilidades marítimas do Porto de Leixões”, PIANC Portugal / LNEC, 2022.
17. Teixeira Duarte. “Extension of the Outer Breakwater and Maritime Access Ways of Leixões Port”, project description with Antifer block quantities and classes.
18. Portos dos Açores / NRV-Norvia / PORTUS. Documentation on the emergency protection and reconstruction of the Port of Lajes das Flores after Hurricane Lorenzo and subsequent storm damage.
