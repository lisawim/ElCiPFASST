# Tutorial

## 1. Components of a DC Microgrid
In order to understand how a DC microgrid works, we take a look to their construction. The main components are a _DC/DC converter_ and the _Pi-model transmission line_ (shortly: _Pi-model line_). 

### 1.1 Pi-model transmission line

```latex {cmd=true hide=true}
\documentclass{standalone}
\usepackage{circuitikz}
\usetikzlibrary{matrix}
\begin{document}
\begin{circuitikz}[american]
\draw (0,0) to[isource, l=$I_0$] (0,3) --
        (2,3)
   to[R=$R_1$] (2,0) -- (0,0);
   \draw (2,3) -- (4,3) to[R=$R_2$]
(4,0) -- (2,0); \end{circuitikz}
\end{document}

### 1.2 Step-down (buck) converter
