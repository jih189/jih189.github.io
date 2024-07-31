---
layout: archive
title: "Train and Play Your Robot"
permalink: /isaaclab_train_play
---
Now, if you want to train your own robot on task, here is the tutorial. You are welcome. In this tutorial, I will train the Fetch Robot, which is initially not in the IsaacLab, to do the Reach task in the [template](https://github.com/isaac-sim/IsaacLabExtensionTemplate.git).

<H3>Prepare Your Robot for the Task</H3>

For simplicity, you can copy the [Reach task](https://github.com/isaac-sim/IsaacLab/tree/main/source/extensions/omni.isaac.lab_tasks/omni/isaac/lab_tasks/manager_based/manipulation/reach) from the IsaacLab and place it into the tasks folder of the template. As a result, your tasks folder should be like following structure:

- **`tasks/`**
    - `__init__.py`
    - **`locomotion/`**
        - ...
    - **`manipulation/`**
        - `__init__.py`
        - **`reach/`**
            - **`config/`**
            - **`mdp/`**
            - `__init__.py`
            - `reach_env_cfg.py`

In the `reach_env_cfg.py`, as mentioned before, this configuration file contains only the task detail without the robot, so we are not going to modify too much thing here. Because, we have mdp directory here, so we want `reach_env_cfg.py` actually to use the mdp directory here, we will modify `reach_env_cfg.py` only the following parts
<pre style="font-size: 15px;color: white;background-color: #000000; padding: 10px;">
<code><span style="color: yellow;"># import omni.isaac.lab_tasks.manager_based.manipulation.reach.mdp as mdp</span>
import [your template name].tasks.manipulation.reach.mdp as mdp</code>
</pre>

Reset the init_state
<pre style="font-size: 15px;color: white;background-color: #000000; padding: 10px;">
<code>    # world
    ground = AssetBaseCfg(
        prim_path="/World/ground",
        spawn=sim_utils.GroundPlaneCfg(),
        init_state=AssetBaseCfg.InitialStateCfg(pos=(0.0, 0.0, <span style="color: green;">0.0</span>)),
    )</code>
</pre>

Then you also need to comment out the table because Fetch will have collision with it
<pre style="font-size: 15px;color: white;background-color: #000000; padding: 10px;">
<code># table = AssetBaseCfg(
#     prim_path="{ENV_REGEX_NS}/Table",
#     spawn=sim_utils.UsdFileCfg(
#         usd_path=f"{ISAAC_NUCLEUS_DIR}/Props/Mounts/SeattleLabTable/table_instanceable.usd",
#     ),
#     init_state=AssetBaseCfg.InitialStateCfg(pos=(0.55, 0.0, 0.0), rot=(0.70711, 0.0, 0.0, 0.70711)),
# )</code>
</pre>

Then, we can enter the `config` folder. If you want, you can delete `franka` and `ur_10` because they may cause warning about the confliction with the IsaacLab.

For Fetch robot, we need to create a `fetch` folder here. Similar to other `joint_pos_env_cfg.py`, we need to define both configuration classes for the tasks. To do that, we need to import both `mdp` and `ReachEnvCfg` from the task.
<pre style="font-size: 15px;color: white;background-color: #000000; padding: 10px;">
<code>import [your template name].tasks.manipulation.reach.mdp as mdp
from [your template name].tasks.manipulation.reach.reach_env_cfg import ReachEnvCfg</code>
</pre>

Because `ReachEnvCfg` does not define the robot configuration yet, we need to define it here. I will use Fetch Robot as the example
<pre style="font-size: 15px;color: white;background-color: #000000; padding: 10px;">
<code>## Import your custom robot configuration here.
import omni.isaac.lab.sim as sim_utils
from omni.isaac.lab.actuators import ImplicitActuatorCfg
from omni.isaac.lab.assets.articulation import ArticulationCfg

FETCH_USD_PATH = f"{ISAACLAB_ASSETS_DATA_DIR}/Robots/FetchRobot/Fetch/fetch.usd"

FETCH_CFG = ArticulationCfg(
    spawn=sim_utils.UsdFileCfg(
        usd_path=FETCH_USD_PATH,
        articulation_props=sim_utils.ArticulationRootPropertiesCfg(enabled_self_collisions=False),
        activate_contact_sensors=False,
    ),
    init_state=ArticulationCfg.InitialStateCfg(
        joint_pos={
            # base
            "r_wheel_joint": 0.0,
            "l_wheel_joint": 0.0,
            "head_pan_joint": 0.0,
            "head_tilt_joint": 0.0,
            # fetch arm
            "torso_lift_joint": 0.2,
            "shoulder_pan_joint": -1.28,
            "shoulder_lift_joint": 1.51,
            "upperarm_roll_joint": 0.35,
            "elbow_flex_joint": 1.81,
            "forearm_roll_joint": 0.0,
            "wrist_flex_joint": 1.47,
            "wrist_roll_joint": 0.0,
            # # tool
            "r_gripper_finger_joint": 0.01,
            "l_gripper_finger_joint": 0.01,

        },
        joint_vel={".*": 0.0},
    ),
    actuators={
        "fetch_torso": ImplicitActuatorCfg(
            joint_names_expr=["torso_lift_joint"],
            effort_limit=1000.0,
            velocity_limit=1.0,
            stiffness=1e5,
            damping=1e3,
        ),
        "fetch_arm": ImplicitActuatorCfg(
            joint_names_expr=["shoulder_pan_joint", "shoulder_lift_joint", "upperarm_roll_joint", "elbow_flex_joint", "forearm_roll_joint", "wrist_flex_joint", "wrist_roll_joint"],
            effort_limit=87.0,
            velocity_limit=100.0,
            stiffness=1000.0,
            damping=50.0,
        ),
        "fetch_hand": ImplicitActuatorCfg(
            joint_names_expr=["r_gripper_finger_joint", "l_gripper_finger_joint"],
            effort_limit=100.0,
            velocity_limit=0.2,
            stiffness=500,
            damping=50,
        ),
        "fetch_head": ImplicitActuatorCfg(
            joint_names_expr=["head_pan_joint", "head_tilt_joint"],
            effort_limit=10.0,
            velocity_limit=0.2,
            stiffness=100,
            damping=40,
        ),
    },
)
</code>
</pre>

I suggest you provide your robot configuration here because robot may have different initial state for different tasks. For those actuators' parameter, you need to tune them close enough to the real robot. That is important for training later.

Then you can create the complete task configuration class.
<pre style="font-size: 15px;color: white;background-color: #000000; padding: 10px;">
<code>
@configclass
class FetchReachEnvCfg(ReachEnvCfg):
    def __post_init__(self):
        # post init of parent
        super().__post_init__()

        # switch robot to Fetch
        self.scene.robot = FETCH_CFG.replace(prim_path="{ENV_REGEX_NS}/Robot")
        # override events
        self.events.reset_robot_joints.params["position_range"] = (-0.1, 0.1)
        # override rewards
        self.rewards.end_effector_position_tracking.params["asset_cfg"].body_names = [<span style="color: green;">"wrist_roll_link"</span>]
        self.rewards.end_effector_position_tracking_fine_grained.params["asset_cfg"].body_names = [<span style="color: green;">"wrist_roll_link"</span>]
        self.rewards.end_effector_orientation_tracking.params["asset_cfg"].body_names = [<span style="color: green;">"wrist_roll_link"</span>]
        # override actions
        self.actions.arm_action = mdp.JointPositionActionCfg(
            asset_name="robot", joint_names=[".*"], scale=0.5, use_default_offset=True
        )
        # override command generator body
        # end-effector is along x-direction
        self.commands.ee_pose.body_name = <span style="color: green;">"wrist_roll_link"</span>
        self.commands.ee_pose.ranges.pitch = (math.pi / 2, math.pi / 2)


...</code>
</pre>
Here, you need to declare which link of the robot as the end-effector.

Then, you need to provide the configurations for each RL library, and you can use the [example](https://github.com/isaac-sim/IsaacLab/tree/main/source/extensions/omni.isaac.lab_tasks/omni/isaac/lab_tasks/manager_based/manipulation/reach/config/ur_10/agents]) from IsaacLab by changing `reach_ur10` to `reach_fetch` in them. <span style="color: red;">You must provide the configuration file for rsl_rl here. Otherwise, there will be [error](https://github.com/isaac-sim/IsaacLab/issues/541).</span>

Now, you can register your task in `__init__.py`
<pre style="font-size: 15px;color: white;background-color: #000000; padding: 10px;">
<code># Copyright (c) 2022-2024, The Isaac Lab Project Developers.
# All rights reserved.
#
# SPDX-License-Identifier: BSD-3-Clause

import gymnasium as gym

from . import agents, joint_pos_env_cfg

##
# Register Gym environments.
##

gym.register(
    id="Isaac-Reach-Fetch-v0",
    entry_point="omni.isaac.lab.envs:ManagerBasedRLEnv",
    disable_env_checker=True,
    kwargs={
        "env_cfg_entry_point": joint_pos_env_cfg.FetchReachEnvCfg,
        "rl_games_cfg_entry_point": f"{agents.__name__}:rl_games_ppo_cfg.yaml",
        "rsl_rl_cfg_entry_point": f"{agents.__name__}.rsl_rl_ppo_cfg:FetchReachPPORunnerCfg",
        "skrl_cfg_entry_point": f"{agents.__name__}:skrl_ppo_cfg.yaml",
    },
)

gym.register(
    id="Isaac-Reach-Fetch-Play-v0",
    entry_point="omni.isaac.lab.envs:ManagerBasedRLEnv",
    disable_env_checker=True,
    kwargs={
        "env_cfg_entry_point": joint_pos_env_cfg.FetchReachEnvCfg_PLAY,
        "rl_games_cfg_entry_point": f"{agents.__name__}:rl_games_ppo_cfg.yaml",
        "rsl_rl_cfg_entry_point": f"{agents.__name__}.rsl_rl_ppo_cfg:FetchReachPPORunnerCfg",
        "skrl_cfg_entry_point": f"{agents.__name__}:skrl_ppo_cfg.yaml",
    },
)</code>
</pre>

<span style="color: red;">Because we create our task in template, the script `list_envs.py` will not show it.</span>

Once you have done the task, you need to setup your python package by
<pre style="font-size: 15px;color: white;background-color: #000000; padding: 10px;">
<code>python -m pip install -e exts/[your template name]/.</code>
</pre>

<H3>Train Robot</H3>

Because we develop in the template, we need to setup the RL library interface to train. Go to the `scripts`, you can place the RL library interface there. You can copy the examples from [here](https://github.com/isaac-sim/IsaacLab/tree/main/source/standalone/workflows). Then, you need to modify the following part to make the train script to find import your tasks.

<pre style="font-size: 15px;color: white;background-color: #000000; padding: 10px;">
<code># import omni.isaac.lab_tasks  # noqa: F401
import [your template name].tasks</code>
</pre>

So now you can train by the following command in the root of template

<pre style="font-size: 15px;color: white;background-color: #000000; padding: 10px;">
<code>python scripts/skrl/train.py --task [your task name ] --headless</code>
</pre>


<H3>Play Robot</H3>

Similar to the Training, you need to modify the following part in the `play.py`
<pre style="font-size: 15px;color: white;background-color: #000000; padding: 10px;">
<code># import omni.isaac.lab_tasks  # noqa: F401
import [your template name].tasks</code>
</pre>

Then, you can check your trained policy with 
<pre style="font-size: 15px;color: white;background-color: #000000; padding: 10px;">
<code>python scripts/skrl/play.py --task [your task name] --num_envs 32 --checkpoint [/PATH/TO/model.pt]</code>
</pre>

Here is the example of my result

<img src="/images/fetch_reach.png" alt="play fetch reach">