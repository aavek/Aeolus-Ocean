# Aeolus-Ocean

## Description

An all-weather day-and-night simulator that can be implemented as a digital twin for the autonomous navigation of maritime vessels as they attempt to reach waypoints while avoiding collisions with other vessels, obstacles and land.

The project consists of an ocean system (Beaufort 1-11) as well as physics algorithms that handle vessel-water interactions and propulsion. Each vessel has its own target acquisition systems (cameras use Object Detection ([YOLO-X](https://github.com/Megvii-BaseDetection/YOLOX)) to visually locate other vessels on-screen and this data is fused with information extracted from a simulated radar system) to detect all other vessels positional data in its environment. The navigational guidance of each vessel is controlled by an intelligent Agent that has been trained (as single-agents in multiple environments) over a range of different scenarios using Deep Reinforcement Learning and Imitation Learning (PPO) with Unity's Machine Learning Agents Toolkit ([ML-Agents](https://github.com/Unity-Technologies/ml-agents)).

Currently, the project is available in binary form only. It can be downloaded as a [release](https://github.com/aavek/Aeolus-Ocean/releases/tag/v1.0). If there is enough interest in the current work, the source code may become available in the future.

## How to Run

Once you download the [release](https://github.com/aavek/Aeolus-Ocean/releases/tag/v1.0), you can run the program with ```AEOLUS OCEAN.exe```. By clicking on the "Simulation" tab in the main-menu you should be presented with the following setup menu.

![setupmenuevening](https://user-images.githubusercontent.com/93454699/220325004-198d7cb9-366e-48f6-9aac-f24d97ec7163.png)

### Simulation Setup

Each of the controllable setup parameters for the simulation are now described:

| Parameter | Description |
| :---: | --- |
| Number of Environments | Number of environments agents will reach waypoints on. In the source code, this is used to train agents in parallel. |
| Agents Per Environment | Each environment will have this many agents in it. NOTE: (Number of Environments) x (Agents Per Environment) must not exceed 32. |
| Environment Spacing | Spacing in meters between consecutive environments. Environments are arranged so they fill, at maximum, a 4x4 grid. |
| Environment Enclosures | Whether to use walls that restrict travel between environments. In the source code, this can speed up training. |
| Ocean Current Factor | Slider that controls how strong ocean currents are in causing the vessel to drift off course. |

| Waypoint Change Distance | Distance in meters to a waypoint that, when reached, causes a new waypoint to be spawned for the current Agent. |
| Show Waypoint Markers | Whether to show graphics for waypoint markers and navigational arrows. |
| Minimum Waypoint Spawn | Minimum distance beyond which a waypoint will spawn from the Environment center as a percentage of the Environment Spacing. This can exceed 1 if you want waypoints to extend beyond the current environment. |
| Maximum Waypoint Spawn | Maximum distance up to which a waypoint will spawn from the Environment center as a percentage of the Environment Spacing. This can exceed 1 for waypoints beyond the current environment. Must be larger than the minimum waypoint spawn value. |
| Waypoint Type | Choose between random waypoint placement, or hard-coded crossing waypoint / head-on waypoint scenarios. |

| Waypoint Type | Choose between random waypoint placement, or hard-coded crossing waypoint / head-on waypoint scenarios. |
