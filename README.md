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
|G8-D3(TruncNormal)|**0.64**|**0.25**|**0.17**|
|G7-D4(TruncNormal)|0.57|0.22|0.14|
|G8-D4(TruncNormal)|0.61|0.24|0.16|
|G8-D3(Normal)|0.62|**0.25**|0.16|

- Metrics in [paper](https://arxiv.org/pdf/1703.10593.pdf)

|Parameter|Mean pixel accuracy|Mean class accuracy|Mean class IoU|
|:-|:-:|:-:|:-:|
|G8-D3|**0.66**|**0.23**|**0.17**|
|GT|0.80|0.23|0.17|
|GT(test)|0.62|0.23|0.16|

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

***

**Note:** In above table, G and D means generator and discriminator respectively, and the number means the layers of each part. We have tried Normal and TruncNormal. For testing, we first resize the synthesized images to 1024*2048 and then feed these resized fake images to [This pre-trained FCN](http://people.eecs.berkeley.edu/~tinghuiz/projects/pix2pix/fcn-8s-cityscapes/). Above tables summarized the segmentation results.


## The code and corresponding models will be pulbic soon

## Dataset
- We use the Cityscapes dataset. To train a model on the full dataset, please download it from the [official website](https://www.cityscapes-dataset.com/) (registration required).

## Acknowledgments
Our implementation borrows heavily from [pytorch-CycleGAN-and-pix2pix](https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix).