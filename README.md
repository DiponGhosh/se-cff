# Event-stereo
This is a code repo for "**Stereo Depth from Events Cameras: Concentrate and Focus on the Future**" - CVPR 2022
[Yeong-oo Nam*](), [Mohammad Mostafavi*](https://smmmmi.github.io/), [Kuk-Jin Yoon](http://vi.kaist.ac.kr/project/kuk-jin-yoon/) and [Jonghyun Choi](http://ppolon.github.io/)(Corresponding author)

If you use any of this code, please cite both following publications:

```bibtex
@inproceedings{nam2022stereo,
  title     =  {Stereo Depth from Events Cameras: Concentrate and Focus on the Future},
  author    =  {Nam, Yeongwoo and Mostafavi, Mohammad and Yoon, Kuk-Jin and Choi, Jonghyun},
  booktitle =  {Proceedings of the IEEE/CVF Conference on Computer Vision and Patter Recognition},
  pages     =  {1-8},
  year      =  {2022}
}
```
```bibtex
@inproceedings{mostafavi2021event,
  title     =  {Event-Intensity Stereo: Estimating Depth by the Best of Both Worlds},
  author    =  {Mostafavi, Mohammad and Yoon, Kuk-Jin and Choi, Jonghyun},
  booktitle =  {Proceedings of the IEEE/CVF International Conference on Computer Vision},
  pages     =  {4258--4267},
  year      =  {2021}
}
```

### Maintainers
* [Yeong-oo Nam]()
* [Mohammad Mostafavi](https://smmmmi.github.io/)

## Table of contents
- [Pre-requisite](#pre-requisite)
    * [Hardware](#hardware)
    * [Software](#software)
    * [Dataset](#dataset)
- [Getting started](#getting-started)
- [Training](#training)
- [Inference](#inference)
    * [Pre-trained model](#pre-trained-model)

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

#### 📂 Data structure
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

## Getting started

### Build docker image
```bash
git clone [repo_path]
cd event-stereo
docker build -t event-stereo ./
```

### Run docker container
```bash
docker run \
    -v <PATH/TO/REPOSITORY>:/root/code \
    -v <PATH/TO/DATA>:/root/data \
    -it --gpus=all --ipc=host \
    event-stereo
```

### Build deformable convolution
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
```bash
cd /root/code
python3 inference.py \
    --data_root /root/data \
    --checkpoint_path <PATH/TO/CHECKPOINT.PTH> \
    --save_root <PATH/TO/SAVE/RESULTS>
```

### Pre-trained model
:gear: You can download pre-trained model from [here](https://drive.google.com/file/d/14_tmyMsXkd1H_0LWWe8GOXa_86OjsboG/view?usp=sharing)

## Benchmark website
The [DSEC website](https://dsec.ifi.uzh.ch) holds the benchmarks and competitions. 

:rocket: Our CVPR 2022 results (this repo), are available in the [DSEC website](https://dsec.ifi.uzh.ch/uzh/disparity-benchmark). We ranked better than the [state-of-the-art method from ICCV 2021](https://openaccess.thecvf.com/content/ICCV2021/papers/Mostafavi_Event-Intensity_Stereo_Estimating_Depth_by_the_Best_of_Both_Worlds_ICCV_2021_paper.pdf) 

:rocket: Our ICCV 2021 paper [Event-Intensity Stereo: Estimating Depth by the Best of Both Worlds](https://openaccess.thecvf.com/content/ICCV2021/papers/Mostafavi_Event-Intensity_Stereo_Estimating_Depth_by_the_Best_of_Both_Worlds_ICCV_2021_paper.pdf) ranked first in the [CVPR 2021 Competition](https://dsec.ifi.uzh.ch/cvpr-2021-competition-results) hosted by the [CVPR 2021 workshop on event-based vision](https://tub-rip.github.io/eventvision2021)
