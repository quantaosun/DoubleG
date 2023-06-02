# DoubleG

### Outline Summary 

#### Imagine you have a protein-ligand docked complex or crystal structure and you want to quantify the binding affinity with a much better method above docking scores. 

Taking a PDB bank structure 3HTB as an example, its native ligand is JZ4

1. 3HTB as a complex go through the solutuion builder workflow, refer to ***CharmmGUI_Input_Generator*** folder
2. JZ4 as a ligand go through the solution builder workflow, refer to ***CharmmGUI_Input_Generator*** folder
3. Build ABF folders and copy the two /gromacs folder to /new/complex and /new/solvent respectively, refer to ***DoubleG*** folder
4. copy the 3.sh and 4.pbs into the two folder as well,  ***Job_control*** folder
5. Modify /toppar/LIG.itp and /toppar/PROA.itp, refer to ***PROA_or_LIG.itp_modification*** folder
6. convert PROA.gro or ligand.gro to pdb in pymol, then open in Maestro to determine the [intermolecular_interactions], ie the restrain needed to be added at last section of topol.top, refer to ***Intermolecular_restrain*** folder
7, modify the solvent /MDP/PROD/ (When running lambda 1.0-1.9 there is an error about rlist or simulated small molecule shows longer bonds and degree than defined cutoff, i.e., rlist ), refer to ***Known_issues*** folder
8. Run the simulation, refer to ***DoubleG*** folder
9. Analysis, refer to ***Analysis*** folder and ***Intermolecular_restrain*** folder.

<img width="770" alt="image" src="https://github.com/quantaosun/DoubleG/assets/75652473/ecc4ee2a-4d84-4c82-8489-57b4f8d3e62b">


### Backgroud and introduction

What we could do is the so called alchemical free energy calculation, since this repo is more about operation rather than theory introduction, you could have a look at https://pubs.rsc.org/en/content/articlelanding/2021/sc/d1sc03472c, next we will just call it absolute binding free energy calculation (ABFE) or just calculation for simplicity, ABFE was used to clarify with the relative binding free energy calculations like what Schrodinger's FEP-Plus has provided. 

ABFE calculations have numerous potential applications, such as evaluating the reliability of docked poses. If a researcher is unsure which of three docked poses is the most likely correct pose, each can undergo ABFE calculations, and the one with the best score can be considered the most probable candidate. For a case study of this approach, see https://pubs.acs.org/doi/10.1021/jacs.6b11467, another good reading is https://pubs.acs.org/doi/10.1021/acs.jcim.0c00815

In practical terms, setting up the workflow has proven to be challenging for many due to the tedious procedures and expertise required. To address this, we introduce a procedure called doubleG, which involves two calculations using Gromacs. One calculation focuses on the protein-ligand system, while the other focuses solely on the ligand.

Instead of developing new software, I provide a clear and streamlined workflow that integrates reliable online web services with the widely used Gromacs platform. This workflow specifically addresses the critical challenge of determining the absolute free energy of binding in protein-small molecule dynamics simulations, particularly in the early stages of drug discovery. Traditional methods that rely solely on the similarity of small molecules often fall short in accurately calculating relative binding free energies, such as FEP.

By adopting this repeatable and easy-to-set-up workflow, we aim to simplify the complex process that typically requires skilled operators, multiple steps, and substantial computing power. Consequently, it helps overcome the challenges associated with its application while reducing costs.

### Prerequisites:

1. Create an account on the Charmm GUI web service by visiting https://www.charmm-gui.org/.

2. Install Gromacs on a Unix-like environment with a minimum of 8 CPUs. Ideally, a decent CPU configuration is recommended.
If available, install Gromacs on a Unix-like environment with more than 8 CPUs and a GPU, preferably Nvidia 3060 or above. This configuration enhances computational performance.

Note: Please ensure you fulfill these prerequisites before proceeding with the subsequent steps.

### Previous tutorials

Several tutorials are available online for reference. However, based on my understanding, these workflows often demand a high level of expertise to utilize effectively and can be time-consuming to learn and implement repeatedly.

<img width="971" alt="image" src="https://github.com/quantaosun/DoubleG/assets/75652473/6af81d69-c014-4ea4-9cf5-f72c7b2c1fc5">


### This procedure

The calculation of absolute binding free energy based on explicit solvent is the focus of this workflow.
CharmmGUI has long been used for simple solution simulations, as well as ABFE calculation for NAMD, Amber and Genesis, but to when this repo was created there is no readily available module on CharmmGUI suporting the widely use Gromacs to do so.

Architecture Overview:
In this Double G workflow, there are three key components: CharmmGui, Gromacs, and GPU.

**CharmmGui**: This graphical user interface plays a crucial role in preparing the necessary inputs for the calculations. Compared to command-line based methods, CharmmGui offers a user-friendly interface, making it easier to learn and utilize effectively.

**Gromacs**: One of the most widely used open-source molecular simulation packages, Gromacs, forms the core of the free energy calculations. It provides robust and reliable algorithms for performing these calculations efficiently.

**GPU** Utilization: To enhance computational efficiency and save time, the workflow takes advantage of GPU computing. By leveraging the power of GPUs, the calculations can be accelerated, leading to faster results.

By combining the strengths of CharmmGui, Gromacs, and GPU computing, this workflow aims to provide an accessible and efficient solution for absolute binding free energy calculations.

In this context, "G" also represents the Gbbis free energy, where **G solvent + G complex** are the two data points we need to simulate.

Therefore, we refer to this approach as "Double G" for easier memorization and to distinguish it from other methods.
<img width="770" alt="image" src="https://github.com/quantaosun/DoubleG/assets/75652473/f79c176d-7d52-4b69-9b3b-6dfe4060b2db">

### Where to start with
The stability or repeatibility of this workflow is first based on the first input generation step, which requires you to go through two independent solution builder process on CharmmGUI.

<img width="642" alt="image" src="https://github.com/quantaosun/DoubleG/assets/75652473/d73c7b8f-8b8f-460e-8890-8f80236dbb5d">





