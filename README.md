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
 Remove any existing CUDA folders you may have in /usr/local/
 ```bash
 sudo rm -rf /usr/local/cuda*
 ```
 ## Install
 
