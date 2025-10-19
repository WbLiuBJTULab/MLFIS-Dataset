# Welcome to the MLFIS Vision Benchmark Suite! 

To address the lack of method's robustness evaluation, we construct an MLFIS dataset and propose a novel robustness evaluation protocol for diverse extreme interference.  In addition, the dataset mainly contains the car and pedestrian categories.

## Raw Data Acquisition

The MLFIS dataset is constructed based on the CARLA simulator [here](https://carla.org/)  [GITHUB](https://github.com/carla-simulator/carla), which are captured by the 64-line Velodyne LiDAR and RGB camera. The CARLA simulator (Car Learning to Act) is an open-source autonomous driving simulation platform jointly developed by Intel Labs and the Toyota Research Institute. It is based on Unreal Engine and provides high-fidelity urban environments, vehicle sensor models (such as cameras, lidar, GPS, IMU, etc.), and flexibly configurable dynamic traffic scenarios to support the development, training, and validation of 3D object detection and autonomous driving methods.


## Dataset Details

### Data Scenarios

The MLFIS dataset contains the diverse unstructured scenarios (including grassland, forest, and mountain) and different fog interference (including mild, moderate, and severe fog).

For the unstructured scenarios, the grassland scenario suffers random occlusions from grass, causing a sharp drop in foreground-background distinction. The forest scenario causes mottled light patterns and deep fissures, and the textures on tree trunks can lead to semantic confusion. In mountain scenario, the rock edges and the vehicle's metal reflections interfere with each other, increasing the uncertainty in edge detection. 

For the different fog interference, Fig.1(a) shows the mild fog scenario that contains lots of distant small and occluded objects, which makes it  difficult to visually distinguish objects from the images, thereby increasing detection difficulty for the occluded and small objects. 

Fig.2(b) illustrates the moderate fog scenario that includes lots of smoke interference and tree coverage, which effectively verifies the method's  detection performance for extreme weather and unstructured terrain. 

Fig.3(c) depicts the severe fog scenario, which presents a huge detection challenge for method robustness evaluation. 

<img src="Fig.png" width="80%" alt="Visualization of samples from the MLFIS dataset. (a) Mild fog scenario. (b) Moderate fog scenario. (c) Severe fog scenario."/>
Fig.1 Visualization of samples from the MLFIS dataset. (a) Mild fog scenario. (b) Moderate fog scenario. (c) Severe fog scenario.


### Data Split

The MLFIS dataset consists of 6,921 training samples (4,500 samples for training and 2,421 samples for validation) and 2,242 test samples, in which 3,985 samples represent mild fog scenarios, 1,815 samples represent moderate fog scenarios, and 3,363 samples represent severe fog scenarios. 

| Data Split     | Mild  | Mod | Sev  | Total |
|----------------|-------|-----|------|--------|
| Training set   | 1,734 | 950 | 1,816 | 4,500 |
| Validation set | 1,000 | 430 | 991  | 2,421 |
| Test set       | 1,251 | 435 | 556  | 2,242 |
| **Total**      | 3,985 | 1,815 | 3,363 | 9,163



### Data Advantage

Compared with the existing datasets, the MLFIS dataset can be applied to research the robustness 3D object detection under Mild, Mod, and Sev fog scenarios containing grassland, forest, and mountain terrain. Compared with the existing evaluation protocol, the robustness evaluation protocol proposes the multi-level fog evaluation that  calculates the APs on diverse fog scenarios, object categories, and recall positions, which fully analyzes method's robustness.


##  Robustness evaluation protocol

For the robustness evaluation protocol, it analyzes various APs for mild, moderate, and severe fog scenarios (abbreviated as Mild, Mod, and Sev), which comprehensively demonstrates the method's robustness performance faced with different interference.

In Algorithm, the car category and pedestrian category are evaluated at the IoU threshold of 0.7 and 0.5, respectively, and reported in terms of 3D AP(R40), 3D AP(R11), and BEV AP(R40) across Mild, Mod, and Sev fog scenarios. For example, when the car category is evaluated on mild fog scenarios DMild, the predicted 3D bounding box Ŷ  is first considered positive if its 3D IoU with the ground-truth box GTMild exceeds 0.7 (IoU3D=0.7). Later, the PR curve can be calculated by Compute() that uses both 11-point interpolation and 40-point interpolation, which yield the Car 3D AP(R11) and Car 3D AP(R40), respectively. Meanwhile, the Car BEV AP(R40) can be obtained by replacing the IoU3D=0.7 with the BEV IoU (IoUbev=0.7) during the above process.

<pre>
Algorithm: The Proposed Robustness Evaluation Protocol
------------------------------------------------------
Input:  
  DMild, GTMild  // mild-fog data & ground truth  
  DMod, GTMod    // moderate-fog  
  DSev, GTSev    // severe-fog  
  Ŷ    // predicted 3D boxes  

for I ∈ {Mild, Mod, Sev} do
    if Class == Car then
        if Task == 3D AP then
            3D AP(R11) ← Compute(Ŷ, GT_I, IoU3D=0.7, 11-point)
            3D AP(R40) ← Compute(Ŷ, GT_I, IoU3D=0.7, 40-point)
        else if Task == BEV AP then
            BEV AP(R40) ← Compute(Ŷ, GT_I, IoUbev=0.7, 40-point)
    end if

    if Class == Pedestrian then
        if Task == 3D AP then
            3D AP(R11) ← Compute(Ŷ, GT_I, IoU3D=0.5, 11-point)
            3D AP(R40) ← Compute(Ŷ, GT_I, IoU3D=0.5, 40-point)
        else if Task == BEV AP then
            BEV AP(R40) ← Compute(Ŷ, GT_I, IoUbev=0.5, 40-point)
    end if
end for

Output:
  Car 3D AP(R11), 3D AP(R40), BEV AP(R40)
  Pedestrian 3D AP(R11), 3D AP(R40), BEV AP(R40)
</pre>



## Academic Research Use Only

Any commercial exploitation, including but not limited to business testing, product integration or profit-making services, is strictly prohibited. If you use these resources in your work, please cite the accompanying paper and comply with the license terms.

## Credits

We thank Beijing Jiaotong University and China North Artificial Intelligence & Innovation Research Institute for supporting this project. We further thank our 3D object labeling task force for doing such a great job: Jicheng Zhu, Zeheng Zhang, Rongrong Jin, Peiting Li.
