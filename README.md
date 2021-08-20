# OpenVINO PaddlePaddle Integration Demo Preview

Note: The work presented in this repository is for demo and preview purposes only. 

This repository provides a set of sample code that demostrate how to run PaddlePaddle models in OpenVINO. 

![scrnli_8_12_2021_7-58-54 PM](https://user-images.githubusercontent.com/1720147/129298808-b084d7fb-9585-404b-95f9-c4346c21da6b.png)

## How to Setup

### Step 1 - Install OpenVINO from source

- To build from source, follow the build instructions in the [Official OpenVINO GitHub Wiki](https://github.com/openvinotoolkit/openvino/wiki/BuildingCode) with the  **Python API wrapper** (e.g., DENABLE_PYTHON=ON option in CMake) enabled.
- This step will install the OpenVINO source library to the openvino_dev directory by default. 

### Step 2 - Install Python Prerequisite for the Notebooks

- Create the virtual environment
```
cd openvino-paddlepaddle-demo
python3 -m venv openvino_env
source openvino_env/bin/activate

#install the dependencies
python -m pip install --upgrade pip
pip install -r requirements.txt

#install the kernel to Jupyter
python -m ipykernel install --user --name openvino_env
```

### Step 3 - Install PaddleDetection and Dependencies
Note: please make sure you are in the openvino-paddlepaddle-demo directory.
```sh
git clone https://github.com/PaddlePaddle/PaddleDetection.git
pip install -r cython
pip install -r PaddeDetection/requirements.txt
python PaddeDetection/setup.py install
```

### Step 4 - Execute the Jupyter Notebooks
- Enable the virtual environment, and also the OpenVINO environment. Then, execute the jupyter lab.   
```sh 
#For Linux and Mac
source openvino_env
source openvino_dev/setupvars.sh
cd openvino-paddlepaddle-demo
jupyter lab notebooks
```

### References:
- [Converting a Paddle* Model]( https://github.com/openvinotoolkit/openvino/blob/35e6c51fc0871bade7a2c039a19d8f5af9a5ea9e/docs/MO_DG/prepare_model/convert_model/Convert_Model_From_Paddle.md)

### Notes and Disclaimers
* Performance varies by use, configuration and other factors. Learn more at [www.Intel.com/PerformanceIndex](http://www.Intel.com/PerformanceIndex).
* Performance results are based on testing as of dates shown in configurations and may not reflect all publicly available updates.  See backup for configuration details.  
* No product or component can be absolutely secure. 
* Intel technologies may require enabled hardware, software or service activation.
* Your costs and results may vary. 
* © Intel Corporation.  Intel, the Intel logo, and other Intel marks are trademarks of Intel Corporation or its subsidiaries.  Other names and brands may be claimed as the property of others. 
