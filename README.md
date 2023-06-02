# logger_code
Various versions of Campbell Scientific logger code developed as standard program for OzFlux

Code notes:

1) "Opec_extended_v3_3.cr3" is the original code inherited from Ed Swiatek at CSI USA. 
This is the final version of the non-EasyFlux code that CSI produced. It is written in a general
format that allows for different selections of instrumentation via initial boolean variables - on
conditional compile, the compiler strips out the redundant code.
2) There was an error in the original "Opec_extended_v3_3.cr3" code - namely that at line 711, the 
delay on the CSAT3B was 0, and should have been 1 scan. This was noticed by Nico Weigand (JCU), and 
confirmed as an error by Simon Leeds at CSI Australia, who contacted Ed Swiatek to confirm. As a result, 
the program code "Opec_extended_v3_3_corr.cr3" is identical to the original code in all respects except
that the delay is changed to 1 scan (and associated documentation line in initial comments - line 8).
Any new conditionally-compiled programs should be generated from the corrected version rather than
the original.
3) The current code in "OzFlux_std_2023_v1.CR6" has diverged significantly from the original program
in terms of variable names, so cannot simply be reproduced by conditionally compiling the original
program. This is not ideal, but the only alternative would be to change the variable names for all possible
instrument combinations. As it stands, one of the aims with respect to naming conventions is where possible to 
remove instrument names from within variable names. Doing this in the original program would lead to a very 
confusing program!

Design principles:

* no instrument names in variables except where required for identification (see below);
* pre-defined standard variable names (see table 1 and related discussion here: https://github.com/OzFlux/PyFluxPro/wiki/Variable-names-and-attributes) to be used where possible;
* a single table should contain all variables requisite to flux calculation, with site-specific variables stored in ancillary tables;
* the program (and the corresponding physical architecture / wiring of the measurement system) should be such that the core code required to produce the turbulent flux data does not 
need to change from program to program; as such, IRGA, sonic anemometer and T / RH sensor should all wire to logger panel and not to expansion peripherals;
T / RH should be first set of differential or SE ports (IRGA and sonic to standard SDM - generally C1, C2 and C3);
* multiple instrument measurements of the same quantity should be denoted by a relevant dimension (e.g. depth for soil moisture) or otherwise by replicate number;
* adopt umol/m^2/s^1 for CO2 flux - quantities are more intuitive than mg/m^2/s^1, which is generally < 1;
* 1) the general philosophy underlying the removal of instrument names from variable names is that the netCDF data format to which the data is ultimately written
allows metadata to be attached to data. At present, metadata are sourced from control files; ideally, a single meta-database would contain the relevant metadata 
down to instrument level. Regardless, as long as the metadata can be attached to the data downstream in the processing pipeline, it is unnecessary to try to insert
it into variable names. This also has the disadvantage of creating unique variable names from site to site rather than a standardised nomenclature, something we are 
trying to move towards.
* stuff here about pulling configuration data into a separate file. I have given up on this, but woth discussing whether it is a good idea. Consensus seems to be no.

Coming: 
* a comma-delimited text file to tie variable names to variable descriptions
