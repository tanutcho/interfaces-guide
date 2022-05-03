#  Using SLURM (IST Cluster)


## IST Cluster
[https://cluster-docs.vistec.ist/](https://cluster-docs.vistec.ist/)

## No brainer Guide by Amrest
[No brainer Guide](https://amrestc.notion.site/No-brainer-Guide-to-SLURM-with-Python-based-program-with-Submit-It-49cd2585306b49f2805e475fa87e18ec)


## Using SLURM with Conda

### SSH to cluster
[Example](https://gist.github.com/topsecret-cs/6c36234c90def65e1754809e6092ddc2)
```console
ssh -i ~/.ssh/vistec_theerawit theerawit@10.204.100.209
```
### Create and install Anaconda environment at ***frontend*** node
```console
1. Get preinstalled Anaconda
module load Anaconda3
```
2. Create an environment fit to your experiment
```console
conda create -n my_env python=3.6.9
```
3. Activate your env and install your dependencies
```console
source ~/.bashrc
conda activate my_env
pip install pip install tensorflow
```
### Create submission file `myjob.sub` to run your python code `my_experiment.py`

```console
vi myjob.sub
```

```
#!/bin/bash
#SBATCH --partition=gpu-cluster
#SBATCH --nodes 1
#SBATCH --mem=35G
#SBATCH --time=72:00:00
#SBATCH --gres=gpu:1     

module load Anaconda3
module load CUDA/10.1
module load cuDNN/7
module load HDF5

source ~/.bashrc
conda activate my_env
python my_experiment.py
```

### Run the submission file
```console
sbatch myjob.sub
```

### View job in queue: `squeue`, `myjob`
```console
myjobs
```

### cancel a job
```console
scancel *jobid*
```
