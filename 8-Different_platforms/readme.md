## Google colab
This is a beta version, it is possible we install Gromacs on google colab, and run all the simulation there, but it did not really use charmm gui but generate all the necessary Gromacs inputs from scratch, then adapt them to ABF calculation. It is great for learning purpose but may be not as efficient as the DoubleG procedure. 

## On a 7 cpu cluster with non-mpi version of Gromacs, with GPU
```
# Loop over lambda windows
for (( a=0; a<$n_windows; a++ ))
do
  # Loop over simulations within each window
  for (( b=0; b<$n_sims; b++ ))
  do
    # Create directories for each simulation step
    mkdir -p lambda.$a.$b/ENMIN
    mkdir -p lambda.$a.$b/NVT
    mkdir -p lambda.$a.$b/NPT
    mkdir -p lambda.$a.$b/PROD

    # Energy minimization step
    cd lambda.$a.$b/ENMIN
    gmx grompp -f ../../MDP/ENMIN/enmin.$a.$b.mdp -c ../../solv_ions.gro -p ../../topol.top -n ../../index_jz4.ndx -o enmin.tpr
    gmx mdrun -v -stepout 1000 -s enmin.tpr -deffnm enmin -ntmpi 1 -ntomp 7
    cd ../

    # NVT equilibration step
    cd NVT
    gmx grompp -f ../../MDP/NVT/nvt.$a.$b.mdp -c ../ENMIN/enmin.gro -p ../../topol.top -n ../../index.ndx -o nvt.tpr -r ../../solv_ions.gro
    gmx mdrun -stepout 1000 -s nvt.tpr -deffnm nvt -ntmpi 1 -ntomp 7
    cd ../

    # NPT equilibration step
    cd NPT
    gmx grompp -f ../../MDP/NPT/npt.$a.$b.mdp -c ../NVT/nvt.gro -t ../NVT/nvt.cpt -p ../../topol.top -n ../../index.ndx -o npt.tpr -r ../../solv_ions.gro
    gmx mdrun -stepout 1000 -s npt.tpr -deffnm npt -ntmpi 1 -ntomp 7
    cd ../

    # Production run
    cd PROD
    gmx grompp -f ../../MDP/PROD/prod.$a.$b.mdp -c ../NPT/npt.gro -t ../NPT/npt.cpt -p ../../topol.top -n ../../index.ndx -o prod.tpr
    gmx mdrun -stepout 1000 -s prod.tpr -deffnm prod -dhdl dhdl -ntmpi 1 -ntomp 7
    cd ../../
  done
done

```

## On a 40 cpu cluster with mpi version of Gromacs without GPU (This only applicable to gmx_mpi version, with OpenMPI or interlMPI in the environment)

Create a file called 3.sh (you can name as whatever you like as long as it ends with *.sh)

```
#!/bin/bash

for (( a = 0; a <=2; a++ ))
do
    for (( b = 0; b <10; b++ ))
    do
        cd lambda.$a.$b
        mkdir ENMIN
        cd ENMIN
        gmx_mpi grompp -f ../../MDP/ENMIN/enmin.$a.$b.mdp -c ../../solv_ions.gro -p ../../topol.top -n ../../index_jz4.ndx -o enmin.tpr
        mpirun -np 1 gmx_mpi mdrun -ntomp 40 -v -stepout 1000 -s enmin.tpr -deffnm enmin
        cd ../
        mkdir NVT
        cd NVT
        gmx_mpi grompp -f ../../MDP/NVT/nvt.$a.$b.mdp -c ../ENMIN/enmin.gro -p ../../topol.top -n ../../index.ndx -o nvt.tpr -r ../../solv_ions.gro
        mpirun -np 1 gmx_mpi mdrun -ntomp 40 -stepout 1000 -s nvt.tpr -deffnm nvt
        cd ../
        mkdir NPT
        cd NPT
        gmx_mpi grompp -f ../../MDP/NPT/npt.$a.$b.mdp -c ../NVT/nvt.gro -t ../NVT/nvt.cpt -p ../../topol.top -n ../../index.ndx -o npt.tpr -r ../../solv_ions.gro
        mpirun -np 1 gmx_mpi mdrun -ntomp 40 -stepout 1000 -s npt.tpr -deffnm npt
        cd ../
        mkdir PROD
        cd PROD
        gmx_mpi grompp -f ../../MDP/PROD/prod.$a.$b.mdp -c ../NPT/npt.gro -t ../NPT/npt.cpt -p ../../topol.top -n ../../index.ndx -o prod.tpr
        mpirun -np 1 gmx_mpi mdrun -ntomp 40 -stepout 1000 -s prod.tpr -deffnm prod -dhdl dhdl
        cd ../../
    done
done

```
## Example of PBS script to use the above 3.sh on a HPC cluster

Create 4.pbs that refers 3.sh to run the simulation

```
#!/usr/bin/csh
#PBS -l select=1:ncpus=40
#PBS -l mem=80gb
#PBS -l walltime=12:00:00
#PBS -o job.o
#PBS -e job.e

cd $PBS_O_WORKDIR

module load intel-mpi/2021.7.1 
module load gromacs/2022.3

sh 3.sh

```
## Submit your job by

```
qsub 4.pbs
```
## Speed and efficiency
For the Justin's tutorial example, 3HTB protein-ligand system, the speed on the 40 CPU only cluster, with Gromacs-mpi/2023, is 25-28 ns/day, for the compelx branch, 50-55ns/day for the ligand branch. One calculation can be done in about 1.5 day without any GPU involved.
