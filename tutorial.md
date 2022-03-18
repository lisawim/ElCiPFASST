
# Tutorial

## 1. Components of a DC Microgrid
In this first chapter of the tutorial, the DC microgrid will be explained and ordinary differential equations (ODE) for each component will be derived for a simulation. In order to understand how a DC microgrid works, we take a look to their construction. The main components are a _DC/DC converter_ and the _Pi-model transmission line_ (shortly: _Pi-model line_). 

### 1.1 Pi-model transmission line

<p align="center">
  <img width = "650" height = "350" src="piline.png">
</p>

The Pi-model line serves as a connection between each power component in the microgrid. The circuit describing the Pi-model line can be seen above and consists of two capacitors, two resistors and an inductor. Here, a voltage source is also added. Later, this circuit is connected to other ODEs describing _DC/DC converters_ and source of voltage will be provided by a battery.

### 1.2 Buck (step-down) converter

<p align="center">
  <img width = "800" height = "350" src="buckconverter.png">
</p>

The figure above shows a simplification of a buck (step-down) converter. The buck converter converts a large input voltage in a smaller output voltage by comparing the output voltage with a predefined target output voltage. When both voltages are equal, then switches will be switch over. Note that both switches are always in opposite state to each other. In order to explain the modelling for the buck converter, first the buck converter is assumed to be in _first state_, which means the switch <img src="https://latex.codecogs.com/svg.image?S_1&space;=&space;1" title="https://latex.codecogs.com/svg.image?S_1 = 1" /> is open and the second switch <img src="https://latex.codecogs.com/svg.image?S_2&space;=&space;0" title="https://latex.codecogs.com/svg.image?S_2 = 0" /> is closed. This results in the circuit:

<p align="center">
  <img width = "800" height = "350" src="buck_first_state.png">
</p>
