# Run-gromacs-devcloud
run gromacs on the intel devcloud
the link to tutorial
https://gitlab.com/gromacs/online-tutorials/tutorials-in-progress/-/blob/bkmgit-water-simulation/basic-intro-water/basic-intro-water.md

install gromacs following 
https://github.com/VCCA2021HPC/GetGromacs

login to devcloud
```bash
git clone https://gitlab.com/gromacs/online-tutorials/tutorials-in-progress
cd tutorials-in-progress/basic-intro-water/data
echo "$HOME/GROMACS/gromacs-2021.3-install/bin/gmx grompp -f min.mdp -c water1.gro -p water1.top -o min.tpr" > job1.sh
qsub -l nodes=1:gen9:ppn=2 -d . job1.sh
echo "$HOME/GROMACS/gromacs-2021.3-install/bin/gmx mdrun -s min.tpr -c em.gro" > job2.sh
qsub -l nodes=1:gen9:ppn=2 -d . job2.sh
echo "$HOME/GROMACS/gromacs-2021.3-install/bin/gmx grompp -f nvt.mdp -c em.gro -p water1.top -o nvt.tpr" > job3.sh
qsub -l nodes=1:gen9:ppn=2 -d . job3.sh
echo "$HOME/GROMACS/gromacs-2021.3-install/bin/gmx mdrun -s nvt.tpr" > job4.sh
qsub -l nodes=1:gen9:ppn=2 -d . job4.sh
echo '$HOME/GROMACS/gromacs-2021.3-install/bin/gmx trjconv -s nvt.tpr -f traj_comp.xtc -o traj_comp_whole.pdb -pbc whole <<< "0"' > job5.sh
qsub -l nodes=1:gen9:ppn=2 -d . job5.sh
```
## download files
from your terminal 
```bash
sftp devcloud
cd tutorials-in-progress/basic-intro-water/data
get  *.pdb
exit
```
view pdb files in pymol or Avogadro or similar 
