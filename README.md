# CARLA 0.9.12 UBUNTU 20.04 설치 방법

기본적으로 다음 링크를 따른다
https://carla.readthedocs.io/en/0.9.12/build_linux/

**Part One: Prerequisites** 

<SOFTWARE REQUIREMENT>

1.  
  pip3 버전을 먼저 20.3 혹은 더 높은 버전으로 설치한다.
  
2.
```
sudo apt-get update && 
sudo apt-get install wget software-properties-common && 
sudo add-apt-repository ppa:ubuntu-toolchain-r/test && 
wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key|sudo apt-key add - && 
sudo apt-get update
```
  
  꼭 **sudo apt-add-repository "deb http://apt.llvm.org/xenial/ llvm-toolchain-xenial-8 main"** 하지 말아야한다.
  그 이유는 clang-8 설치를 막기 때문.
  관련 링크:
  https://github.com/carla-simulator/carla/issues/3441

2.
  sudo apt-get install build-essential clang-8 lld-8 g++-7 cmake ninja-build libvulkan1 python python-dev python3-dev libpng-dev libtiff5-dev libjpeg-dev tzdata sed curl unzip autoconf libtool rsync libxml2-dev git
  
3.
  sudo update-alternatives --install /usr/bin/clang++ clang++ /usr/lib/llvm-8/bin/clang++ 180 &&
  sudo update-alternatives --install /usr/bin/clang clang /usr/lib/llvm-8/bin/clang 180

4.
  pip3 install --user -Iv setuptools==47.3.1 &&
  pip3 install --user distro &&
  pip3 install --user wheel auditwheel
  

<UnrealEngine>
  혹시 아직 Unreal Engine 계정과 github 계정이 연결이 안되어있다면 [다음 링크][https://www.unrealengine.com/en-US/ue4-on-github] 를 따라서 연결하길 바란다.
  
  
