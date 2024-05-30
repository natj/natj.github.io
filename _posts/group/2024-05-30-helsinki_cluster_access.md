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


This is a short tutorial to help setup an computing account at the University of Helsinki's computing cluster. The guide is only relevant for UH students and staff.

As a very first step, you need to contact Joonas to add you to the cluster user group. After that is done, you can follow these steps to log in and install runko.

## Preliminary access

First, test that you can login to `turso` cluster with

```bash
ssh -YA username@turso.cs.helsinki.fi
```
where you need to replace `username` with your uni account name. The connection only works within the university internet network, i.e., you have to be physically at the campus. If you are greeted with the turso terminal, you can continue to the next step.

If you want to connect from outside the university you need to first jump through via e.g., `melkinpaasi.cs.helsinki.fi`. Tips for this below.


## SSH connection

### SSH keys for easier login

A regular ssh connection requires you to type the (university) password on every login. You can make your life a bit easier by adding your SSH public key to the accepted connections on `turso`. 

The following steps need to be done only once per machine that you will use to login to the terminal.

First, we need to generate a public SSH key (if you dont already have one). On your own machine's home directory (i.e., `~/`) execute

```bash
mkdir .ssh 
ssh-keygen
```
and press enter for the default suggested directory and for passphrase (i.e. it leave empty).

The command generates 
- `.ssh/id_rsa` private ssh key
- `.ssh/id_rsa.pub` public ssh key (for sharing)

In practice, print out the public key on your own local machine and copy the content to clipboard with

```bash
cat .ssh/id_rsa.pub
```

Next, we need to add the public keys to the remote machines so they can identify it is you who is logging in. SSH to turso (command above) and copy the content of the `id_rsa.pub` text and paste it to `~/.ssh/authorized_keys`. Then, repeat the same and ssh to `username@melkinpaasi.cs.helsinki.fi` and copy the same key to the file of the same name there as well.

### SSH shortcut to your .ssh/config

One final touch can be done by configuring your own SSH connections to include `turso` as a known host. The following steps need to be done only once per machine that you will use to login to the terminal.

Add to your own machine's `~/.ssh/config`
```
Host turso
    HostName turso.cs.helsinki.fi
    User your_username
    IdentityFile ~/.ssh/id_rsa
    ProxyJump your_username@melkinpaasi.cs.helsinki.fi
```
and replace `your_username` with the university account name (note that it appears in 2 places here).

After this, you should be able to connect to turso from anywhere with

```bash
ssh turso
```

## Runko installation

### Modules

Next, we will automate the loading of the necessary HPC modules on turso. SSH to `turso` and move to the `vakka` work disk space, and clone `runko` there for later access:

```bash
ssh turso
cd /wrk-vakka/users/$USER
git clone --recursive https://github.com/natj/runko.git
```

Then, move back to the turso home directory, create a `modules/runko` folder and copy the module file template there with
```bash
cd ~
mkdir modules
cd modules
mkdir runko
cp /wrk-vakka/users/$USER/runko/archs/modules/5.0.0.lua ~/modules/runko/5.0.0.lua 
```

Next, we need to introduce our own `module` directory to lmod. Its best to automate this by adding to your `~/.bash_profile` on `turso` a line (and create the file if does not exist)
```bash
module use --append /home/your_username/modules
```
where `your_username` needs to be replaced with the real one. Now, when you login to turso, the available module list will be automatically updated.


### Virtual Python environment

Finally, we need to setup the virtual python environment. To do this, first load the (incomplete) modules we just created with
```bash
module use --append /home/$USER/modules
```

and create a python virtual environment on `turso` home directory with
```bash
mkdir venvs
cd ~/venvs
virtualenv runko
```

Then activate the environment with
```bash
source ~/venvs/runko/bin/activate
```
after which you should see the terminal status bar change to 
```bash
(runko) username@turso2:~$ 
```

or similar.

Then, we can install the python requirements (stored and reloaded automatically when we activate the venv) with

```bash
pip install mpi4py h5py scipy matplotlib numpy
```

The computing environment is now ready for compilation.

### Installation

Runko installation is now easy. We login to `turso`, load the `runko` module, 
```bash
ssh turso
module load runko
```

and can compile runko in `/wrk-vakka` (which was the location where we cloned the code in the SSH setup stage) with
```bash
cd /wrk-vakka/users/$USER/runko
mkdir build
cd build
cmake ..
make -j8
```
After which you should see the compilation take place and the tests being run.


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
sbatch 1ds3.turso
```

with the content of `1ds3.turso` being something like
```bash
#!/bin/bash
#SBATCH -J 1ds3              # user-given SLURM job name
#SBATCH -M ukko              # machine name [ukko, kale, carrington, hile]
#SBATCH -p short             # partition; use "sinfo -M all" for options
#SBATCH --output=%J.out      # output file name
#SBATCH --error=%J.err       # output error file name
#SBATCH -t 0-05:00:00        # maximum job duration
#SBATCH --nodes=1            # number of computing nodes
#SBATCH --ntasks-per-node=16 # MPI tasks launched per node
#SBATCH --constraint=amd     # target specific nodes; [amd, intel]
#SBATCH --exclusive          # reserve the full node for the job

# INFO: ukko AMD nodes have 128 EPYC Rome cores

# modules
module use /home/jnattila/modules
module load runko

# HPC configurations
export OMP_NUM_THREADS=1
export PYTHONDONTWRITEBYTECODE=true
export HDF5_USE_FILE_LOCKING=FALSE

# go to working directory
cd $RUNKODIR/projects/pic-shocks/

mpirun -n 16 python pic.py --conf 2dsig3.ini
```

This uses ukko (`-M ukko`) to run a job in the short queue (`-p short`) on one node (`--nodes=1`) with 16 cores (`--ntasks-per-node=16`).


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























