# TensorFlow安裝流程
先安裝Anaconda3-5.1.0-Windows-x86_64.exe
要勾選Anaconda3-5.1.0路徑，之後建立TensorFlow虛擬環境才會成功


命令提示字元:  conda create --name tensorflow python=3.5 anaconda

啟動anaconda 虛擬環境:   activate tensorflow

安裝tensorflow: pip install tensorflow

若TensorFlow無法安裝打這行安裝

pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/windows/cpu/tensorflow-1.1.0-cp35-cp35m-win_amd64.whl

安裝 keras:  pip install keras

