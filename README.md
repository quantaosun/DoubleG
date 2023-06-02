# DoubleG

### Prerequest: Account of Charmm GUI webservice.

### The theoritical backgroud is solid but the actual setting up has been remaining extremely challenging 

There are some tutorials online but to the best of my knowledge these workflow requires a high level of expertise to use and takes quite long time to learn and even repeat.

<img width="909" alt="image" src="https://github.com/quantaosun/DoubleG/assets/75652473/88777929-321c-475a-a4f9-b504e69d6903">


### I am not developing any new software on top of already so many, but I do provide a clear workflow that intergrates the good online webservice and widely used Gromacs to tacle the important free energy problem in a repeatable and easy-to-set up manner.

The absolute free energy of binding plays a crucial role in protein-small molecule dynamics simulations, particularly in early-stage drug discovery, when the similarity of small molecules is insufficient for calculating relative binding free energies like FEP. However, this calculation process is highly complex, requiring skilled operators, multiple steps, and significant computing power, thus posing challenges in its application and often resulting in high costs.

### Double G calculaion

On a practical sense, the seting up has been quite a headache for many given the tedious procedure and expertise it requires. Here we introduce a procedure called doubleG which means two calculation with Gromacs. One of them involves protein-ligand system and the other involves only ligand.

<img width="615" alt="image" src="https://github.com/quantaosun/DoubleG/assets/75652473/72839200-65b5-4ac5-aed0-9f08808d2a17">

### Platform supported: It is quite flexible, if you have GPU good, but if not, it also works just a bit slow.

1. CPU only
2. GPU+CPU
