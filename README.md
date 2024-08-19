# wildwing
### Autonomous UAS Software for In Situ Imageomics Missions

<img src="images/overview.png" alt="Thumbnail" width="600"/>

#### This repo contains software to autonomously track group-living animals using Parrot Anafi drones.

## Instructions for use
#### Hardware Requirements
This tool requires a Parrot Anafi drone and its controller, and a laptop running Ubuntu OS on AMD.

#### Software Requirements
See requirements.txt for required packages.

### Step 1: Set-up hardware
- Power on drone, controller, and laptop.
- Connect drone and controller following the instructions in the FreeFlight app.
- Plug the controller into the laptop using USB-C cable.
- Using [VLC media player](https://www.videolan.org/), connect to drone live-stream. From the “Media” menu of VLC, select “Open network stream”. Enter “rtsp://192.168.53.1/live” in the Network URL field.

### Step 2: Initialize software parameters
Initialize the following parameters in the python scripts. You can use these parameters to customize the mission for specific weather conditions, species, and habitats.
- [controller.py](controller.py)
  - DURATION: number of sections to execute autonomous tracking mission
- [navigation.py](navigation.py)
  - x_dist: move +/- X meters in forward/backward plane
  - x_dist_no_subject: move +/- X meters forward if no subject detected
  - y_dist: move +/- X meters in left/right plane
  - z_dist: move +/- X meters in up/down plane

### Step 3: Launch drone
- Place drone in an area that is clear of obstructions
- Execute ./[launch.sh](launch.sh) from the command line. This will launch the drone, and initialize the log and telemetry files to record the mission data.
```
./launch.sh
```

- Optional: manually maneuver from to a higher altitude using hand-held controller

### Step 3: Monitor the system
- Monitor the drone's PoV using the VLC livestream
- Monitor the YOLO model output and telemetry data in /missions/mission_record_YYYYMMDD_HHMMSS/
- Check logs in /log/outputs_YYYYMMDD_HHMMSS.log

### Step 4: End mission
Once the mission duration is complete, you may continue the autonomous tracking mission, or land the drone using the remote controller.
To continue the mission without first landing, comment out line 111 in [controller.py](controller.py), shown below, and save the file. Run ./[launch.sh](launch.sh)from the terminal to start the new mission.

```
# drone.piloting.takeoff()
```

### Step 5: Analyze video data
This script saves the video recordings, telemetry data, and YOLO outputs for each mission. See the [WildWing HuggingFace data repo](https://huggingface.co/datasets/imageomics/wildwingdeployment) for example outputs.
To automatically label video data with behavior, we recommend using [KABR tools](https://github.com/Imageomics/kabr-tools).


## Overview of WildWing framework
![](images/framework.png)
Framework of the WildWing unmanned aerial system (UAS) autonomous navigation control logic


## Citation
If you use this repo in your work, please use this citation:
```
@software{wildwing2024
  author={Jenna Kline and Kevyn Irizarry and Alison Zhong},
  doi={},
  title={WildWing},
  year={2024},
  url={}
}
```

## Funding Acknowledgements
The [Imageomics Institute](https://imageomics.osu.edu/) is supported by the National Science Foundation Award No. 2118240.

The [ICICLE Institute](https://imageomics.osu.edu/) is funded by the National Science Foundation (NSF) under grant number OAC-2112606.
