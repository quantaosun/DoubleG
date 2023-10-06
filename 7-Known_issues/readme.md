
1. modify the solvent /MDP/PROD/ (When running lambda 1.0-1.9 there is an error about rlist or simulated small molecule showing longer bonds and degree than defined cutoff, i.e., rlist )
2. the observed error may related to bonded-lambda, this line should be comment off on the solvent side due to the fact there is no intermolecular restrain (or there is but all being 0, calculated analytically afterwards)
3.in some Gromacs versions, rlist should be kept the same as rcoulomb and rvdw
4. It has been noticed, after execution, Gromacs quietly changed rlist to 1.2, but rvdw and rcoulomb remain unchanged
```
Reading file prod.tpr, VERSION 2022.2 (single precision)
Changing nstlist from 20 to 100, rlist from 1.2 to 1.2
```

