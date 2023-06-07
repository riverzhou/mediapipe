
Mediapipe v0.10.0 @ Ubuntu 22.04 (22.04c):

```bash

su -

apt update && apt upgrade -y

apt install -y linux-oem-22.04c linux-tools-oem-22.04c linux-modules-nvidia-530-oem-22.04c

apt install -y mesa-common-dev libegl1-mesa-dev libgles2-mesa-dev mesa-utils
apt install -y libnvidia-compute-530 libnvidia-decode-530 nvidia-compute-utils-530
apt install -y nvidia-cuda-dev nvidia-cuda-toolkit libcupti-dev libcupti11.5 nvidia-cudnn
apt install -y libopencv-contrib-dev libopencv-dev libopencv-dnn-dev libopencv-ml-dev libopencv-photo-dev ffmpeg
apt install -y protobuf-compiler python3-pip
apt install -y libmkl-dev libdnnl-dev libmkl-full-dev

wget https://github.com/bazelbuild/bazel/releases/download/6.1.1/bazel_6.1.1-linux-x86_64.deb
apt install ./bazel_6.1.1-linux-x86_64.deb

pip install -U numpy

reboot

su -

cd /usr/lib/nvidia-cuda-toolkit/nvvm
mkdir nvvm
cd nvvm
ln -s ../libdevice

cd /usr/include/python3.10
rm numpy
ln -s /usr/local/lib/python3.10/dist-packages/numpy/core/include/numpy .

cd /usr/include/
ln -s opencv4/opencv2 .

cd /usr/lib/x86_64-linux-gnu/
ln -s libopencv_calib3d.so.4.5.4d libopencv_calib3d.so.4.5
ln -s libopencv_features2d.so.4.5d libopencv_features2d.so.4.5
ln -s libopencv_highgui.so.4.5d libopencv_highgui.so.4.5
ln -s libopencv_video.so.4.5d libopencv_video.so.4.5
ln -s libopencv_videoio.so.4.5d libopencv_videoio.so.4.5
ln -s libopencv_imgcodecs.so.4.5d libopencv_imgcodecs.so.4.5
ln -s libopencv_imgproc.so.4.5d libopencv_imgproc.so.4.5
ln -s libopencv_core.so.4.5d libopencv_core.so.4.5

vim /etc/profile.d/tf-cuda.sh
export TF_CUDA_PATHS=/usr/include,/usr/include/x86_64-linux-gnu,/usr/lib/x86_64-linux-gnu,/usr/lib/nvidia-cuda-toolkit,/usr/lib/nvidia-cuda-toolkit/bin

git clone https://github.com/riverzhou/mediapipe.git
git checkout origin/cuda -b cuda

python3 setup.py gen_protos && python3 setup.py bdist_wheel

```

