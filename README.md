# DoubleG

<img width="284" alt="image" src="https://github.com/quantaosun/DoubleG/assets/75652473/2f96d6b9-c63c-48fa-90a4-01afb2f3b07c">

I am not developing any new software, considering the abundance of existing options. Instead, I offer a clear and streamlined workflow that integrates reliable online web services with the widely used Gromacs platform. This approach addresses the critical challenge of determining absolute free energy of binding in protein-small molecule dynamics simulations, especially during the early stages of drug discovery. Traditional methods relying solely on the similarity of small molecules are often insufficient for accurately calculating relative binding free energies, such as FEP. By adopting this repeatable and easy-to-set-up workflow, we simplify the complex process that typically requires skilled operators, multiple steps, and substantial computing power. Consequently, it helps overcome the challenges associated with its application while reducing costs.

### Prerequisites:

Create an account on the Charmm GUI web service by visiting https://www.charmm-gui.org/.
Install Gromacs on a Unix-like environment with a minimum of 8 CPUs. Ideally, a decent CPU configuration is recommended.
If available, install Gromacs on a Unix-like environment with more than 8 CPUs and a GPU, preferably Nvidia 3060 or an equivalent model. This configuration enhances computational performance.
Note: Please ensure you fulfill these prerequisites before proceeding with the subsequent steps.

### Previous tutorials

Several tutorials are available online for reference. However, based on my understanding, these workflows often demand a high level of expertise to utilize effectively and can be time-consuming to learn and implement repeatedly.

<img width="909" alt="image" src="https://github.com/quantaosun/DoubleG/assets/75652473/88777929-321c-475a-a4f9-b504e69d6903">


### This procedure

On a practical sense, the seting up has been quite a headache for many given the tedious procedure and expertise it requires. Here we introduce a procedure called doubleG which means two calculation with Gromacs. One of them involves protein-ligand system and the other involves only ligand.

We will perform two calculations: one for the protein-small molecule system and another for the isolated small molecule system.

In each calculation, the small molecule in the corresponding system will be gradually "eliminated," allowing us to obtain the energy changes in the system after removing the small molecule. The difference between these two values represents the binding free energy between the small molecule and the protein.

Both calculations will be conducted using Gromacs software.

In this context, "G" also represents the Gbbis free energy, where **G solvent + G complex** are the two data points we need to simulate.

Therefore, we refer to this approach as "Double G" for easier memorization and to distinguish it from other methods.

<img width="615" alt="image" src="https://github.com/quantaosun/DoubleG/assets/75652473/72839200-65b5-4ac5-aed0-9f08808d2a17">


