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
