# DoubleG

<img width="284" alt="image" src="https://github.com/quantaosun/DoubleG/assets/75652473/2f96d6b9-c63c-48fa-90a4-01afb2f3b07c">

I am not developing any new software, considering the abundance of existing options. Instead, I offer a clear and streamlined workflow that integrates reliable online web services with the widely used Gromacs platform. This approach addresses the critical challenge of determining absolute free energy of binding in protein-small molecule dynamics simulations, especially during the early stages of drug discovery. Traditional methods relying solely on the similarity of small molecules are often insufficient for accurately calculating relative binding free energies, such as FEP. By adopting this repeatable and easy-to-set-up workflow, we simplify the complex process that typically requires skilled operators, multiple steps, and substantial computing power. Consequently, it helps overcome the challenges associated with its application while reducing costs.

### Prerequest: 

1. Account of Charmm GUI webservice :https://www.charmm-gui.org/
2. Gromacs installed on a Unix-like environemnt with > 8 CPU (decent CPU) or
3. Gromacs installed on a Unix-like environemnt with > 8 CPU + GPU (> Nvidia 3060 or equvalent)

### The theoritical backgroud is solid but the actual setting up has been remaining extremely challenging 

There are some tutorials online but to the best of my knowledge these workflow requires a high level of expertise to use and takes quite long time to learn and even repeat.

<img width="909" alt="image" src="https://github.com/quantaosun/DoubleG/assets/75652473/88777929-321c-475a-a4f9-b504e69d6903">


### Double G calculaion

On a practical sense, the seting up has been quite a headache for many given the tedious procedure and expertise it requires. Here we introduce a procedure called doubleG which means two calculation with Gromacs. One of them involves protein-ligand system and the other involves only ligand.

We will perform two calculations: one for the protein-small molecule system and another for the isolated small molecule system.

In each calculation, the small molecule in the corresponding system will be gradually "eliminated," allowing us to obtain the energy changes in the system after removing the small molecule. The difference between these two values represents the binding free energy between the small molecule and the protein.

Both calculations will be conducted using Gromacs software.

In this context, "G" also represents the Gbbis free energy, where G solvent + G complex are the two data points we need to simulate.

Therefore, we refer to this approach as "Double G" for easier memorization and to distinguish it from other methods.

<img width="615" alt="image" src="https://github.com/quantaosun/DoubleG/assets/75652473/72839200-65b5-4ac5-aed0-9f08808d2a17">

### Platform supported: It is quite flexible, if you have GPU good, but if not, it also works just a bit slow.

1. CPU only
2. GPU+CPU
