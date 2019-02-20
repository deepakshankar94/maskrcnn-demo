# maskrcnn-demo


## Install Anaconda 

- Get the Anaconda install file using 

```bash
wget https://repo.anaconda.com/archive/Anaconda3-2018.12-Linux-x86_64.sh

chmod +x Anaconda3-2018.12-Linux-x86_64.sh

./Anaconda3-2018.12-Linux-x86_64.sh
```

- Follow the instructions from the installer


## Create a conda environment

- Create the conda environment where the libraries will be setup

```bash
conda create -n maskrcnn_demo python=3

source activate maskrcnn_demo
```

## compile the pytorch library from source 

(This step might break on the ryzen because of mkl-dnn library )

- Setup the environment variable required for compiling pytorch without CUDA

```bash
export NO_CUDA=1
```

- Install Dependencies


```
conda install numpy pyyaml mkl mkl-include setuptools cmake cffi typing
```


- Get the PyTorch Source
```bash
git clone --recursive https://github.com/pytorch/pytorch
cd pytorch
```

- Install PyTorch

```bash
export CMAKE_PREFIX_PATH=${CONDA_PREFIX:-"$(dirname $(which conda))/../"}
python setup.py install
```

## install project dependencies

```bash
# this installs the right pip and dependencies for the fresh python
conda install ipython

# maskrcnn_benchmark and coco api dependencies
pip install ninja yacs cython matplotlib


conda install pytorch-nightly -c pytorch

export INSTALL_DIR=$PWD
# install torchvision
cd $INSTALL_DIR
git clone https://github.com/pytorch/vision.git
cd vision
python setup.py install

# install pycocotools
cd $INSTALL_DIR
git clone https://github.com/cocodataset/cocoapi.git
cd cocoapi/PythonAPI
python setup.py build_ext install

# install PyTorch Detection
cd $INSTALL_DIR
git clone https://github.com/facebookresearch/maskrcnn-benchmark.git
cd maskrcnn-benchmark

python setup.py build develop

#install the correct version of scikit
conda install scikit-image=0.14.0

unset INSTALL_DIR

cd ..
```

## run the demo

```bash
chmod +x run.sh

./run.sh

#if the 
```