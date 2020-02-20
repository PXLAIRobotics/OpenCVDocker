# OpenCVDocker

This repository contains a simple Computer Vision with OpenCV (Python and C++) docker container for exemplary and educational purposes. 


## Prerequisites

First of all you need to run Linux ubuntu natively on your host. An Ubuntu LTS distribution is recommended.
Although other distributions (Arch/Manjaro, Debian, RedHat/CentOS) might also work as long as Docker, `bash` and `glxinfo` from `mesa-utils` are available.

If your host is equiped with a (recent) NVIDIA graphics card, nvidia-docker is recommended instead of the standard docker installation.

### TL;DR

* Linux (Ubuntu LTS recommended)
* Docker or [nvidia docker](https://github.com/NVIDIA/nvidia-docker)
* `bash`
* mesa-utils (`sudo apt install mesa-utils`)


## Structure and usage

The end result of this repository is an Ubuntu 18.04 based OpenCV Docker container.
To differentiate between NVIDIA hosts and normal computers, an intermedate "base" image will be created and used as the fundament for the OpenCV container.
The provided Bash script `0001_build_images.sh` will automatically build the correct base image (in `01a_nvidia_ubuntu18.04/` or `01b_dri_ubuntu18.04/`) for your system.
Thereafter the OpenCV container (in `02_opencv/`) will be build. 

A few Python and C++ OpenCV examples reside in the `Projects` directory. 
This directory will be used as an volume when running the OpenCV container.
All the files and directories will be accessible from inside and when the container is destroyed, the files will still be on your host.
Besides source code the `Projects` directory also contians a few images.

### Building the images

Just run:

```bash
$ ./0001_build_images.sh

```


### Start the OpenCVDocker container

Execute the following command:

```bash
$ ./0002_start_opencv_container.sh
non-network local connections being added to access control list
user@476750474b19:~$
```


### Running the OpenCV examples
The following commands are execute from with in the OpenCV container.

*Remark: Use `<esc>` to close the created windows.*

#### Python

```bash
user@476750474b19:~$ cd Projects/Python/Examples
user@476750474b19:~/Projects/Python/Examples$ python3 example1.py 

   . . .
   
user@476750474b19:~/Projects/Python/Examples$ python3 example2.py 

   . . .
   
user@476750474b19:~/Projects/Python/Examples$ cd ../Webcam/
user@476750474b19:~/Projects/Python/Webcam$ python3 webcam.py 

   . . . 

```

#### C++ 
C++ examples must be build before running.


```bash
user@476750474b19:~$ cd Projects/C++/DisplayImage/
user@476750474b19:~/Projects/C++/DisplayImage$ cmake .
-- The C compiler identification is GNU 7.4.0
-- The CXX compiler identification is GNU 7.4.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Found OpenCV: /usr (found version "3.2.0") 
-- Configuring done
-- Generating done
-- Build files have been written to: /home/user/Projects/C++/DisplayImage
user@476750474b19:~/Projects/C++/DisplayImage$ make
Scanning dependencies of target DisplayImage
[ 50%] Building CXX object CMakeFiles/DisplayImage.dir/DisplayImage.cpp.o
[100%] Linking CXX executable DisplayImage
[100%] Built target DisplayImage
user@476750474b19:~/Projects/C++/DisplayImage$ ./DisplayImage 
usage: DisplayImage.out <Image_Path>
user@476750474b19:~/Projects/C++/DisplayImage$ ./DisplayImage ../../Images/Lenna.png 

   . . .

```
