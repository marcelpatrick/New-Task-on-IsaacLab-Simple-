# New-Task-on-IsaacLab-Simple

# Prerequisites

Install IsaacSim and IsaacLab: https://github.com/marcelpatrick/IsaacSim-IsaacLab-installation-for-Windows-Easy-Tutorial?search=1

# Steps

1. Create an External Project: `https://github.com/marcelpatrick/create-a-new-external-isaaclab-project/blob/main/README.md`
   - In this example I created a project named `MyIsaacLabProject`
     
1. Check which library the project was generated with (eg. rsl_rl, rl_games). Check the Script folder in `C:\Users\[YOUR USER]\MyIsaacLabProject\scripts` and look for the library folders. The library will determine which files to change and how to run the task.

1. Rename folder from MyIsaacLabProject to Cartpole
   - Path: `C:\Users\[YOUR USER]\MyIsaacLabProject\source\MyIsaacLabProject\MyIsaacLabProject\tasks\manager_based\MyIsaacLabProject`
     
1. Copy the new task folder from the original [IsaacLab](https://github.com/isaac-sim/IsaacLab) project to your project.
   - In this example we are copying the Ant task: `Isaac-Ant-v0`
   - Origin Path: `"C:\Users\[YOUR USER]\IsaacLab\source\isaaclab_tasks\isaaclab_tasks\manager_based\classic\ant"`
   - Destination Path: `C:\Users\[YOUR USER]\MyIsaacLabProject\source\MyIsaacLabProject\MyIsaacLabProject\tasks\manager_based\ant`
     
1. Rename Project
   - In your external project, find file: Path: `"C:\Users\[YOUR USER]\MyIsaacLabProject\source\MyIsaacLabProject\MyIsaacLabProject\tasks\manager_based\ant\__init__.py"`
   - Rename project's name in id -> Your project's name must contain the "Template-" prefix otherwise it will not register on Gymnasium and you will not be able to run it with your custom parameters. 
   - `id="Template-My-Isaac-Ant-v0",      # << RENAME`

1. Rename Experiment (if running on rsl_rl)
  - If using the rsl_rl library to run this task, change the experiment name in the rsl_rl config file:
  - Path: `"C:\Users\[YOUR USER]\MyIsaacLabProject\source\MyIsaacLabProject\MyIsaacLabProject\tasks\manager_based\ant\agents\rsl_rl_ppo_cfg.py"`
  - `experiment_name = "my_ant" # << RENAME`
  - rl_games will automatically generate a timestamp-based name for each run.

6. Customize **TRAINING** Parameters
  - The Config file will depend on the library you are using.
  - For rl_games:
    - File: `rl_games_ppo_cfg.yaml`.
    - Path: `C:\Users\[YOUR USER]\MyIsaacLabProject\source\MyIsaacLabProject\MyIsaacLabProject\tasks\manager_based\ant\agents\rl_games_ppo_cfg.yaml` 
  - For rsl_rl 
    - file: `rsl_rl_ppo_cfg.py`
    - Path: `C:\Users\[YOUR USER]\MyIsaacLabProject\source\MyIsaacLabProject\MyIsaacLabProject\tasks\manager_based\ant\agents\rsl_rl_ppo_cfg.py`

7. Customize **REWARD** Parameters
  - File: `ant_env_cfg.py`
  - Path: `"C:\Users\[YOUR USER]\MyIsaacLabProject\source\MyIsaacLabProject\MyIsaacLabProject\tasks\manager_based\ant\ant_env_cfg.py"`

8. RUN:
  - In your Anaconda Prompt terminal, at the project root `(env_isaaclab) C:\Users\[YOUR USER]\MyIsaacLabProject>` or inside the VSCode project, run: `python scripts/[LIBRARY]/train.py --task=[YOUR TASK NAME]`. eg:
    - For rsl_rl: run: `python scripts/rsl_rl/train.py --task=Template-My-Isaac-Ant-v0` (make sure you have the rsl_rl library in your Scripts folder)
    - For rl_games: run: `python scripts/rl_games/train.py --task=Template-My-Isaac-Ant-v0` (make sure you have the rl_games library folder in your Scripts folder)
- Exit with `Ctrl C`

9. Read results
 - For rsl_rl:
   - check results in the CLI output  
 - For rl_games:
   - run: `tensorboard --logdir logs/rl_games/ant/2026-02-03_10-18-27` or select the last created folder inside `logs/rl_games/ant`
   - Open the provided localhost address in your browser
