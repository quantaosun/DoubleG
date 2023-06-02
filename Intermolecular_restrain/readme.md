
When selecting atoms for the restraint potential, several options are available. However, the key principle is to choose atoms that are highly rigid and less prone to relative displacement during the simulation. For small molecules, it is advisable to select atoms close to the center of mass position. In the case of proteins, it is recommended to choose the main chain atoms of amino acids.

Specifically for proteins, it is ideal for the three atoms (denoted as A, B, and C) to form an angle between them ranging from 90 to 120 degrees, with A being the atom closest to the ligand. For the ligand atoms (denoted as a, b, and c), it is preferable to have an angle of 90 degrees, although this requirement is not as strict as the A-B-C angle criterion.

If you are uncertain about how to select atoms, you can consider choosing the main chain atoms of neighboring amino acids that can engage in pi-pi interactions. Alternatively, atoms near the central region of the small molecule that can form hydrogen bonds could also be considered.

For example, when working with the COVID-19 crystal structure using Maestro, you have the flexibility to manually select and define the restraints following the aforementioned guidelines.

<img width="790" alt="image" src="https://user-images.githubusercontent.com/75652473/232963498-57755fba-87e0-4f9c-a151-5bd329c43f1b.png">

```
Ligand: a:4712; b:4685; c: 4707 
Protein: A:2541; B:2526; C:2525 
r(a-A) = 3.00 
angle baA =159.2 
angle aAB =111.8 
dihedral cbaA =-115.5 
dihedral baAB =87.9 
dihedral aABC =3.9
```
Add the following block to the end of the Gromacs topology file

```
[ intermolecular_interactions]
[ bonds ]
; ai     aj    type   bA      kA     bB      kB
 4712    2541  6      0.30   0.0    0.30   4184.0

[ angles ]
; ai     aj    ak     type    thA      fcA        thB      fcB
 4685   4712   2541   1       159.2     0.0        159.2     41.84
 4712   2541   2526   1       111.8     0.0        111.8     41.84

[ dihedrals ]
; ai     aj    ak    al    type     thA      fcA       thB      fcB
 4707  4685  4712  2541    2       -115.5    0.0     -115.5    41.84
 4685  4712  2541  2526    2        87.9     0.0      87.9     41.84
 4712  2541  2526  2525    2         3.9     0.0      3.9      41.84
```
