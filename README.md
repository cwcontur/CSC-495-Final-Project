## Human Pose Detection on Arduino Portenta H7

The goal of this project is to deploy a trained Convolution Neural Network (CNN) to a microprocessor. In our case, we trained a CNN to detect human posture. The model is trained on more than 17000 320 x 320 images to capture key datapoints (ankle, wrist, shoulders, hips) in an image of human. The trained model is then prunned and quantized before deploying to Arduino Portenta H7.

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
  - [Model ready annotation dataset](https://drive.google.com/file/d/1tIxbZ3NE1jQJRF0FUcDXetxHoXZCGKGn/view?usp=sharing) - place the file under `data` directory







Group repository for our final project in 495

Object tracking system\
Posture Detection:
- Machine learning model to detect joint positions
- Servo motors to control small model that replicates movement seen from vision (Motor driver board)
- Model will just detect and replicate posture/movement
- Model that replicates movement is miniature
- Miniature model can be made from foam board and hot glued together
- Use multiple portentas to generalize movement from different vision angles
- “Stick figure” model to represent joints + movement in simple fashion

Links:
- https://www.amazon.com/10Pcs-Servos-Helicopter-Airplane-Controls/dp/B08KY49SFX/ref=asc_df_B08KY49SFX/?tag=hyprod-20&linkCode=df0&hvadid=475740798427&hvpos=&hvnetw=g&hvrand=13111227009810616170&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9009647&hvtargid=pla-1186208374440&psc=1
- https://www.amazon.com/Longruner-Stepper-Uln2003-arduino-LK67/dp/B015RQ97W8/ref=asc_df_B015RQ97W8/?tag=hyprod-20&linkCode=df0&hvadid=241948263033&hvpos=&hvnetw=g&hvrand=700369305293697484&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9009648&hvtargid=pla-569411026209&psc=1
- https://www.makesense.ai/

Think a little bit smaller in the beginning to make sure that you have a concept that works for the micro controller and the machine learning model. Condense down to smallest unit before starting.
