# Welcome to the MLFIS Vision Benchmark Suite! 

To address the lack of method's robustness evaluation, we construct an MLFIS dataset and propose a novel robustness evaluation protocol for diverse extreme interference. The MLFIS dataset is constructed based on the CARLA simulator, which contains  diverse unstructured scenarios (including grassland, forest, and mountain) and different fog interference (including mild, moderate, and severe fog). The MLFIS dataset consists of 6,921 training samples (4,500 samples for training and 2,421 samples for validation) and 2,242 test samples, in which 3,985 samples represent mild fog scenarios, 1,815 samples represent moderate fog scenarios, and 3,363 samples represent severe fog scenarios. In addition, the dataset mainly contains the car and pedestrian categories, which are captured by the 64-line Velodyne LiDAR and RGB camera.

## Raw Data Acquisition

The MLFIS dataset is constructed based on the CARLA simulator [here](https://carla.org/)  [GITHUB](https://github.com/carla-simulator/carla), which are captured by the 64-line Velodyne LiDAR and RGB camera. The CARLA simulator (Car Learning to Act) is an open-source autonomous driving simulation platform jointly developed by Intel Labs and the Toyota Research Institute. It is based on Unreal Engine and provides high-fidelity urban environments, vehicle sensor models (such as cameras, lidar, GPS, IMU, etc.), and flexibly configurable dynamic traffic scenarios to support the development, training, and validation of 3D object detection and autonomous driving methods.




## Dataset Details

The MLFIS dataset consists of 6,921 training samples (4,500 samples for training and 2,421 samples for validation) and 2,242 test samples, in which 3,985 samples represent mild fog scenarios, 1,815 samples represent moderate fog scenarios, and 3,363 samples represent severe fog scenarios. In addition, the dataset mainly contains the car and pedestrian categories, which are captured by the 64-line Velodyne LiDAR and RGB camera.


| Data Split     | Mild  | Mod | Sev  | Total |
|----------------|-------|-----|------|--------|
| Training set   | 1,734 | 950 | 1,816 | 4,500 |
| Validation set | 1,000 | 430 | 991  | 2,421 |
| Test set       | 1,251 | 435 | 556  | 2,242 |
| **Total**      | 3,985 | 1,815 | 3,363 | **9,
