# Fine-tuning DETR for object detection

[DETR](https://arxiv.org/abs/2005.12872) (DEtection TRansformer) is a model designed for detecting objects in images. Initially, it supports 91 classes for detection; however, there are situations where only one class is needed, which may not be included among the classes used during DETR's initial training.

Here we are fine-tuning DETR to detect baloons on images.

## Architecture
![](/.github/images/detr_arc.png)
Model has backbone to retrieve image embeddings, encoder, decoder, bounding box predictor and class label classifier. To fine-tune DETR we freeze backbone and backpropagate on encoder, decoder, bounding box predictor and class label classifier. For optimization, we use Hungarian loss from original paper.

## Balloons dataset
[V2 Balloon Detection Dataset](https://www.kaggle.com/datasets/vbookshelf/v2-balloon-detection-dataset/data)

Balloons is a class that is not in initial classes set of DETR, therefore we need fine-tuning. 
For training and validation steps, that is crucial to resize images to some common size. For testing, that is not required.

### Augmentations
As augmentations we apply:
- Horizonatal Flip
- Random Brightness Contrast
- Dropout (Random block of pixels drops)

Augmentations increase mAP score for object detection.

## Examples of balloon detection
![](/.github/images/balloons_garden.png)
![](/.github/images/balloons_white.png)

More examples are in the jupyter notebook!
