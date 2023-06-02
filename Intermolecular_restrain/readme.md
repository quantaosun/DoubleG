
When selecting atoms for the restraint potential, several options are available. However, the key principle is to choose atoms that are highly rigid and less prone to relative displacement during the simulation. For small molecules, it is advisable to select atoms close to the center of mass position. In the case of proteins, it is recommended to choose the main chain atoms of amino acids.

Specifically for proteins, it is ideal for the three atoms (denoted as A, B, and C) to form an angle between them ranging from 90 to 120 degrees, with A being the atom closest to the ligand. For the ligand atoms (denoted as a, b, and c), it is preferable to have an angle of 90 degrees, although this requirement is not as strict as the A-B-C angle criterion.

If you are uncertain about how to select atoms, you can consider choosing the main chain atoms of neighboring amino acids that can engage in pi-pi interactions. Alternatively, atoms near the central region of the small molecule that can form hydrogen bonds could also be considered.

For example, when working with the COVID-19 crystal structure using Maestro, you have the flexibility to manually select and define the restraints following the aforementioned guidelines.
