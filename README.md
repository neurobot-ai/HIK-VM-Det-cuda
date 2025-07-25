# 基于yolo的目标检测（海康算子输出ROIBOX数组）使用文档
## 2. 环境配置
1. 支持的操作系统：Windows10/11 X64
**此项目只支持在Nvidia显卡上运行。**
1. 运行时依赖 ：此项目需要使用cuda,因此需要安装cuda toolkit以及cuDNN。
   1. 显卡驱动下载：若电脑在此前从未安装过相应的驱动，需先安装显卡驱动，英伟达显卡驱动[下载连接](https://www.nvidia.com/en-us/software/nvidia-app/)。
   2. cuda工具包下载：在安装前现在命令台输入("nvidia-smi.exe")查询**最高支持**的cuda version（就只是最高而已，不需要一定下载这个，强烈建议就只下载cuda11.7），如图所示：
   ![alt text](image/14.jpg)
   在cuda工具包[下载链接](https://nbai-cloud-3-0.oss-ap-southeast-1.aliyuncs.com/yolo-sdk/dependencies/cuda_11.7.1_516.94_windows.exe)下载后安装。(如果是win10的电脑需从官网下载，[下载链接](https://developer.nvidia.com/cuda-11-7-1-download-archive?target_os=Windows&target_arch=x86_64&target_version=10&target_type=exe_local))
   3. cuDNN下载：[下载链接](https://nbai-cloud-3-0.oss-ap-southeast-1.aliyuncs.com/yolo-sdk/dependencies/cudnn-windows-x86_64-8.5.0.96_cuda11-archive.zip)下载完成后解压
   ![alt text](image/20.jpg)
   进入解压完的文件夹，**复制**"bin"、"include"、"lib"这三个文件夹
   ![alt text](image/21.jpg)
   打开“C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA”里面有你安装的对应的cuda工具包版本，再打开这个文件夹。
   ![alt text](image/22.jpg)
   ![alt text](image/23.jpg)
   将cuDNN中复制的三个文件夹粘贴进此文件夹。粘贴完后进入"bin"中应该可以看到里面包含cudnn
   ![alt text](image/24.jpg)
   
1. [下载链接](https://nbai-cloud-3-0.oss-ap-southeast-1.aliyuncs.com/yolo-sdk/dependencies/PublicFile.rar),下载此"PublicFile"文件，解压后打开此"PublicFile"文件夹如下图所示
![alt text](image/1.jpg)
复制里面的内容，粘贴进“C盘”-"Program Files"-"VisionMaster4.4.0"-"Applications"-"PublicFile"-"x64"中
![alt text](image/2.jpg)
2. 复制此文档所在文件夹中的"YOLO_Det",粘贴进“C盘”-"Program Files"-"VisionMaster4.4.0"-"Applications"-"Module(sp)"-"x64"-"Collection"中。
![alt text](image/3.jpg)
![alt text](image/4.jpg)

## 3. 快速入门
下面给出一个示例，帮助您快速了解如何使用此项目完成C++软件开发。本示例使用VS2022版本给出示例。

1. 打开"visionMaster"软件-"通用方案"
![alt text](image/5.jpg)
2. 1. 点击"采集"-"图像源"，将其拖出至中间
   ![alt text](image/6.jpg)
   2. 双击"0图像源1",将像素格式修改为"RGB24"
   ![alt text](image/7.jpg)
3. 1. 点击"逻辑工具"-"格式化"，拖出**两个**
   ![alt text](image/8.jpg)
   ![alt text](image/9.jpg)
   2. 双击"1格式化1"，点击"添加"，“T”，在下面的行中输入“标签路径”（names.txt所在路径），然后点击右下角“保存”
   ![alt text](image/10.jpg)
   3. 双击"2格式化2"，点击"添加"，“T”，在下面的行中输入“模型路径”，然后点击右下角保存
   ![alt text](image/11.jpg)
4. 1. 点击“采集”-“YOLO_Det”,将其拖出，按照如图所示连接
   ![alt text](image/12.jpg)
   ![alt text](image/13.jpg)
   2. 按下图所示，点击"运行参数" -"标签路径最右侧的按钮"-"链接标志的按钮"-"1格式化1"-"格式化结果"
   ![alt text](image/25.jpg)
   3. 同理，点击"模型路径最右侧的按钮"-"链接标志的按钮"-"2格式化2"-"格式化结果"
   ![alt text](image/26.jpg)
   4. 点击右下角的"确定"
5. 1. 点击"逻辑工具"-"脚本",将其拖出，并"3YOLO_Det1"和他连接
   ![alt text](image/28.jpg)
   ![alt text](image/29.jpg)
   2. 双击打开"4脚本1"，点击"输入变量右侧的铅笔"，将"类型"切换成"string",在点击"初始值处的按钮"-"3YOLO_Det1"-"outputString"
   ![alt text](image/30.jpg)
   点击右上角"完成"
   ![alt text](image/31.jpg)
   3. 点击"输出设置",点击"输出变量右侧的铅笔"，修改成如图所示，增加一行是按红框中的"+"
   ![alt text](image/32.jpg)
   点击右上角"完成"
   4. 打开此文档所在文件夹中的"脚本.txt",复制其中的内容，粘贴进visionMaster4.4中的"4脚本"的右侧，替换其中的原有代码
   ![alt text](image/33.jpg)
   ![alt text](image/34.jpg)
6. 搭建完毕，运行你需要检测的图片，就可以在"4脚本1"中看到检测结果，其中如果你后续想要使用对应的置信度，检测框的位置，对应的标签，都在"4脚本1"的模块结果处。
![alt text](image/35.jpg)
roibox数组是检测框，num是检测到的目标总数，label数据标签数组，conf是置信度数组。