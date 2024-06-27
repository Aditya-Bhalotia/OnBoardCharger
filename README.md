# Design of an universal on board charger using PFC and PSFB converters

## Overview
The project is based on the design of an universal on board charger for charging batteries with voltage in the range 200-336V from an AC supply of 85-265V rms and frequency of 45-65Hz.
The charger should switch between Constant current mode (when charged from 20% SoC to 80% SoC) and in constant voltage beyond that. 

## Various components
1. Totem Pole Power Factor Correction(PFC) converter (connected between AC supply and DC bus maintained at 400V)
2. Phase Shifted Full Bridge(PSFB) converter between the DC bus and battery.
3. Current controllers and voltage controllers for each of these converters.

### Totem Pole PFC
- **Input**: AC supply with
	- Vrms : 85V to 265V
	- Frequency: 45Hz to 65Hz
- **Function**: 
1. Convert the AC supply to a DC voltage i.e., a DC bus at 400V.
2. Draw sinusoidal current from the AC supply i.e., power factor should be close to 1.

- **Specification** :
| Variables     | Value                                     | Range 		|
|------------|----------------------------------------------|--------------------
| Vrms	     | 230V                			    |	85-265V		|
| frequency  |50/60Hz				            |			|
| Vdc	     | 400V (nominal) at 230V rms input	    |			|
| $\Delta i_{L}$ | 25% of peak current		             |			|
|$\Dleta V_{dc2\omega}$| 20V 				    |	$2\omega$ frequency ripple|
|Power Factor  | $>$ 0.99					|		|
| $f_{sw} 	|	50 kHz					|		|



### Diode bridge rectifier based PSFB
- **Input**: DC bus at 400V
- **Function**: 
1. Convert DC bus voltage level to lower voltage level which can be used to charge batteries.
2. Maintains required current or voltage depending on the charging mode of the battery at the output.
- **Specification** :
| Variables     | Value                                     | Range 		|
|------------|----------------------------------------------|--------------------
| Vdc	     | 400V                			    |		|
| Vout	     | 296V (nominal) 	    |			|
| $\Delta i_{L}$ | 75% of average current		             |			|
|$\Dleta V_{dcsw}$| 2V 				    |	Switching frequency ripple|
| $f_{sw} 	|	100 kHz					|		|

### Current controller and voltage controllers

-Appropriate modelling of the plant was done to ensure proper design of the controllers.
- All the controllers are PI controllers to ensure zero steady state error between the quantity of interest and reference.
- Anti-windup technique has been implemented to ensure faster settling of the transients and avoid unnecessary overshoots in current and voltages.
- While designing the controller for PSFB it was assumed that BMS will provide the information for the SoC of the battery.
