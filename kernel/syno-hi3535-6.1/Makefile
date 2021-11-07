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
KernelConfig = $(WORK_DIR)/../modify/linux/synoconfigs/hi3535
KernelTarget = uImage
KernelImagePath = $(KernelDir)/arch/arm/boot/$(KernelTarget)
SynoKERNEL_CFG =syno_kernel
KernelTargetOutPath = $(WORK_DIR)/../../../../DSM_NVR216/modify/
KO_TARGET_DIR=$(WORK_DIR)/../../../../DSM_NVR216/modify/modules/
KernelModifyDIR = $(WORK_DIR)/../modify/linux/
##########################################################################################
#task [2]	build kernel
##########################################################################################
kernel: 
	@echo "---------task [2] build kernel"
	cp $(KernelConfig) $(KernelDir)/arch/arm/configs/$(SynoKERNEL_CFG)_defconfig
	cp -rf $(KernelModifyDIR) $(KernelDir)
	make -C $(KernelDir) ARCH=$(ARCH) CROSS_COMPILE=$(ToolChainPrefix)  $(SynoKERNEL_CFG)_defconfig
	make -C $(KernelDir) ARCH=$(ARCH) CROSS_COMPILE=$(ToolChainPrefix)  $(KernelTarget) -j 16 
	cp $(KernelImagePath) $(KernelTargetOutPath)/zImage

kernel_menuconfig:
	cp $(KernelConfig) $(KernelDir)/arch/arm/configs/$(SynoKERNEL_CFG)_defconfig
	make -C $(KernelDir) ARCH=$(ARCH) CROSS_COMPILE=$(ToolChainPrefix)  $(SynoKERNEL_CFG)_defconfig
	make -C $(KernelDir) ARCH=$(ARCH) CROSS_COMPILE=$(ToolChainPrefix)  menuconfig

kernel_savecfg:
	cp $(KernelDir)/.config  $(KernelConfig);

kernel_modules: kernel
	make -C $(KernelDir) ARCH=$(ARCH) CROSS_COMPILE=$(ToolChainPrefix) modules -j 16
	make -C $(KernelDir) ARCH=$(ARCH) CROSS_COMPILE=$(ToolChainPrefix) modules_install INSTALL_MOD_PATH=$(KO_TARGET_DIR)
	
	
kernel_clean:
	make -C $(KernelDir) ARCH=$(ARCH) CROSS_COMPILE=$(ToolChainPrefix) distclean