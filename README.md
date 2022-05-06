## Human Pose Detection on Arduino Portenta H7

The goal of this project is to deploy a trained Convolution Neural Network (CNN) to a microprocessor. In our case, we trained a CNN to detect human posture. The model is trained on more than 17000 320 x 320 images to capture key datapoints (ankle, wrist, shoulders, hips) in an image of human. The trained model is then prunned and quantized before deploying to Arduino Portenta H7.

## MPII Human Pose Dataset
[MPII Human Pose dataset](http://human-pose.mpi-inf.mpg.de/#overview) is a state of the art benchmark for evaluation of articulated human pose estimation. The dataset includes around 25K images containing over 40K people with annotated body joints. The images were systematically collected using an established taxonomy of every day human activities. 

Author: Mykhaylo Andriluka and Leonid Pishchulin and Peter Gehler and Schiele, Bernt\
Title: 2D Human Pose Estimation: New Benchmark and State of the Art Analysis\
Booktitle: IEEE Conference on Computer Vision and Pattern Recognition (CVPR)\
Year: 2014\
Month: June

### Download
- [Images (12.9 GB)](https://datasets.d2.mpi-inf.mpg.de/andriluka14cvpr/mpii_human_pose_v1.tar.gz)
- [Annotations (12.5 MB)](https://datasets.d2.mpi-inf.mpg.de/andriluka14cvpr/mpii_human_pose_v1_u12_2.zip)

#### Methodology:
+ To train the model, we used the MPII Human Pose Dataset. You can download the images from [here](https://datasets.d2.mpi-inf.mpg.de/andriluka14cvpr/mpii_human_pose_v1.tar.gz).
+ Unzip the images to `data/images` directory.
+ The annotation for the images is already inside the `data` directory.
+ The annotation format from MPII was changed to meet the requirements of this project. So, run the `update_annotation_format.ipynb` notebook. This will create a new dataset named `updated_mpii_dataset.csv` under `data` directory.
+ Once you have the unzipped images and the *updated* MPII dataset, run `image_manipulation.ipynb` notebook. This notebook makes different adjustments to the images like cropping, resizing and the new images are saved inside `data/updated` directory.
+ With the manipulation done on the images, the pixel coordinates also have to be updated to match the datapoints correctly in new images. The `image_manipulation.ipynb` notebook also saves the new annotation as `data/final_model_ready_dataset.csv`.
+ Additionally, to confirm that the datapoints in the updated images are correctly lined up with the joints in the images, a copy of each image highlighting the posture is stored inside `data/confirmation` directory.
+ Inside `updated` and `confirmation` directory, you will find multiple folder, each folder containing at most 100 images.
+ Since we are manipulation a large number of images, the system might run out of memory and the kernel might die at some point. If that happens, run the `image_manipulation.ipynb` notebook again as long as the progress bar does not hit 100%. The previously manipulated images and the annotation will be stored in temporary files and the notebook will continue from a checkpoint.
+ Run the code till the last cell to remove the temporary files.
+ If you do not want to run the manipulation notebook, you can download the new images and dataset from the links below:
  - [Updated images](https://drive.google.com/file/d/19sLSGhUiB5DDTKFmY_PRcGHa6jmgbU7v/view?usp=sharing) - unzip the files inside `data/updated` directory
  - [Confirmation images](https://drive.google.com/file/d/1WrNZmDgZTgQ_e1wReHbrxLLhO57AuWvT/view?usp=sharing) - unzip the files under `data/confirmation` directory
  - [Real Time images](https://drive.google.com/file/d/1Xjros5UcFwOydrF0bl_s0EbWZeFye95D/view?usp=sharing) - unzip th files under `data/real_time` directory
  - [Model ready annotation dataset](https://drive.google.com/file/d/1tIxbZ3NE1jQJRF0FUcDXetxHoXZCGKGn/view?usp=sharing) - place the file under `data` directory

### Model/Architecture Resources:
- [TensorFlow](https://www.tensorflow.org/)
- [MobileNet V2](https://www.tensorflow.org/api_docs/python/tf/keras/applications/mobilenet_v2)
- [MobileNet V3](https://www.tensorflow.org/api_docs/python/tf/keras/applications/mobilenet_v3)
- [TensorFlow Blog](https://blog.tensorflow.org/2018/05/real-time-human-pose-estimation-in.html)
- [PoseNet Repo](https://github.com/tensorflow/tfjs-models/tree/master/posenet)



### Posture Detection:
- Machine learning model to detect joint positions
- Servo motors to control small model that replicates movement seen from vision (Motor driver board)
- Model will just detect and replicate posture/movement
- Model that replicates movement is miniature
- Miniature model can be made from foam board and hot glued together
- Use multiple portentas to generalize movement from different vision angles
- “Stick figure” model to represent joints + movement in simple fashion

Annotations:
- https://www.makesense.ai/
