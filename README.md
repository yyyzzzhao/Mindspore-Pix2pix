# Mindspore-Pix2pix
[Mindspore](https://www.mindspore.cn/) is a deep learning framework develop by [Huawei](https://www.huawei.com/cn/?ic_medium=direct&ic_source=surlent). This is an Implementation of [Pix2pix](https://arxiv.org/pdf/1703.10593.pdf). More implementation will be released soon on my [site](https://github.com/yyyzzzhao).
Tutorials about this deep learning framework is on [Mindspore](https://www.mindspore.cn/doc/programming_guide/zh-CN/master/index.html)

## This is the results of our implementation 
- Our label-to-streetview results
<p align='center'>  
  <img src='imgs/cityscapes.png' width='400'/>

- label-to-facades results
<p align='center'>  
  <img src='imgs/facades.png' width='400'/>
</p>

## Some metrics on Cityscapes dataset
- FCN scores in our model

|Parameter|Mean pixel accuracy|Mean class accuracy|Mean class IoU|
|:-|:-:|:-:|:-:|
|G8-D3(TruncNormal)|0.57|0.23|0.14|
|G7-D4(TruncNormal)|0.57|0.22|0.14|
|G8-D4(TruncNormal)|0.61|0.24|**0.16**|
|G8-D3(Normal)|**0.62**|**0.25**|**0.16**|

- Metrics in [paper](https://arxiv.org/pdf/1703.10593.pdf)

|Parameter|Mean pixel accuracy|Mean class accuracy|Mean class IoU|
|:-|:-:|:-:|:-:|
|G8-D3|**0.66**|**0.23**|**0.17**|
|GT|0.80|0.23|0.17|
|GT(test)|0.61|0.23|0.15|

- Detailed each class segmentation results are given below

|Class name     |Accuracy |Iou     |
|:-|:-:|:-:|
|road           | 0.874824|0.671461|
|sidewalk       | 0.278808|0.157644|
|building       | 0.605877|0.465707|
|wall           | 0.000313|0.000310|
|fence          | 0.000480|0.000473|
|pole           | 0.002323|0.002223|
|traffic light  | 0.000137|0.000134|
|traffic sign   | 0.001298|0.001266|
|vegetation     | 0.885950|0.491481|
|terrain        | 0.565743|0.202593|
|sky            | 0.925028|0.790719|
|person         | 0.001581|0.001507|
|rider          | 0.000007|0.000007|
|car            | 0.570559|0.334637|
|truck          | 0.000016|0.000016|
|bus            | 0.000033|0.000032|
|train          | 0.000024|0.000024|
|motorcycle     | 0.000016|0.000016|
|bicycle        | 0.000021|0.000021|

***

**Note:** In above table, G and D means generator and discriminator respectively, and the number means the layers of each part. We have tried Normal and TruncNormal. For testing, we first resize the synthesized images to 1024*2048 and then feed these resized fake images to [This pre-trained FCN](http://people.eecs.berkeley.edu/~tinghuiz/projects/pix2pix/fcn-8s-cityscapes/). Above tables summarized the segmentation results.


## The code and corresponding models will be pulbic soon

## Dataset
- We use the Cityscapes dataset. To train a model on the full dataset, please download it from the [official website](https://www.cityscapes-dataset.com/) (registration required).

## Acknowledgments
Our implementation borrows heavily from [pytorch-CycleGAN-and-pix2pix](https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix).