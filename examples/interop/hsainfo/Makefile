# ===--------------------------------------------------------------------------
#               ATMI (Asynchronous Task and Memory Interface)
#
#  This file is distributed under the MIT License. See LICENSE.txt for details.
# ===--------------------------------------------------------------------------
SHELL=/bin/bash

#BUILDROOT
BUILDROOT = $(shell pwd | sed 's/examples.*$$//')
#$(info BUILDROOT $(BUILDROOT))
-include $(BUILDROOT)/atmi-config.mak

#Set ATMI Environment variables
ATMI_RUNTIME_PATH ?= /opt/rocm/atmi

ATMI_BIN ?= ${ATMI_RUNTIME_PATH}/bin
ATMI_INC ?= ${ATMI_RUNTIME_PATH}/include
ATMI_LIB ?= ${ATMI_RUNTIME_PATH}/lib

#Set HSA Environment variables
HSA_RUNTIME_PATH ?= /opt/rocm/hsa
#Set ROCM device environment variables
ROCM_DEVICE_PATH ?= /opt/rocm

#Set ROCM device lib environment variables
ROCM_DEVICE_PATH ?= /opt/rocm

#Set LC Environment variables
AMDLLVM ?= /opt/amd/llvm

AMDGPU_TARGET_TRIPLE ?= amdgpu--amdhsa

#MCPU
MCPU ?= $(shell ${ATMI_RUNTIME_PATH}/bin/mygpu)
#$(info MCPU $(MCPU))

# Host compiler
CXX = g++
CXXFLAGS =-O3 -g -std=c++11
#CXXFLAGS += -v

INC_FLAGS=-I${ATMI_INC} -I${HSA_RUNTIME_PATH}/include -I${HSA_RUNTIME_PATH}/include/hsa -I.

LIBS=-latmi_runtime -lhsa-runtime64
LIB_FLAGS=-L${ATMI_RUNTIME_PATH}/lib -L${HSA_RUNTIME_PATH}/lib

OBJS = hsainfo

.PHONY: clean all

all: $(OBJS)

hsainfo: hsainfo.cpp 
	$(CXX) -o $@ hsainfo.cpp $(CXXFLAGS) $(LIBS) $(LIB_FLAGS) $(INC_FLAGS)

clean:
	rm -rf *.o $(OBJS)

test:
	env LD_LIBRARY_PATH=${ATMI_RUNTIME_PATH}/lib:${HSA_RUNTIME_PATH}/lib:${LD_LIBRARY_PATH} ./hsainfo
