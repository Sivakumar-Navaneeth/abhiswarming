# Abhiswarming ROS package

## Index

## Special Instructions

### Add ROSDEP dependencies

```sh
cd ~/ros2_ws
source /opt/ros/humble/setup.bash
sudo apt update
rosdep update
rosdep install --from-paths src --ignore-src -r
```

### Micro-XRCE-DDS-Gen

**Warning: Have JAVA Installed**
```sh
git clone --recurse-submodules https://github.com/ardupilot/Micro-XRCE-DDS-Gen.git
cd Micro-XRCE-DDS-Gen
./gradlew assemble
```

### ArduPilot Installation

#### Ardupilot

In home directory:
```
cd ~
sudo apt install git
git clone https://github.com/ArduPilot/ardupilot.git
cd ardupilot
git checkout Copter-3.6
git submodule update --init --recursive
```

```
sudo apt install python-matplotlib python-serial python-wxgtk3.0 python-wxtools python-lxml python-scipy python-opencv ccache gawk python-pip python-pexpect
```

```
sudo pip install future pymavlink MAVProxy
```

Add these lines to end of `~/.bashrc`/`~/.zsshrc` (the file open in the text editor):
```
export PATH=$PATH:$HOME/ardupilot/Tools/autotest
export PATH=/usr/lib/ccache:$PATH
```

To install ArduPilot, you'll need to follow these steps:

#### Ardupilot Plugin

1. Install required dependencies:

    ```sh
    sudo apt install libgz-sim8-dev rapidjson-dev
    ```

2. Set up Gazebo workspace:

    ```sh
    mkdir -p gz_ws/src && cd gz_ws/src
    git clone https://github.com/ArduPilot/ardupilot_gazebo
    ```

3. Build ArduPilot Gazebo plugin:

    ```sh
    export GZ_VERSION=harmonic
    cd ardupilot_gazebo
    mkdir build && cd build
    cmake .. -DCMAKE_BUILD_TYPE=RelWithDebInfo
    make -j4
    ```

### Special Python3 Link

For ArduPilot to work correctly, it requires `python` to be available at `/usr/bin/env`. You can create a symbolic link for this purpose:

```sh
ln -s /usr/bin/python3 /usr/bin/python
```

This command creates a soft link named `python` pointing to `/usr/bin/python3`.
This version breaks down the ArduPilot installation process into clear steps and provides a more structured approach to the instructions. Additionally, it explains the purpose of creating the symbolic link for ArduPilot.

### ROS2 Check

```sh
source ~/ros2_ws/install/setup.bash
# See the node appear in the ROS graph
ros2 node list
# See which topics are exposed by the node
ros2 node info /ardupilot_dds
# Echo a topic published from ArduPilot
ros2 topic echo /ap/geopose/filtered
```

### MAV Proxy

```sh
mavproxy.py --console --map --aircraft test --master=:14550
```