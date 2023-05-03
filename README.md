The basic idea is to do the two step classification:

1. object detection
2. object classification

These are implemented in point cloud and rgb images. We finally combine the two models and generate a result.

#### Detection

This part is done with Open3D ML library. Object detection is built on top of a pretrained KITTI model.

#### Classification

Train a classifier with given bounding boxes. Bounding boxes are gained by directly projecting the bounding box from 3D to 2D, and normalize the ones that are outside of RGB image.

Specifically, on rgb image level:

- crop out regions within the bounding box
- train a classifier on such regions
  - utilizing pretrained image models
  - Built an MLP on top of it

#### Prediction

Specifically for this task, this is not a general task.

For this specific task, many images are similar. By similar it means that they are sequential pictures on a same object with minor changes. 

Therefore, for this task, it is better to group similar pictures together and make the prediction using the best shot.

#### Others

There are some weird cases in test set and train set.

Take this picture for example.

![0007_image](https://user-images.githubusercontent.com/53202324/235971386-dcab58ce-5dd2-42ff-9673-5ce2bd893667.jpg)

My initial predition was something like normal cars. But after I encoded motorcycle detection and labeled motorcycles as correct, my total accuracy dropped.
