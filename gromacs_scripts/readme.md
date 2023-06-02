
Change the lambda desity of solvent
write 4 individual mdp file for enmin, nvt, npt, and prod
change the 20 lambda plan to 30, also include the bonded-lambda, which allwo small molecule to be solt between bonded atoms.

then duplicate each to 30 files with initial-lambda = $LAMBDA$

```
for i in {1..29}
do
    cp /path/to/source/file /path/to/destination/new_file_$i
done

```
replace $LAMBDA$ to $i

```
for i in {0..29}
do
    awk '{gsub(/\$LAMBDA\$/, "'"$i"'")}1' enmin.$i.mdp > enmin.$i.mdp.tmp
    mv enmin.$i.mdp.tmp enmin.$i.mdp
done

```
then change file name format from XX.$i.mdp to XX.a.b.mdp

```
for i in {0..29}
do
    new_i1=$((i / 10))
    new_i2=$((i % 10))
    mv enmin.$i.mdp enmin.$new_i1.$new_i2.mdp
done

```
