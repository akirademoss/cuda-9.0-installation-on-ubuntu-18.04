# CUDA 9.0 installation on Ubuntu 18.04 LTS 
This file contains step by step instructions to install cuda v9.0 and cudnn 7.3.0 in ubuntu 18.04.  This version of CUDA will work with the tensorflow-gpu install.

## Summary of Steps 
```
1.) Verify you hava a cuda capable GPU
2.) Install nvidia cuda toolkit's software dependencies
3.) Download and install the nvidia cuda toolkit and cudnn
4.) Setup environmental variables
5.) Verify the installation
```


## 1.) Verify you hava a CUDA capable GPU

#### run the following command
```
lspci | grep -i nvidia
```

## 2.) Install nvidia cuda toolkit's software dependencies

#### install nvidia driver 
```
sudo apt install nvidia-compute-utils-390 
sudo apt install nvidia-driver-390 
```

#### install other import packages
```
sudo apt-get install g++ freeglut3-dev build-essential libx11-dev libxmu-dev libxi-dev libglu1-mesa libglu1-mesa-dev
```

#### cuda 9 requireces gcc>=6, g++>=6, verify that your system meets these requrements if so, move to step 2.)
```
g++ -v
gcc -v
```

#### cuda 9 requires gcc>=6
```
sudo apt install gcc-6
sudo apt install g++-6
```

#### set up symlinks for gcc/g++
```
sudo ln -s /usr/bin/gcc-6 /usr/local/cuda/bin/gcc
sudo ln -s /usr/bin/g++-6 /usr/local/cuda/bin/g++
```

## 3.) Download and install the nvidia cuda toolkit and cudnn

#### downoad one of the "runfile (local)" installation packages from cuda toolkit archive 
```
wget https://developer.nvidia.com/compute/cuda/9.0/Prod/local_installers/cuda_9.0.176_384.81_linux-run
```

#### make the download file executable
```
chmod +x cuda_9.0.176_384.81_linux.run 
sudo ./cuda_9.0.176_384.81_linux.run --override
```

#### answer following questions while installation begin
```
You are attempting to install on an unsupported configuration. Do you wish to continue? y
Install NVIDIA Accelerated Graphics Driver for Linux-x86_64 384.81? n
Install the CUDA 9.0 Toolkit? y
```

#### install cuDNN v7.3.0 for cuda 9
in order to download cuDNN you have to be regeistered [here](https://developer.nvidia.com/cudnn)
```
To access the file you will first need to login and agree to terms of use
You will need to manually download version 7.3.0 for Cuda 9.0.
It will appear in your Downloads directory as cudnn-9.0-linux-x64-v7.3.0.29.tgz
```

#### extract cuda directory
```
cd ~/Downloads
tar -xzvf cudnn-9.0-linux-x64-v7.3.0.29.tgz
```

#### copy the following files into the cuda toolkit directory.
```
sudo cp -P cuda/include/cudnn.h /usr/local/cuda-9.0/include
sudo cp -P cuda/lib64/libcudnn* /usr/local/cuda-9.0/lib64/
sudo chmod a+r /usr/local/cuda-9.0/lib64/libcudnn*
```

## 4.) Setup your environment variables

#### add cuda-9.0/bin to your path and cuda-9.0/lib64 to your library path
```
echo 'export PATH=/usr/local/cuda-9.0/bin:$PATH' >> ~/.bashrc
echo 'export LD_LIBRARY_PATH=/usr/local/cuda-9.0/lib64:$LD_LIBRARY_PATH' >> ~/.bashrc
source ~/.bashrc
```

## 5.) Verify the installation

#### reboot to activate changes
```
reboot
```

#### verify installation
```
nvidia-smi
nvcc -V
```

#### your terminal output should look similar to this:
![nvidia-smi](https://user-images.githubusercontent.com/8731829/50403622-ae5e0780-0765-11e9-96c3-cf649dbaeac3.png)

