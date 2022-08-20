------------
This repository comprises the NASA CFL3D V6.7 code, as of year 2022. Though the entire package of files is extracted from official NASA Git (https://github.com/nasa/CFL3D), the purpose of creating this repository is to share the Cmake build system for the code. This Cmake build system for CFL3D code was originally written by Dr. Cheng Di (https://github.com/nasa/CFL3D/pulls) few years back. The procedure to install using this Cmake system is provided below as well as in the notes.txt file.

### Compilation and running
```shell
## prerequirement (tested in Ubuntu 16.04)
sudo apt-get install libopenmpi-dev gfortran build-essential git cmake -y
# in RHEL/CentOS, you may try this:
sudo yum install openmpi-devel gcc gcc-gfortran git cmake


## manually build cgns 2.5 without hdf5 and mpi
# you can also use your own cgns library if you put your cgnslib_f.h and libcgns.a in /usr/share/include and /usr/share/lib respectively
cd CFL3D/external/cgns
./build_cgns

## build cfl3d executables out of source
cd ../build
cmake ..
make
# or you may benefit from parallel run, try:
make -j`nproc`
# There will be a lot of warnings because I do not turn off all warnings as the original CFL3D build system do.
cd bin
# Add this path in the basic file for env. For Example see below #
pwd
# Add Environment in your bashrc (Modify the path according to your installation) #

#CFL3D
export PATH=~/CFL3D/build/bin:$PATH
alias use_cfl3d='export PATH=~/CFL3D/build/bin:$PATH'

Now, refresh the basrhrc file -

source ~/.bashrc

close the terminal and restart system/logout and login if using a cluster.
————————————————————————
THATS IT. YOU ARE GOOD TO GO!

————————————————————————
# FOR TESTING CFL3D
----------------------------------------------------
cd CFL3D-master/docs/Cfl3dv6/  (testcase directory)
cd 2DTestcases/Flatplate/      (2D Flatplate testcase)
gunzip Flatplate.tar.Z
tar -xvf Flatplate.tar
cd Flatplate
splitter < split.inp_1blk
cfl3d_seq < grdflat5.inp &
tail -f cfl3d.out # To monitor the steps and residuals
----------------------------------------------------
The complete set of instructions to run each such testcase, can be found in the official CFL3D site.
```
