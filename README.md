# VINS-Mono-QPEP
The QPEP (Quadratic Pose Estimation Problems) Enhanced VINS-Mono (Originated from https://github.com/HKUST-Aerial-Robotics/VINS-Fusion) . The details of the QPEP can be found in https://github.com/zarathustr/LibQPEP. 

We use the QPEP to solve the problem that in previous version of VINS-Mono, the PnP algorithm in the initialization SFM framework was not completely working. The original problem was that, due to the usage of OpenCV PnP and improper initial guess (e.g. R = I and t = 0), the PnP algorithm, being a highly non-convex one, was not able to converge to a satisfactory global minimum. This problem has been solved by using the QPEP, which guarantees the global optimality.

## Usage
Some of the codes are modified to adapt the ROS Noetic and Clang compiler. Therefore, the use of ROS Noetic is recommended. First go to https://github.com/zarathustr/LibQPEP for the repo of ```LibQPEP```. Then, follow the instructions to install the library:
```
cd LibQPEP
mkdir build
cd build
cmake .. -DCMAKE_BUILD_TYPE=Release
make install
```

Then, clone the current repo to your catkin workspace and conduct catkin build:
```
cd catkin_ws/src
git clone https://github.com/zarathustr/VINS-Mono-QPEP
catkin build
```

Once finished, use the following command to run the demo from EuroC MAV Dataset:
```
roslaunch vins_estimator_QPEP euroc.launch
```
In another independent terminal, run
```
roslaunch vins_estimator vins_rviz.launch
```
In the terminal window of vins_estimator_QPEP, you will find:
```
QPEP PnP Converged
```
if the QPEP has been successfully executed for initialization of VINS-Mono.
