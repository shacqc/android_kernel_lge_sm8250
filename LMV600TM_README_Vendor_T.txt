1. Android build
  - Download original android source code ( android-11.0.0_r35 ) from http://source.android.com
  ( $repo init -u https://android.googlesource.com/platform/manifest -b android-11.0.0_r35
    $repo sync -cdq -j12 --no-tags
    $repo start android-11.0.0_r35 --all
  )
	   
  - Then, merge the source into the android source code
  - Before Doing Android Compilation please untar kernel tar file, as there are some dependency files exists between android and Kernel.
  - Run following scripts to build android
    a) source build/envsetup.sh
    b) lunch 1                                        
    c) make -j4
	
	
  - When you compile the android source code, you have to add google original prebuilt source(toolchain) into the android directory.
  - After build, you can find output at out/target/product/generic

2. Kernel Build  
  - Uncompress using following command at the android directory
    a) tar -xvzf *_Kernel_T.tar.gz 
  - When you compile the kernel source code, you have to add google original "prebuilt" source(toolchain) into the android directory.
  - Run following scripts to build kernel

 1. cd kernel/msm-4.19 
 2. mkdir -p out 
 3. echo CONFIG_BUILD_ARM64_DT_OVERLAY=y >> arch/arm64/configs/vendor/timelm-perf_defconfig 
 4. make ARCH=arm64 O=./out REAL_CC=../../../prebuilts/clang/host/linux-x86/clang-r353983c/bin/clang CLANG_TRIPLE=aarch64-linux-gnu- CROSS_COMPILE=../../../prebuilts/gcc/linux-x86/aarch64/aarch64-linux-android-4.9/bin/aarch64-linux-android- DTC_EXT=../../../prebuilts/misc/linux-x86/dtc/dtc vendor/timelm-perf_defconfig 
 5. make ARCH=arm64 O=./out REAL_CC=../../../prebuilts/clang/host/linux-x86/clang-r353983c/bin/clang CLANG_TRIPLE=aarch64-linux-gnu- CROSS_COMPILE=../../../prebuilts/gcc/linux-x86/aarch64/aarch64-linux-android-4.9/bin/aarch64-linux-android- DTC_EXT=../../../prebuilts/misc/linux-x86/dtc/dtc -j4


 * "-j4" : The number, 4, is the number of multiple jobs to be invoked simultaneously. 
        - After build, you can find the build image(Image.gz) at out/arch/arm64/boot.
.
	
 