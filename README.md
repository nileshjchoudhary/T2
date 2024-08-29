# T2
to check energetics at any stage.  gmx energy -f ener.edr -o temp.xvg or pr.xvg or te.xvg 

In folder wmsystem

vmd 1met.pdb 

%once visualise the pdb close (x) vmd main

gmx solvate -cp 1met.pdb -cs spc216.gro -o solmet.pdb -maxsol 24

vmd solmet.pdb


%once visualise the pdd close (x) vmd main
cd NVT/
%make sure you are in NVT folder, %visualize existing files
cp ../solmet.pdb .
gmx grompp -p sys.top -f nvt.mdp -c solmet.pdb -o vt.tpr -maxwarn 1
gmx mdrun -s vt.tpr -c nvtout.pdb
%observe the changes edr trr output stucuture 
cd ../NVE/

ls  %observe the exsiting files of NVE folder
cp ../NVT/nvtout.pdb .
cp ../NVT/state.cpt .
 gmx grompp -f nve.mdp -p sys.top -c nvtout.pdb -t state.cpt -o ve.tpr -maxwarn  1
 gmx mdrun -s ve.tpr -c outnve.pdb
 
 gmx trjconv -f traj.trr -s ve.tpr -pbc whole -o view.xtc


 

