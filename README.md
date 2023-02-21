# Aeolus-Ocean

## Description

An all-weather day-and-night  simulator that can be implemented as a digital twin for the autonomous navigation of maritime vessels as they attempt to reach waypoints while avoiding collisions with other vessels, obstacles and land.

The project consists of an ocean system (Beaufort 1-11) as well as physics algorithms that handle vessel-water interactions and propulsion. Each vessel has its own target acquisition systems (cameras use Object Detection ([YOLO-X](https://github.com/Megvii-BaseDetection/YOLOX)) to visually locate other vessels on-screen and this data is fused with information extracted from a simulated radar system) to detect all other vessels positional data in its environment. The navigational guidance of each vessel is controlled by an intelligent Agent that has been trained (as single-agents in multiple environments) over a range of different scenarios using Deep Reinforcement Learning and Imitation Learning (PPO) with Unity's Machine Learning Agents Toolkit ([ML-Agents](https://github.com/Unity-Technologies/ml-agents)).

Currently, the project is available in binary form only. It can be downloaded as a [release](https://github.com/aavek/Aeolus-Ocean/releases/tag/v1.0). If there is enough interest in the current work, the source code may become available in the future.

## How to Run

Once you download the [release](https://github.com/aavek/Aeolus-Ocean/releases/tag/v1.0), you can run the program with ```AEOLUS OCEAN.exe```. By clicking on the "Simulation" tab in the main-menu you will be presented with the following setup menu.

![setupmenu](https://user-images.githubusercontent.com/93454699/220318083-cb00aaca-970d-46e1-afba-a18ab2121977.png)

### Simulation Setup

Each of the controllable parameters for the simulation are now described:

Number of Environments : Number of environments agents will reach waypoints on. In the source code, this is used to train the agents in parallel.
Agents Per Environment : Each environment will have this many agents within in. Note that (Number of Environments) x (Agents Per Environment) must not exceed 32.

