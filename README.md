# Concrete Antifer Cubes

## Executive Summary

Antifer cubes are massive grooved unreinforced concrete armour units used in rubble-mound breakwaters and related maritime protection works. They were developed for the Port of Antifer, Normandy, in the early 1970s, as a robust improvement over the plain concrete cube. The geometry remains compact and structurally conservative, but adds four lateral grooves and controlled tapering to improve hydraulic behaviour, roughness, interlock and resistance to face-to-face rearrangement.

This repository contains a Python production tool that generates a closed vectorial Antifer armour-unit solid from input unit weight $W$ and concrete unit weight $W_c$. The tool exports the same validated geometry to IFC, STL, OBJ and DXF. It is a geometric CAD/BIM production and documentation tool; hydraulic stability design remains a separate project-specific task.

Two dimensional conventions are implemented:

| Convention | Purpose | Volume relation | Reference-height meaning |
|---|---|---:|---|
| Pita (1986) | historical proportional Antifer reference | $V/H^3=1.024700000000$ | drawing height used in the historical coefficient set |
| Carvalho (2026) | volume-normalised CAD/BIM reference | $V/H^3=1.000000000000$ | $H=D_n=V^{1/3}$ |

The same vectorial topology is used in both conventions: a tapered body, no top bevel, four lateral plan chamfers and four single circular-arc side grooves. The Carvalho convention is obtained by horizontally normalising the Pita plan and groove coefficients by a common factor so that the final non-dimensional volume coefficient becomes unity.

## Repository Scope

This repository is concerned with the reproducible geometric reconstruction of Antifer cubes. It does not replace hydraulic model testing, breakwater stability design, overtopping analysis, toe design, crest design or construction-method verification.

The main outputs are:

| Output | Description |
|---|---|
| IFC | IFC4 `IfcFacetedBrep` model with property and quantity data |
| STL | closed triangular surface mesh in metres |
| OBJ | indexed triangular surface mesh in metres |
| DXF | AutoCAD 2018 / AC1032 file with an ACIS-backed `3DSOLID` |
| TXT | `output.txt` calculation and validation report |

## Historical and Engineering Context

The Antifer cube is an improved massive concrete cube. It should not be treated as a slender high-interlock unit. Its engineering value lies in combining hydraulic improvement with structural robustness.

The unit became especially relevant after the structural-integrity problems observed in some slender concrete armour units during the late 1970s and early 1980s. Antifer cubes retain large resistant concrete sections and avoid slender arms, reducing the risk of bending-sensitive prototype breakage. This robustness comes at the cost of relatively high concrete consumption compared with modern monolayer armour units.

Representative contexts in which Antifer units have been used or studied include:

| Case | Main relevance |
|---|---|
| Port of Antifer | origin and prototype context |
| Sines West Breakwater | repair and rehabilitation after Dolos armour-layer failure |
| Zeebrugge | prototype overtopping and run-up measurements |
| Douro Bar / Cabedelo do Douro | model testing, high-density units and monitoring |
| Leixoes Outer Breakwater | contemporary Portuguese port-extension use |
| Lajes das Flores | Atlantic island-port emergency protection and reconstruction |
| Mohammedia | severe-exposure international breakwater context |
| Brunei | documented manufacture, curing and placement practice |

These examples are engineering context only. They do not define a universal stability coefficient.

## Geometry and Dimensional Convention

### Adopted Production Geometry

| Item | Adopted convention |
|---|---|
| Vertical reference | $H$ is the total unit height |
| Bottom section | $A$ is the bottom bounding width at $z=0$ |
| Top section | $B$ is the top bounding width at $z=H$ |
| Top face | single horizontal plane; no top bevel |
| Chamfers | $D$ is a lateral plan-chamfer offset |
| Grooves | four identical side grooves |
| Groove type | one continuous circular arc per side |
| Groove radius | $R$, with $r=R/H$ |
| Groove centre offset | $E$, with $e=E/H$, outside the side face |
| Generated groove depth | $C_{\mathrm{arc}}=R-E$, with $c_{\mathrm{arc}}=r-e$ |
| Groove half-opening | $Q=\sqrt{R^2-E^2}$, with $q=Q/H=\sqrt{r^2-e^2}$ |
| Geometry source | pure vectorial B-rep generation; no imported template geometry |

### Master Coefficient Table

All Pita and Carvalho coefficients used by the production script are consolidated here. Later sections refer back to this table instead of repeating the same coefficient set.

| Quantity | Meaning | Pita (1986) | Carvalho (2026) |
|---|---|---:|---:|
| $K_V$ | final volume coefficient, $V/H^3$ | $1.024700000000$ | $1.000000000000$ |
| $f$ | horizontal factor applied to Pita coefficients | $1.000000000000$ | $0.987874174182$ |
| $a=A/H$ | bottom width coefficient | $1.086000000000$ | $1.072831353161$ |
| $b=B/H$ | top width coefficient | $1.005000000000$ | $0.992813545052$ |
| $d=D/H$ | lateral chamfer coefficient | $0.024000000000$ | $0.023708980180$ |
| $r=R/H$ | groove-radius coefficient | $0.121500000000$ | $0.120026712163$ |
| $e=E/H$ | outside groove-centre offset | $0.025906459610$ | $0.025592322393$ |
| $c_{\mathrm{arc}}=r-e$ | generated circular-arc groove-depth coefficient | $0.095593540390$ | $0.094434389770$ |
| $q=\sqrt{r^2-e^2}$ | groove half-opening coefficient | $0.118705961731$ | $0.117266553915$ |
| $2q$ | full groove-opening coefficient | $0.237411923462$ | $0.234533107831$ |

The historical Pita notation often reports $C/H=0.095600$. The production geometry uses the volume-consistent circular-arc value $c_{\mathrm{arc}}=0.095593540390$, which is the generated depth obtained from $C_{\mathrm{arc}}=R-E$.

## Algebraic Volume Definition

The generated unit volume is computed from a simple geometric balance:


$$
\frac{V}{H^3}
=
K_{\mathrm{frustum}}
-
K_{\mathrm{chamfers}}
-
K_{\mathrm{grooves}}.
$$


The components are:

| Component | Non-dimensional expression | Meaning |
|---|---:|---|
| Gross tapered square frustum | $K_{\mathrm{frustum}}=(a^2+ab+b^2)/3$ | volume before groove and chamfer removals |
| Four corner chamfers | $K_{\mathrm{chamfers}}=2d^2$ | four triangular plan removals carried through the height |
| One circular groove | $A_g=r^2\arccos(e/r)-e\sqrt{r^2-e^2}$ | circular-segment area removed by one side groove |
| Four side grooves | $K_{\mathrm{grooves}}=4A_g$ | total groove subtraction |
| Final coefficient | $K_V=K_{\mathrm{frustum}}-K_{\mathrm{chamfers}}-K_{\mathrm{grooves}}$ | final value of $V/H^3$ |

### Demonstration of the Square-Frustum Formula

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

### Compact Numerical Balance

| Convention | Gross frustum | Chamfers | Grooves | Final $V/H^3$ |
|---|---:|---:|---:|---:|
| Pita (1986) | $1.093617000000$ | $0.001152000000$ | $0.067765000000$ | $1.024700000000$ |
| Carvalho (2026) | $1.067255782180$ | $0.001124231482$ | $0.066131550698$ | $1.000000000000$ |

For Pita, the one-groove area is:


$$
A_g=\frac{1.092465000000-1.024700000000}{4}
=
0.016941250000.
$$


With $r=0.121500000000$, this value is obtained by solving:


$$
A_g=r^2\arccos(e/r)-e\sqrt{r^2-e^2},
$$


which gives:


$$
e=0.025906459610,\qquad
q=0.118705961731,\qquad
c_{\mathrm{arc}}=0.095593540390.
$$


For Carvalho, all Pita horizontal plan and groove coefficients are multiplied by:


$$
f=\sqrt{\frac{1.000000000000}{1.024700000000}}
=
0.987874174182.
$$


Because the vertical reference height remains $H$, the non-dimensional area terms scale with $f^2$, giving $K_V=1.000000000000$.

## Dimensional Scaling from Input Weight

The script uses the input unit weight $W$ and concrete unit weight $W_c$ to compute the unit volume:


$$
V=\frac{W}{W_c}.
$$


The selected dimensional convention then gives the reference height:

| Convention | Height relation |
|---|---:|
| Pita (1986) | $H=\left(V/1.024700000000\right)^{1/3}$ |
| Carvalho (2026) | $H=V^{1/3}=D_n$ |

Once $H$ is known, all absolute dimensions are obtained by multiplying the coefficient table values by $H$. For example, $A=aH$, $B=bH$, $D=dH$, $R=rH$ and $E=eH$.

## Nominal Diameter

The Van der Meer nominal diameter is:


$$
D_n=V^{1/3}.
$$


The relation between $D_n$ and the drawing height depends on the selected convention:

| Convention | Relation |
|---|---:|
| Pita (1986) | $D_n=(1.024700000000)^{1/3}H=1.008166460709H$ |
| Carvalho (2026) | $D_n=H$ |

This distinction is important when hydraulic sizing is expressed through $D_n$ but CAD geometry is generated through a drawing height $H$.

## Horizontal Section and Groove Construction

A horizontal section has local half-width $h=w/(2H)$, where $w$ is the non-dimensional section width. The east-side groove can be written in local non-dimensional coordinates as:


$$
x(y)=h+e-\sqrt{r^2-y^2},
\qquad
-q\le y\le q.
$$


Key points are:

| Feature | Coordinate or relation |
|---|---:|
| Groove mouth | $y=\pm q,\;x=h$ |
| Deepest groove point | $y=0,\;x=h+e-r=h-c_{\mathrm{arc}}$ |
| Other sides | obtained by 90-degree rotations |
| Corner chamfers | four lateral plan chamfers using offset $d$ |

This section definition is used consistently in IFC, STL, OBJ and DXF exports.

## Hydraulic Stability Interpretation

Antifer hydraulic stability is not governed by geometry alone. It depends strongly on the armour-layer system: placement method, packing density, slope, wave climate, storm duration, underlayer, toe support, crest details and damage criterion.

The Hudson formula remains a common preliminary sizing relation:


$$
W=
\frac{\gamma_c H_D^3}
{K_D \Delta^3 \cot\alpha},
\qquad
\Delta=\frac{\gamma_c}{\gamma_w}-1.
$$


The stability number formulation is often more convenient for comparison:


$$
N_s=\frac{H_s}{\Delta D_n}.
$$


For regular two-layer cubes and Antifer-calibrated formulae, a Van der Meer-type empirical structure may be used:


$$
N_s
=
\left(
k_1\frac{N_{od}^{k_2}}{N_z^{k_3}}+k_4
\right)
s_{0m}^{-k_5}.
$$


Typical coefficient sets are:

| Armour unit and slope | $k_1$ | $k_2$ | $k_3$ | $k_4$ | $k_5$ |
|---|---:|---:|---:|---:|---:|
| Regular cube, $\cot\alpha=1.5$ | 6.700 | 0.400 | 0.300 | 1.000 | 0.100 |
| Regular cube, $\cot\alpha=2.0$ | 7.374 | 0.400 | 0.300 | 1.101 | 0.100 |
| Antifer, $\cot\alpha=1.5$ | 6.951 | 0.443 | 0.291 | 1.082 | 0.082 |
| Antifer, $\cot\alpha=2.0$ | 6.138 | 0.443 | 0.276 | 1.164 | 0.070 |

These formulae are preliminary design tools, not substitutes for project-specific verification. Reported $K_D$ values for Antifer vary widely because placement method and damage definition dominate the result.

## Placement, Packing and Failure Modes

The same Antifer geometry can perform differently depending on armour-layer architecture.

| Placement tendency | Main benefit | Main risk |
|---|---|---|
| regular placement | higher displacement stability | greater reflection and overtopping in some cases |
| irregular placement | greater roughness and reduced overtopping | lower displacement stability |
| dense packing | higher contact restraint | reduced porosity and possible paving behaviour |
| open packing | higher porosity and roughness | greater movement risk |

Relevant failure and degradation mechanisms include:

| Mechanism | Description |
|---|---|
| rocking | repeated angular movement without extraction |
| displacement | block moves out of its stable position |
| chain failure | movement of one block destabilises adjacent units |
| smoothing or paving | armour surface becomes more regular and less rough |
| concrete cracking | thermal, shrinkage, handling, impact or fatigue damage |
| toe or underlayer failure | loss of support leading to progressive armour instability |
| overtopping-induced rear damage | crest or rear-side damage due to transmitted water |

A defensible Antifer design must therefore consider the full armour system, not only the isolated concrete unit.

## Manufacture, Materials and Quality Control

Antifer units are normally manufactured as plain unreinforced concrete blocks. The main production advantages are simple formwork, robust geometry and straightforward inspection. The main risks are thermal cracking, honeycombing, density variation and handling damage.

| Aspect | Typical practice or control |
|---|---|
| Concrete | normally unreinforced; low heat of hydration recommended |
| Strength class | commonly C25/30 in manual-type references |
| Formwork | four-face mould, open top and bottom in typical production |
| Casting | top casting with vibration |
| Curing | prolonged moist curing, especially for large units |
| Handling | controlled lifting, rotation and storage procedures |
| Mass control | verify $W=W_cV$ |
| Dimensional control | verify mould dimensions and generated volume |
| Rejection logic | reject significant cracks, honeycombing, cold joints or excessive corner loss |

A dimensional error is a stability error. A density error is also a stability error. For CAD/BIM production, a volume error in the digital solid becomes a procurement, fabrication and quality-control error.

## Python Script Installation and Usage

### Requirements

Python 3.10 or newer is recommended. Tkinter must be available; on standard Windows Python installations it is normally included.

Install the runtime packages with:

```bash
python -m pip install ezdxf trimesh pillow
```

`pillow` is recommended for broad Windows and PyInstaller compatibility with optional `ezdxf` drawing add-ons.

### Windows Virtual Environment

Create a virtual environment:

```powershell
py -m venv .venv
```

Activate it:

```powershell
.\.venv\Scripts\activate
```

Upgrade `pip`:

```powershell
python -m pip install --upgrade pip
```

Install the dependencies:

```powershell
python -m pip install ezdxf trimesh pillow
```

For standalone executable compilation, also install PyInstaller:

```powershell
python -m pip install pyinstaller
```

### Running the Application

Run the graphical application with:

```bash
python script_final_production.py
```

Typical workflow:

1. Enter the Antifer unit weight $W$ in kN.
2. Enter the concrete unit weight $W_c$ in kN/m^3.
3. Select Pita (1986) or Carvalho (2026).
4. Select the output folder.
5. Review the calculation and validation preview.
6. Press **Generate IFC + STL + OBJ + DXF**.

Example output names:

```text
antifer_pita1986_500kN_Wc24kNm3.ifc
antifer_pita1986_500kN_Wc24kNm3.stl
antifer_pita1986_500kN_Wc24kNm3.obj
antifer_pita1986_500kN_Wc24kNm3.dxf
output.txt
```

### Viewing the Exported Files

| Format | Recommended inspection |
|---|---|
| IFC | IFC/BIM viewers supporting faceted B-rep geometry |
| STL | mesh viewers or CAD applications with mesh import |
| OBJ | mesh viewers or modelling tools |
| DXF | AutoCAD/ZWCAD-type CAD inspection as ACIS-backed `3DSOLID` |
| TXT | direct review of dimensions and validation values |

All exported geometry is dimensional and written in metres. The exported XY origin is placed at the homogeneous centre of mass, while the exported Z datum remains the physical bottom level $z=0$.

### Standalone Executable Compilation

A PyInstaller spec file is recommended for repeatable Windows production builds:

```powershell
pyi-makespec --onefile --windowed --name script --collect-all ezdxf script_final_production.py
pyinstaller --clean --noconfirm script.spec
```

The compiled executable is written to the `dist` folder.

## Verification Checklist

Before issuing geometry for technical use, check:

| Check | Required result |
|---|---|
| selected convention | Pita or Carvalho coefficients match the master table |
| top face | one flat horizontal face at $z=H$, with no top bevel |
| chamfers | four lateral plan chamfers only |
| grooves | one circular arc per side, radius $R$, centre offset $E$ |
| closed shell | every B-rep edge shared by exactly two faces |
| volume | generated volume matches the selected $K_V$ |
| IFC/STL/OBJ/DXF | all formats generated from the same B-rep source |
| output report | dimensions and validation values recorded in `output.txt` |

## Limitations

This repository does not provide:

- new hydraulic model tests;
- prototype monitoring data;
- finite-element structural-integrity analysis;
- a complete breakwater design method;
- a universal Antifer $K_D$;
- project-specific wave, overtopping, toe, crest or underlayer verification.

Critical works should be verified through physical modelling or equivalent project-specific evidence.

## Conclusions

The production geometry is a reproducible algebraic reconstruction of an Antifer cube as a square frustum with four lateral plan chamfers and four circular side grooves. Pita preserves the historical volume coefficient $V/H^3=1.024700000000$. Carvalho keeps the same topology but horizontally normalises the plan and groove coefficients so that $V/H^3=1.000000000000$ and $H=D_n$.

The geometric definition is necessary for reliable CAD/BIM production, drawing control, volume calculation and quality assurance. It does not remove the need for hydraulic verification. Antifer stability remains governed primarily by armour-layer placement, packing density, wave climate, slope, storm duration, toe support, construction tolerance and accepted damage.

## Dedication

This work is respectfully dedicated to the memory of **Carlos Alberto Roldao Maia Pita** (1950-2002), Portuguese civil engineer and specialist in maritime hydraulics and rubble-mound breakwater design. His LNEC *Memoria n.º 670 - Dimensionamento Hidraulico do Manto Resistente de Quebra-Mares de Talude* remains an important technical reference for Portuguese maritime engineering and provides a key historical basis for the geometric interpretation of Antifer cubes.

## References

1. Pita, C. A. R. M. *Dimensionamento Hidraulico do Manto Resistente de Quebra-Mares de Talude*. Laboratorio Nacional de Engenharia Civil, Memoria n.º 670, Lisboa, 1986.
2. BSI. *BS 6349-7:1991 Maritime structures - Part 7: Guide to the design and construction of breakwaters*, with 2010 corrigenda.
3. CIRIA; CUR; CETMEF. *The Rock Manual: The use of rock in hydraulic engineering*, 2nd ed., 2007.
4. U.S. Army Corps of Engineers. *Coastal Engineering Manual*. Engineer Manual EM 1110-2-1100, U.S. Army Corps of Engineers, Washington, D.C., 2002.
5. Yagci, O.; Kapdasli, S.; Cigizoglu, H. K. "The stability of the antifer units used on breakwaters in case of irregular placement", *Ocean Engineering*, 31, 1111-1127, 2004.
6. Frens, A. B. *The Impact of Placement Method on Antifer-block Stability*. MSc thesis, Delft University of Technology, 2007.
7. Neves, M. G.; Silva, L. G.; Reither, S. *Stability and overtopping of rubble-mound breakwaters: influence of the placement method and density of cubic blocks*. LNEC / PIANC Portugal.
8. Chegini, V.; Aghtouman, P. Hydraulic stability formulae for Antifer blocks, 2006.
9. Freitas, P. M. G. *Hydraulic Stability of Antifer Cubes: Physical Model Study*. MSc dissertation, Instituto Superior Tecnico, 2013.
10. Scaravaglione, G.; Latham, J.-P.; Xiang, J.; Francone, A.; Tomasicchio, G. R. "Historical overview of the structural integrity of Concrete Armour Units", 2022.
11. Edge, B. L.; Magoon, O. T.; et al. ASCE-ICCE documentation on the rehabilitation of the West Breakwater of Sines and the use of high-density Antifer cubes.
12. Reis, M. T.; Fortes, C. J. E. M.; Neves, M. G.; et al. "Rehabilitation of Sines west breakwater: wave overtopping study", *Proceedings of the Institution of Civil Engineers - Maritime Engineering*, 2011.
13. Troch, P.; De Rouck, J.; Van Damme, L. "Full-scale wave-overtopping measurements on the Zeebrugge rubble mound breakwater", *Coastal Engineering*, 2004.
14. Geeraerts, J.; De Rouck, J.; Troch, P.; et al. "Effects of new variables on the overtopping discharge at steep rubble mound breakwaters: the Zeebrugge prototype case", 2009.
15. Jensen, O. J. Historical syntheses on the evolution of armour units and recent observations on Antifer behaviour on highly exposed breakwaters.
16. Luis, L.; Freire, S.; Barros, J.; Lopes, H.; Lemos, R.; Fortes, C.; Neves, G. "Estudos e projetos do prolongamento do quebra-mar exterior e das acessibilidades maritimas do Porto de Leixoes", PIANC Portugal / LNEC, 2022.
17. Teixeira Duarte. "Extension of the Outer Breakwater and Maritime Access Ways of Leixoes Port", project description with Antifer block quantities and classes.
18. Portos dos Acores / NRV-Norvia / PORTUS. Documentation on the emergency protection and reconstruction of the Port of Lajes das Flores after Hurricane Lorenzo and subsequent storm damage.
