
1. modify the solvent /MDP/PROD/ (When running lambda 1.0-1.9 there is an error about rlist or simulated small molecule shows longer bonds and degree than defined cutoff, i.e., rlist )
2. the observed error may related to bonded-lambda, this line should be comment off in solvent side due to the fact there is no intermolecular restrain (or there is but all being 0, calculated analytically afterwards)
3.in some gromacs version, rlist should be kept the same as rcoulomb and rvdw

