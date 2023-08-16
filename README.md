# wsl mlsetting

## 1. wsl 

### 생성

관리자 권한 powershell에서 생성/삭제

- 설치
```
wsl --install -d ubuntu-20.04
```

- 목록 보기
```
wslconfig.exe /l
```

- 삭제
```
wslconfig.exe /u Ubuntu-20.04
```
 
## 2. anaconda


- 다운로드 

[https://www.anaconda.com/download#downloads](https://www.anaconda.com/download#downloads)

64-bit (x86) installer 다운로드 

- 설치

```
sudo bash Anaconda3-2023.07-2-Linux-x86_64.sh

미니콘다가 훨씬 빠름

```

꽤 오래 걸림

- path 등록
```
nano ~/.bashrc

다음을 입력
export <설치경로>:$PATH

저장 후

source ~/.bashrc

로 입력한 path 적용

```

- 가상환경 생성
```
conda create -n <환경명> python=<버전>

ex) 
  conda create -n ml python=3.9

```


## 3. CUDA

[https://developer.nvidia.com/cuda-toolkit-archive](https://developer.nvidia.com/cuda-toolkit-archive)

11.8 -> Linux -> x86_64 -> Ubuntu -> 20.04 -> deb(local)

선택하면 나오는 명령어 입력



```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin
sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda-repo-ubuntu2004-11-8-local_11.8.0-520.61.05-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2004-11-8-local_11.8.0-520.61.05-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2004-11-8-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda
```


## 4. cuDNN

[phttps://developer.nvidia.com/cudnn](https://developer.nvidia.com/cudnn)

Download cudnn

Local Installer for Linux x86_64

```
sudo cp cudnn-*-archive/include/cudnn*.h /usr/local/cuda/include 
sudo cp -P cudnn-*-archive/lib/libcudnn* /usr/local/cuda/lib64 
sudo chmod a+r /usr/local/cuda/include/cudnn*.h /usr/local/cuda/lib64/libcudnn*
```

~/.bashrc 에 다음 라인 추가

```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-11.8/lib64/
```

설치 성공 여부 확인
```
/usr/local/cuda-11.8/extras/demo_suite/deviceQuery
```

## 5. tensorflow

윈도우 네이티브엔 gpu버전 설치 불가, cpu 버전만 설치 가능

다음 페이지에 윈도우 wsl2 에 있는 내용대로 따라 하면 됨

[https://www.tensorflow.org/install/pip?hl=ko](https://www.tensorflow.org/install/pip?hl=ko)



## 6. pytorch

[https://pytorch.org/get-started/locally/](https://pytorch.org/get-started/locally/)

conda 설정으로 하니 잘 됨


```
import torch

torch.cuda.is_available()

```

True 나오면 gpu 세팅 된것