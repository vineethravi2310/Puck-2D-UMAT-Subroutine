# Puck 2D UMAT Subroutine

<p align="center">
<img src="Images/10.5923.s.cmaterials.201310.07_001.gif" width = 700 alt>
</p>
<p align="center">
<em>Different Modes of Inter-Fiber Failure Modes</em>
</p>

The following is a UMAT subroutine for Puck failure criteria in Abaqus. It applies only to unidirectional composites. The general form of the Puck criterion utilizes the entire 3D state of stress and strain, but this UMAT considers only in-plane stresses and strains consistent with Classical Laminate Theory. This UMAT also considers the influence of the stress $\sigma_1$ on the Inter-Fiber Failure(IFF).

### Fiber Failure in Tension

$$f_{E,FF} = \frac{\sigma_1}{R^t_\parallel}$$

### Fiber Failure in Compression

$$f_{E,FF} = -\frac{\sigma_1}{R^c_\parallel}$$

### Inter-Fiber Failure : Mode A
This mode is valid when $\sigma_2 \geq 0$
$$f_{E,IFF} = \sqrt{\Bigl(   \frac{\tau_{21}  }{ R_{\perp\parallel} } \Bigl)^2 +  \Bigl( 1 - p^t_{\perp \parallel} \frac{R^t_\perp}{R_{\perp\parallel}}\Bigl)^2  \Bigl( \frac{\sigma_2}{R^t_\perp} \Bigl)^2 } + p^t_{\perp \parallel} \frac{\sigma_2}{R_{\perp\parallel}}$$

### Inter-Fiber Failure : Mode B
This mode is valid when $\sigma_2 < 0$ and $0\leq  \big| \frac{\sigma_2}{\tau_{21}} \big| \leq \frac{R^A_{\perp\perp}}{|\tau_{21c}|}$
$$f_{E,IFF} = \frac{1}{R_{\perp \parallel}} \Bigl[ \sqrt{ \tau_{21}^2 + ( p_{\perp \parallel}^c \sigma_2 )^2 } +  p_{\perp \parallel}^c \sigma_2 \Bigr] $$

### Inter-Fiber Failure : Mode C
This mode is valid when $\sigma_2 < 0$ and $0\leq  \big| \frac{\tau_{21}}{\sigma_2} \big| \leq \frac{|\tau_{21c}|}{R^A_{\perp\perp}}$
$$f_{E,IFF} = \Big( \frac{R^c_\perp}{ -\sigma_2} \Big) \Bigl[  \Bigl(\frac{\tau_{21}}{2(1+P^c_{\perp\perp})R_{\perp\parallel}}  \Bigr)^2 + \Bigl(\frac{\sigma_2}{R^c_\perp}\Bigr)^2  \Bigr] $$

### Influence of Fiber-Parallel Stress on Inter-Fiber Fracture.

Sometimes there can be an influence of FF on IFF. The new inter-fiber failure index after considering the effect of $\sigma_1$ is given by

$$f_{E,IFF}^1 = \frac{f^0_{E,IFF}}{\lambda}$$

The superscripts 0 and 1 indicate the before and after considerations of $\sigma_1$. It is only valid when $\frac{1}{a_0} \geq \delta \geq \lambda_{min}$

$$\delta = \frac{f^0_{E,IFF}}{f_{E,FF}}$$

$$a = \frac{1 - a_0}{\sqrt{1-\lambda_{min}^2}}$$

$$\lambda = \frac{a_0 + a\sqrt{1 + \delta^2(a^2-a_0^2)}}{1+a^2\delta^2}\delta$$

$$$$

The recommended values for $a_0$ and $\lambda_{min}$ are 0.5
# Input to the Model

The following properties need to be entered in the following order. The superscripts $t$ and $c$ are for tension and compression. The subscripts $\parallel$ and $\perp$ are for the transverse, parallel to the fiber direction of a UD lamina.
  * Longitudinal Modulus $E_{\parallel}$
  * Transverse Modulus $E_{\perp}$
  * Major Poisson's Ratio in 1-2 Plane $\nu_{\perp\parallel}$ (German 2014 VDI Guideline)
  * In-plane Shear Modulus $G_{\parallel\perp}$
  * Longitudinal Tensile Strength $R^t_\parallel$
  * Longitudinal Compressive Strength $R^c_\parallel$
  * Transverse Tensile Strength $R^t_\perp$
  * Transverse Compressive Strength $R^c_\perp$
  * In-plane Shear Strength $R_{\perp\parallel}$
  * Flag for Indicating the Type of Material
     * 1 for CFRP
     * 2 for GFRP
  * Additional Value for Puck $a_0$
  * Additional Value for Puck $\lambda_{min}$
 
 # Output Visualization
 
There are five solution-dependent state variables. They are as follows
  * SDV1 : Fiber Failure in Tension
  * SDV2 : Fiber Failure in Compression
  * SDV3 : Inter Fiber Failure : Mode A
  * SDV4 : Inter Fiber Failure : Mode B
  * SDV5 : Inter Fiber Failure : Mode C

# Verification

<p align="center">
<img src="Images/BC.png" width = 1000 alt>
</p>
<p align="center">
<em>FE Model and Boundary Conditions</em>
</p>

A simple compressive test is performed to check the working of the UMAT. The specimen dimensions are 100 mm x 10 mm. The ply layup is [0°/+45°/-45°/90°/90°/-45°/+45°/0°], and each ply is 0.125 mm thick. The left end of the specimen is fixed in X, Z, ROTX, ROTY, and ROTZ, and the middle of the left end is fixed in Y. A displacement of -1.0 mm is applied on the right end. The material properties are
* $E_{\parallel}$ = 135e3 MPa
* $E_{\perp}$ = 10e3 MPa
* $\nu_{\perp\parallel}$ = 0.25
* $G_{\perp\parallel}$ = 4.3e3 MPa
* $R^t_\parallel$ = 2410 MPa
* $R^c_\parallel$ = 1300 MPa
* $R^t_\perp$ = 86 MPa
* $R^c_\perp$ = 200 MPa
* $R_{\perp\parallel}$ = 152 MPa  
* Type of Material is CFRP
* $a_0$ = 0.5
* $\lambda_{min}$ = 0.5 

<p align="center">
<img src="Images/Puck_eLamX.png" width = 5000 >
</p>
<p align="center">
<em>eLamX² Results</em>
</p>

The same model has been created in eLamX²; a composite calculator developed at TU Dresden. Above are the results of the eLamX² calculator. From the above image, It can be seen that the failure occurs in the 0° ply. Now we shall be comparing these with the Abaqus UMAT results.


<p align="center">
<img src="Images/Ply1.png" width = 5000 >
</p>
<p align="center">
<em>Ply 1</em>
</p>

For the 1st ply, the dominant failure mode is fiber compression (SDV 2), and the failure index is 1.037. The inverse of the failure index is called the Reserve Factor(RF), and its value is 0.964

<p align="center">
<img src="Images/Ply2.png" width = 5000 >
</p>
<p align="center">
<em>Ply 2</em>
</p>

<p align="center">
<img src="Images/Ply3.png" width = 5000 >
</p>
<p align="center">
<em>Ply 3</em>
</p>

For the 2nd and 3rd ply, the dominant mode is an inter-fiber failure: mode C (SDV 5). The failure index is 0.4251, and the reserve factor is 2.352

<p align="center">
<img src="Images/Ply4.png" width = 5000 >
</p>
<p align="center">
<em>Ply 4</em>
</p>

For the 4th ply, the dominant mode is an inter-fiber failure: mode C (SDV 5). The failure index is 0.4631, and the reserve factor is 2.159

The results of the UMAT do match eLamX² results and predict the dominant mode of failure correctly.

# Reference
Knops, M. Analysis of failure in fiber polymer laminates: the theory of Alfred Puck.
Springer Science & Business Media, 2008.
47
