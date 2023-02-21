# Aeolus-Ocean

## Description

An all-weather, day-and-night, simulator that can be implemented as a digital twin for the autonomous navigation of maritime vessels as they attempt to reach waypoints while avoiding collisions with other vessels, obstacles and land.

The project consists of an ocean system (Beaufort 1-11) as well as physics algorithms that handle vessel-water interactions and propulsion. Each vessel has its own target acquisition systems (cameras use Object Detection ([YOLO-X](https://github.com/Megvii-BaseDetection/YOLOX)) to visually locate other vessels on-screen and this data is fused with information extracted from a simulated radar system) to detect all other vessels positional data in its environment. Land is detected with a simplified sonar-like system. The navigational guidance of each vessel is controlled by an intelligent Agent that has been trained (as single-agents in multiple environments) over a range of different scenarios using Deep Reinforcement Learning and Imitation Learning (PPO) with Unity's Machine Learning Agents Toolkit ([ML-Agents](https://github.com/Unity-Technologies/ml-agents)).

Currently, the project is available in binary form only. It can be downloaded as a [release](https://github.com/aavek/Aeolus-Ocean/releases/tag/v1.0). If there is enough interest in the current work, the source code may become available in the future.

## How to Run

Once you download the [release](https://github.com/aavek/Aeolus-Ocean/releases/tag/v1.0), you can safely run the program with ```AEOLUS OCEAN.exe```. The binary is created directly from Unity's build settings, and Windows might ask you to trust it as it may come from an 'unknown publisher'.

By clicking on the "Simulation" tab in the main-menu you should be presented with the following setup menu.

![setupmenuevening](https://user-images.githubusercontent.com/93454699/220325004-198d7cb9-366e-48f6-9aac-f24d97ec7163.png)

### Simulation Setup

Each of the controllable setup parameters (default values shown) for the simulation are now described:

| **Environment Parameters** | Description |
| :---: | --- |
| Number of Environments | Number of environments agents will reach waypoints on. In the source code, this is used to train agents in parallel. |
| Agents Per Environment | Each environment will have this many agents in it. NOTE: (Number of Environments) x (Agents Per Environment) must not exceed 32. |
| Environment Spacing | Spacing in meters between consecutive environments. Environments are arranged so they fill, at maximum, a 4x4 grid. |
| Environment Enclosures | Whether to use walls that restrict travel between environments. In the source code, this can speed up training. |
| Ocean Current Factor | Slider that controls how strong ocean currents are in causing the vessel to drift off course. |

<br>

| **Waypoint Parameters** | Description |
| :---: | --- |
| Waypoint Change Distance | Distance in meters to a waypoint that, when reached, causes a new waypoint to be spawned for the current Agent. |
| Show Waypoint Markers | Whether to show graphics for waypoint markers and navigational arrows. |
| Minimum Waypoint Spawn | Minimum distance beyond which a waypoint will spawn from the Environment center as a percentage of the Environment Spacing. This can exceed 1 if you want waypoints to extend beyond the current environment. |
| Maximum Waypoint Spawn | Maximum distance up to which a waypoint will spawn from the Environment center as a percentage of the Environment Spacing. This can exceed 1 for waypoints beyond the current environment. Must be larger than the minimum waypoint spawn value. |
| Waypoint Type | Choose between random waypoint placement, or hard-coded crossing waypoint / head-on waypoint scenarios. |

<br>

| **Procedural Island Parameters (Perlin Noise)** | Description |
| :---: | --- |
| Generate Island Per Environment | Generates an island at the center of each Environment. |
| Scale | Larger values control how smooth the surface of the island is while smaller values lead to many a more spiky surface. |
| Height Multiplier | Multiplies the height and depth values of the surface by this amount. |
| Falloff Multiplier | Multiplies the depth values at the edges of the island. Larger values mean deeper edges. |
| Octaves | Controls how many levels of perlin noise will be applied for this island. |
| Smooth A & B | As these values increase, the island shape transitions between a pyramid-like shape to a rectangular shape. |
| Persistance | For values of less than 1, controls how the dominant the first layers of perlin noise are over the next consecutive ones. For values of more than 1, this leads to a more spiky surface to more contributions from each noise layer.|
| Lacunarity | Smaller values lead to smoother surfaces while larger values lead to increased surface roughness. |
| Offset X & Y | This can be used to randomize the surface generation process. |

<br>

| **Designated Ego Vessel (DEV) Parameters** | Description |
| :---: | --- |
| DEV ID | Slider that allows the user to select which vessel from this setup will be the DEV. Selecting a DEV tells the program on which vessel to implement the sensors system. |
| DEV Camera | For a given DEV ID, whether to observe the environment from the on-board vessel camera. |
| Computer Vision | Whether to use Deep Learning Computer Vision with object detection to visually locate other vessels on-screen. |
| Sensors | 'Full Dynamic Awareness' allows all vessels to know all positional data of each other. 'Computer Vision and Simulated Radar' uses the DEV's on-board sensors to navigate its environment. |
| Detection Rate | Interval period in seconds by which the object detection algorithm will read a frame and output detections (if any). Larger values lead to better overall performance at the cost of accuracy. |
| Confidence | Threshold for object detections. Smaller values will be stricter while larger values will lead to more false positives. |
| Vision Detection Distance | Distance in meters by which the DEV camera sensor will lock onto the nearest vessel and track it. If the target vessel is further than this distance, tracking stops. |
| Radar Distance | Distance in meters by which the DEV radar sensor will pick up nearby vessels.
| Radar Sweep | Rotations per minute of the radar sweep. Higher values may track nearby vessels more accurately at the cost of not detecting distant ones.

<br>

When each setting is chosen as required, click on "Autonomous Vessel Control".

### During the Simulation

As the simulation is running, the user can choose to allow the autonomous operation to continue or override the control by clicking on the "Autonomous Control" button. This will switch it into a "User Control" mode where the vessel can be controlled by the keyboard arrow keys. A GUI button on the top-left of the screen allows the user to customize weather and lighting conditions. If "Show Waypoint Markers" is on, the green navigational arrow on the top shows the direction towards the next waypoint, while the blue arrow shows the directional vector of the vessels velocity. If rain or snow is enabled in the simulation, camera water drops are generated which can have an adverse impact on target vessel detection.  

(Image) Vessel approaching towards waypoint during the day | (Image) DEV tracking another target vessel at night
:-------------------------:|:-------------------------:
 <img src="https://user-images.githubusercontent.com/93454699/220351883-c5557f2d-7aba-446e-a6cd-bdb64dff0147.png" width="500" />  | <img src="https://user-images.githubusercontent.com/93454699/220360839-1e61cfe1-bf99-4fdf-8c05-a868c1a6921b.png" width="500" />
(GIF) Vessels respect COLREG Rule 14 (head-on) & 16 | (GIF) Vessels respect COLREG Rule 15 (crossing) & 16
 <img src="https://user-images.githubusercontent.com/93454699/220360839-1e61cfe1-bf99-4fdf-8c05-a868c1a6921b.png" width="500" /> | <img src="https://user-images.githubusercontent.com/93454699/220360839-1e61cfe1-bf99-4fdf-8c05-a868c1a6921b.png" width="500" />
 
## Limitations

* Currently, only a single vessel type (motorboat) has been trained for a sufficiently long enough time. 
* Additionally, in this version (v1.0) only the same type of vessels are allowed to be simulated in each environment. Future versions will allow for different vessel types, each with their own Agent Brains.
* Foam is based on a simplified particle system and so may not look great with larger waves.
