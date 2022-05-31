#  Image Colorization
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://github.com/HiteshSharma-github/Auto-Colouration/blob/main/AutoColorization.ipynb)

<p align='center'>
<img src='imgs/teaser.png' width=1000>
</p>

Image colorization is inherently an ill-posed problem with multi-modal uncertainty. Previous methods leverage the deep neural network to map input grayscale images to plausible color outputs directly. Although these learning-based methods have shown impressive performance, they usually fail on the input images that contain multiple objects. The leading cause is that existing models perform learning and colorization on the entire image. In the absence of a clear figure-ground separation, these models cannot effectively locate and learn meaningful object-level semantics. In this paper, we propose a method for achieving instance-aware colorization. Our network architecture leverages an off-the-shelf object detector to obtain cropped object images and uses an instance colorization network to extract object-level features. We use a similar network to extract the full-image features and apply a fusion module to full object-level and image-level features to predict the final colors. Both colorization networks and fusion modules are learned from a large-scale dataset. Experimental results show that our work outperforms existing methods on different quality metrics and achieves state-of-the-art performance on image colorization.


## Prerequisites
* [CUDA 10.1](https://developer.nvidia.com/cuda-10.1-download-archive-update2)
* Python3
* Pytorch >= 1.5
* Detectron2
* OpenCV-Python
* Pillow/scikit-image
* Please refer to the [env.yml](env.yml) for detail dependencies.

## Getting Started
1. Clone this repo:
```sh
git clone https://github.com/hiteshsharma-github/InstColorization
cd InstColorization
```
2. Install [conda](https://www.anaconda.com/).
3. Install all the dependencies
```sh
conda env create --file env.yml
```
4. Switch to the conda environment
```sh
conda activate instacolorization
```
5. Install other dependencies
```sh
sh scripts/install.sh
```

## Pretrained Model
1. Download it from [google drive](https://drive.google.com/open?id=1Xb-DKAA9ibCVLqm8teKd1MWk6imjwTBh).
```sh
sh scripts/download_model.sh
```
2. Now the pretrained models would place in [checkpoints](checkpoints).

## Instance Prediction
Please follow the command below to predict all the bounding boxes fo the images in `example` folder.
```
python inference_bbox.py --test_img_dir example
```
All the prediction results would save in `example_bbox` folder.

## Colorize Images
Please follow the command below to colorize all the images in `example` foler.
```
python test_fusion.py --name test_fusion --sample_p 1.0 --model fusion --fineSize 256 --test_img_dir example --results_img_dir results
```
All the colorized results would save in `results` folder.

* Note: all the images would convert into L channel to colorize in [test_fusion.py's L51](test_fusion.py#L51)


## Acknowledgments
My code borrows heavily from the amazing [colorization-pytorch](https://github.com/richzhang/colorization-pytorch) repository.
