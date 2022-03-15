# 演示：OpenVINO如何支持PaddlePaddle

[[English]](README.md) | [[简体中文]](README_CN.md)

本项目通过一些示例演示了如何通过OpenVINO运行PaddlePaddle模型。

![scrnli_8_12_2021_7-58-54 PM](https://user-images.githubusercontent.com/1720147/129298808-b084d7fb-9585-404b-95f9-c4346c21da6b.png)

## 运行环境搭建

### 第一步 - 克隆本项目 
克隆本项目。注意：默认以openvino-paddlepaddle-demo文件夹作为工作目录。  
```
git clone https://github.com/raymondlo84/openvino-paddlepaddle-demo.git
cd openvino-paddlepaddle-demo
```

### 第二步 - 从源码编译安装OpenVINO
OpenVINO对paddlepaddle的原生支持计划于**openvino 2022.1**版本发布。在这之前开发者可以从**github**上的**master**分支提前体验相关功能。跟之前对其它框架的支持不同的是，开发者可以直接将PaddlePaddle的模型传递给OpenVINO直接进行推理，而无需先用ModelOptimizer转换成IR（参考文档TBD）。

默认将openvino安装在openvino/openvino_dist目录下。用户也可以通过改变cmake选项"CMAKE_INSTALL_PREFIX"将其安装到其它目录下。

注意：若不能使用代理顺利的访问github服务的机器（如中国国内的用户），建议将以下配置添加到本机~/.gitconfig。否则接下来从github克隆openvino的某些子项目很可能会失败。
```
    [url "git://github.com"]
	      insteadOf="https://github.com"
```

从GitHub克隆OpenVINO及其子项目。
```
git clone https://github.com/openvinotoolkit/openvino.git
cd openvino
git submodule update --init --recursive
```

安装OpenVINO源码编译依赖。
-  Linux平台
```
chmod +x install_build_dependencies.sh
./install_build_dependencies.sh
pip3 install -r inference-engine/ie_bridges/python/src/requirements-dev.txt
```

-  对Mac平台请参照官方指导手册 [guideline](https://github.com/openvinotoolkit/openvino/wiki/BuildingForMacOS)并安装 [Brew](https://brew.sh/). 
```
#install Python Dependencies
pip install -r inference-engine/ie_bridges/python/src/requirements-dev.txt
```

编译安装。可能需要若干分钟，具体取决于用户机器配置。

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

### 第三步 - 安装本项目
创建python的虚拟环境并安装相关依赖。

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

### 第四步 - 设置PaddleDetection
我们将通过PaddlePaddle模型库[PaddleDetection]( https://github.com/PaddlePaddle/PaddleDetection.git)导出PPYolo的静态图模型。

```sh
# 注意：当前工作目录仍为openvino-paddlepaddle-demo。
git clone https://github.com/PaddlePaddle/PaddleDetection.git
cd PaddleDetection && git checkout release/2.1 && cd - 
pip install paddlepaddle -i https://mirror.baidu.com/pypi/simple
pip install --upgrade -r PaddleDetection/requirements.txt -i https://mirror.baidu.com/pypi/simple
# 无须编译安装
# python PaddeDetection/setup.py install
```

### 第五步 - 启动Jupyter Notebooks
激活python虚拟环境，配置OpenVINO环境变量，启动jupyter lab。注意，每一次新的会话，如终端关闭或重启都需要该步骤。

```sh 
#For Linux and Mac
source openvino_env/bin/activate
source openvino/openvino_dist/setupvars.sh
jupyter lab notebooks
```

### 演示结果
PPYolo - [notebooks/101-object-detection-yolo](notebooks/101-object-detection-yolo). 
![yolo-output](https://user-images.githubusercontent.com/1720147/130380687-0de42836-c959-4d86-908c-9034e0eda90a.png)
MobilenetV3 Large - [notebooks/100-mobilenetv3](notebooks/100-mobilenetv3).
![scrnli_8_22_2021_7-13-22 PM](https://user-images.githubusercontent.com/1720147/130380796-2a6084df-3753-4642-b5ff-32ba491bc944.png)


注意：确保选择openvino_env作为Notebook Kernel.

### 参考文档
- [Compiling OpenVINO from Source](https://github.com/openvinotoolkit/openvino/wiki/BuildingCode)
- [Converting a Paddle* Model]( https://github.com/openvinotoolkit/openvino/blob/35e6c51fc0871bade7a2c039a19d8f5af9a5ea9e/docs/MO_DG/prepare_model/convert_model/Convert_Model_From_Paddle.md)

### 注意事项和声明
* 性能因用户的机器配置等因素而异，不代表官方发布的数据。参见 [www.Intel.com/PerformanceIndex](http://www.Intel.com/PerformanceIndex).
* 本项目使用的OpenVINO为非正式发布版。
* © Intel Corporation.  Intel, the Intel logo, and other Intel marks are trademarks of Intel Corporation or its subsidiaries.  Other names and brands may be claimed as the property of others. 
