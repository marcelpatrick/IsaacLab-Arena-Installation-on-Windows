# IsaacLab-Arena-Installation-on-Windows

# WARNING: 
- This implementation is meant to work on Windows with a Ubuntu/WSL2 Container.
- For a Linux native implementation, look at: https://github.com/marcelpatrick/IsaacLab-Arena-Installation-on-Linux-Docker/blob/main/README.md


# Official Documentation 
1. https://developer.nvidia.com/blog/simplify-generalist-robot-policy-evaluation-in-simulation-with-nvidia-isaac-lab-arena
2. https://isaac-sim.github.io/IsaacLab-Arena/main/index.html
3. https://isaac-sim.github.io/IsaacLab-Arena/main/pages/quickstart/installation.html
4. https://github.com/isaac-sim/IsaacLab-Arena

# Pre-Requisites
- Have Anaconda Prompt installed
- Have an conda environment with IsaacSim and IsaacLab installed. Check: https://github.com/marcelpatrick/IsaacSim-IsaacLab-installation-for-Windows-Easy-Tutorial. (in this example, the name of our environment is "env_isaaclab") 

```
# Check IsaacLab version (Arena expects 0.47.x)
python -c "import isaaclab; print(f'IsaacLab: {isaaclab.__version__}')"

# Check Isaac Sim and PyTorch
python -c "import torch; print(f'PyTorch: {torch.__version__}, CUDA: {torch.cuda.is_available()}')"

# Check RL frameworks
python -c "import rsl_rl; print('rsl_rl OK')"
python -c "import skrl; print('skrl OK')"

# If any of these fail, STOP here — fix your base environment first
```

# Step 1: Activate your working environment
Open an Anaconda Prompt terminal
``conda activate env_isaaclab``

# Step 2: Clone Arena  
```
git clone https://github.com/isaac-sim/IsaacLab-Arena.git
cd IsaacLab-Arena
```

# Step 3: Initialize the submodules and install dependencies
```
git config submodule.submodules/IsaacLab.url https://github.com/isaac-sim/IsaacLab.git
git config submodule.submodules/Isaac-GR00T.url https://github.com/NVIDIA/Isaac-GR00T.git
git submodule update --init --recursive
```

Install Pinnochio library with scipy and numpy versions that will not conflict to IsaacSim and IsaacLab dependencies:
```
conda install -c conda-forge pinocchio "numpy<2.0.0" scipy==1.15.3 --freeze-installed

pip install onnxruntime lightwheel_sdk
```

# Step 4: Install Arena as a Python package into your existing environment without touching any existing dependencies
```pip install --no-deps -e .```

# Step 5: Check installation worked for all packages and modules
```
# Core packages are installed and findable
python -c "import isaaclab_arena; print('isaaclab_arena OK')"
python -c "import isaaclab; print(f'isaaclab {isaaclab.__version__} OK')"
python -c "import torch; print(f'torch {torch.__version__}, CUDA: {torch.cuda.is_available()}')"

# RL frameworks
python -c "import rsl_rl; print('rsl_rl OK')"
python -c "import skrl; print('skrl OK')"
python -c "import stable_baselines3; print('sb3 OK')"

# Arena submodules exist on disk
dir %USERPROFILE%\IsaacLab-Arena\submodules\IsaacLab
dir %USERPROFILE%\IsaacLab-Arena\submodules\Isaac-GR00T

# Arena's key directories are present
dir %USERPROFILE%\IsaacLab-Arena\isaaclab_arena\environments
dir %USERPROFILE%\IsaacLab-Arena\isaaclab_arena\embodiments
dir %USERPROFILE%\IsaacLab-Arena\isaaclab_arena\tasks
dir %USERPROFILE%\IsaacLab-Arena\isaaclab_arena\examples

# Arena package is editable-installed pointing to the right place
pip show isaaclab-arena
```

# Step 6: Tests
```
pytest -sv -m with_cameras isaaclab_arena/tests/
pytest -sv -m "not with_cameras" isaaclab_arena/tests/
```

# Step 7: Run a first Arena Environment
```
set KMP_DUPLICATE_LIB_OK=TRUE
%USERPROFILE%\IsaacLab\isaaclab.bat -p isaaclab_arena\examples\compile_env_notebook.py
```
