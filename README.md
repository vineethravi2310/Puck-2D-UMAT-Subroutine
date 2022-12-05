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

