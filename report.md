10204 snapshots

- 7573 for training
- 2631 for testing

Each snapshot  contains:

- an RGB image
- a point cloud
- the camera matrix
- a list of  3D bounding boxes (only for trainval)
  - bbox.bin file: array with 11 columns
  - each row: rotation vector,  position (centroid x, y, z), size of the bounding box (length, width,  height), class id, and a flag





The basic idea is to do the two step classification:

1. object detection
2. object classification

These are implemented in both point cloud and rgb images. We finally combine the two models and generate a result.

#### Detection

#### Classification

Train a classifier with given bounding boxes.

Specifically, on rgb image level:

- crop out regions within the bounding box
- train a classifier on such regions
  - utilizing pretrained image models
  - Built an MLP on top of it

On point cloud level:

- crop out points within the bounding box
- train a classifier on such points





We stack 3 models together: 3d object detection, vehicle identification, and 2d image classification