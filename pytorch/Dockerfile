FROM dustynv/l4t-pytorch:r35.3.1

# The current Seeed reComputer J4012 balenaOS image is based on L4T 35.3.1

# Add NVIDIA sources to install software - not really needed here as base image has all dependencies...
RUN echo "deb https://repo.download.nvidia.com/jetson/common r35.3 main" >>  /etc/apt/sources.list.d/nvidia.list \
    && echo "deb https://repo.download.nvidia.com/jetson/t234 r35.3 main" >>  /etc/apt/sources.list.d/nvidia.list \
    && apt-key adv --fetch-key http://repo.download.nvidia.com/jetson/jetson-ota-public.asc
    
# Don't prompt with any configuration questions
ENV DEBIAN_FRONTEND noninteractive

# Install some utils and CUDA/CuDNN dependencies
RUN \
    apt-get update && apt-get install -y lbzip2 unzip jq libegl1 binutils xz-utils bzip2


# Download and install BSP binaries for L4T 35.3.1
RUN \
    cd /tmp/ && wget https://developer.nvidia.com/downloads/embedded/l4t/r35_release_v3.1/release/jetson_linux_r35.3.1_aarch64.tbz2 && \
    tar xf jetson_linux_r35.3.1_aarch64.tbz2 && \
    cd Linux_for_Tegra && \
    sed -i 's/config.tbz2\"/config.tbz2\" --exclude=etc\/hosts --exclude=etc\/hostname/g' apply_binaries.sh && \
    sed -i 's/install --owner=root --group=root \"${QEMU_BIN}\" \"${L4T_ROOTFS_DIR}\/usr\/bin\/\"/#install --owner=root --group=root \"${QEMU_BIN}\" \"${L4T_ROOTFS_DIR}\/usr\/bin\/\"/g' nv_tegra/nv-apply-debs.sh && \
    sed -i 's/chroot . \//  /g' nv_tegra/nv-apply-debs.sh && \
    ./apply_binaries.sh -r / --target-overlay && cd .. \
    rm -rf Linux_for_Tegra && \
    echo "/usr/lib/aarch64-linux-gnu/tegra" > /etc/ld.so.conf.d/nvidia-tegra.conf && ldconfig
    

ENV CUDA_INSTALL_DIR /usr/local/cuda-11.4
ENV CUDNN_INSTALL_DIR /usr/local/cuda-11.4


CMD ["sleep", "infinity"]
