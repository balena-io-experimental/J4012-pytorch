# Seeed J4012 PyTorch/TensorRT Example

This is a sample for running visual inferencing on the Seeed J4012 reComputer (NVIDIA Jetson Orin NX) hardware using balenaOS.

## Usage

This sample is still under development...

To test the TensorRT is running correctly on the NVIDIA hardware:

- Go to the `/usr/src/tensorrt/samples` folder
- Run `make TARGET=aarch64` - this could take 15 minutes to compile all the samples
- Go to the `/usr/src/tensorrt/bin` folder
- Run `./sample_onnx_mnist`

You should see `Building and running a GPU inference engine for Onnx MNIST` and a bunch of test output, ending with:

`&&&& PASSED TensorRT.sample_onnx_mnist [TensorRT v8502] # ./sample_onnx_mnist`

## More information

This is running the project https://github.com/dusty-nv/jetson-inference

Usage tutorial: [https://www.forecr.io/blogs/ai-algorithms/hello-ai-world](https://www.forecr.io/blogs/ai-algorithms/hello-ai-world)

To use the tutorial above, follow the steps at "How to Build the Project from Source".
