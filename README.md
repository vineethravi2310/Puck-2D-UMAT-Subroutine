# Puck-2D-Subroutine

The following is a UMAT subroutine for Puck failure criteria in Abaqus. It applies only to unidirectional composites. The general form of the Puck criterion utilizes the full 3-D state of stress and strain, but this subroutine is used for only 2D elements. And also progressive damage isn't implemented at present.


# Failure Modes
Basically there are two fiber failure modes and three inter fiber failure modes. The fiber failure is same as the maximum stress criterion in this case.

## Fiber Failure in Tension

The fiber failure in tension is given by

$$ f = \frac{\sigma_{11}}{X_T} $$

The above equation is valid only when $\sigma_{11} \geq 0$

## Fiber Failure in Compression

The fiber failure in compression is given by

$$ f = - \frac{\sigma_{11}}{X_C} $$

The above equation is valid only when $\sigma_{11} < 0$

## Inter Fiber Failure : Mode A

Mode A corresponds to a fracture angle of 0°. The criterion is invoked if $\sigma_{22} > 0$

$$  f = \sqrt{  \Bigl(   \frac{\tau_{12}  }{ S_{12} } \Bigl)^2 +  \Bigl( 1 - p^+_{\perp\parallel} \frac{Y_T}{S}\Bigl)^2  \Bigl( \frac{\sigma_{22}}{Y_T} \Bigl)^2 } + p^{+}_{\perp\parallel} \frac{\sigma_{22}}{S_{12}} $$

