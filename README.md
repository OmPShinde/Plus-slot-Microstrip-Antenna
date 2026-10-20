# Plus Slot Microstrip Patch Antenna for 2.4 GHz (CST Studio Suite)

Design and simulation of an inset-fed microstrip patch antenna with a plus-shaped slot, built on FR-4 and matched to a 50 ohm feed so that S11 falls below -10 dB at 2.4 GHz (Wi-Fi / ISM band). The antenna is modelled and simulated in CST Studio Suite 2025.

## Overview

A rectangular patch on a 1.6 mm FR-4 substrate is fed by a 3 mm microstrip line. A plus-shaped slot cut into the centre of the patch tunes the resonance, and a notch cut into the radiating edge around the feed (an inset feed) brings the input impedance close to 50 ohm, which gives the impedance match at 2.4 GHz.

## Design Specifications

### Materials

| Part      | Material                                            |
|-----------|-----------------------------------------------------|
| Substrate | FR-4 (lossy), relative permittivity 4.3, loss tangent 0.025 |
| Substrate thickness | 1.6 mm                                    |
| Patch, feed, ground | Annealed copper, 0.035 mm thick           |

### Dimensions

All parameters are defined as named variables in the CST project, so the design can be tuned directly.

| Parameter | Value (mm) | Description                                   |
|-----------|------------|-----------------------------------------------|
| lg        | 39         | Ground plane and substrate length (x)         |
| wg        | 47.6       | Ground plane and substrate width (y)          |
| l         | 28.9       | Patch length (x)                              |
| w         | 30         | Patch width (y)                               |
| vs        | 8          | Length of the horizontal slot arm (x)         |
| v         | 1.5        | Width of the horizontal slot arm (y)          |
| hs        | 1.5        | Width of the vertical slot arm (x)            |
| h         | 8          | Length of the vertical slot arm (y)           |

Fixed dimensions in the model:

| Feature        | Value                                                              |
|----------------|--------------------------------------------------------------------|
| Feed line width| 3 mm, running from the patch edge to the substrate edge            |
| Inset notch    | Depth l/6 (about 4.8 mm), 5 mm wide, leaving a 1 mm gap on each side of the feed |
| Port position  | At the substrate edge, x = 19.5 mm                                 |

## Impedance Matching

Matching is done in two ways:

- The 3 mm microstrip feed line on 1.6 mm FR-4 acts as the 50 ohm transmission line connecting the port to the patch.
- The inset notch moves the feed point inwards from the patch edge, where the edge impedance of a patch is high, to a point where the input impedance is close to 50 ohm. The inset depth and gap are the main tuning knobs for S11.

The plus slot lengthens the current path on the patch, which shifts the resonance down towards 2.4 GHz.

## Simulation Setup

| Setting           | Value                                                      |
|-------------------|------------------------------------------------------------|
| Software          | CST Studio Suite 2025 (Microwave Studio)                   |
| Solver            | High frequency time domain, hexahedral mesh (about 150,000 cells) |
| Frequency range   | 1.4 GHz to 3.4 GHz                                         |
| Port              | One waveguide port, 50 ohm normalisation                   |
| Boundaries        | Expanded open on all sides                                 |
| Steady state limit| -40 dB                                                     |
| Monitors          | H-field and farfield at 1.4, 2.4 and 3.4 GHz               |

## Results

### Return Loss (S11)

S11 drops below -10 dB around 2.4 GHz, with a minimum of about -22 dB at the design frequency, so the antenna is well matched to 50 ohm in the Wi-Fi / ISM band. The response is narrow band, with a single sharp resonance and S11 close to 0 dB elsewhere in the 1.4 to 3.4 GHz sweep.

### Radiation Pattern

Farfield directivity at 2.4 GHz (Phi = 90 cut):

| Parameter               | Value      |
|-------------------------|------------|
| Main lobe magnitude     | 5.77 dBi   |
| Main lobe direction     | 0 deg (broadside) |
| Angular width (3 dB)    | 92.1 deg   |
| Side lobe level         | -6.4 dB    |

The pattern is broadside, as expected for a patch antenna, with a wide beam suitable for general purpose Wi-Fi coverage.

## How to Run

1. Open `simulation/Plus_Slot_MSA.cst` in CST Studio Suite 2025 or later.
2. Start the time domain solver.
3. Open 1D Results, then S-Parameters, and select S1,1 to view the return loss around 2.4 GHz.
4. Change any parameter (for example the slot length or the inset geometry) in the parameter list and re-run to see how the match shifts.

## Future Scope

- Parametric sweep of the inset depth and slot size to widen the bandwidth
- Gain and efficiency analysis, and patterns in other planes
- Fabrication on FR-4 and measurement with a vector network analyser
- Comparison with a low-loss substrate such as Rogers
