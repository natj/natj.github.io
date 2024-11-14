---
layout: single
title: "Helsinki cluster access"
author_profile: true
permalink: /group/clusters/
toc: true
share: true
sidebar:
  nav: "general"
image:
  teaser: blank.png
excerpt: "A short user guide for setting up an account at University of Helsinki cluster."
---


This is a short tutorial to help setup a computing account at the University of Helsinki's computing cluster. The guide is only relevant for UH students and staff.

As a very first step, you need to ask your group leader to add you to the cluster user group. After that is done, you can follow these steps to log in and install runko.

## Preliminary steps

First, you need to login to `turso` cluster at least once to initialize your home directory structure:

```bash
ssh -YA username@turso.cs.helsinki.fi
```
where `username` needs to be replaced by your uni-account name. The password is your standard university selected one. The connection only works within the university's eduroam internet network, i.e., you have to be physically at the campus. If you are greeted with the turso terminal, you can continue to the next step.

If you want to connect from outside the university you need to first jump through via e.g., `melkinpaasi.cs.helsinki.fi`. Tips for how to automate this are given below.


## SSH connection

### SSH keys for easier login

Next, you need to identify your machine and update the SSH public keys on the gateway hosts.
This step needs to be done only once per machine that you will use to login (or jump to other machines).

First, generate a public SSH key (if you dont already have one). On your own machine's home directory (i.e., `~/`) with

```bash
mkdir .ssh 
ssh-keygen -t rsa
```
and press enter for the default suggested directory and for passphrase (i.e. it leave empty).

The command generates 
- `.ssh/id_rsa` private ssh key
- `.ssh/id_rsa.pub` public ssh key (for sharing)

In order to whitelist your computer you need to copy the `id_rsa.pub` key to the host machine's SSH config and update the ssh agent. In practice, 

```bash
ssh-add
ssh-copy-id USER@melkinpaasi.cs.helsinki.fi
ssh-copy-id USER@turso.cs.helsinki.fi
```

### SSH shortcut to your .ssh/config

One final touch is to configure your own SSH connections to include `hile` as a known host. The following step need to be done only once per machine that you will use to login to `hile`.

Append to your own machine's `~/.ssh/config` (or create the directory and file if it does not exist)

```bash
Host turso
    HostName turso.cs.helsinki.fi
    User username
    IdentityFile ~/.ssh/id_ed25519
    ProxyJump username@melkinpaasi.cs.helsinki.fi
Host hile
    HostName hile01.it.helsinki.fi
    User username
    IdentityFile ~/.ssh/id_rsa
    ProxyJump username@melkki.cs.helsinki.fi
```
and replace `username` with the university account name (note that it appears in 4 places here). Note that the whitespace on the command is made via tabs (not spaces).

After this, you should be able to connect to `hile` from your own machine with

```bash
ssh hile
```

## Runko installation


### Modules

Next, we will automate the loading of the necessary HPC modules on `hile`. SSH to `hile` and then add to your `~/.bashrc`:

```bash
## hile modules
module purge

# Cray
module load PrgEnv-cray
module load craype-x86-milan # or rome
module load cce
module load craype

# OFI
module load cray-mpich
module load craype-network-ofi
module load libfabric

# shared memory support
module load cray-pmi
module load cray-dsmml
module load cray-openshmemx

# other tools
module load cray-hdf5
module load cray-python
module load cray-libsci
module load perftools-base

export CXX=CC
export CC=cc

source /wrk-kappa/users/$USER/venvs/runko-cray/bin/activate

#--------------------------------------------------
export RUNKODIR=/wrk-kappa/users/$USER/runko

PYTHONPATH="${PYTHONPATH:+${PYTHONPATH}:}$RUNKODIR/"
PYTHONPATH="${PYTHONPATH:+${PYTHONPATH}:}$RUNKODIR/lib"
PYTHONPATH="${PYTHONPATH:+${PYTHONPATH}:}$RUNKODIR/external/corgi/lib"
export PYTHONPATH
```

This loads the correct Cray HPC modules when you login to the cluster.


### Virtual Python environment

Next, we need to initialize our own python virtual environment.
You need to have the correct modules (defined above) loaded so if you have not done so yet, logout and login to load the Cray HPC dev environment.

First, we need to create a directory for storing the virtual python packages with
```bash
cd $RUNKODIR
mkdir venvs
cd venvs
python3 -m venv runko-cray
```

Then, activate the environment with
```bash
source venvs/runko-cray/bin/activate
```
after which you should see the terminal status bar change to 
```bash
(runko-cray) username@hile:~$ 
```

or similar. Note that our `.bashrc` should already have the activation command in it so in the future, when you login back to hile, you should automatically have the correct python environment loaded.

Then, we can install the python requirements (stored and reloaded automatically when we login and activate the venv) with

```bash
pip3 install mpi4py --force-reinstall --no-binary mpi4py 
pip3 install h5py scipy matplotlib numpy
```

The `mpi4py` needs to be installed separately because the mpi from `cray-python` is configured incorrectly (its modules are compiled with GCC, not CC)

The computing environment is now ready for compilation and regular use.


### Runko installation

All simulation files that need to be accessed by the compute nodes have to reside in the `kappa` disk space. Therefore, we will also install all of your scripts there.
First, move to the `kappa` work disk space, and clone the `runko` repository:

```bash
cd /wrk-kappa/users/$USER
git clone --recursive https://github.com/natj/runko.git
```

It is also recommended to modify the `runko/CMakeLists.txt` and activate `hile` specific compiler flags by adding (around line 30):

```bash
set(CMAKE_CXX_FLAGS_RELEASE "-Ofast -flto -ffp=4 -march=znver3 -mtune=znver3 -fopenmp -fsave-loopmark") // cray compiler flags
```

Runko installation is now possible. We can compile the code with

```bash
cd runko
mkdir build
cd build
CC=cc CXX=CC cmake -DPython_EXECUTABLE=$(which python3) -DCMAKE_BUILD_TYPE=Release ..
make -j4
```
After which you should see the compilation take place and the tests being run. Note that the CMake will not find the correct Cray compilers if they are not provided via the prefix `CC=c-compiler CXX=c++-compiler` before the `cmake` call.

## Runko and SLURM usage

### Submitting an example job

The code can be ran by e.g., submitting an example SLURM job in the shock project directory

```bash
cd $RUNKODIR
cd projects/pic-shocks
cd jobs
```
and submitting the example job
```bash
sbatch 1dsig3.hile
```

with the content of `1dsig3.hile` being something like
```bash
#!/bin/bash
#SBATCH -J 1ds3
#SBATCH -p cpu
#SBATCH --output=%J.out
#SBATCH --error=%J.err
#SBATCH -c 1                   # cores per task
#SBATCH --ntasks-per-node=32  # 128 for amd epyc romes
#SBATCH -t 00-03:00:00         # max run time
#SBATCH --nodes=1              # nodes reserved
#SBATCH --mem-per-cpu=7G       # max 7G/128 cores
#SBATCH --distribution=block:block

# SBATCH --exclude=  # exclude some nodes
# SBATCH --nodelist= # white list some nodes

# HILE-C node list
# x3000c0s14b1n0,x3000c0s14b2n0,x3000c0s14b3n0,x3000c0s14b4n0,x3000c0s16b1n0,x3000c0s16b2n0,x3000c0s16b3n0,x3000c0s16b4n0,x3000c0s18b1n0,x3000c0s18b2n0,x3000c0s18b3n0,x3000c0s18b4n0

# specific environment variable settings
export OMP_NUM_THREADS=1
export PYTHONDONTWRITEBYTECODE=true
export HDF5_USE_FILE_LOCKING=FALSE

# Cray optimizations
export MPICH_OFI_STARTUP_CONNECT=1  # create mpi rank connections in the beginning, not on the fly
export FI_CXI_DEFAULT_TX_SIZE=16384 # 4096 # increase max MPI msgs per rank
# export FI_CXI_RDZV_THRESHOLD=16384 # same but for slingshot <2.1
export FI_CXI_RX_MATCH_MODE=hybrid # in case hardware storate overflows, we use software mem

# export FI_OFI_RXM_SAR_LIMIT=524288 # mpi small/eager msg limit in bytes
# export FI_OFI_RXM_BUFFER_SIZE=131072 # mpi msg buffer of 128KiB

# go to working directory
cd $RUNKODIR/projects/pic-shocks/

srun --mpi=cray_shasta python3 pic.py --conf 1dsig3.ini   # Cray
```

This uses hile to run a job in the cpu queue (`-p cpu`) on one node (`--nodes=1`) with 32 cores (`--ntasks-per-node=32`).


### Basic SLURM commands

You can check the status of the SLURM queue with
```bash
squeue
```

and status of your own jobs with

```bash
sacct
```

Sometimes you might also need information about the available partitions which can be accessed with
```bash
sinfo -M all
```























