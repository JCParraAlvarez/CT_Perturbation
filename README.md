# CT_Perturbation
Matlab and Mathematica codes to build a first order perturbation approximation to the solution of continuous-time DGSE models

/* All programs have been tested in Matlab R2018 and Mathematica 11.0.1.0 */

This version: 25/05/2021

MATLAB CODE:

1. The file SGM_PPP_2021_Matlab.m computes a first-order perturbation approximation to the Stochastic Growth Model. It builds a first-order Taylor series expansion to the costates variables using Proposition 1, Theorem 2 and Proposition 3 in the paper. 

	The model has nx = 2 state variables (x = capital, K, and productivity, A) and ny = 2 costate variables (y = VK and VA). The perturbation parameter is denoted by eta>=0. 

	The user must provide the following inputs:
		*Input 1: Parameter values 
		*Input 2: Symbolic definition of control and state variables
		*Input 3: Coefficients a (nx by 1), b (nx by 1) and c (nx^2 by 1) of the system of quasilinear PDEs
		*Input 4: Deterministic steady state, DSS: (x,y,eta) = (xss,yss,0).

	Matrices a, b and c define the model class

	H(x,y,y_x,y_xx) = a(x,y) + y_x b(x,y) + eta y_xx c = 0

	that summarizes the equilibrium in the economy. 

	The solution is given by the policy function y = g(x,eta) which is approximated as

	g(x,eta) = g(xss,0) + gx (x-xss) + geta*eta.

	Using the approximation to the costate functions, the code also reports a first-order approximation to the control variables defined by the first order condition u = u(x,y). For the Stochastic Growth Model, u = consumption. Its approximation is given by

	u(x,eta) = u(xss,0) + ux (x-xss) + ueta*eta.


2. The file SGM_PPP_2021_simple_Matlab.m is a simplified version of SGM_PPP_2021_Matlab.m where only the costate for the capital stock y = VK is approximated. See Section 3.3 of the paper. 

-------
MATHEMATICA CODE:

The file SGM_PPP_2021_Mathematica.nb computes a first- and second-order perturbation approximation to the Stochastic Growth Model. The approximations are built using a brute force approach - it successively  computes the derivatives of the unknown policy functions (y,u)=((VK,VA),C) and evaluates them at the DSS, (x,y,eta) = (xss,yss,0). 

The first step is to define the functional F(x,eta) = H(x,g(x,eta),gx(x,eta),gxx(x,eta)) = 0. From there, the code computes successively all the required derivatives to build the approximats to the policy functions:
	
	"Perfect-foresight" component
	Fx(x,eta) = Fxx(x,eta) = Fxxx(x,eta) = Fxxxx(x,eta) = 0 
	
	and 
	
	"Stochastic" component
	Feta = Fxeta = Fxxeta = Fetaeta = 0. 
