# tusimple-annotation
This repository provides instructions on how to create a lane detection dataset in tusimple format.

To create a dataset in tusimple format, we will use [VIA annotation tool](https://www.robots.ox.ac.uk/~vgg/software/via/). Download the zip file from that link and open it `via.html` using a browser. 

![demo image](sample-annotation.png)

1. Use `Add files` option to select images from your local directory.
2. Select `polyline` option from `Region Shape` section.
3. Start drawing line/points from bottom to top on top of lanes. At least keep 6-7 points per lane to ensure a good result from Spline model. Also, make sure x-coordinates of a lane are in order, for example, [239, 250, 270, 320, 380, ... 570] or [ 710, 650, 623, 589, .... 345, 310]. It should not be like [239, 250, 245, 270, 320, 380, ... 570].
4. Save the project for later use.
5. Export the annotations in `json` format.

After annotating all the images and exporting the annotation file, run each cell of `tusimple_annotation.ipynb` to get the dataset in tusimple format. Make sure to edit the file location in line 1 and raw_images location in `dictionary[raw_file]` object.

## Class annotation
If you want to annotate lane classes like solid, dash, etc, then create a .txt file of the same name as the json file. Like if your json file name is `LVLane_train_sunny.json` and then create a file named by `LVLane_train_sunny_classes.txt`. For each image, we will have one line in that txt file. If one image contains 5 lanes, we will have 5 class labels separated by space in that line. Use [this](https://github.com/zillur-av/tusimple-annotation/blob/main/class_mapping.txt) to get class names. Run [this](https://github.com/zillur-av/tusimple-annotation/blob/main/vis.py) code to get lane visualization. You have to modify the location and json names in lines https://github.com/zillur-av/tusimple-annotation/blob/d149a89fbaa5c95243db1ef002d29174449f0783/vis.py#L112. You can edit the time in https://github.com/zillur-av/tusimple-annotation/blob/d149a89fbaa5c95243db1ef002d29174449f0783/vis.py#L80. For now, it is set to 4 seconds. So, we will get consecutive images from the json file at each 4 seconds period. The .txt file will be something like this:
```
2 4 5
2 1 4 6
3 5 5 2
.
.
.
4 5 7 3
```
We could use directly via tool too to annotate the classes but it may take a longer period of time. I found this way faster.
## Citation
If you use our tool, please cite the following the paper as well as  [VIA annotation tool](https://www.robots.ox.ac.uk/~vgg/software/via/)
```
@article{rahman2023lvlane,
  title={LVLane: Deep Learning for Lane Detection and Classification in Challenging Conditions},
  author={Rahman, Zillur and Morris, Brendan Tran},
  journal={2023 IEEE International Conference on Intelligent Trabsportation Systems (ITSC)},
  year={2023}
}

```
