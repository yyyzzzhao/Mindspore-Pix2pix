- label-to-streetview results

<p align='center'>  
  <img src='imgs/cityscapes.png' width='400'/>
</p>

- label-to-facades results

<p align='center'>  
  <img src='imgs/facades.png' width='400'/>
</p>

# Contents

- Pix2pix description

- Model Archetecture

- Dataset

- Features

- Environment Requirements

- Quick Start

- Script Description

- Model Description

- Description of Random Situation

- ModelZoo Homepage

# Pix2pix description

Pix2pix model is a conditional GAN, which includes two modules--generator and discriminator. This model transforms an input image into a corresponding output image. The essence of the model is the mapping from pixel to pixel. In the generator part, the model can be any pixel to pixel mapping network (and in the raw paper, the author proposed to use Unet or Resnet). In the discriminator part, a patch GAN is used to judge whether each N*N patches is fake or true, thus can improve the reality of the generated image.

[Paper](https://arxiv.org/pdf/1703.10593.pdf)Isola P , Zhu J Y , Zhou T , et al. Image-to-Image Translation with Conditional Adversarial Networks[J]. 2016.

# Model Architecture

- Generator (Unet)
Encoder:  C64-C128-C256-C512-C512-C512-C512-C512
Decoder:  CD512-CD1024-CD1024-C1024-C1024-C512-C256-C128

- Discriminator
C64-C128-C256-C512

C is Convlution and CD is Convolution followed by concatenate. The kernel size is 4×4 both in generator and descriminator.

# Dataset

Dataset used: [Cityscapes](https://www.cityscapes-dataset.com/)

	Dataset size: 105M, 3475 images, downsample to 256*256.
    	2975 train images 
		500 validation images
	Data format：.png images

Dataset used can refer to [paper](http://www.cv-foundation.org/openaccess/content_cvpr_2016/html/Cordts_The_Cityscapes_Dataset_CVPR_2016_paper.html).

# Features

** G and D alternating train**

# Environment Requirements

+ Hardware（GPU）

+ Framework

	+ [Mindspore](https://www.mindspore.cn/)

# Quick Start

- run on GPU

```
# run training example
python pix2pix.py --phase train

# run metric values caculation example
python evaluate.py
```

To caculate metic values, please install [Caffe](http://caffe.berkeleyvision.org/) and download pretrained [FCN](http://people.eecs.berkeley.edu/~tinghuiz/projects/pix2pix/fcn-8s-cityscapes/fcn-8s-cityscapes.caffemodel) model.

# Script Description

## Script and Sample Code

```
├── model_zoo
    ├── README.md                          // descriptions about all the models
    ├── pix2pix        
        ├── README.md                    // descriptions about pix2pix
        ├── scripts 
        │   ├──run_train.sh             // shell script for training on GPU
        │   ├──run_eval.sh              // shell script for evaluation on GPU
        ├── src 
        │   ├──dataset.py             // creating dataset
        │   ├──model.py          // pix2pix architecture
        │   ├──utils.py            // helper define 
        ├── pix2pix.py               // training script 
        ├── evaluate.py               //  evaluation script 
```

# Script Parameters

# Training Process

- run on GPU

`python pix2pix.py`

```
epoch: 1 step: 10, g_loss 29.128304 d_loss 0.72615474
epoch: 1 step: 20, g_loss 28.025646 d_loss 0.8659742
epoch: 1 step: 30, g_loss 19.780151 d_loss 0.6306171
```

The model checkpoint will be saved in the **/ckpt** directory.


# Evaluation Process

- After training process ended, the model perform prediction on validation dataset automaticly. The predicted results will saved at directory **/result_cityscapes**.

- To caculate metric values, the [Caffe](http://caffe.berkeleyvision.org/) is needed to installed and please download pretrained [FCN](http://people.eecs.berkeley.edu/~tinghuiz/projects/pix2pix/fcn-8s-cityscapes/fcn-8s-cityscapes.caffemodel) model. The FCN score will be given by:
`python evaluate.py`
And the output report will be generated at directory **/submit**
```
Mean pixel accuracy: 0.636858
Mean class accuracy: 0.253351
Mean class IoU: 0.168609
```

# Model Description

## Performance

|Parameter|Mean pixel accuracy|Mean class accuracy|Mean class IoU|
|:-|:-:|:-:|:-:|
|G8-D3(TruncNormal)|**0.64**|**0.25**|**0.17**|
|G7-D4(TruncNormal)|0.57|0.22|0.14|
|G8-D4(TruncNormal)|0.61|0.24|0.16|
|G8-D3(Normal)|0.62|**0.25**|0.16|

- Metrics in [paper](https://arxiv.org/pdf/1703.10593.pdf)

|Parameter|Mean pixel accuracy|Mean class accuracy|Mean class IoU|
|:-|:-:|:-:|:-:|
|G8-D3|**0.66**|**0.23**|**0.17**|
|GT|0.80|0.23|0.17|
**Compare:** In our implementation, the **Mean pixel accuracy** slightly droped, while the **Mean class accuracy** increased by 0.02 **(0.23 --> 0.25)**. The **Mean class IoU** keeps the same with raw implementation.

- Detailed each class segmentation results are given below

|Class name     |Accuracy |Iou     |
|:-|:-:|:-:|
|road           | 0.907593|0.695943|
|sidewalk       | 0.270474|0.179812|
|building       | 0.561524|0.458200|
|wall           | 0.000225|0.000223|
|fence          | 0.000645|0.000639|
|pole           | 0.002148|0.002037|
|traffic light  | 0.000176|0.000171|
|traffic sign   | 0.000772|0.000751|
|vegetation     | 0.939161|0.509794|
|terrain        | 0.581532|0.235047|
|sky            | 0.911143|0.776436|
|person         | 0.002126|0.002021|
|rider          | 0.000015|0.000015|
|car            | 0.636050|0.342392|
|truck          | 0.000020|0.000020|
|bus            | 0.000010|0.000010|
|train          | 0.000012|0.000012|
|motorcycle     | 0.000020|0.000019|
|bicycle        | 0.000026|0.000026|

- Parameters 

|Parameters         | GPU                        |
|:-|:-:|
|Model Version      |  pix2pix                   |
|Resource           |  Titan V100                |
|uploaded Date      | 11/12/2020 (month/day/year)|
|MindSpore Version  | 1.0                        |
|Dataset            | Cityscapes			     |
|Training Parameters|epoch=200, step: 595000, batch_size=1, lr=2*1e-3|
|Optimizer          | Adam(beta1=0.5, beta2=0.999)|
|Loss Function      | L1, Binary Cross Entropy   |
|Loss		        | G: 10~30  D: 0.01~1.5      |
|Speed				| 1pc: 53 ms/step            |
|Total time         | 1pc: 8.7 hours			 |
|Parameters (M)     | G: 207  D:105              |

# Description of Random Situation

In dataset.py, we used random crop and random flip for data augmentation. And in pix2pix model, a dropout layer is used.

# ModelZoo Homepage
Please check the official [homepage](https://gitee.com/mindspore/mindspore/tree/master/model_zoo).
