# logger_code
Various versions of Campbell Scientific logger code developed as standard program for OzFlux

Notes:

1) "Opec_extended_v3_3.cr3" is the original code inherited from Ed Swiatek at CSI USA. 
This is the final version of the non-EasyFlux code that CSI produced. It is written in a general
format that allows for different selections of instrumentation via initial boolean variables - on
conditional compile, the compiler strips out the redundant code.
2) There was an error in the original "Opec_extended_v3_3.cr3" code - namely that at line 711, the 
delay on the CSAT3B was 0, and should have been 1 scan. This was noticed by Nico Weigand (JCU), and 
confirmed as an error by Simon Leeds at CSI Australia, who contacted Ed Swiatek. As a result, the
program code "Opec_extended_v3_3_corr.cr3" is identical to the original code in all respects except
that the delay is changed to 1 scan (and associated documentation line in initial comments - line 8).
Any new conditionally-compiled programs should be generated from the corrected version rather than
the original.
