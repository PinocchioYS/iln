ILN - Implicit LiDAR Network: LiDAR Super-Resolution via Interpolation Weight Prediction
======

This project covers the LiDAR super-resolution task, but without the resolution constraint of a deep network.
The Implicit LiDAR Network (ILN) reconstructs the dense LiDAR points based on the sparse sensor measurements, 
depending on the system's requirement.
It can predict the detection distance of any continuous query laser within the sensor's field of view. 
You can see technical details on the [project page](http://sgvr.kaist.ac.kr/publication/iln).

DEPENDENCY
----------
The implementation is mainly based on the [PyTorch](https://pytorch.org/) framework for network training.
Also, We use the [ROS](https://www.ros.org/) for 3D visualization and other robotic applications, but it can be optional.

The "requirements.txt" file includes the major Python packages we used.
Check the dependencies or install them in your environment using the command:  

    pip3 install -r python_src/requirements.txt

Our package uses the [Pybind11](https://github.com/pybind/pybind11) library to call several C++ voxelization functions from Python code.
If you get this project by the "git clone", the Pybind11 source exists in the "extern" directory;
otherwise you need to set the library manually. 
Use these commands to build the voxelization module:

    mkdir build
    cd build
    cmake ..
    make

You can use the "catkin_make" command if this package is located in the ROS build system.
The "voxelizer.XXX.so" output file can be found in the "python_src" directory.


CARLA DATASET
-------------
We collected the training dataset by LiDAR simulation using the [CARLA](https://carla.org/).
This dataset consists the 9-realistic outdoor scenes, and each scene has LiDAR data with four different resolutions: 16x1024, 64x1024, 128x2048, and 256x4096 (vertical x horizontal angles).
You can download our dataset from the [link](https://sgvr.kaist.ac.kr/~yskwon/papers/icra22-iln/carla.zip) or the following command.

    cd python_src/dataset
    wget https://sgvr.kaist.ac.kr/~yskwon/papers/icra22-iln/Carla.zip
    unzip Carla.zip

These commands put the dataset into "python_src/dataset/Carla" which our example codes use as the default directory.


PRE-TRAINED MODELS
------------------
This project provides several models that we trained with the CARLA dataset: ILN [Ours, ICRA22], LIIF [CVPR21], and LiDAR-SR [RAS20].
You can download the model files from the [link](https://sgvr.kaist.ac.kr/~yskwon/papers/icra22-iln/trained.zip) or the following commands.

    cd python_src/models/trained
    wget https://sgvr.kaist.ac.kr/~yskwon/papers/icra22-iln/trained.zip
    unzip trained.zip

These commands make the pre-trained models into "python_src/models/trained" where our default model "iln_1d_400.pth" is located.
