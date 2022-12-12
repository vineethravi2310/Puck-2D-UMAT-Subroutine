# Puck-2D-Subroutine

The following is a UMAT subroutine for Puck failure criteria in Abaqus. It applies only to unidirectional composites. The general form of the Puck criterion utilizes the entire 3-D state of stress and strain, but this subroutine is used for only 2D elements. For fiber failure, the maximum stress criterion is used. More information regarding the inter-fiber failure can be found [here](http://www2.me.rochester.edu/courses/ME204/nx_help/index.html#uid:id1196302).

# Input to the Model

The following properties need to be entered in the following order.
  * Youngs Modulus in 11 Direction $E_{11}$
  * Youngs Modulus in 22 Direction $E_{22}$
  * Poisson's Ratio in 1-2 Plane $\nu_{12}$
  * Inplane Shear Modulus $G_{12}$
  * Longitudinal Strength in 11 Direction $X_T$
  * Compressive Strength in 11 Direction $X_C$
  * Longitudinal Strength in 22 Direction $Y_T$
  * Compressive Strength in 22 Direction $Y_C$
  * Inplane Shear Strength $S$
  * Flag for Indicating the Type of Material
     * 1 for CFRP
     * 2 for GFRP
 
 # Output Visualization
 
There are five solution-dependent state variables. They are as follows
  * SDV1 : Fiber Failure in Tension
  * SDV2 : Fiber Failure in Compression
  * SDV3 : Inter Fiber Failure : Mode A
  * SDV4 : Inter Fiber Failure : Mode B
  * SDV5 : Inter Fiber Failure : Mode C

# Verification

| ![](Images/BC.png) | 
|:--:| 
| *FE Model and Boundary Conditions* |

A simple tensile test is performed to check the working of the UMAT. The specimen dimensions are 100mm x 10mm. The ply layup is $[0/+45/-45/90]_s$, and each ply is 0.125mm thick. The left end of the specimen is fixed in X, Z, ROTX, ROTY, and ROTZ, and the middle of the left end is fixed in Y. A displacement of 0.15mm is applied on the right end. The material properties are
* $E_{11}$ = 135e3 MPa
* $E_{22}$ = 10e3 MPa
* $\nu_{12}$ = 0.25
* $G_{12}$ = 4.3e3 MPa
* $X_T$ = 2410 MPa
* $X_C$ = 1300 MPa
* $Y_T$ = 86 MPa
* $Y_C$ = 200 MPa
* $S$ = 152 MPa
* Type of Material is CFRP

| ![](Images/Puck_Tensile.png) | 
|:--:| 
| *eLamX Results* |

The same model has been created in eLamX; a composite calculator developed at TU Dresden. Above are the results of the eLamX calculator. From the above image, It can be seen that the failure occurs in the 90° ply. Now we shall be comparing these with the Abaqus UMAT results.


| ![](Images/Ply1.png) | 
|:--:| 
| *Ply 1* |

For the 1st ply, the dominant failure mode is the fiber tension(SDV 1). The failure index is 0.8393. The inverse of the failure index is called the Reserve Factor(RF). The reserve factor for ply 1 is 1.193

| ![](Images/Ply2.png) | 
|:--:| 
| *Ply 2* |

| ![](Images/Ply3.png) | 
|:--:| 
| *Ply 3* |

For the 2nd and 3rd ply, the dominant mode is an inter-fiber failure: mode A (SDV 3). The failure index is 0.9705. The reserve factor for ply 2 and 3 is 1.03

| ![](Images/Ply4.png) | 
|:--:| 
| *Ply 4* |

For the 4th ply, the dominant mode is an inter-fiber failure: mode A (SDV 3). The failure index is 1.615, which means the failure has started as its value is more than 1. The reserve factor is 0.619

The results of the UMAT do match eLamX results and predict the dominant mode of failure correctly.
