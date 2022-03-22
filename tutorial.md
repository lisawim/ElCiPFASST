
# Tutorial

## 1. Basics
Before we dive in to the complex world of power systems, some theory about electrical circuits has to be looked at and explained. Relations between current and voltage for circuit elements provide the fundamentals for a derivation of a system of ordinary differential equations (ODE). Furthermore, _Kirchhoff's laws_ are needed to describe the connections of currents and voltages in a circuit. 

### 1.1 Relation between current and voltage
This subsection deals with the relation between current and voltages of an object. It illustrates the basis for the modelling. One of the relation is _Ohm's law_, which states that the relation between current and voltage in an object is described by

<p align="center">
  <img src="https://latex.codecogs.com/svg.image?I=\dfrac{V}{R}," title="https://latex.codecogs.com/svg.image?I=\dfrac{V}{R}," />
</p>
  
where <img src="https://latex.codecogs.com/svg.image?V" title="https://latex.codecogs.com/svg.image?V" /> is the measured voltage across the object (in volts), <img src="https://latex.codecogs.com/svg.image?I" title="https://latex.codecogs.com/svg.image?I" /> is the current flowing through the object (in amperes) and <img src="https://latex.codecogs.com/svg.image?R" title="https://latex.codecogs.com/svg.image?R" /> describes the resistance (measured in ohms). For circuit elements, this relation is applied for resistors.

Another important relations are those for capacitors and inductors. First, the relation between current and voltage through a capacitor is given by

<p align="center">
  <img src="https://latex.codecogs.com/svg.image?I(t)=C\dfrac{dV(t)}{dt}," title="https://latex.codecogs.com/svg.image?I(t)=C\dfrac{dV(t)}{dt}," />
</p>

where the voltage and the current are assumend to be time-dependent on time <img src="https://latex.codecogs.com/svg.image?t" title="https://latex.codecogs.com/svg.image?t" /> and <img src="https://latex.codecogs.com/svg.image?C" title="https://latex.codecogs.com/svg.image?C" /> ist the capacitance of the capacitor. For the last circuit element that is considered, the relation is also using a derivative with respect to time <img src="https://latex.codecogs.com/svg.image?t" title="https://latex.codecogs.com/svg.image?t" />:

<p align="center">
  <img src="https://latex.codecogs.com/svg.image?\dfrac{dI(t)}{dt}=\dfrac{1}{L}V(t)," title="https://latex.codecogs.com/svg.image?\dfrac{dI(t)}{dt}=\dfrac{1}{L}V(t)," />
</p>

where <img src="https://latex.codecogs.com/svg.image?L" title="https://latex.codecogs.com/svg.image?L" /> is the inductance of the inductor.

### 1.2 Kirchhoff's laws 

There are two laws formulated by Gustav Kirchhoff. The first law, the _current law_, states that the sum of currents flowing in a node is equal to the sum of currents flowing out of a node. Another equivalent formulation of this law is that the sum of all currents that come together at a node is zero:

<p align="center">
  <img src="https://latex.codecogs.com/svg.image?\sum_{k=1}^{n}I_{k}=0" title="https://latex.codecogs.com/svg.image?\sum_{k=1}^{n}I_{k}=0" />
</p>

The _voltage law_, which is the second of Kirchhoff's laws states that the sum of the voltages in a closed loop is zero:

<p align="center">
  <img src="https://latex.codecogs.com/svg.image?\sum_{k=1}^{n}V_{k}=0" title="https://latex.codecogs.com/svg.image?\sum_{k=1}^{n}V_{k}=0" />
</p>

## 2. Components of a DC Microgrid
In the second chapter of the tutorial, the DC microgrid will be explained and an ODE system for each component will be derived for a simulation. In order to understand how a DC microgrid works, we take a look to their construction. The main components are a _DC/DC converter_ and the _Pi-model transmission line_ (shortly: _Pi-model line_). 

### 2.1 Pi-model transmission line

<p align="center">
  <img width = "650" height = "350" src="piline.png">
</p>

The Pi-model line serves as a connection between each power component in the microgrid. The circuit describing the Pi-model line can be seen above and consists of two capacitors, two resistors and an inductor. Here, a voltage source is also added. Later, this circuit is connected to other ODEs describing _DC/DC converters_ and source of voltage will be provided by a battery. 

In a simulation, the interesting values are the voltages of the capacitors and the current of the inductor. These values namely have a relation containing a derivative. For a construction of an ODE system to simulate the Pi-model line, the _Kirchhoff's laws_ provides important regularities in an electrical circuit. The Pi-line satisfies the following:

**Kirchhoff's current law**:
- for node <img src="https://latex.codecogs.com/svg.image?v_{0}" title="https://latex.codecogs.com/svg.image?v_{0}" />: <img src="https://latex.codecogs.com/svg.image?i_{V_{s}}(t)-i_{R_{s}}(t)&space;=&space;0" title="https://latex.codecogs.com/svg.image?i_{V_{s}}(t)-i_{R_{s}}(t) = 0" />
- for node <img src="https://latex.codecogs.com/svg.image?v_{1}" title="https://latex.codecogs.com/svg.image?v_{1}" />: <img src="https://latex.codecogs.com/svg.image?i_{R_{s}}(t)-i_{C_{1}}(t)-i_{R_{\pi}}(t)=0" title="https://latex.codecogs.com/svg.image?i_{R_{s}}(t)-i_{C_{1}}(t)-i_{R_{\pi}}(t)=0" />
- for node <img src="https://latex.codecogs.com/svg.image?v_{2}" title="https://latex.codecogs.com/svg.image?v_{2}" />: <img src="https://latex.codecogs.com/svg.image?i_{R_{\pi}}(t)-i_{L_{\pi}}(t)=0" title="https://latex.codecogs.com/svg.image?i_{R_{\pi}}(t)-i_{L_{\pi}}(t)=0" />
- for node <img src="https://latex.codecogs.com/svg.image?v_{3}" title="https://latex.codecogs.com/svg.image?v_{3}" />: <img src="https://latex.codecogs.com/svg.image?i_{L_{\pi}}(t)-i_{C_{2}}(t)-i_{R_{\ell}}(t)=0" title="https://latex.codecogs.com/svg.image?i_{L_{\pi}}(t)-i_{C_{2}}(t)-i_{R_{\ell}}(t)=0" />

**Kirchhoff's voltage law**:
1. <img src="https://latex.codecogs.com/svg.image?V_{s}&space;(t)-V_{R_{s}}&space;(t)&space;-&space;V_{C_{1}}&space;(t)&space;=&space;0" title="https://latex.codecogs.com/svg.image?V_{s} (t)-V_{R_{s}} (t) - V_{C_{1}} (t) = 0" />
2. <img src="https://latex.codecogs.com/svg.image?V_{C_{1}}&space;(t)&space;-&space;V_{R_{\pi}}(t)&space;-&space;V_{L_{\pi}}&space;(t)&space;-&space;V_{C_{2}}&space;(t)&space;=&space;0" title="https://latex.codecogs.com/svg.image?V_{C_{1}} (t) - V_{R_{\pi}}(t) - V_{L_{\pi}} (t) - V_{C_{2}} (t) = 0" />
3. <img src="https://latex.codecogs.com/svg.image?V_{C_{2}}(t)&space;-&space;V_{R_{\ell}}(t)&space;=&space;0" title="https://latex.codecogs.com/svg.image?V_{C_{2}}(t) - V_{R_{\ell}}(t) = 0" />

Then, the ODE system for modelling the Pi-model line is of the form <img src="https://latex.codecogs.com/svg.image?\dfrac{d}{dt}u(t)=Au(t)&plus;f(t)" title="https://latex.codecogs.com/svg.image?\dfrac{d}{dt}u(t)=Au(t)+f(t)" />  with:

<p align="center">
  <img src="https://latex.codecogs.com/svg.image?A=\begin{pmatrix}&space;-1/(R_{s}C_{1})&space;&&space;0&space;&&space;-1/C_{1}\\&space;0&space;&&space;-1/(R_{\ell}C_2)&space;&&space;1/C_{2}\\&space;1/L_{\pi}&space;&&space;-1/L_{\pi}&space;&&space;-R_{\pi}/L_{\pi}\\\end{pmatrix},&space;f(t)=\begin{pmatrix}&space;V_{s}/(R_{s}C_{1})\\&space;0\\&space;&space;&space;&space;&space;&space;0\end{pmatrix}" title="https://latex.codecogs.com/svg.image?A=\begin{pmatrix} -1/(R_{s}C_{1}) & 0 & -1/C_{1}\\ 0 & -1/(R_{\ell}C_2) & 1/C_{2}\\ 1/L_{\pi} & -1/L_{\pi} & -R_{\pi}/L_{\pi}\\\end{pmatrix}, f(t)=\begin{pmatrix} V_{s}/(R_{s}C_{1})\\ 0\\ 0\end{pmatrix}" />
</p>

and
  <p align="center">
    <img src="https://latex.codecogs.com/svg.image?u(t)=\begin{pmatrix}&space;v_{C_{1}}(t)\\&space;v_{C_{2}}(t)\\&space;&space;&space;&space;&space;&space;i_{L_{\pi}}(t)\end{pmatrix}" title="https://latex.codecogs.com/svg.image?u(t)=\begin{pmatrix} v_{C_{1}}(t)\\ v_{C_{2}}(t)\\ i_{L_{\pi}}(t)\end{pmatrix}" />
  </p>
the vector of unknown values containing the voltage of the first and second capacitor <img src="https://latex.codecogs.com/svg.image?v_{C_{1}}(t)" title="https://latex.codecogs.com/svg.image?v_{C_{1}}(t)" /> and <img src="https://latex.codecogs.com/svg.image?v_{C_{2}}(t)" title="https://latex.codecogs.com/svg.image?v_{C_{2}}(t)" /> and the current on the inductor <img src="https://latex.codecogs.com/svg.image?i_{L_{\pi}}(t)" title="https://latex.codecogs.com/svg.image?i_{L_{\pi}}(t)" />.


  
### 2.2 Buck (step-down) converter

<p align="center">
  <img width = "800" height = "350" src="buckconverter.png">
</p>

The figure above shows a simplification of a buck (step-down) converter. The buck converter converts a large input voltage in a smaller output voltage by comparing the output voltage with a predefined target output voltage. When both voltages are equal, then switches will be switch over. Note that both switches are always in opposite state to each other. In order to explain the modelling for the buck converter, first the buck converter is assumed to be in _first state_, which means the switch <img src="https://latex.codecogs.com/svg.image?S_1&space;=&space;1" title="https://latex.codecogs.com/svg.image?S_1 = 1" /> is open and the second switch <img src="https://latex.codecogs.com/svg.image?S_2&space;=&space;0" title="https://latex.codecogs.com/svg.image?S_2 = 0" /> is closed. This results in the circuit:

<p align="center">
  <img width = "800" height = "350" src="buck_first_state.png">
</p>

Note that this circuit corresponds to the Pi-model line. Then, to model this electrical circuit, the _Kirchhoff's laws_ are used. They are:

**Kirchhoff's current law**:
- for node <img src="https://latex.codecogs.com/svg.image?v_{0}" title="https://latex.codecogs.com/svg.image?v_{0}" />: <img src="https://latex.codecogs.com/svg.image?i_{V_{s}}(t)-i_{R_{s}}(t)&space;=&space;0" title="https://latex.codecogs.com/svg.image?i_{V_{s}}(t)-i_{R_{s}}(t) = 0" />
- for node <img src="https://latex.codecogs.com/svg.image?v_{1}" title="https://latex.codecogs.com/svg.image?v_{1}" />: <img src="https://latex.codecogs.com/svg.image?i_{R_{s}}(t)-i_{C_{1}}(t)-i_{R_{\pi}}(t)=0" title="https://latex.codecogs.com/svg.image?i_{R_{s}}(t)-i_{C_{1}}(t)-i_{R_{\pi}}(t)=0" />
- for node <img src="https://latex.codecogs.com/svg.image?v_{2}" title="https://latex.codecogs.com/svg.image?v_{2}" />: <img src="https://latex.codecogs.com/svg.image?i_{R_\pi}(t)-i_{L_1}(t)=0" title="https://latex.codecogs.com/svg.image?i_{R_\pi}(t)-i_{L_1}(t)=0" />
- for node <img src="https://latex.codecogs.com/svg.image?v_{3}" title="https://latex.codecogs.com/svg.image?v_{3}" />: <img src="https://latex.codecogs.com/svg.image?i_{L_{1}}(t)-i_{C_{2}}(t)-i_{R_{\ell}}(t)=0" title="https://latex.codecogs.com/svg.image?i_{L_{1}}(t)-i_{C_{2}}(t)-i_{R_{\ell}}(t)=0" />
    
**Kirchhoff's voltage law**:
1. <img src="https://latex.codecogs.com/svg.image?V_{s}&space;(t)-V_{R_{s}}&space;(t)&space;-&space;V_{C_{1}}&space;(t)&space;=&space;0" title="https://latex.codecogs.com/svg.image?V_{s} (t)-V_{R_{s}} (t) - V_{C_{1}} (t) = 0" />
2. <img src="https://latex.codecogs.com/svg.image?V_{C_{1}}&space;(t)&space;-&space;V_{R_\pi}(t)-&space;V_{L_{1}}&space;(t)&space;-&space;V_{C_{2}}&space;(t)&space;=&space;0" title="https://latex.codecogs.com/svg.image?V_{C_{1}} (t) - V_{R_\pi}(t)- V_{L_{1}} (t) - V_{C_{2}} (t) = 0" />
3. <img src="https://latex.codecogs.com/svg.image?V_{C_{2}}(t)&space;-&space;V_{R_{\ell}}(t)&space;=&space;0" title="https://latex.codecogs.com/svg.image?V_{C_{2}}(t) - V_{R_{\ell}}(t) = 0" />

As in the case of the Pi-model line, the ODE system of the first state of the buck converter has the form <img src="https://latex.codecogs.com/svg.image?\dfrac{d}{dt}u(t)=Au(t)&plus;f(t)" title="https://latex.codecogs.com/svg.image?\dfrac{d}{dt}u(t)=Au(t)+f(t)" /> with coefficient matrix and right-hand side:

<p align="center">
  <img src="https://latex.codecogs.com/svg.image?A=\begin{pmatrix}&space;-1/(R_{s}C_{1})&space;&&space;0&space;&&space;-1/C_{1}\\&space;0&space;&&space;-1/(R_{\ell}C_2)&space;&&space;1/C_{2}\\&space;1/L_{1}&space;&&space;-1/L_{1}&space;&&space;-R_{\pi}/L_{1}\\\end{pmatrix},&space;f(t)=\begin{pmatrix}&space;V_{s}/(R_{s}C_{1})\\&space;0\\&space;&space;&space;&space;&space;&space;0\end{pmatrix}" title="https://latex.codecogs.com/svg.image?A=\begin{pmatrix} -1/(R_{s}C_{1}) & 0 & -1/C_{1}\\ 0 & -1/(R_{\ell}C_2) & 1/C_{2}\\ 1/L_{1} & -1/L_{1} & -R_{\pi}/L_{1}\\\end{pmatrix}, f(t)=\begin{pmatrix} V_{s}/(R_{s}C_{1})\\ 0\\ 0\end{pmatrix}" />
</p>

and solution vector

<p align="center">
    <img src="https://latex.codecogs.com/svg.image?u(t)=\begin{pmatrix}&space;v_{C_{1}}(t)\\&space;v_{C_{2}}(t)\\&space;&space;&space;&space;&space;&space;i_{L_{\pi}}(t)\end{pmatrix}." title="https://latex.codecogs.com/svg.image?u(t)=\begin{pmatrix} v_{C_{1}}(t)\\ v_{C_{2}}(t)\\ i_{L_{\pi}}(t)\end{pmatrix}." />
  </p>

Switching to the second state means that the switches have the states <img src="https://latex.codecogs.com/svg.image?S_1&space;=&space;0" title="https://latex.codecogs.com/svg.image?S_1 = 0" /> and <img src="https://latex.codecogs.com/svg.image?S_2&space;=&space;1" title="https://latex.codecogs.com/svg.image?S_2 = 1" />, which yields the circuit:

<p align="center">
  <img width = "800" height = "350" src="buck_second_state.png">
</p>

Modelling requires the both laws:

**Kirchhoff's current law**:
- for node <img src="https://latex.codecogs.com/svg.image?v_{0}" title="https://latex.codecogs.com/svg.image?v_{0}" />: <img src="https://latex.codecogs.com/svg.image?i_{V_{s}}(t)-i_{R_{s}}(t)&space;=&space;0" title="https://latex.codecogs.com/svg.image?i_{V_{s}}(t)-i_{R_{s}}(t) = 0" />
- for node <img src="https://latex.codecogs.com/svg.image?v_{1}" title="https://latex.codecogs.com/svg.image?v_{1}" />: <img src="https://latex.codecogs.com/svg.image?i_{R_{s}}(t)-i_{C_{1}}(t)=0" title="https://latex.codecogs.com/svg.image?i_{R_{s}}(t)-i_{C_{1}}(t)=0" />
- for node <img src="https://latex.codecogs.com/svg.image?v_{2}" title="https://latex.codecogs.com/svg.image?v_{2}" />: <img src="https://latex.codecogs.com/svg.image?i_{C_{1}}(t)-i_{R_{\pi}}(t)=0" title="https://latex.codecogs.com/svg.image?i_{C_{1}}(t)-i_{R_{\pi}}(t)=0" />
- for node <img src="https://latex.codecogs.com/svg.image?v_{3}" title="https://latex.codecogs.com/svg.image?v_{3}" />: <img src="https://latex.codecogs.com/svg.image?i_{R_\pi}(t)-i_{L_1}(t)=0" title="https://latex.codecogs.com/svg.image?i_{R_\pi}(t)-i_{L_1}(t)=0" />
- for node <img src="https://latex.codecogs.com/svg.image?v_{4}" title="https://latex.codecogs.com/svg.image?v_{4}" />: <img src="https://latex.codecogs.com/svg.image?i_{L_{1}}(t)-i_{C_{2}}(t)-i_{R_{\ell}}(t)=0" title="https://latex.codecogs.com/svg.image?i_{L_{1}}(t)-i_{C_{2}}(t)-i_{R_{\ell}}(t)=0" />

**Kirchhoff's voltage law**:
1. <img src="https://latex.codecogs.com/svg.image?V_{s}&space;(t)-V_{R_{s}}&space;(t)&space;-&space;V_{C_{1}}&space;(t)&space;=&space;0" title="https://latex.codecogs.com/svg.image?V_{s} (t)-V_{R_{s}} (t) - V_{C_{1}} (t) = 0" />
2. <img src="https://latex.codecogs.com/svg.image?V_{R_\pi}&space;(t)&space;&plus;&space;V_{L_{1}}&space;(t)&space;&plus;&space;V_{C_{2}}&space;(t)&space;=&space;0" title="https://latex.codecogs.com/svg.image?V_{R_\pi} (t) + V_{L_{1}} (t) + V_{C_{2}} (t) = 0" />
3. <img src="https://latex.codecogs.com/svg.image?V_{C_{2}}(t)&space;-&space;V_{R_{\ell}}(t)&space;=&space;0" title="https://latex.codecogs.com/svg.image?V_{C_{2}}(t) - V_{R_{\ell}}(t) = 0" />

Finally, the ODE system is also of the form <img src="https://latex.codecogs.com/svg.image?\dfrac{d}{dt}u(t)=Au(t)&plus;f(t)" title="https://latex.codecogs.com/svg.image?\dfrac{d}{dt}u(t)=Au(t)+f(t)" /> with coefficient matrix and right-hand side:

<p align="center">
  <img src="https://latex.codecogs.com/svg.image?A=\begin{pmatrix}&space;-1/(R_{s}C_{1})&&space;0&space;&&space;0\\&space;0&space;&&space;-1/(R_{\ell}C_2)&space;&&space;1/C_{2}&space;\\&space;&space;&space;&space;&space;&space;&space;&space;&space;R_\pi&space;/\left(L_1&space;R_s\right)&space;&&space;-1/L_{1}&space;&&space;0\end{pmatrix},&space;f(t)=\begin{pmatrix}&space;V_{i}/(R_{s}C_{1})\\&space;0\\&space;&space;&space;&space;&space;&space;&space;&space;&space;-R_\pi&space;V_s&space;/\left(L_1&space;R_s\right)\end{pmatrix}&space;" title="https://latex.codecogs.com/svg.image?A=\begin{pmatrix} -1/(R_{s}C_{1})& 0 & 0\\ 0 & -1/(R_{\ell}C_2) & 1/C_{2} \\ R_\pi /\left(L_1 R_s\right) & -1/L_{1} & 0\end{pmatrix}, f(t)=\begin{pmatrix} V_{i}/(R_{s}C_{1})\\ 0\\ -R_\pi V_s /\left(L_1 R_s\right)\end{pmatrix} " />
</p>

and the vector of unknowns
  <p align="center">
    <img src="https://latex.codecogs.com/svg.image?u(t)=\begin{pmatrix}&space;v_{C_{1}}(t)\\&space;v_{C_{2}}(t)\\&space;&space;&space;&space;&space;&space;i_{L_{\pi}}(t)\end{pmatrix}." title="https://latex.codecogs.com/svg.image?u(t)=\begin{pmatrix} v_{C_{1}}(t)\\ v_{C_{2}}(t)\\ i_{L_{\pi}}(t)\end{pmatrix}." />
  </p>

## 3. Control
In the last section about the buck converter, the circuit can be in two different states. A few questions arise: Which state is the current state? When does the converter switch to the other state? In order to answer these questions and learn a little bit more about the functionality of a DC microgrid, this section deals with the controlling of the output voltage. Remember that the buck converter reduces the input voltage. Moreover, it can reduce the input voltage to a target output voltage. The controller can realise this via comparing the actual output voltage with a desired output value in every time step.

### 3.1 Duty cycle
The duty cycle specifies the relation between the ON-time and OFF-time of a switch. It is defined as a percentage or as relative value. Then, a duty cycle of 0.75 (or 75 %) means that the ON-time in a period accounts for 75% of the time. In ths 75% the switch is closed. In the other 25 %, the switch is closed. This process is illustrated in the picture:

<p align="center">
  <img width = "600" height = "350" src="duty.png">
</p>
