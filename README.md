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

```diff
+ After installing CUDA we reboot the system
```

To install cuDNN library we download cuDNN Runtime, Developper and and Code Samples int (.deb)  format from [here](http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64/).  
Download -->  cuDNN Runtime Library  for cuda 10.1  
Download -->  cuDNN Developper Library  for cuda 10.1   
Download -->  cuDNN Code Samples and User Guide  for cuda 10.1  
Depackage and Install downloaded packages
```bash
sudo dpkg -i libcudnn7_7.6.5.32-1+cuda10.1_amd64.deb
sudo dpkg -i libcudnn7-dev_7.6.5.32-1+cuda10.1_amd64.deb
sudu dpkg -i libcudnn7-doc_7.6.5.32-1+cuda10.1_amd64.deb
```
Our cuda file should be in **/usr/local** directory as ***cuda-10.1***  
but compile Makefile knows it as cuda. So we should rename this directory as ***cuda***  
or create a new directory as ***cuda*** and copy ***cuda-10.1*** to this one.  
Another option is to create a symlink as **cuda** to ***cuda-10.1*** directory.  
```bash
# 1. Option: rename the directory
sudo mv /usr/local/cuda-10.1  /usr/local/cuda

# 2. Option: create new directory
sudo mkdir /usr/local/cuda
sudo cp -r /usr/local/cuda-10.1 /usr/local/cuda

# 3. Option: create a symlink to the directory
sudo ln -s /usr/local/cuda-10.1  /usr/local/cuda
```
After installing, let's open our **.profile** file and add this short script using vim.  
```
# open .profile
sudo vim ~/.profile

# add this script and save
if [ -d "/usr/local/cuda/bin/" ]; then
    export PATH=/usr/local/cuda/bin${PATH:+:${PATH}}
    export LD_LIBRARY_PATH=/usr/local/cuda/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
fi
```
So to activate it, let's run this command
```
source ~/.profile
```
As we just added the CUDA path to our **.profile**, now the shell knows where to find CUDA.  

<br />

Now let's verify our cuDNN installation  /*/optional\*\
```bash
cp -r /usr/src/cudnn_samples_v7/ $HOME
cd $HOME/cudnn_samples_v7/mnistCUDNN
make clean && make
./mnistCUDNN
```


