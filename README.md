# PaddleSharp [![QQ](https://img.shields.io/badge/QQ_Group-579060605-52B6EF?style=social&logo=tencent-qq&logoColor=000&logoWidth=20)](https://jq.qq.com/?_wv=1027&k=K4fBqpyQ)

💗.NET Wrapper for `PaddleInference` C API, include [PaddleOCR](./docs/ocr.md), [PaddleDetection](./docs/detection.md), support **Windows**(x64), NVIDIA GPU and **Linux**(Ubuntu-20.04 x64).

[PaddleOCR](./docs/ocr.md) support 14 OCR languages model download on-demand, allow rotated text angle detection, 180 degree text detection.

[PaddleDetection](./docs/detection.md) support PPYolo detection model and PicoDet model.

## NuGet Packages/Docker Images

| NuGet Package                                        | Version                                                                                                                                                                                  | Description                                                                         |
| ---------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| Sdcb.PaddleInference                                 | [![NuGet](https://img.shields.io/nuget/v/Sdcb.PaddleInference.svg)](https://nuget.org/packages/Sdcb.PaddleInference)                                                                     | Paddle Inference C API .NET binding                                                 |
| Sdcb.PaddleOCR                                       | [![NuGet](https://img.shields.io/nuget/v/Sdcb.PaddleOCR.svg)](https://nuget.org/packages/Sdcb.PaddleOCR)                                                                                 | PaddleOCR library(based on Sdcb.PaddleInference)                                    |
| Sdcb.PaddleOCR.KnownModels                           | [![NuGet](https://img.shields.io/nuget/v/Sdcb.PaddleOCR.KnownModels.svg)](https://nuget.org/packages/Sdcb.PaddleOCR.KnownModels)                                                         | Helper to download PaddleOCR models                                                 |
| Sdcb.PaddleInference.runtime.win64.mkl               | [![NuGet](https://img.shields.io/nuget/v/Sdcb.PaddleInference.runtime.win64.mkl.svg)](https://nuget.org/packages/Sdcb.PaddleInference.runtime.win64.mkl)                                 | Paddle Inference C API Windows x64(mkl-dnn) Native binding                          |
| Sdcb.PaddleInference.runtime.win64.cuda11_cudnn8_tr7 | [![NuGet](https://img.shields.io/nuget/v/Sdcb.PaddleInference.runtime.win64.cuda11_cudnn8_tr7.svg)](https://nuget.org/packages/Sdcb.PaddleInference.runtime.win64.cuda11_cudnn8_tr7.mkl) | Paddle Inference C API Windows x64(GPU CUDA 11/cuDNN 8.0/TensorRT 7) Native binding |
| Sdcb.PaddleDetection                                 | [![NuGet](https://img.shields.io/nuget/v/Sdcb.PaddleDetection.svg)](https://nuget.org/packages/Sdcb.PaddleDetection)                                                                     | PaddleDetection library(based on Sdcb.PaddleInference)                              |

**Note**: Linux does not need a native binding `NuGet` package like windows(`Sdcb.PaddleInference.runtime.win64.mkl`), instead, you can/should based from a [Dockerfile](https://hub.docker.com/r/sdflysha/ubuntu20-dotnet6-paddleocr2.2.1) to development:

| Docker Images                               | Version                                                                                                                                                        | Description                                                                        |
| ------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| sdflysha/ubuntu20-dotnet6-paddleocr2.2.1    | [![Docker](https://img.shields.io/docker/v/sdflysha/ubuntu20-dotnet6-paddleocr2.2.1)](https://hub.docker.com/r/sdflysha/ubuntu20-dotnet6-paddleocr2.2.1)       | PaddleInference 2.2.1, OpenCV 4.5.3, based on official Ubuntu 20.04 .NET 6 Runtime |
| sdflysha/ubuntu20-dotnet6sdk-paddleocr2.2.1 | [![Docker](https://img.shields.io/docker/v/sdflysha/ubuntu20-dotnet6sdk-paddleocr2.2.1)](https://hub.docker.com/r/sdflysha/ubuntu20-dotnet6sdk-paddleocr2.2.1) | PaddleInference 2.2.1, OpenCV 4.5.3, based on official Ubuntu 20.04 .NET 6 SDK     |

# Usage
* PaddleOCR: [PaddleOCR](./docs/ocr.md)
* PaddleDetection: [PaddleDetection](./docs/detection.md)

# FAQ
## Why my code runs good in my windows machine, but DllNotFoundException in other machine:
1. Please ensure the [latest Visual C++ Redistributable](https://aka.ms/vs/17/release/vc_redist.x64.exe) was installed in `Windows`(typically it should automatically installed if you have `Visual Studio` installed)
Otherwise, it will failed with following error(Windows only):
   ```
   DllNotFoundException: Unable to load DLL 'paddle_inference_c' or one of its dependencies (0x8007007E)
   ```

2. Many old CPUs does not support AVX instructions, please ensure your CPU supports AVX, or download the x64-noavx-openblas dlls and disable Mkldnn: `PaddleConfig.Defaults.UseMkldnn = false;`

## How to enable GPU?
Enable GPU support can significantly improve the throughput and lower the CPU usage.

Steps to use GPU in windows:
1. (for windows) Install the package: `Sdcb.PaddleInference.runtime.win64.cuda11_cudnn8_tr7` instead of `Sdcb.PaddleInference.runtime.win64.mkl`, **do not** install both.
2. Install CUDA from NVIDIA, and configure environment variables to `PATH` or `LD_LIBRARY_PATH`(linux)
3. Install cuDNN from NVIDIA, and configure environment variables to `PATH` or `LD_LIBRARY_PATH`(linux)
4. Install TensorRT from NVIDIA, and configure environment variables to `PATH` or `LD_LIBRARY_PATH`(linux)

You can refer this blog page for GPU in Windows: [关于PaddleSharp GPU使用 常见问题记录](https://www.cnblogs.com/cuichaohui/p/15766519.html)

If you're using Linux, you need to compile your own OpenCvSharp4 environment following the [docker build scripts](./build/docker/ubuntu20-dotnet6-paddleocr2.2.1/Dockerfile) follow the CUDA/cuDNN/TensorRT configuration tasks.

After these steps completed, you can try specify `PaddleConfig.Defaults.UseGpu = true` in begin of your code and then enjoy😁.

# Thanks & Sponsors
* 深圳-钱文松
* iNeuOS工业互联网操作系统：http://www.ineuos.net

# Contact
QQ group of C#/.NET computer vision technical communicate(C#/.NET计算机视觉技术交流群): **579060605**
![](./assets/qq.png)
