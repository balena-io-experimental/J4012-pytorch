# Seeed J4012 PyTorch/TensorRT Example

This is a sample for running visual inferencing on the Seeed J4012 reComputer (NVIDIA Jetson Orin NX) hardware using balenaOS. See the [Getting Started Guide](https://docs.balena.io/learn/getting-started/jetson-orin-nx-seeed-j4012/nodejs/), [Jetson-flash](https://github.com/balena-os/jetson-flash), and [our Forums](https://forums.balena.io/) if you need more details getting started using the balena platform.

## Usage

For one-click deploy, click the button below:

[![balena deploy button](https://www.balena.io/deploy.svg)](https://dashboard.balena-cloud.com/deploy?repoUrl=https://github.com/balena-io-experimental/J4012-pytorch)

To test the TensorRT is running correctly on the NVIDIA hardware:

- Go to the `/usr/src/tensorrt/samples` folder
- Run `make TARGET=aarch64` - this could take 15 minutes to compile all the samples
- Go to the `/usr/src/tensorrt/bin` folder
- Run `./sample_onnx_mnist`

You should see `Building and running a GPU inference engine for Onnx MNIST` and a bunch of test output, ending with:

`&&&& PASSED TensorRT.sample_onnx_mnist [TensorRT v8502] # ./sample_onnx_mnist`

## More information


This example repo is using the project https://github.com/dusty-nv/jetson-inference, which is based on the [NVIDIA l4T PyTorch](https://catalog.ngc.nvidia.com/orgs/nvidia/containers/l4t-pytorch) base image.

However, the "jetson-interface" project fails to build in the container, so you should use the [NVIDIA-supplied examples](https://docs.nvidia.com/deeplearning/tensorrt/archives/tensorrt-713/sample-support-guide/index.html#samples) which are located in the container at `/usr/src/tensorrt/samples` as mentioned above. Below is another NVIDIA example that does run in the container.

## Object Detection With The ONNX TensorRT Backend In Python 

Here is a quick start to run this example: (full documentation [here](https://docs.nvidia.com/deeplearning/tensorrt/archives/tensorrt-713/sample-support-guide/index.html#yolov3_onnx))

In the container, do the following: (note: `/inference-store` is simply a persistent volume for storing models, etc...)

```
cd /usr/src/tensorrt/samples/python/
python3 downloader.py -d /inference-store -f /usr/src/tensorrt/samples/python/yolov3_onnx/download.yml
cd yolov3_onnx
python3 yolov3_to_onnx.py -d /inference-store
python3 onnx_to_tensorrt.py  -d /inference-store
```

If successful, you should see:

```
Running inference on image /jetson-inference/python/training/classification/models/samples/python/yolov3_onnx/dog.jpg...
[[134.94005922 219.30816557 184.32604687 324.51474599]
 [ 98.63753808 136.02425953 499.65646314 298.39950069]
 [477.79566252  81.31128895 210.98671105  86.85283442]] [0.9985233  0.99885205 0.93972876] [16  1  7]
Saved image with bounding boxes of detected objects to dog_bboxes.png.
```

Now you can modify `onnx_to_tensorrt.py` to run your own inferences!

