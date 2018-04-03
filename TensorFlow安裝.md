# TensorFlow安裝流程
先安裝Anaconda3-5.1.0-Windows-x86_64.exe
要勾選Anaconda3-5.1.0路徑，之後建立TensorFlow虛擬環境才會成功


命令提示字元:  conda create --name tensorflow python=3.5 anaconda

啟動anaconda 虛擬環境:   activate tensorflow

安裝tensorflow: pip install tensorflow

若TensorFlow無法安裝打這行安裝

pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/windows/cpu/tensorflow-1.1.0-cp35-cp35m-win_amd64.whl

安裝 keras:  pip install keras

# Win10下安裝TensorFlow並用GPU做加速

https://rreadmorebooks.blogspot.tw/2017/04/win10tensorflowgpu.html

TensorFlow是一款Google推出用於機器學習的開源軟體庫，官方表明，在Python底下擁有最完整以及簡單的方案。

首先，請先完成兩個動作，可以參考之前之文章
1.安裝CUDA與cuDNN
1.5版請參考： 
於Win10環境下配置CUDA 9.0與cuDNN 7.0

1.4版請參考：
於Win10環境下配置CUDA 8.0與cuDNN 6.0

2.安裝Python
於Win10下安裝Anaconda


若要用GPU加速TensorFlow需滿足以下條件：

支援CUDA Toolkit 的顯卡

支援CUDA Toolkit 的顯卡驅動

CUDA Toolkit 
cuDN 
