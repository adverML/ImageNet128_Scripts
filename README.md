# Scripts for generating a CIFAR-style ImageNet128 dataset

## Introduction
Based on the [code](https://github.com/PatrykChrabaszcz/Imagenet32_Scripts) for generating ImageNet32 and ImageNet64, this code is a memory-efficient variant that can generate ImageNet128 on a machine with only 64 GB RAM. Following the procedure for creating ImageNet32 and ImageNet64, the 'box' algorithm is used by default for resizing images. Note that you can also generate datasets of different image sizes or of different number of classes (e.g., ImageNet256 with 10 classes).

## Example
- Download and extract the [ImageNet dataset](http://www.image-net.org/challenges/LSVRC/2012/nonpub-downloads)
- Resize the images to 128x128:
  ```sh
  python3 image_resizer_imagenet.py -i ~/datasets/ImageNet/ILSVRC2012_img_train -o ~/datasets/ImageNet/ILSVRC2012_img_train_128 -r
  python3 image_resizer_imagenet.py -i ~/datasets/ImageNet/ILSVRC2012_img_val -o ~/datasets/ImageNet/ILSVRC2012_img_val_128
  ```
- Convert the resized images to pickles:
  ```sh
  python3 image2numpy_imagenet_train.py  -i ~/datasets/ImageNet/ILSVRC2012_img_train_128/box -o ~/datasets/ImageNet128
  python3 image2numpy_imagenet_val.py  -i ~/datasets/ImageNet/ILSVRC2012_img_val_128/box -o ~/datasets/ImageNet128
  ```
- Load the dataset:
  ```py
  gen = imagenet128.load(MODE, BATCH_SIZE, data_dir=DATA_DIR)
  while True:
    for images, labels in gen():
      yield images, labels
  ```



python3 image_resizer_imagenet.py -s 240 -i /home/lorenzp/datasets/ImageNet3/train -o /home/DATA/ITWM/Imagenet240x240/train_data -r
python3 image_resizer_imagenet.py -s 240 -i /home/lorenzp/datasets/ImageNet3/val -o /home/DATA/ITWM/Imagenet240x240/val_data -r
