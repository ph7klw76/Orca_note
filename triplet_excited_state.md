
To optimize triplet excited state
'''python
! DEF2-SVP OPT CPCM(Toluene)  # functional you want to use followed by Opt to optimize into ggeometrical minimum in Toluene solvent under Cconductive polarizable continuum model 
%TDDFT  NROOTS  3 # The number of desired roots. It is good to have at least 2 more roots above a desired roots to be optimized
        IRoot 1  #The root to be optimized
        IRootMult Triplet #  optimize the first triplet excited state.
        TRIPLETS TRUE       
END    
%method
        method dft
        functional HYB_GGA_XC_LRC_WPBEH  # using wpbeh
	ExtParamXC "_omega" 0.072945
END
%maxcore 2000  #This sets a limit of 2000 MB (2 GB) of memory per core for the calculation.
%pal nprocs 16 end  # Use 16 processor
* XYZFILE 0 1 EHBIPO0.07294535118797844.xyz

'''



# NOTE
For systems where triplet states are energetically close to singlet states, enabling triplet calculations ensures that these interactions are properly accounted for, which is essential for accurate modeling of photochemical and photophysical properties.

ExtParamXC "_omega" in ORCA is used to modify the 
ω parameter for range-separated hybrid functionals. This parameter controls the separation of short-range and long-range contributions in these functionals. The ExtParamXC syntax allows users to customize this and other parameters provided by the LibXC interface.
