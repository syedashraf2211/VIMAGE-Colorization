# VIMAGE Colorization

Automatic colorization of black-and-white images and videos using OpenCV's DNN module and a pretrained Caffe colorization model (Zhang et al., "Colorful Image Colorization").

## How it works

The script loads a Caffe model (`colorization_deploy_v2.prototxt` + cluster centers in `pts_in_hull.npy`) through OpenCV's `cv.dnn` module. For each input frame it:

1. Converts the frame to Lab color space and extracts the L (lightness) channel.
2. Feeds the L channel through the network to predict the a/b color channels.
3. Recombines L with the predicted a/b channels and converts back to RGB.

Images are processed in a single pass; videos are processed frame-by-frame and written out with the same FPS as the input.

## Setup & run

Download the pretrained model weights (not included in this repo due to size) and place the file alongside the notebook:

```bash
wget https://github.com/richzhang/colorization/raw/caffe/colorization/models/colorization_release_v2.caffemodel
```

Then open `VimageColorization.ipynb` and run all cells. You'll be prompted to:

1. Choose `1` for image colorization or `2` for video colorization.
2. Enter the filename (with extension) of the image/video to process.

Output is saved alongside the input — `<name>_colorized.avi` for video.

## Tech stack

Python · OpenCV (`cv.dnn`) · Caffe (pretrained model)
