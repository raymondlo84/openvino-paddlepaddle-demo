# OpenVINO PaddlePaddle Integration Demo Preview

Note: The work presented in this repository is for demo and preview purposes only. 

This repository provides a set of sample code that demostrate how to run PaddlePaddle models in OpenVINO. 

![scrnli_8_12_2021_7-58-54 PM](https://user-images.githubusercontent.com/1720147/129298808-b084d7fb-9585-404b-95f9-c4346c21da6b.png)

## How to Setup

### Step 1 - Install OpenVINO from source

- To build from source, follow the build instructions in the [Official OpenVINO GitHub Wiki](https://github.com/openvinotoolkit/openvino/wiki/BuildingCode) with the  **Python API wrapper** (e.g., DENABLE_PYTHON=ON option in CMake) enabled.

### Step 2 - Install Python Prerequisite

- Create the virtual environment
```
python3 -m venv openvino_env
source openvino_env/bin/activate

#install the dependencies
pip install -r requirements.txt

#install the kernel to Jupyter
python -m ipykernel install --user --name openvino_env

```

### Step 3 - Execute the Jupyter Notebooks

- Enable the virtual environment, and also the OpenVINO environment. Then, execute the jupyter lab.   
```sh 
#For Linux and Mac
source openvino_env
source /usr/local/bin/setupvar.sh
cd openvino-paddlepaddle-demo
jupyter lab notebooks
```

### References:
- [Converting a Paddle* Model]( https://github.com/openvinotoolkit/openvino/blob/35e6c51fc0871bade7a2c039a19d8f5af9a5ea9e/docs/MO_DG/prepare_model/convert_model/Convert_Model_From_Paddle.md)

### Notes and Disclaimers
* Other names and brands may be claimed as the property of others.
