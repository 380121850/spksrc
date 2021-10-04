KERNEL_ARCH = hi3535
KERNEL_VERS = 6.1
KERNEL_BUILD = 15152
KERNEL_DIST = linux-3.4.x
KERNEL_BASE_ARCH = arm

include ../../mk/spksrc.kernel.mk
# Configure the included makefiles

NAME= $(KERNEL_NAME)
ARCH=$(KERNEL_BASE_ARCH)
ToolChainPrefix=$(TC_PREFIX)
KernelDir = $(WORK_DIR)/linux/
KernelConfig = $(KernelDir)/synoconfigs/hi3535
KernelTarget = uImage
KernelImagePath = $(KernelDir)/arch/arm/boot/$(KernelTarget)
SynoKERNEL_CFG =syno_kernel
KernelTargetOutPath = $(WORK_DIR)/../../../../../../tmp/DSM_NVR216_15284/

##########################################################################################
#task [2]	build kernel
##########################################################################################
kernel: 
	@echo "---------task [2] build kernel"
	cp $(KernelConfig) $(KernelDir)/arch/arm/configs/$(SynoKERNEL_CFG)_defconfig
	make -C $(KernelDir) ARCH=$(ARCH) CROSS_COMPILE=$(ToolChainPrefix)  $(SynoKERNEL_CFG)_defconfig
	make -C $(KernelDir) ARCH=$(ARCH) CROSS_COMPILE=$(ToolChainPrefix)  $(KernelTarget) -j 16 
	cp $(KernelImagePath) $(KernelTargetOutPath)/

kernel_menuconfig:
	cp $(KernelConfig) $(KernelDir)/arch/arm/configs/$(SynoKERNEL_CFG)_defconfig
	make -C $(KernelDir) ARCH=$(ARCH) CROSS_COMPILE=$(ToolChainPrefix)  $(SynoKERNEL_CFG)_defconfig
	make -C $(KernelDir) ARCH=$(ARCH) CROSS_COMPILE=$(ToolChainPrefix)  menuconfig

kernel_savecfg:
	cp $(KernelDir)/.config  $(KernelConfig);

kernel_modules: kernel
	make -C $(OSDRV_DIR)/$(KERNEL_VER) ARCH=arm CROSS_COMPILE=$(OSDRV_CROSS)- O=$(PUB_KERNEL_TARGET_DIR) modules -j 16
	
kernel_clean:
	rm $(PUB_IMAGE_DIR)/$(UIMAGE) -rf
	make -C $(OSDRV_DIR)/$(KERNEL_VER) ARCH=arm CROSS_COMPILE=$(OSDRV_CROSS)- O=$(PUB_KERNEL_TARGET_DIR) distclean
	rm $(OSDRV_DIR)/$(KERNEL_VER)/arch/arm/configs/$(KERNEL_CFG)_defconfig -rf
	rm $(PUB_KERNEL_TARGET_DIR) -rf