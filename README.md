# DoubleG

<img width="284" alt="image" src="https://github.com/quantaosun/DoubleG/assets/75652473/2f96d6b9-c63c-48fa-90a4-01afb2f3b07c">

### Imperfect situation

In practical terms, setting up the workflow has proven to be challenging for many due to the tedious procedures and expertise required. To address this, we introduce a procedure called doubleG, which involves two calculations using Gromacs. One calculation focuses on the protein-ligand system, while the other focuses solely on the ligand.

Instead of developing new software, I provide a clear and streamlined workflow that integrates reliable online web services with the widely used Gromacs platform. This workflow specifically addresses the critical challenge of determining the absolute free energy of binding in protein-small molecule dynamics simulations, particularly in the early stages of drug discovery. Traditional methods that rely solely on the similarity of small molecules often fall short in accurately calculating relative binding free energies, such as FEP.

By adopting this repeatable and easy-to-set-up workflow, we aim to simplify the complex process that typically requires skilled operators, multiple steps, and substantial computing power. Consequently, it helps overcome the challenges associated with its application while reducing costs.

### Prerequisites:

Create an account on the Charmm GUI web service by visiting https://www.charmm-gui.org/.
Install Gromacs on a Unix-like environment with a minimum of 8 CPUs. Ideally, a decent CPU configuration is recommended.
If available, install Gromacs on a Unix-like environment with more than 8 CPUs and a GPU, preferably Nvidia 3060 or an equivalent model. This configuration enhances computational performance.
Note: Please ensure you fulfill these prerequisites before proceeding with the subsequent steps.

### Previous tutorials

Several tutorials are available online for reference. However, based on my understanding, these workflows often demand a high level of expertise to utilize effectively and can be time-consuming to learn and implement repeatedly.

<img width="909" alt="image" src="https://github.com/quantaosun/DoubleG/assets/75652473/88777929-321c-475a-a4f9-b504e69d6903">


### This procedure

The calculation of absolute binding free energy based on explicit solvent is the focus of this workflow.

Architecture Overview:
In this Double G workflow, there are three key components: CharmmGui, Gromacs, and GPU.

**CharmmGui**: This graphical user interface plays a crucial role in preparing the necessary inputs for the calculations. Compared to command-line based methods, CharmmGui offers a user-friendly interface, making it easier to learn and utilize effectively.

**Gromacs**: One of the most widely used open-source molecular simulation packages, Gromacs, forms the core of the free energy calculations. It provides robust and reliable algorithms for performing these calculations efficiently.

**GPU** Utilization: To enhance computational efficiency and save time, the workflow takes advantage of GPU computing. By leveraging the power of GPUs, the calculations can be accelerated, leading to faster results.

By combining the strengths of CharmmGui, Gromacs, and GPU computing, this workflow aims to provide an accessible and efficient solution for absolute binding free energy calculations.

In this context, "G" also represents the Gbbis free energy, where **G solvent + G complex** are the two data points we need to simulate.

Therefore, we refer to this approach as "Double G" for easier memorization and to distinguish it from other methods.

<img width="615" alt="image" src="https://github.com/quantaosun/DoubleG/assets/75652473/72839200-65b5-4ac5-aed0-9f08808d2a17">


