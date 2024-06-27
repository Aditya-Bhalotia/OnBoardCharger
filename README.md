# Design of an Universal On-Board Charger Using PFC and PSFB Converters

## Overview

The project involves designing a universal on-board charger capable of charging batteries with voltages ranging from 200V to 336V. It operates from an AC supply of 85-265V RMS and 45-65Hz frequency. The charger switches between constant current mode (20% to 80% State of Charge, SoC) and constant voltage mode beyond that range.

## Various Components

1. **Totem Pole Power Factor Correction (PFC) Converter**
   - **Input:**
     - Vrms: 85V to 265V
     - Frequency: 45Hz to 65Hz
   - **Function:**
     - Convert AC supply to a DC bus maintained at 400V.
     - Achieve high power factor (close to 1) by drawing sinusoidal current from the AC supply.
   - **Specifications:**
     | Variables            | Value                               | Range                          |
     |----------------------|-------------------------------------|--------------------------------|
     | Vrms                 | 230V                                | 85-265V                        |
     | frequency            | 50/60Hz                             | 45-65Hz                        |
     | Vdc                  | 400V (nominal) at 230V rms input    |                                |
     | $\Delta i_{L}$       | 25% of peak current                 |                                |
     | $\Delta V_{dc2\omega}$ | 20V                               | $2\omega$ frequency ripple     |
     | Power Factor         | $>$ 0.99                            |                                |
     | $f_{sw}$             | 50 kHz                              |                                |

2. **Phase Shifted Full Bridge (PSFB) Converter**
   - **Input:**
     - DC bus at 400V
   - **Function:**
     - Step down DC bus voltage to a level suitable for charging batteries.
     - Maintain required current or voltage based on battery charging mode.
   - **Specifications:**
     | Variables         | Value                     | Range                          |
     |-------------------|---------------------------|--------------------------------|
     | Vdc               | 400V                      |                                |
     | Vout              | 296V (nominal)            | 200V-336V                      |
     | Pout              | 3.6kW (max.)              | 360-3600W                      |
     | $\Delta i_{L}$    | 75% of average current    |                                |
     | $\Delta V_{dcsw}$ | 2V                        | Switching frequency ripple     |
     | $f_{sw}$          | 100 kHz                   |                                |

3. **Current Controller and Voltage Controllers**
   - Appropriate plant modeling ensures proper controller design.
   - All controllers are PI controllers to maintain zero steady-state error.
   - Anti-windup technique implemented for faster transient settling and to prevent overshoots.
   - PSFB controller design assumes Battery Management System (BMS) provides State of Charge (SoC) information.

