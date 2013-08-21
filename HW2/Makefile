NVCC=nvcc
CC=arm-linux-gnueabihf-g++-4.7

###################################
# These are the default install   #
# locations on most linux distros #
###################################

CUDA_PATH        := /usr/local/cuda
CUDA_INCLUDEPATH := $(CUDA_PATH)/include
export PATH := $(CUDA_PATH)/bin:$(PATH)

OPENCV_PATH        := /home/ender/Downloads/kayla/rootfs/opt/opencv
OPENCV_LIBPATH     := $(OPENCV_PATH)/lib
OPENCV_INCLUDEPATH := $(OPENCV_PATH)/include

###################################################
# On Macs the default install locations are below #
###################################################

#OPENCV_LIBPATH=/usr/local/lib
#OPENCV_INCLUDEPATH=/usr/local/include

OPENCV_LIBS=-lopencv_core -lopencv_imgproc -lopencv_highgui

######################################################
# On Macs the default install locations are below    #
# ####################################################

#CUDA_INCLUDEPATH=/usr/local/cuda/include
#CUDA_LIBPATH=/usr/local/cuda/lib

NVCC_OPTS=-O3 -arch=sm_35 -target-cpu-arch=ARM -Xcompiler -Wall -Xcompiler -Wextra -m32 -ccbin=$(CC)

GCC_OPTS=-O3 -Wall -Wextra

student: main.o student_func.o compare.o reference_calc.o Makefile
	$(NVCC) -o HW2 main.o student_func.o compare.o reference_calc.o -L $(OPENCV_LIBPATH) $(OPENCV_LIBS) $(NVCC_OPTS)

main.o: main.cpp timer.h utils.h HW2.cpp
	$(CC) -c main.cpp $(GCC_OPTS) -I $(OPENCV_INCLUDEPATH) -I $(CUDA_INCLUDEPATH)

student_func.o: student_func.cu reference_calc.cpp utils.h
	$(NVCC) -c student_func.cu $(NVCC_OPTS)

compare.o: compare.cpp compare.h
	$(CC) -c compare.cpp -I $(OPENCV_INCLUDEPATH) $(GCC_OPTS) -I $(CUDA_INCLUDEPATH)

reference_calc.o: reference_calc.cpp reference_calc.h
	$(CC) -c reference_calc.cpp -I $(OPENCV_INCLUDEPATH) $(GCC_OPTS) -I $(CUDA_INCLUDEPATH)

clean:
	rm -f *.o *.png hw
