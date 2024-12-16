With orca_plotyYou have the following options:

1) Generate Difference Densities directly from CI Vectors by selecting option 6 in the folowing menu


```plaintext
1 - Enter type of plot
       2 - Enter no of orbital to plot
       3 - Enter operator of orbital (0=alpha,1=beta)
       4 - Enter number of grid intervals
       5 - Select output file format
       6 - Plot CIS/TD-DFT difference densities
       7 - Plot CIS/TD-DFT transition densities
       8 - Set AO(=1) vs MO(=0) to plot
       9 - List all available densities
      10 - Perform Density Algebraic Operations

```
2) Generate Difference Densities by selecting option 2 in the algebraic operations menu

```plaintext

Enter a number: 10
-----------------------------------------------------------------------
Available Algebraic Operations:
-----------------------------------------------------------------------
       1 - Pair Densities Addition
       2 - Pair Densities Subtraction
       3 - Pair Densities Multiplication
       4 - Pair Densities Division
       5 - Density Normalization
       6 - Make Natural Transition Orbitals
       7 - Make Natural Difference Orbitals
       8 - Leave Section - Return to Main Manu
3) Generate Natural Difference Orbitals by selecting option 7 in the following menu
```

```plaintext
Enter a number: 10
-----------------------------------------------------------------------
Available Algebraic Operations:
-----------------------------------------------------------------------
       1 - Pair Densities Addition
       2 - Pair Densities Subtraction
       3 - Pair Densities Multiplication
       4 - Pair Densities Division
       5 - Density Normalization
       6 - Make Natural Transition Orbitals
       7 - Make Natural Difference Orbitals
       8 - Leave Section - Return to Main Manu
In particular for tasks 2 and 3 you need to generate the state densities of the ground and excited states
For doing this also for triplets you need to activate the following flags

```plaintext
DoSOC TRUE
        DoMCD TRUE
```
Then in an example similar to yours

```plaintext
! TPSSh DEF2-TZVPD DEF2/J  KEEPTRANSDENSITY
! SMD(H2O) D4
%CIS
        NROOTS 10
        TRIPLETS TRUE
        DOSOC TRUE
        DoMCD TRUE
END

* int 0 1
C 0 0 0 0.00 0.0 0.00
O 1 0 0 1.20 0.0 0.00
H 1 2 0 1.08 120 0.00
H 1 2 3 1.08 120 180.00
*
```
running orca plot and directing towards the NDOs generation menu will give you among many others
The states densities of the ground states "Tdens-CIS-0-0-0-0" and the state density of the first triplet state "Tdens-CIS-1-1-1-1"

```plaintext
    1:                                                       test.P0.tmp
    2:                                                 Tdens-CIS-0-0-0-0
    3:                                                 Tdens-CIS-0-0-0-1
    4:                                                 Tdens-CIS-0-0-0-2
    5:                                                 Tdens-CIS-0-0-0-3
    ...
    123:                                                 Tdens-CIS-1-1-1-1
  124:                                                 Tdens-CIS-1-1-1-2
  125:                                                 Tdens-CIS-1-1-1-3
  126:                                                 Tdens-CIS-1-1-1-4
  127:                                                 Tdens-CIS-1-1-1-5
  128:                                                 Tdens-CIS-1-1-1-6
  129:                                                 Tdens-CIS-1-1-1-7
  130:                                                 Tdens-CIS-1-1-1-8
  131:                                                 Tdens-CIS-1-1-1-9
```    
Having on the desired densities one may proceed to generate the NDOs as

```plaintext
-----------------------------------------------------------------------
Performing Algebraic Operations Over Densities: => MAKE_NDOS
-----------------------------------------------------------------------
Enter FileName for Density[  0]: Tdens-CIS-0-0-0-0
Provide a Scale Factor for Density[  0] (Default => 1.00): 1
Enter FileName for Density[  1]: Tdens-CIS-1-1-1-1
Provide a Scale Factor for Density[  1] (Default => 1.00): 1
-----------------------------------------------------------------------
NATURAL DIFFERENCE ORBITALS GENERATION:
-----------------------------------------------------------------------
Warning: The one-electron matrix doesn't exist - is recalculated (SHARK)
Calculating the overlap matrix            ... done!

------------------------------------------------
NATURAL DIFFERENCE ORBITALS FOR STATE     1 3A  
------------------------------------------------

STATE    1 3A  :  E=   0.133614 au      3.636 eV    29324.8 cm**-1

Threshold for printing occupation numbers 1.0000e-04

     0  : n=  0.49930879
     1  : n=  0.02095662
     2  : n=  0.02095632
     3  : n=  0.00020417
     4  : n=  0.00019744
     5  : n=  0.00018749
     6  : n=  0.00009644
     7  : n=  0.00009644
     8  : n=  0.00007712
     9  : n=  0.00007152
    10  : n=  0.00006368
    11  : n=  0.00006022
    12  : n=  0.00005675

=> Natural Difference Orbitals (donor   ) were saved in Tdens-CIS-0-0-0-0-Tdens-CIS-1-1-1-1.1-3A_ndo-donor.gbw
=> Natural Difference Orbitals (acceptor) were saved in Tdens-CIS-0-0-0-0-Tdens-CIS-1-1-1-1.1-3A_ndo-acceptor.gbw
-----------------------------------------------------------------------
Provide a Number of NDOs to plot (Default => 1): 1
-----------------------------------------------------------------------
-----------------------------------------------------------------------
Reading Donor NDO-file   : Tdens-CIS-0-0-0-0-Tdens-CIS-1-1-1-1.1-3A_ndo-donor.gbw
-----------------------------------------------------------------------
Generating cube file for Donor NDO[0]:=> Tdens-CIS-0-0-0-0-Tdens-CIS-1-1-1-1.1-3A_ndo-donor.gbw.0.cube
-----------------------------------------------------------------------
Reading Acceptor NDO-file   : Tdens-CIS-0-0-0-0-Tdens-CIS-1-1-1-1.1-3A_ndo-acceptor.gbw
-----------------------------------------------------------------------
Generating cube file for Acceptor NDO[0]:=> Tdens-CIS-0-0-0-0-Tdens-CIS-1-1-1-1.1-3A_ndo-acceptor.gbw.0.cube
Similarly of course one can generate the difference densities as
Code: Select all

-----------------------------------------------------------------------
Performing Algebraic Operations Over Densities: => SUBTRACTION
-----------------------------------------------------------------------
Number of Densities to be Processed from the List =>   2:
-----------------------------------------------------------------------
Enter FileName for Density[  0]: Tdens-CIS-0-0-0-0
Provide a Scale Factor for Density[  0] (Default => 1.00): 1
Enter FileName for Density[  1]: Tdens-CIS-0-0-1-1
Provide a Scale Factor for Density[  1] (Default => 1.00): 1
-----------------------------------------------------------------------
INTERPRETTING EQUATION:
-----------------------------------------------------------------------
1/sqrt(N) * [(1.00) * {Tdens-CIS-0-0-0-0} - (1.00) * {Tdens-CIS-0-0-1-1}]
-----------------------------------------------------------------------
Current-settings:
```
