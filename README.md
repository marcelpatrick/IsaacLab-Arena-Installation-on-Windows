# IsaacLab-Arena-Installation-on-Windows

# IsaacLab-Arena-Tutorial-with-Docker

# WARNING: 
- This implementation only works on native Linux
- If you are running on windows, even on Ubuntu/WSL/WSL2, it will not work because the Ubuntu container won't be able to access Vulkan (the graphics rendering application). 

# Official Documentation 
1. https://developer.nvidia.com/blog/simplify-generalist-robot-policy-evaluation-in-simulation-with-nvidia-isaac-lab-arena
2. https://isaac-sim.github.io/IsaacLab-Arena/main/index.html
3. https://isaac-sim.github.io/IsaacLab-Arena/main/pages/quickstart/installation.html
4. https://github.com/isaac-sim/IsaacLab-Arena

# Pre-Requisites
- Have Ubuntu 22.04 installed. check ``wsl --list --verbose``
- Have Docker Desktop installed and running (open it and let it running on the background): check ``docker info | findstr "Operating System"``. You should see something like: Operating System: Docker Desktop
- Ubuntu has GPU access: test open Ubuntu and run ``docker run --rm --gpus all nvidia/cuda:12.2.0-base-ubuntu22.04 nvidia-smi``. You should see your GPU info if everything is configured correctly.
