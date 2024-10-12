# Imperial HPC Tutorial

### This tutorial provides an introduction to using Imperial College London's High Performance Computing (HPC) resources, which can be essential for tasks such as conducting literature reviews.

## FAQ:
**Q: What is HPC?**  
**A:** HPC stands for High Performance Computing (aka. Supercomputing).

**Q: Why would I need to use Imperial HPC?**  
**A:** Imperial HPC offers scalable resources, better performance than a typical laptop, and is freely available for academic use.

**Q: Is it difficult to learn how to use?**  
**A:** No, it is relatively straightforward. The main thing you need to learn is how to use a few simple Linux commands.

## Tutorial
Imperial College operates three main HPC clusters:
- **CX3**
- **CX3-Phase 2**
- **HX1**

Users have access to `CX3` and `CX3-Phase 2` by default. For access to `HX1`, a support ticket must be raised.

The official documentation can be found at: [Imperial HPC User Guide](https://icl-rcs-user-guide.readthedocs.io/en/latest/)

### Summary of Steps (Based on the Official Documentation):
1. SSH into the login node.
2. Create a job file.
3. Submit the job.
4. Retrieve your data.

### Important Notes:
- Each cluster has its own login node, and resources are separated. For example, if you log into the `CX3` login node, you cannot submit jobs to `CX3-Phase 2` or `HX1`.
  - CX3: `login.hpc.imperial.ac.uk`
  - CX3-Phase 2: `login.cx3.hpc.ic.ac.uk`
  - HX1: `login.hx1.hpc.ic.ac.uk`
  
- **Login nodes** are used for job management, not for processing data. To process data or debug code, create a JupyterLab session using the RCS Self Service Portal.

## Step 1 - SSH into the login node
### What is SSH?
SSH (Secure Shell) sets up remote, encrypted connections between devices over unsecured networks. Using SSH allows you to control a remote machine.

### SSH Options:
- **Windows**:  
  It is recommended to use [XSHELL](https://www.xshell.com/en/free-for-home-school/), which offers a free version for home and school use.

- **MacOS**:  
  The default terminal can be used for SSH connections.

### Instructions for SSH Setup:

#### Windows (Using XSHELL):
1. Download and install XSHELL.
2. Create a new session.
3. Edit the session details:
   - Session Name: (e.g., Imperial HPC)
   - Host: (e.g., `login.hpc.imperial.ac.uk`)
   - Under "Authentication," enter your short college username and password.
4. Click OK to save.
5. Double-click the session to connect and accept the fingerprint when prompted.

#### Linux:
1. Open the terminal.
2. Type `ssh username@login.hpc.imperial.ac.uk` (replace `username` with your short college username) and press Enter.
3. Type `yes` to accept the fingerprint.
4. Enter your college password when prompted.

## Step 2 - Creating a Job File

### What is a Job File?

In high-performance computing (HPC), a scheduler is typically used to manage resources. When you submit a job to the queue, it waits there until the required resources become available. The job file you create is essentially a shell script that specifies the resources you need and outlines the workflow you want to execute.

Once submitted, you have no further control over the job, unless you choose to remove it from the queue.

### Example Job Files

#### CPU Job Example:
```bash
#!/bin/bash
#PBS -l select=1:ncpus=1:mem=1gb
#PBS -l walltime=00:01:00
#PBS -N hello_world

cd $PBS_O_WORKDIR

module load tools/prod

myprog path/to/input.txt
```

#### GPU Job Example:
```bash
#!/bin/bash
#PBS -l select=1:ncpus=4:mem=24gb:ngpus=1:gpu_type=RTX6000
#PBS -l walltime=00:01:00
#PBS -N hello_world

cd $PBS_O_WORKDIR

module load tools/prod

myprog path/to/input.txt
```

### Explanation of the Job File Elements

- `#PBS -l select=1:ncpus=1:mem=1gb`: Specifies the resources your job requires. 
  - `select` indicates the number of nodes (server nodes) you need.
  - `ncpus` is the number of CPU cores.
  - `mem` specifies the amount of memory (RAM).

- For a GPU job, an additional line like `#PBS -l select=1:ncpus=4:mem=24gb:ngpus=1:gpu_type=RTX6000` is used. 
  - `ngpus` defines the number of GPUs needed.
  - `gpu_type` defines the specific GPU model.

- `#PBS -l walltime=00:01:00`: Defines the maximum runtime of the job. If the job exceeds this time (in the format `hh:mm:ss`), it will be forcibly terminated by the system.

- `#PBS -N hello_world`: Assigns a name to your job, which will appear in the job queue.

- `module load tools/prod`: Loads essential tools for your job. It's recommended to include this line in all job files.

- `myprog.py path/to/input.txt`: This line executes your Python program.

### GPU Types for Different Clusters

Different clusters have varying GPU models available. Here's a table showing which GPU models can be used on specific clusters:

| Cluster      | GPU Models          |
|--------------|---------------------|
| CX3          | RTX6000             |
| CX3-Phase 2  | L40S, A100, A40     |
| HX1          | A100                |


