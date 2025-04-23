# DynSuperCLEVR

[![arXiv](https://img.shields.io/badge/arXiv-2406.00622-b31b1b.svg)](https://arxiv.org/abs/2406.00622) ![License](https://img.shields.io/github/license/XingruiWang/SuperCLEVR-Physics)


A dynamical 3D scene understanding dataset for Video Question Answering. The scenes are annotated with objects' (1) static properties (**shape**, **color**) and (2) 3D dynamical properties (**3D position**, **velocities**, **external forces**), and (3) physical properties (**mass**, **frictions**, **restitution**); and Collision Event (objects involved, frame). 

<img alt="SuperCLEVR Physics Videos" src="https://github.com/XingruiWang/SuperCLEVR-Physics/blob/master/imgs/merged_animated_grid.gif?raw=true">
<p align="center"><small>(Note: the color space is compressed for visualization)</small></p>

### Related works
- [SuperCLEVR](https://github.com/Lizw14/Super-CLEVR). Visual question answering (VQA) dataset for domain robustness in four factors: visual complexity, question redundancy, concept distribution, concept compositionality.

- [SuperCLEVR-3D](https://github.com/XingruiWang/superclevr-3D-question). A VQA dataset for 3D awareness scene understanding the objects from images including 3D poses, parts, and occlusions. 

## Video Question Answering

We design questions about the dynamical properties under 4D space of objects and their collision events.

There are types of questions: factual question, predictive question and counterfactual question from the generated scenes.



## How to generate your own data

<h3>1. Environment</h3> 
<details>

<summary>Setup Environment</summary>

#### Python version

We use python version 3.10. The python version will affect the compatibility of bpy packages.

#### Install Dependencies

 Please use the following steps to install packages. Our project is built upon [Kubric](https://github.com/google-research/kubric). We modified the original package to control more dynamical properties.

```
pip install -r requirements.txt
```

#### Install bpy

This is the python package for [blender](https://www.blender.org/) software, which is able to be installed from pip now. ([PyPI](https://pypi.org/project/bpy/), [official site](https://www.blender.org/))

```
pip install bpy==3.5
```
If 3.5 is not applicable, 3.4 should also be compatible to this repo.

</details>

### 2. Video rendering

Run `bash run.sh` directly for new scene creation and video rendering. 

Example of generating 100 videos.

```bash
time="$(date +%Y-%m-%d_%H-%M-%S)"
for num in {0..100}
do 
    CUDA_VISIBLE_DEVICES=xx python sim_render_color_defined_load_scene.py \
        --data_dir=assets \
        --job-dir=output/superclevr-physics \
        --scratch_dir=output/tmp/tmp-$time \
        --camera=fixed \
        --height=realistic \
        --iteration=$num \
        --scene_size 5 
done
```

The output folder will be like

```
output/superclevr-physics
└───super_clevr_0
│   └───events.json
|   └───metadata.json
|   └───rgba_00000.png
|   └───rgba_00001.png
|   └───...
|   └───rgba_00120.png
└───super_clevr_1
│   └───events.json
|   └───metadata.json
|   └───rgba_00000.png
|   └───rgba_00001.png
|   └───...
|   └───rgba_00120.png
```

## Citation
```
@article{wang2024compositional,
  title={Compositional 4D Dynamic Scenes Understanding with Physics Priors for Video Question Answering},
  author={Wang, Xingrui and Ma, Wufei and Wang, Angtian and Chen, Shuo and Kortylewski, Adam and Yuille, Alan},
  journal={arXiv preprint arXiv:2406.00622},
  year={2024}
}
```

<!--
## Video Question Answering

### 1. Factual questions

### 2. Predictive questions

### 3. Counterfactual questions
-->
