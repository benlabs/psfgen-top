Usage

GENERIC
1)Use psfgen the same way as you would when generating a psf for namd
2)instead of writepsf you have to issue a writetop

EXAMPLE: SHORT CELLULOSE CHAIN
1)Download a CHARMM FF for sugars: Parameter file: CSFF_parm.inp Topology file: CSFF_top.inp 
2)start your modified psfgen, load the topology
 -> droppedImage.png
4) define a new segment, create molecules
shortcut: the script to generate the topology can be downloaded: generate_myhg.psfgen
 -> droppedImage_1.png
5) convert molecules from alpha sugar into beta sugars
 -> droppedImage_2.png
6) bond monomers together through a beta-1-4 linkage
 -> droppedImage_3.png
7) (optional) initialize some atomic coordinates
 -> droppedImage_4.png
8) (optional) let psfgen guess remaining coordinates automatically (IC table entries in CHARMM topology file)
 -> droppedImage_5.png
9) write out topology and (optional) coordinates
 -> droppedImage_6.png
this will leave you with a gromacs formatted topology file
10) generate a gromacs box: editconf -f myhg.pdb -d 0.5 -bt cubic
11) solvate box: genbox -cp out.gro -cs -p myhg.top
12) generate configuration file: touch mdout.mdp && grompp -f mdout
13) make index file: make_ndx -f out.gro
14) edit configuration: integrator = steep , energygrps  = AGLC SOL nstenergy                = 1
15) grompp -f mdout -c out.gro -p myhg.top  -n index.ndx
15) mdrun
15) g_energy