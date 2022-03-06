# event-stereo
This is a code repo for Learning to Super Resolve Intensity Images from Events

### Maintainer
* [Yeong-oo Nam]

## Table Of Contents
- [Pre-requisite](#pre-requisite)
    * [Hardware](#hardware)
    * [Software](#software)
    * [Dataset](#dataset)
- [Getting Started](#getting-started)
- [Training](#training)
- [Inference](#inference)
    * [Pre-trained Model](#pre-trained-model)

## Pre-requisite
The following sections list the requirements for training/evaluation the model.

### Hardware
Tested on:
- **CPU** - 2 x Intel(R) Xeon(R) Silver 4210R CPU @ 2.40GHz
- **RAM** - 256 GB
- **GPU** - 8 x NVIDIA A100 (40 GB)
- **SSD** - Samsung MZ7LH3T8 (3.5 TB)

### Software
Tested on:
- [Ubuntu 18.04](https://ubuntu.com/)
- [NVIDIA Driver 450](https://www.nvidia.com/Download/index.aspx)
- [NVIDIA Container Toolkit](https://github.com/NVIDIA/nvidia-docker)

### Dataset
Download [DSEC](https://dsec.ifi.uzh.ch/) datasets.

#### 📂 Data Structure
Our folder structure is as follows:
```
DSEC
├── train
│   ├── interlaken_00_c
│   │   ├── calibration
│   │   │   ├── cam_to_cam.yaml
│   │   │   └── cam_to_lidar.yaml
│   │   ├── disparity
│   │   │   ├── event
│   │   │   │   ├── 000000.png
│   │   │   │   ├── ...
│   │   │   │   └── 000536.png
│   │   │   └── timestamps.txt
│   │   └── events
│   │       ├── left
│   │       │   ├── events.h5
│   │       │   └── rectify_map.h5
│   │       └── right
│   │           ├── events.h5
│   │           └── rectify_map.h5
│   ├── ...
│   └── zurich_city_11_c                # same structure as train/interlaken_00_c
└── test
    ├── interlaken_00_a
    │   ├── calibration
    │   │   ├── cam_to_cam.yaml
    │   │   └── cam_to_lidar.yaml
    │   ├── events
    │   │   ├── left
    │   │   │   ├── events.h5
    │   │   │   └── rectify_map.h5
    │   │   └── right
    │   │       ├── events.h5
    │   │       └── rectify_map.h5
    │   └── interlaken_00_a.csv
    ├── ...
    └── zurich_city_15_a                # same structure as test/interlaken_00_a
```

## Getting Started

### Build Docker Image
```bash
git clone [repo_path]
cd event-stereo
docker build -t event-stereo ./
```

### Run Docker Container
```bash
docker run \
    -v <PATH/TO/REPOSITORY>:/root/code \
    -v <PATH/TO/DATA>:/root/data \
    -it --gpus=all --ipc=host \
    event-stereo
```

### Build Deformable Convolution
```bash
cd /root/code/src/components/models/deform_conv && bash build.sh
```

## Training
### Usage
```bash
cd /root/code/scripts
bash distributed_main.sh
```

## Inference
Inference code will be updated soon.

### Pre-trained Model
Pre-trained model will be updated soon.
