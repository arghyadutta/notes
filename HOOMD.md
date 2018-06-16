# Compiling HOOMD from source
HOOMD is capable of efficiently runnning numerical calculations on GPU (NVIDIAs only afaik) capable devices. This setup method worked on the uni-strasbourg HPC cluster. 

Reminder: Easiest way ofcourse is to use conda/miniconda. This method tries to compile HOOMD from source code. Might be tricky.

### Compiling HOOMD on a HPC
The info provided on the glotzer page is a bit outdated. 

```
module purge
module load compilers/gnu7
module load compilers/cuda-9.1 
module load mpi/openmpi-3.gcc7-cuda9 
module load languages/python-2.7.13.g63 
module load batch/slurm
git clone https://bitbucket.org/glotzer/hoomd-blue.git
cd hoomd-blue
mkdir build
ccmake ../
```
Within the ccmake environment, `press c` to do an intial configuration.
INSTALL PREFIX was also changed to the directory which leads to the clone path. Make sure you provide proper paths for C and CXX compilers.
I had to turn off some parts of the config file in the advanced mode `press t`: 
JIT, VALIDATION, TESTING, HEADERS, VERBOSE MAKEFILE, EMBED CUDA, DOXYGEN HOOMD STYLE, STATIC, TBB.
One known problem was with the MKL LIBRARIES. I removed the paths to these LIBRARIES and it reconfigured perfectly `press c`. `press q` after the configuration completes.

See `cmake.help` in this repo for a configuration that worked for me.

Continue setup:

```
cmake ../
make -j20
```

### Update python path
Depending on where you built the hoomd package, add the path to that directory in your bashrc as a PYTHONPATH :
```
export PYTHONPATH+=:~${USER}/.local/lib/python2.7/site-packages/
```
Reload your bashrc with `source ~/.bashrc`

### Check installation and running on a terminal
IN HPC you might want to load some modules before you run on a terminal:
```
module purge
module load compilers/gnu7 compilers/cuda-9.1 mpi/openmpi-3.gcc7-cuda9  languages/python-2.7.13.g63 batch/slurm
```
To test the hoomd package try a simple code in iPython (on a node that has GPU access):
```
import hoomd
from hoomd import md
hoomd.context.initialize("") #should list the GPU used
from hoomd import deprecated
deprecated.init.create_random(N=1000000, phi_p=0.1)
nl = md.nlist.cell()
lj = md.pair.lj(r_cut=3.0, nlist=nl)
lj.pair_coeff.set('A', 'A', epsilon=1.0, sigma=1.0)
hoomd.md.integrate.mode_standard(dt=0.005)
hoomd.md.integrate.nvt(group=hoomd.group.all(), kT=1.2, tau=0.5)
hoomd.run(10000)
```

### With a HPC queueing system (slurm)
Ask for nodes with GPU capability in the slurm script and put the above hoomd code in a .py file: 

```
#SBATCH -n 2                # N*16 Coeurs
#SBATCH --gres=gpu:2
#SBATCH -t 24:00:00            # for 24 hour
#SBATCH -p grantgpu           ## Sur la file hpcpublic
#SBATCH -A g2017a107
#SBATCH --distribution=cyclic # avoid random distribution of proccess over nodes
#SBATCH --switches=1          # restriction over network topology for efficiency 

source /usr/local/Modules/latest/init/bash
export MAXBLOCK=1

export plog=./pbslog.$SLURM_JOB_ID

module purge
module load  compilers/gnu7 compilers/cuda-9.1 mpi/openmpi-3.gcc7-cuda9 languages/python-2.7.13.g63 batch/slurm

export MPIRUN=mpirun

#ls -la >> $plog
echo "### start program script" >> $plog
#echo "Temperature: $Temperature" >>$plog

set -e
export script_dir=~user/film/

$MPIRUN -np 2 python lj.py >> ${SLURM_JOB_NAME}.${SLURM_JOB_ID}.log

```