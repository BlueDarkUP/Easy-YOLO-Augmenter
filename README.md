# Easy-Augment-Toolkit

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Python Version](https://img.shields.io/badge/Python-3.8%2B-brightgreen.svg)]()
[![Framework](https://img.shields.io/badge/Framework-PyQt5-orange.svg)]()
[![Backend](https://img.shields.io/badge/Backend-Albumentations-red.svg)]()

一个强大且直观的桌面应用程序，用于图像数据集的增强，特别为目标检测任务（YOLO 格式）优化。通过友好的图形用户界面，您无需编写任何代码即可快速扩增您的数据集。

An intuitive and powerful desktop application for image dataset augmentation, especially optimized for object detection tasks (YOLO format). Augment your dataset in minutes without writing a single line of code, thanks to a friendly graphical user interface.

**支持语言 (Languages Supported):** English, 简体中文.
---

### ✨ 核心特性

*   **直观的图形界面**: 所有操作都在可视化界面中完成，告别复杂的命令行。
*   **高性能处理**: 基于 `multiprocessing` 实现多进程并行处理，充分利用多核CPU，显著提升增强速度。
*   **强大的增强后端**: 由业界领先的 `Albumentations` 库驱动，提供丰富、高效的增强变换。
*   **专为目标检测优化**: 完全支持 **YOLO (.txt)** 格式的边界框（bounding box）同步增强，确保标签与图像完美匹配。
*   **高度可配置**: 自由组合多种增强方法，并对每一种方法的参数进行精细调整。
*   **跨语言支持**: 内置中文和英文界面，方便不同地区的用户使用。

---

### 🚀 快速开始

直接双击运行 `AugmentationTool.exe` 即可启动程序。无需安装 Python 或任何依赖！

### 📖 使用指南

1.  **选择目录**:
    *   **源数据集目录**: 选择您原始数据集的根目录。该目录应包含一个名为 `images` 的文件夹，以及一个可选的 `labels` 文件夹。
        ```
        - my_dataset/
          - images/
            - train/
              - img1.jpg
              - img2.png
            - val/
              - img3.jpg
          - labels/ (可选)
            - train/
              - img1.txt
              - img2.txt
            - val/
              - img3.txt
        ```
    *   **输出目录**: 选择一个用于保存增强后数据的新目录。
2.  **配置参数**:
    *   **每图生成数量**: 设置每张原始图片需要生成多少张增强图片。
    *   **处理进程数**: 设置用于处理任务的CPU核心数。默认为最大核心数以获得最佳性能。
    *   **应用到子集**:勾选您希望处理的子集（如 `train`, `val`）。
3.  **选择并配置增强变换**:
    *   在列表中勾选您想使用的增强方法。
    *   鼠标悬停在方法名称上可以查看其功能说明。
    *   根据需要修改右侧的参数。
4.  **开始任务**:
    *   点击 "开始增强" 按钮。
    *   进度条会显示当前进度，下方的日志窗口会实时输出处理信息。

---

### 🔬 增强变换详解

以下是本工具支持的所有增强方法及其参数说明。

| 变换 (Transform)         | 说明 (Description)                               |
| ------------------------ | ------------------------------------------------ |
| **HorizontalFlip**       | 以一定概率对图像和边界框进行水平翻转。           |
| **VerticalFlip**         | 以一定概率对图像和边界框进行垂直翻转。           |
| **Rotate**               | 在指定角度范围内随机旋转图像和边界框。           |
| **Affine**               | 组合了旋转、缩放、平移的仿射变换，功能强大。     |
| **RandomBrightnessContrast** | 随机改变图像的亮度和对比度。                     |
| **ColorJitter**          | 随机改变图像的亮度、对比度、饱和度和色调。       |
| **GaussNoise**           | 向图像中添加高斯噪声，模拟低光照条件。           |
| **GaussianBlur**         | 使用高斯核模糊图像，模拟失焦效果。               |
| **MotionBlur**           | 模拟相机移动或物体快速移动时产生的运动模糊。     |
| **ISONoise**             | 模拟相机传感器的 ISO 噪声。                      |
| **RGBShift**             | 随机偏移图像的 R, G, B 通道值，产生颜色失真。    |
| **HueSaturationValue**   | 随机改变图像的色调(H)、饱和度(S)和明度(V)。      |
| **RandomResizedCrop**    | 随机裁剪图像的一部分并将其缩放到指定尺寸，对检测小目标友好。 |

#### 参数详细说明

*   **p**: `(float)` 应用该变换的概率，取值范围为 `[0.0, 1.0]`。例如 `p=0.5` 意味着有50%的几率应用此变换。

*   **limit / *_limit**: `(int or tuple)` 定义变换的范围。
    *   如果是一个整数 `L` (如 `Rotate` 的 `limit=20`)，表示范围是 `(-L, L)`。
    *   如果是一个元组 `(min, max)` (如 `GaussianBlur` 的 `blur_limit=(3, 7)`)，表示从 `min` 到 `max` 中随机取值。

*   **scale**: `(float or tuple)` 缩放因子或范围。例如 `(0.9, 1.1)` 表示图像将被随机缩放到原始尺寸的90%到110%之间。

*   **translate_percent**: `(float or tuple)` 按图像尺寸百分比进行平移的范围。例如 `(-0.1, 0.1)` 表示在水平和垂直方向上最多移动图像宽度或高度的10%。

*   **size**: `(int, int)` 裁剪后图像的目标尺寸，格式为 `(height, width)`。
---

### 🤝 贡献

欢迎任何形式的贡献！如果您有好的建议或发现了Bug，请随时提交 [Issues](https://github.com/你的用户名/Easy-Augment-Toolkit/issues)。
如果您想贡献代码，请 Fork 本仓库并提交 Pull Request。

### 📄 许可证

本项目采用 [MIT License](LICENSE) 开源。

### 🙏 致谢

*   **[Albumentations](https://github.com/albumentations-team/albumentations)** - 提供了强大、快速的图像增强核心库。
*   **[PyQt5](https://riverbankcomputing.com/software/pyqt/)** - 构成了本应用的图形用户界面框架。
