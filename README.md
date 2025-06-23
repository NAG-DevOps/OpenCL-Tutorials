# OpenCL Tutorials

Hey guys, each sub-directory containing tutorials is a holistic self inclusive directory, with all the necessary source code needed to run, but not necessarily to build. These tutorials require CL2.hpp but use depreciated features from opencl version 1.2. As such setting up your own system may be a tad strange.

I have included CMake files in each directory that can be run using the build.sh file, or manually. These files are to help you with the requirements, and they are quite strict. However if you have better things to do than worry about dependencies and all their nuances, then simply  use docker instead, which will create some lightweight virtualmachines for you to work with instead automatically.

You need only 2 things, docker itself, and nvidia-container-toolkit, the latter is for GPU containers so you can use nvidia GPUs from inside any given container. For further information please see the following two sources:

https://nemesyst.readthedocs.io/en/latest/docker/ while not specifically for these tutorials it gives a good summary of how to use Dockerfiles.

https://wiki.archlinux.org/index.php/Docker the holy bible of linux, which shall endow you with super powers, including usage of docker, and installation of things like nvidia-container-toolkit.

## quick-start:

### create a docker image with all our sources/ everything ready
```sudo docker build -t archer/opencl-tuts .```

### run our docker image with all the GPUs available
```sudo docker run --gpus all -it archer/opencl-tuts bash```

### OR if you dont have nvidia gpus/ you dont want to use GPUs/ don't have nvidia-container-toolkit installed
```sudo docker run -it archer/opencl-tuts bash```

May the force be with you.

# Legacy

The presented tutorials were developed and tested on Windows 10, Visual Studio 2019 and [Intel SDK for OpenCL](https://software.intel.com/en-us/intel-opencl) so that can be run on Windows PCs in the computing labs. Tutorial 4 also depends on the Boost library. If you would like to develop OpenCL programs on your computer you have two options:
 - replicate the [Windows setup](#windows-setup) from the computing labs;
 - use the [multi_os](https://github.com/gcielniak/OpenCL-Tutorials/tree/multi_os) branch, which should allow for running the tutorials on different operating systems, programming environments and OpenCL SDKs. There is limited documentation for this option, however, so you should only choose that option if you are comfortable with installing custom libraries on your specific OS.
 
## Windows Setup
 - OS + IDE: Windows 10, Visual Studio 2019
 - OpenCL SDK: the SDK enables you to develop and compile the OpenCL code. In our case, we use [Intel SDK for OpenCL Applications](https://software.intel.com/en-us/intel-opencl). You are not tied to that choice, however, and can use SDKs by NVidia or AMD - just remember to make modifications in the project include paths. Each SDK comes with a range of additional tools which make development of OpenCL programs easier.
 - OpenCL runtime: the runtime drivers are necessary to run the OpenCL code on your hardware. Both NVidia and AMD GPUs have OpenCL runtime included with their card drivers. For CPUs, you will need to install a dedicated driver by [Intel](https://software.intel.com/en-us/articles/opencl-drivers) or APP SDK for older AMD processors. It seems that AMD’s OpenCL support for newer CPU models was dropped unfortunately. You can check the existing OpenCL support on your PC using [GPU Caps Viewer](http://www.ozone3d.net/gpu_caps_viewer/).
 - Boost library: install the recent [Boost library Windows binaries](https://sourceforge.net/projects/boost/files/boost-binaries/) (e.g. [boost_1_72_0](https://sourceforge.net/projects/boost/files/boost-binaries/1.72.0/boost_1_72_0-msvc-14.2-64.exe/download) for VS2019). Then, add two environmental variables in the command line specifying the location of the include and lib Boost directories. For example, with boost_1_72_0 the commands would look as follows: `setx BOOST_INCLUDEDIR "C:\local\boost_1_72_0"` and `setx BOOST_LIBRARYDIR "C:\local\boost_1_72_0\lib64-msvc-14.2"`.
 - A useful reference if you are struggling to get going: [OpenCL on Windows](http://streamcomputing.eu/blog/2015-03-16/how-to-install-opencl-on-windows/).

## Dependencies

### Ubuntu
 - OpenCL development libs: `sudo apt install ocl-icd-opencl-dev`
 - OpenCL runtime drivers
 - Boost.Compute: from boost-1.61.0, it is part of the library. In particular situations, when you need to keep the older versions of boost (e.g. Ubuntu 16 + ROS Kinetic) you may need to apply the following ugly hack:
 ```
 cd /tmp/
 git clone git://github.com/kylelutz/compute.git
 sudo mv /tmp/compute/include/boost/compute /usr/include/boost
 sudo mv /tmp/compute/include/boost/compute.hpp /usr/include/boost/
```
