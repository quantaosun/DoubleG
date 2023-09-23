### Note, all mdp files provided are not easy to use, you need to use them as a template and with the help of the script below to generate multiple mdp files for each of them, replacing $LAMBDA$ with correct values that essentially control the free energy calculation process.
Change the lambda density of solvent
write 4 individual mdp files for enmin, nvt, npt, and prod
change the 20 lambda plan to 30, and also include the bonded lambda, which allows small molecule to be solt between bonded atoms.

### Build mdp file structure

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
then change the file name format from XX.$i.mdp to XX.a.b.mdp

```
for i in {0..29}
do
    new_i1=$((i / 10))
    new_i2=$((i % 10))
    mv enmin.$i.mdp enmin.$new_i1.$new_i2.mdp
done

```

### Build lambda file structure

```
for (( a = 0; a <=1; a++ ));
do 
  for (( b = 0; b <10; b++ ))
    do
    mkdir lambda.$a.$b
done
done
```
The lambda simulation folder and MDP mdp file should be in such a relevant path that as shown in 3.sh
