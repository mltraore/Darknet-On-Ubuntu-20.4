# Darknet-On-Ubuntu-20.4
Installing  YOLO Darknet  with GPU, CUDA, cuDNN and openCV  on  ubuntu 20.04

## 1. Cleaning up
Open a terminal window and type the following three commands to get rid of  
any NVIDIA/CUDA packages you may already have installed  
```bash
sudo rm /etc/apt/sources.list.d/cuda*
sudo apt remove --autoremove nvidia-cuda-toolkit
sudo apt remove --autoremove nvidia-*
```
Purge any remaining NVIDIA configuration files and the associated dependencies  
that they may have been installed with.
```bash
sudo apt-get purge nvidia*
sudo apt-get autoremove
sudo apt-get autoclean
```
 Remove any existing CUDA folders you may have in **/usr/local/**
 ```bash
 sudo rm -rf /usr/local/cuda*
 ```
 ## 2. Install
 Setting up the CUDA PPA.  About [PPA in ubuntu](https://itsfoss.com/ppa-guide/).  
 CUDA is added to source.list file.  
```bash
sudo apt update
sudo add-apt-repository ppa:graphics-drivers
sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
sudo bash -c 'echo "deb http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/cuda.list'
sudo bash -c 'echo "deb http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/cuda_learn.list'
```
Install cuda 10.1 packages
```bash
sudo apt update
sudo apt install cuda-10-1
```
>**Note:**  
>&nbsp;&nbsp;&nbsp;  While installing cuda-10.1, apt manager may install libcublas package for cuda-10.2 instead of  
>&nbsp;&nbsp;&nbsp;  the one compatible with cuda 10.1, which can cause issues when using gpu functionality.  

To avoid this problem, let's remove this package and install the compatible package for cuda-10.1.  
```bash
# remove libcublas10.2
apt-remove libcublas10* 

# download cublas runtime and developper libraries (.deb)
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/libcublas10_10.1.0.105-1_amd64.deb      
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/libcublas-dev_10.1.0.105-1_amd64.deb

# install (.deb) files
dpkg -i libcublas10_10.1.0.105-1_amd64.deb
dpkg -i libcublas-dev_10.1.0.105-1_amd64.deb
```


