# High-Speed Pen Plotter — Netherlands parts list

Prepared 24 August 2026 for the IVProjects **High-Speed Pen Plotter** shown in video `wX90X4rVUr8`.

Project files: [IVProjects GitHub folder](https://github.com/IVProjects/Engineering_Projects/tree/main/ProjectFiles/High-Speed%20Pen%20Plotter) · [creator's original BOM](https://github.com/IVProjects/Engineering_Projects/blob/main/ProjectFiles/High-Speed%20Pen%20Plotter/BOM.txt) · [STEP assembly](https://github.com/IVProjects/Engineering_Projects/tree/main/ProjectFiles/High-Speed%20Pen%20Plotter/.STEP%20Assem)

## Short recommendation

Build it with the original Arduino Uno + CNC Shield V3 + A4988 architecture. Use **three identical 1.8° NEMA-17 motors with 5 mm shafts**, ideally 38–40 mm bodies and roughly 1.2–1.5 A/phase. The 123-3D DMO00051 is a very close dimensional match, but was temporarily unavailable when checked. Do not buy the 2.5 A, 48 mm motor for this build: it is heavier and beyond the TinyTronics A4988 carrier's 1 A continuous rating.

Expect roughly **€150–€220**, excluding filament, tools and shipping. The design is buildable, but it is not a fully documented kit: the CAD assembly is effectively the assembly manual.

## 1. Electronics

| Qty | Part to buy | Exact requirement / recommendation | Suggested source | Status |
|---:|---|---|---|---|
| 1 | Arduino Uno R3-compatible board | ATmega328P, Uno R3 shield layout, USB serial | [TinyTronics compatible Uno R3](https://www.tinytronics.nl/en/development-boards/microcontroller-boards/arduino-compatible/uno-r3-compatible-met-atmega16u2) | Confirmed architecture |
| 1 | CNC Shield V3 | Uno-format, accepts Pololu-footprint A4988 modules | [TinyTronics CNC Shield V3](https://www.tinytronics.nl/en/mechanics-and-actuators/motor-controllers-and-drivers/adapter-boards/cnc-shield-v3) | Confirmed |
| 4 | A4988 stepper driver + heatsink | Three required; buy one spare. Set all three axes to 1/16 microstepping. TinyTronics carrier: 8–35 V motor supply, 1 A continuous / 2 A peak, 0.05 Ω sense resistors | [TinyTronics red A4988](https://www.tinytronics.nl/en/mechanics-and-actuators/motor-controllers-and-drivers/stepper-motor-controllers-and-drivers/a4988-motor-driver-module-red) | Confirmed; spare recommended |
| 3 | NEMA-17 bipolar stepper motor | **1.8°**, 4-wire, **5 mm shaft**, body about **38–40 mm**, shaft about **22–24 mm**, nominal current around **1.2–1.5 A/phase** | Closest NL option: [123-3D DMO00051](https://www.123-3d.nl/123-3D-NEMA17-stappenmotor-1-8-graden-per-stap-40-mm-lang-4-08-kg-cm-SL42S240A105-0524-i3421.html). Exact-size alternative: StepperOnline 17HE15-1504S, preferably the 3-pack | CAD confirms 2× 38 mm plus 1× 38 mm/23 mm-shaft model; use three identical motors |
| 1 | 24 V DC supply | Original BOM says at least 45 W. Prefer a **fully enclosed, CE-approved 24 V / 3 A (72 W) desktop brick**, not an exposed mains PSU | Example specification: RS PRO stock 204-7566, 24 V/3 A/72 W, 5.5×2.1 mm centre-positive | Confirmed voltage; 3 A adds safe headroom |
| 1 | 24 V axial fan | **40 × 40 × 10 mm (4010), 24 V, axial**, 2-wire | [123-3D 24 V axial fans](https://www.123-3d.nl/3D-printer-onderdelen/Motoren/Ventilatoren/Axiaal-p15052.html), item DMO00009 | CAD confirms dimensions; do not order a radial blower |
| 1 | USB cable | USB-A-to-B, or USB-C-to-B if that suits your Mac | Any reputable cable | Required for flashing and UGS |
| 1 | DC input adapter | Female 5.5×2.1 mm barrel socket to screw terminal, matching the chosen brick | TinyTronics / Kiwi / electronics supplier | Only if using a barrel-plug brick |
| 1 set | Low-voltage wiring | 0.5–0.75 mm² (roughly AWG20–18) for 24 V input/fan; motor leads/cables for all three motors; ferrules or proper crimp terminals | TinyTronics | Confirm connector order against motors |
| 1 | Low-voltage switch and fuse | 24 V-rated switch; inline 3–4 A fuse on the DC side | Electronics supplier | Recommended safety/convenience addition |

### Motor choice verdict

The motor page you found contains several different motors. The best match is **DMO00051**, not simply any NEMA-17:

- 1.8° per step — matches the original calibration logic.
- 42.3 × 42.3 × 40 mm — only 2 mm longer than the 38 mm CAD motor.
- 5 mm × 22 mm shaft — compatible with the pulley and 5-to-5 mm coupler.
- 1.2 A/phase and 4.08 kg·cm holding torque.

It was listed as temporarily unavailable when checked. The 48 mm / 2.5 A versions are a poor substitute for this particular plotter: the moving X motor becomes heavier, and the A4988 carrier is rated for only 1 A continuous. The 27 mm motors save mass but are much weaker. The 0.9° motors work only after doubling the relevant GRBL steps/mm and are not the closest drop-in choice.

## 2. Motion hardware and shafts

| Qty | Part to buy | Exact specification | Suggested source / search term | Confidence |
|---:|---|---|---|---|
| 1 | X-axis smooth rod | **Ø10 mm × 280 mm**; STEP geometry is 277.5 mm. Buy 300 mm and cut/test-fit | `10 mm hardened linear shaft 300 mm` from a 3D-printer/CNC supplier | High |
| 1 | Y grit-roller driveshaft | **Ø5 mm × 250 mm** | Buy Ø5 mm precision shaft/rod and cut | From STEP CAD |
| 2 | Lever/idler pins | **Ø5 mm × 45 mm** | Cut from the same Ø5 mm rod | From STEP CAD |
| 2 | Lever/idler pins | **Ø5 mm × 33–35 mm**; CAD geometry is 33 mm, filename says 35 mm | Cut long, then trim during assembly | Medium; CAD naming conflict |
| 1 | Ø5 mm rod stock | Buy at least **500 mm**, preferably 1 m, to cover the 250 + 2×45 + 2×35 mm pieces and cutting allowance | `5 mm precision smooth rod 1 m` | Recommended buy quantity |
| 5 | 605ZZ bearings | **5 × 14 × 5 mm**, metal-shielded. Buy 6–10 because the fit is sensitive | Search `605ZZ 5x14x5`; [dimensional reference](https://www.kugellager-express.de/miniature-deep-groove-ball-bearing-605-ZZ-5x14x5-mm) | Confirmed by BOM |
| 1 | MR115ZZ bearing | **5 × 11 × 4 mm** | Search `MR115ZZ 5x11x4` | Confirmed by BOM/CAD |
| 1 | 5-to-5 mm rigid shaft coupler | **5 mm bore at both ends**. Prefer rigid/slit style if aligned; the available [123-3D rigid coupler](https://www.123-3d.nl/123-3D-Motor-koppeling-5-mm-5-mm-i3153.html) is closer than a spring coupler | 123-3D DMO00046 or equivalent | Confirmed |
| 1 | GT2 drive pulley | **GT2, 20 teeth, 5 mm bore, for 6 mm belt** | [123-3D 20T/5 mm pulley](https://www.123-3d.nl/123-3D-GT2-Pulley-hoge-resolutie-6-mm-riem-20-tanden-5-mm-as-i2081.html) | Strong CAD-derived match; calibrate steps/mm |
| 1 | GT2 idler | Smooth idler for 6 mm belt, 5 mm mounting bore, or reproduce the CAD bearing-based idler | [123-3D smooth 6 mm-belt idler](https://www.123-3d.nl/123-3D-Spanrol-gladde-pulley-hoge-resolutie-6-mm-riem-5-mm-as-i2086.html) | Original BOM does not give dimensions |
| 1 m | GT2 open belt | **GT2 pitch 2 mm, 6 mm wide, open-ended**, glass-fibre reinforced preferred | [TinyTronics 1 m GT2 belt](https://www.tinytronics.nl/en/mechanics-and-actuators/parts/timing-belts/gt2-timing-belt-6mm-1m) or [123-3D 1 m belt](https://www.123-3d.nl/123-3D-GT2-timing-belt-6-mm-1-meter-i6539.html) | Length not specified by creator; 1 m is safely sufficient |
| 1 pack | Dremel 432 sanding bands | **13 mm diameter, 13 mm long, 120 grit**, six-pack; two used as grit wheels | Dremel order no. **2615000432**, EAN 0080596004323; [official dimensions](https://www.dremel.com/gn/en/p/sanding-band-13-mm-120-grit-2615000432) | Confirmed |
| 1 | Pinch-lever weight | **Ø12.7 mm (1/2 inch) steel bar × 240 mm** | Local metal supplier / model-engineering stockist | Critical, confirmed by BOM and CAD |
| 1 | Baseboard | **381 × 457.2 × about 13 mm** (15 × 18 × about 1/2 inch), flat plywood or MDF | Local bouwmarkt; have it cut square | Present in CAD but omitted from creator BOM |

Do not substitute a threaded M5 rod for the 5 mm smooth shafts. Its actual diameter, rough surface and straightness are wrong for the bearings and grit wheels.

## 3. Fasteners and small consumables

The creator only says “M3 hardware”; neither the BOM nor repository supplies a screw schedule. The least frustrating purchase is an M3 assortment plus spares:

| Qty | Part | Recommendation |
|---:|---|---|
| 1 kit | M3 socket-head screws | M3×6, ×8, ×10, ×12, ×16, ×20, ×25 and ×30 mm; at least 10 of each |
| 30 each | M3 nuts and washers | Standard nuts plus washers; add 10 nyloc nuts |
| 1 small pack | M4 screws/nuts | For a commercial GT2 pulley/idler if its mounting hardware requires M4 |
| 1 | Small ceramic screwdriver | For live Vref adjustment without shorting the driver potentiometer |
| 1 | Medium-strength threadlocker | For metal-to-metal pulley and coupler grub screws only; keep away from plastic |
| 1 | Light machine oil | Very small amount for steel shafts/bearings; keep it away from grit bands and paper |
| — | Cable ties, heat-shrink, crimp terminals | For strain relief and fan/power wiring |
| — | Thin card/shims | Useful when aligning the writing surface and grit rollers |

Buy screws after printing one side frame and checking hole depth if you want exact quantities. There are no fastener models in the published assembly, so any “exact” online screw list would be guesswork.

## 4. Parts to print

Print the repository STLs at their original scale. The creator's BOM plus the repository require:

| Qty | STL |
|---:|---|
| 1 | `Left Side Frame.STL` |
| 1 | `lRight Side Frame.STL` |
| 1 | `PrintHead.STL` |
| 1 | `Writing Surface.STL` |
| 1 | `Tru-Red Pen Adapter.STL` |
| 1 | `IdlerLever.STL` |
| 1 | `Mirrored IdlerLever.STL` |
| 2 | `IdlerTire.STL` |
| 2 | `IdlerShaftCap.STL` |
| 1 | `Pen Lifter Bar.STL` |
| 2 | `GritWheelAdapter.STL` |
| 1 | `FeedTableSupport.STL` |
| 1 | `SlopedSupportTable.STL` |
| 1 | `5mmShaftConnector.STL` |
| 1 | `ElectonicsBox.STL` |
| 1 | `ElectronicsBoxTop.STL` — present in the repository but omitted from the text BOM |

Suggested starting print setup (recommendation, not creator-specified):

- PETG for frames, levers, printhead and shaft adapters; PLA can work but may creep in a warm electronics box.
- 0.20 mm layers, 4 perimeters, 5 top/bottom layers, 30–40% gyroid/cubic infill.
- 50–70% infill and 5–6 perimeters for the two side frames, levers and grit-wheel adapters.
- Print the two `IdlerTire` parts in TPU 95A if the geometry slices cleanly; otherwise print the published parts in PETG and add a thin rubber sleeve only if traction is insufficient.
- Ream/drill bearing and shaft holes to final size rather than scaling the whole model.

## 5. Pen compatibility

The supplied adapter was designed around a **0.7 TRU RED gel pen refill**, a US office-supply product. A random European G2-style refill is not guaranteed to fit. Print the adapter first and measure it before buying many pens. The STEP assembly also contains a Bic-style adapter, but the root download folder exposes only the Tru-Red adapter STL; modifying that small part may be necessary.

## 6. Critical issues before ordering

1. **There is no build manual.** Download the STEP assembly and inspect it in FreeCAD, Fusion or another STEP viewer before cutting rods. It shows part orientation and resolves omissions in the text BOM.
2. **The 123-3D category contains incompatible motors.** Use 1.8°, 5 mm shaft, about 38–40 mm body. Avoid the 2.5 A/48 mm motors with A4988 drivers, and avoid 0.9° motors unless you intentionally recalculate GRBL steps/mm.
3. **A4988 current must be set before serious motion tests.** The TinyTronics red carrier uses 0.05 Ω sense resistors and is rated at 1 A continuous. Start low, verify the motor stays reliable, and keep the 24 V fan blowing directly over all three heatsinks. Do not blindly copy a Vref value for a different carrier.
4. **Never feed 24 V into the Arduino's barrel jack or 5 V pin.** Feed 24 V only to the CNC Shield motor-power input and fan. Power the Uno over USB unless your particular shield documentation explicitly provides a safe regulated path.
5. **Driver orientation is destructive if wrong.** With power disconnected, match `EN/STEP/DIR` and `VMOT/GND` markings on each A4988 to the shield silkscreen; clone board colours are not a reliable guide.
6. **Never connect/disconnect a motor while powered.** Doing so commonly destroys A4988 drivers.
7. **The grit roller is the make-or-break subsystem.** Use genuine 13 mm Dremel 432 bands, a straight 5 mm driveshaft, equal left/right pressure and the specified 12.7 mm × 240 mm weight. Test paper tracking with a blank sheet before mounting a pen.
8. **The half-inch weight matters.** A 12 mm metric bar is about 11% lighter at the same length. It may still work, but be prepared to lengthen it or add small weights equally on both sides.
9. **The machine has no published endstops or automatic homing.** Stock operation requires manually positioning the axes and setting the work zero at every startup. Adding endstops requires printed brackets, wiring and GRBL configuration changes.
10. **The pen-lift motor can overheat.** It is a stepper held at a fixed position, not a servo. Set its driver current only as high as needed and avoid leaving the machine energised unattended.
11. **Base flatness and frame squareness control accuracy.** A warped base or side frames that are not parallel will cause binding and rounded corners before software calibration can help.
12. **The GT2 idler is underspecified.** The CAD uses a compact bearing-based arrangement, while the BOM only says “timing belt idler pulley.” Check its fit against the printed frame before purchasing a bulky commercial idler.

## 7. Suggested order split

### TinyTronics

- 1× Uno R3 compatible
- 1× CNC Shield V3
- 4× red A4988 with heatsinks
- 1× 1 m open-ended GT2 belt, 6 mm
- Wiring, connectors and a ceramic adjustment screwdriver as needed

### 123-3D

- 3× DMO00051 motors **if back in stock**, otherwise order an exact 38 mm-class 3-pack elsewhere
- 1× 20T GT2 pulley, 5 mm bore, 6 mm belt
- 1× suitable compact idler only after checking the CAD/printed frame
- 1× rigid 5-to-5 mm coupler
- 1× 24 V axial 4010 fan (DMO00009)
- 1× 1 m GT2 belt if not bought at TinyTronics
- Motor cables if they are not supplied with the motors

### Bearings / shaft supplier

- 5× 605ZZ (buy 6–10)
- 1× MR115ZZ / 5×11×4 (buy 2)
- 300 mm of Ø10 mm hardened smooth shaft
- At least 500 mm of Ø5 mm precision smooth shaft

### Bouwmarkt / metal supplier

- Flat 381 × 457.2 × 12–13 mm baseboard
- 240 mm of Ø12.7 mm steel bar
- M3 fastener assortment and consumables

## 8. First checks after parts arrive

1. Dry-fit each 605ZZ and shaft in the printed parts; correct holes individually.
2. Assemble the 10 mm X rod and confirm the carriage traverses freely by hand.
3. Verify the 5 mm Y shaft is straight and both grit adapters run concentrically.
4. Wire one motor and one driver at a time at low current.
5. Fit all three 1/16-step jumper sets under the drivers before installing them.
6. Confirm fan airflow reaches the driver heatsinks.
7. Calibrate X and Y independently with a measured 100 mm move. For a 1.8° motor, 1/16 microstepping and a 20T GT2 pulley, the theoretical X starting value is **80 steps/mm**; calibrate the grit-driven Y axis empirically from actual paper travel.
8. Run repeated rectangles without a pen and check whether the paper returns to the same marks. Only then fit and tune the pen.

## Source notes

The creator's published BOM confirms the electronics, 24 V/45 W minimum supply, Dremel bands, 240 mm half-inch weight, 280 mm × 10 mm rod, bearing counts and generic M3 hardware. The published STEP assembly supplies dimensions omitted from that BOM, including the 250 mm grit-wheel shaft, short 5 mm pins, 38 mm-class motors, 40×40×10 fan and 381×457.2×13 mm baseboard. Where the creator supplied neither a dimension nor a part number—especially the belt length, idler and fastener schedule—this list deliberately labels the recommendation rather than presenting it as original specification.
