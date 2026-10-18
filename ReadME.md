# 2.4 GHz Microstrip Bandpass Filter Design Project

Design, simulation, and fabrication of a microstrip hairpin bandpass filter.
Course project for High-Frequency Electronics at HAW Hamburg.

Design and simulation were done with AWR Microwave Office (Axiem 2.5D MoM).
Fabrication was done at JLCPCB.

## Specification and Design Goals

| Parameter | Specification Goal |
|---|---|
| Center frequency f<sub>c</sub> | 2.4 GHz |
| 3 dB bandwidth | Wideband, 480 MHz+ |
| S<sub>11</sub> passband | < −15 dB |
| S<sub>21</sub> passband | > −3 dB |

### Stackup

<p align="center">
  <img src="images/stackup.png" alt="PCB stackup" width="60%">
</p>

## Design and Simulation

The iFilter wizard in AWR MWO provided a good starting geometry for reaching the
desired specifications. For optimization, the 2.5D Axiem solver was chosen to
simulate a more realistic behavior of the microstrip lines. Since the filter needs
connectors for measurement, the required tapers were also included in the simulation.


| Key Characteristic | Simulation |
|---|---|
| Center frequency f<sub>c</sub> | 2.4 GHz |
| 3 dB bandwidth | 580 MHz (2110–2690 MHz) |
| S<sub>11</sub> passband | < −15 dB between 2220–2640 MHz |
| S<sub>21</sub> passband | > −4.7 dB, peak at −1.7 dB |


<p align="center">
  <img src="images/schematic.png" alt="Simulated S-parameters" width="80%">
</p>

<p align="center">
  <img src="images/layout.png" alt="Simulated S-parameters" width="80%">
</p>

<p align="center">
  <img src="images/s_parameters_simu.png" alt="Simulated S-parameters" width="80%">
</p>


## Measurement

Measurements were performed with a PicoVNA.
**Note:** The provided Touchstone files contain raw, uncalibrated data.

<p align="center">
  <img src="images/fabricated_filter.jpg" alt="Fabricated filter" width="60%">
</p>

| Key Characteristic | Measurement |
|---|---|
| Center frequency f<sub>c</sub> | 2.303 GHz |
| 3 dB bandwidth | 526 MHz |
| S<sub>11</sub> passband | < −15 dB |
| S<sub>21</sub> passband | > −3 dB |


<p align="center">
  <img src="images/s_parameters_measurement.png" alt="Simulated S-parameters" width="80%">
</p>

<p align="center">
  <img src="images/s11_comparison.png" alt="Simulated S-parameters" width="80%">
</p>

<p align="center">
  <img src="images/s21_comparison.png" alt="Simulated S-parameters" width="80%">
</p>

## Differences Between Simulation and Measurement

As expected, the measurements differ from the simulation. A shift in center
frequency, a reduction in bandwidth, and worse S<sub>11</sub> can be observed.
Worse S<sub>11</sub> refers to more reflection at the input port.

The shift from 2.4 GHz to 2.303 GHz indicates that the actual FR4 permittivity
was slightly higher than the simulated value (higher ε<sub>r</sub> → shorter
wavelength → lower resonant frequency). FR4 is inexpensive, but its dielectric
constant varies significantly between batches and even across a single PCB.

A measured peak S<sub>21</sub> of −1.8 dB was reached, matching the simulation
well.

The raw (uncalibrated) Touchstone data shows S<sub>11</sub> values above 0 dB
around 3.5 GHz and 1.2 GHz. These are measurement artifacts from the
uncalibrated setup (cables, connectors) rather than physical behavior. The
connector is rated only from DC to 3 GHz, and higher-order modes likely
contribute near 3.5 GHz.





## Conclusion

This project was a very good learning experience and yielded good results for a
first attempt. Even though the simulation used only 2.5D MoM, the resulting
S<sub>11</sub>/S<sub>21</sub> parameters are good enough for use in a real design,
with S<sub>21</sub> as low as −1.8 dB. Manufacturing effects such as the shifted
center frequency became visible.

For future iterations, a more suitable substrate should be chosen, and a small
test strip for measuring the relative permittivity should be included on the PCB.