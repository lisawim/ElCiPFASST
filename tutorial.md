
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

Note that this circuit corresponds to the Pi-model line. Then, to model this electrical circuit, the _Kirchhoff's laws_ are used. They are:

**Kirchhoff's Current Law**:
- for node 0: <img src="https://latex.codecogs.com/svg.image?i_{V_{s}}(t)-i_{R_{s}}(t)&space;=&space;0" title="https://latex.codecogs.com/svg.image?i_{V_{s}}(t)-i_{R_{s}}(t) = 0" />
- for node 1: <img src="https://latex.codecogs.com/svg.image?i_{R_{s}}(t)-i_{C_{1}}(t)-i_{R_{\pi}}(t)=0" title="https://latex.codecogs.com/svg.image?i_{R_{s}}(t)-i_{C_{1}}(t)-i_{R_{\pi}}(t)=0" />
- for node 2: <img src="https://latex.codecogs.com/svg.image?i_{R_\pi}(t)-i_{L_1}(t)=0" title="https://latex.codecogs.com/svg.image?i_{R_\pi}(t)-i_{L_1}(t)=0" />
- for node 3: <img src="https://latex.codecogs.com/svg.image?i_{L_{1}}(t)-i_{C_{2}}(t)-i_{R_{\ell}}(t)=0" title="https://latex.codecogs.com/svg.image?i_{L_{1}}(t)-i_{C_{2}}(t)-i_{R_{\ell}}(t)=0" />
    
**Kirchhoff's Voltage Law**:
1. <img src="https://latex.codecogs.com/svg.image?V_{s}&space;(t)-V_{R_{s}}&space;(t)&space;-&space;V_{C_{1}}&space;(t)&space;=&space;0" title="https://latex.codecogs.com/svg.image?V_{s} (t)-V_{R_{s}} (t) - V_{C_{1}} (t) = 0" />
2. <img src="https://latex.codecogs.com/svg.image?V_{C_{1}}&space;(t)&space;-&space;V_{R_\pi}(t)-&space;V_{L_{1}}&space;(t)&space;-&space;V_{C_{2}}&space;(t)&space;=&space;0" title="https://latex.codecogs.com/svg.image?V_{C_{1}} (t) - V_{R_\pi}(t)- V_{L_{1}} (t) - V_{C_{2}} (t) = 0" />
3. <img src="https://latex.codecogs.com/svg.image?V_{C_{2}}(t)&space;-&space;V_{R_{\ell}}(t)&space;=&space;0" title="https://latex.codecogs.com/svg.image?V_{C_{2}}(t) - V_{R_{\ell}}(t) = 0" />
