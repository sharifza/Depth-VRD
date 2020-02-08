# Improving Visual Relation Detection using Depth Maps

#### by [Sahand Sharifzadeh](https://www.dbs.ifi.lmu.de/cms/personen/mitarbeiter/sharifzadeh/index.html)<sup>1</sup>, [Sina Moayed Baharlou](https://www.sinabaharlou.com)<sup>2*</sup>, [Max Berrendorf](https://www.dbs.ifi.lmu.de/cms/personen/mitarbeiter/berrendorf/index.html)<sup>1*</sup>, [Rajat Koner](https://www.dbs.ifi.lmu.de/cms/personen/mitarbeiter/koner1/index.html)<sup>1</sup>, [Volker Tresp](https://www.dbs.ifi.lmu.de/cms/personen/professoren/tresp/index.html)<sup>1,3</sup>
<sup>1 </sup> Ludwig Maximilian University, Munich, Germany, <sup>2 </sup> Sapienza University of Rome, Italy<br/>
<sup>3 </sup> Siemens AG, Munich, Germany<br/>
<sup>* </sup> Equal contribution

## Abstract

State-of-the-art visual relation detection methods mostly rely on object information extracted from RGB images 
such as predicted class probabilities, 2D bounding boxes and feature maps. Depth maps can additionally provide
valuable information on object relations, e.g. helping to detect not only spatial relations, such as <i>standing behind</i>,
but also non-spatial relations, such as <i>holding</i>. In this work, we study the effect of using different object information
with a focus on depth maps. To enable this study, we release a new synthetic dataset of depth maps, <i>VG-Depth</i>,
as an extension to Visual Genome (VG). We also note that given the highly imbalanced distribution of relations in VG, 
typical evaluation metrics for visual relation detection cannot reveal improvements of under-represented relations. 
To address this problem, we propose using an additional metric, calling it <i>Macro Recall@K</i>, and demonstrate 
its remarkable performance on VG. Finally, our experiments confirm that by effective utilization of depth maps within a simple,
yet competitive framework, the performance of visual relation detection can be significantly improved.

## Model

<p align="center"><img src="docs/architecture.png" width="720" title="The proposed architecture"></p>
 
## Highlights

* We perform an extensive study on the effect of using different sources of object information 
in visual relation detection. We show in our empirical evaluations using the VG dataset, that our
model can outperform competing methods by a margin of up to 8\% points, even those using external language sources or contextualization.

* We release a new synthetic dataset [<i>VG-Depth</i>](https://drive.google.com/open?id=1-BQcGwsnwS-cYHSWIAkmToSCINUnNZQh), to compensate for the lack of depth maps in Visual Genome.

* We propose <i>Macro Recall@K</i> as a competitive metric for evaluating the visual relation detection performance in highly imbalanced 
datasets such as Visual Genome.

## Results

<p align="center"><img src="docs/results.png" width="720" title="The results of our model compared to other works."></p>

## Paper
For further information, please read our paper [here](https://arxiv.org/abs/1905.00966).
## Bibtex
```
@misc{sah2019improving,
    title={Improving Visual Relation Detection using Depth Maps},
    author={Sahand Sharifzadeh and Sina Moayed Baharlou and Max Berrendorf and Rajat Koner and Volker Tresp},
    year={2019},
    eprint={1905.00966},
    archivePrefix={arXiv},
    primaryClass={cs.CV}
}
```
## Depth Dataset

We release a new dataset called VG-Depth as an extension to Visual Genome. This dataset contains synthetically generated depth maps from Visual Genome images and can be downloaded from the following link: [VG-Depth](https://drive.google.com/open?id=1-BQcGwsnwS-cYHSWIAkmToSCINUnNZQh)

You can see some examples of Visual Genome images and their corresponding depth maps that we have provided in this dataset:
<p align="center"><img src="docs/depth_samples.png" width="720" title="Depth Map Samples"></p>

## Code

### Requirements
The main requirements of the provided code are as follows:

>- Python >= 3.6 </br>
>- PyTorch >= 1.1
>- TorchVision >= 0.2.0 
>- TensorboardX
>- CUDA Toolkit 10.0
>- Pandas
>- Overrides
>- Gdown

### Setup
Please make sure you have Cuda Toolkit 10.0 installed, then you can setup the environment by calling the following script:

```
./setup_env.sh
```

This script will perform the following operations:

1. Install the required libraries.
2. Download the Visual-Genome dataset.
3. Download the Depth version of VG.
4. Download the necessary checkpoints.
5. Compile the CUDA libraries.
6. Prepare the environment.

If you have already installed some of the libraries or downloaded the datasets, you can run the following scripts individually: 
```
./data/fetch_dataset.sh             # Download Visual-Genome
./data/fetch_depth_1024.sh          # Download VG-Depth
./checkpoints/fetch_checkpoints.sh  # Download the Checkpoints
```


### How to Run

Update the config.py file to set the datasets paths, and adjust your PYTHONPATH: (e.g. export PYTHONPATH=/home/sina/Depth-VRD).

To train or evaluate the networks, run the following scripts and select between different models and hyper-parameters by passing the pre-defined arguments:
 
* To train the depth models separately (without the fusion layer): 
```
./scripts/shz_models/train_depth.sh 1.1
``` 
* To train the each modality seperately: 
```
./scripts/shz_models/train_individual.sh 1.1
``` 
* To train the fusion models: 
```
./scripts/shz_models/train_fusion.sh 1.1
``` 

* To evaluate the models: 
```
./scripts/shz_models/eval_scripts.sh 1
``` 
The training scripts will be performed for eight different random seeds and 25 epochs each. 


## Checkpoints 

You can also separately download the full model (LCVD) [here](https://drive.google.com/open?id=1ZkHseT3zA2bk1CBxJ6fhI18GuqwUIAwM). Please note that this checkpoint generates results that are
slightly different that the ones reported in our paper. The reason is that for a fair comparison, we have reported the mean values from evaluations over several models.

## Contributors

This repository is created and maintained by [Sahand Sharifzadeh](https://github.com/sharifza), [Sina Moayed Baharlou](https://github.com/Sina-Baharlou), and [Max Berrendorf](https://github.com/mberr).

## Acknowledgements

The skeleton of our code is built on top of the nicely organized [Neural-Motifs](https://github.com/rowanz/neural-motifs) framework (incl. the rgb data loading pipeline and part of the evaluation code). 
We have upgraded these parts to be compatible with PyTorch 1. To enable a fair comparison of models, our object detection backbone also uses the same Faster-RCNN weights as that work.


