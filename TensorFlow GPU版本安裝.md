# TensorFlow GPU版本安裝

https://developer.nvidia.com/cuda-gpus

點 CUDA-Enabled GeForce Products，看筆電GPU是符合那一個版本

https://developer.nvidia.com/cuda-downloads

https://developer.nvidia.com/cuda-downloads?target_os=Windows&target_arch=x86_64&target_version=10&target_type=exelocal

Download Installers for Windows 10 x86_64

Installer Type  exe(local)

選 Base Installer 下載安裝


安裝NVIDIA cuDNN

https://developer.nvidia.com/cudnn

https://developer.nvidia.com/developer-program/signup

帳號：jack820075@gmail.com

密碼：Love52014

下載Win10 cudnn-9.1-windows10-x64-v7.1

https://developer.nvidia.com/rdp/cudnn-download


命令提示字元: conda create --name tensorflow-gpu python=3.5 anaconda

啟動anaconda 虛擬環境:   activate tensorflow-gpu

離開anaconda 虛擬環境: deactivate tensorflow-gpu

安裝tensorflow: pip install tensorflow-gpu

若tensorflow-gpu套件有模組無法安裝，打以下的指令就可以完整安裝

pip install --upgrade --ignore-installed tensorflow-gpu

安裝 keras: pip install keras

Anaconda要裝個人使用，tensorflow-gpu虛擬環境中的Jupyter Notebook、Spyder才可以安裝起來

C:\Users\jack\Anaconda3\envs

## [如何在Jupyter Notebook中使用Tensorflow](https://blog.csdn.net/xue_wenyuan/article/details/51545845)

https://blog.csdn.net/index20001/article/details/73555182

D:\>conda info --envs

D:\>activate tensorflow
