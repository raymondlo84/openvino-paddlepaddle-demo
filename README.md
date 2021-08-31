# OpenVINO PaddlePaddle Integration Demo Preview

[[English]](README.md) | [[简体中文]](README_CN.md)

Note: The work presented in this repository is for demo and preview purposes only. 

This repository provides a set of sample code that demostrate how to run PaddlePaddle models in OpenVINO. 

![scrnli_8_12_2021_7-58-54 PM](https://user-images.githubusercontent.com/1720147/129298808-b084d7fb-9585-404b-95f9-c4346c21da6b.png)

## How to Setup

### Step 0 - Clone the repository 

Download this OpenVINO PaddlePaddle sample repository! Please note that we will install materials inside the openvino-paddlepaddle-demo folder as the default working directory.  
```
git clone https://github.com/raymondlo84/openvino-paddlepaddle-demo.git
cd openvino-paddlepaddle-demo
```

### Step 1 - Install OpenVINO from source
Upcoming release **openvino 2022.1** will officially support PaddlePaddle. But users can experience this feature from OpenVINO github master branch in advance.

We install the OpenVINO source library to the openvino/openvino_dist directory by default.  Users can change it by modifying the cmake option "CMAKE_INSTALL_PREFIX".

For users who may have connection problem to github, may add this configuration to ~/.gitconfig :
```
    [url "git://github.com"]
	      insteadOf="https://github.com"
```

Clone the OpenVINO source code from GitHub.
```
git clone https://github.com/openvinotoolkit/openvino.git
cd openvino
git submodule update --init --recursive
```

Install the dependencies for OpenVINO source and Python.
- For Linux
```
chmod +x install_build_dependencies.sh
./install_build_dependencies.sh
pip3 install -r inference-engine/ie_bridges/python/src/requirements-dev.txt
```

- For Mac. Please follow the official [guideline](https://github.com/openvinotoolkit/openvino/wiki/BuildingForMacOS) and also install [Brew](https://brew.sh/). 
```
#install Python Dependencies
pip install -r inference-engine/ie_bridges/python/src/requirements-dev.txt
```

Compile the source code with the Python option enabled. It may take a few minute depending on your pc.

```
export OPENVINO_BASEDIR=`pwd`
mkdir build
cd build
cmake \
-DCMAKE_BUILD_TYPE=Release \
-DCMAKE_INSTALL_PREFIX="${OPENVINO_BASEDIR}/openvino_dist" \
-DPYTHON_EXECUTABLE=$(which python3) \
-DENABLE_MYRIAD=OFF \
-DENABLE_VPU=OFF \
-DENABLE_PYTHON=ON \
-DNGRAPH_PYTHON_BUILD_ENABLE=ON \
..

make -j$(nproc); make install
```

### Step 2 - Setup the OpenVINO PaddlePaddle Sample from GitHub
Create the virtual environment and install dependencies. Now let's start from the working directory openvino-paddlepaddle-demo. 

```sh
cd openvino-paddlepaddle-demo
python3 -m venv openvino_env
source openvino_env/bin/activate

#install the dependencies
python -m pip install --upgrade pip
pip install -r requirements.txt -i https://mirror.baidu.com/pypi/simple

#install the kernel to Jupyter
python -m ipykernel install --user --name openvino_env
```

### Step 3 - Setup PaddleDetection and Dependencies
This step is required as we are going to export the static paddlepaddle model  from PaddlePaddle Open Model Zoo [PaddleDetection]( https://github.com/PaddlePaddle/PaddleDetection.git), and may also do inference with PaddlePaddle as well.

```sh
# Note: please make sure you are in the openvino-paddlepaddle-demo directory.
git clone https://github.com/PaddlePaddle/PaddleDetection.git
cd PaddleDetection && git checkout release/2.1 && cd - 
pip install paddlepaddle -i https://mirror.baidu.com/pypi/simple
pip install --upgrade -r PaddleDetection/requirements.txt -i https://mirror.baidu.com/pypi/simple
#Optional
#python PaddeDetection/setup.py install
```

### Step 4 - Execute the Jupyter Notebooks
Enable the virtual environment, and also the OpenVINO environment. Then, execute the jupyter lab.  These steps are required if a new session is used (i.e., the terminal was closed or restarted).

```sh 
#For Linux and Mac
source openvino_env/bin/activate
source openvino/openvino_dist/bin/setupvars.sh
jupyter lab notebooks
```

### Sample Output
PPYolo - [notebooks/101-object-detection-yolo](notebooks/101-object-detection-yolo). 
![yolo-output](https://user-images.githubusercontent.com/1720147/130380687-0de42836-c959-4d86-908c-9034e0eda90a.png)
MobilenetV3 Large - [notebooks/100-mobilenetv3](notebooks/100-mobilenetv3).
![scrnli_8_22_2021_7-13-22 PM](https://user-images.githubusercontent.com/1720147/130380796-2a6084df-3753-4642-b5ff-32ba491bc944.png)


Note: Please make sure you select the openvino_env as the Kernel in the Notebooks.

### References:
- [OpenVINO Notebooks](https://github.com/openvinotoolkit/openvino_notebooks) - Great tutorials and simple pip install setup! (Recommended) 
- [Compiling OpenVINO from Source](https://github.com/openvinotoolkit/openvino/wiki/BuildingCode)
- [Converting a Paddle* Model]( https://github.com/openvinotoolkit/openvino/blob/35e6c51fc0871bade7a2c039a19d8f5af9a5ea9e/docs/MO_DG/prepare_model/convert_model/Convert_Model_From_Paddle.md)

### Notes and Disclaimers
* Performance varies by use, configuration and other factors. Learn more at [www.Intel.com/PerformanceIndex](http://www.Intel.com/PerformanceIndex).
* Performance results are based on testing as of dates shown in configurations and may not reflect all publicly available updates.  See backup for configuration details.  
* No product or component can be absolutely secure. 
* Intel technologies may require enabled hardware, software or service activation.
* Your costs and results may vary. 
* © Intel Corporation.  Intel, the Intel logo, and other Intel marks are trademarks of Intel Corporation or its subsidiaries.  Other names and brands may be claimed as the property of others. 
