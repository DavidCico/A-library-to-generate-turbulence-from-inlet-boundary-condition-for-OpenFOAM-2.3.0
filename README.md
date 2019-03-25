# A-library-to-generate-turbulence-from-inlet-boundary-condition-for-OpenFOAM-2.3.X
This repository contains a turbulence generator for inlet boundary condition in OpenFOAM 2.3.X.

## Prerequisites

<p align="justify">This library is developed for OpenFOAM 2.3.X, and requires the latter version of the Open Source CFD Toolbox. For more information on how to install this version, the reader is referred to <a href="https://sites.google.com/site/foamguides/installation/installing-openfoam-2-3-x">this web page</a>.</p>

Compile using:
    wmake libso

This will create the library libInflowTurbulence.so in your $FOAM_USER_LIBBIN

Add this to the case controlDict:

    libs ("libInflowTurbulence.so");

And specify for U at inlet with settings fitting your case

    inlet
    {
      overlap         0.5;    // how much the vortons can overlap each other
        L               0.01;    // integral length scale
        eta             1e-04;  // Kolmogorov length
        Cl              6.783;  // Constant used for E(k) 6.783 ni paper
        Ceta            0.4;  // Constant used for E(k) 0.4 in paper
        type            inflowGenerator<homogeneousTurbulence>;
        fluctuationScale (1 1 1);
        referenceField  uniform (10 0 0);
        R               uniform (1 0 0 1 0 1);
        value           uniform (10 0 0);
    }

