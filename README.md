# CARLA 0.9.12 UBUNTU 20.04 설치 방법

기본적으로 다음 링크를 따른다
https://carla.readthedocs.io/en/0.9.12/build_linux/

## Part One: Prerequisites

**[SOFTWARE REQUIREMENT]**

1.  pip3 버전을 먼저 20.3 혹은 더 높은 버전으로 설치한다.
  
2.
```
sudo apt-get update && 
sudo apt-get install wget software-properties-common && 
sudo add-apt-repository ppa:ubuntu-toolchain-r/test && 
wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key|sudo apt-key add - && 
sudo apt-get update
```
  
> 꼭 **sudo apt-add-repository "deb http://apt.llvm.org/xenial/ llvm-toolchain-xenial-8 main"** 하지 **말아야**한다. 
> 
> 그 이유는 clang-8 설치를 막기 때문.
> 
> 관련 링크: https://github.com/carla-simulator/carla/issues/3441

3. 빌드 시 필요한 것들 설치
  ```
  sudo apt-get install build-essential clang-8 lld-8 g++-7 cmake ninja-build libvulkan1 python python-dev python3-dev libpng-dev libtiff5-dev libjpeg-dev tzdata sed curl unzip autoconf libtool rsync libxml2-dev git
  ```
  
4. UnrealEngine과 CARLA 모두 clang-8을 사용해 빌드를 하므로 clang-8 버전을 기본으로 설정한다.
  ```
  sudo update-alternatives --install /usr/bin/clang++ clang++ /usr/lib/llvm-8/bin/clang++ 180 &&
  sudo update-alternatives --install /usr/bin/clang clang /usr/lib/llvm-8/bin/clang 180
  ```

5.
  ```
  sudo apt install python3-testresources &&
  pip3 install --user -Iv setuptools==47.3.1 &&
  pip3 install --user distro &&
  pip3 install --user wheel auditwheel
  ```
  
**[UnrealEngine]**

  혹시 아직 Unreal Engine 계정과 github 계정이 연결이 안되어있다면 링크: [access link](https://www.unrealengine.com/en-US/ue4-on-github "accesslink") 를 따라서 연결하길 바란다.

  1. git clone을 통해 다운을 받는다. (git clone --depth 1 -b "주소" "다운받을 공간")
  ```
  git clone --depth 1 -b carla https://github.com/CarlaUnreal/UnrealEngine.git ~/UnrealEngine_4.26
  ```
  2021 8월부터 보안문제로 아이디와 토큰(password부분)을 기입해야 다운이 가능하다.(일시적인 오류라는데 아직까지 해결되지는 않았다.)
  
  다음 링크: [token link]( https://hoohaha.tistory.com/37 "tokenlink") 를 참고하기 바란다.
  
  2. 다운받은 공간내의 UnrealEngine 폴더에 들어간 다음,
  ```
  cd ~/UnrealEngine_4.26
  ```
  
  3. 빌드 시작
  ```
  ./Setup.sh && ./GenerateProjectFiles.sh && make
  ```
  
  4. 잘 빌드가 되었는지 확인하기 위해 에디터 실행
  ```
  cd ~/UnrealEngine_4.26/Engine/Binaries/Linux && ./UE4Editor
  ```
  ------------------------------------------------------------------
  
  
## Part Two: Build CARLA

  1. CARLA 0.9.12 버전 다운로드 (git clone --branch <tag_name> <repo_url>)
  ```
  git clone --branch 0.9.12 https://github.com/carla-simulator/carla
  ```
  **그냥 branch 설정없이 git clone을 하게되면 가장 최신 버전이 다운되니 조심하기 바란다.**
  
  2. CARLA root 폴더에 들어가서 assets 다운로드
  ```
  ~cd ~/carla && ./Update.sh~
  ```
  **[주의]** 위와 같이 하면 최신 버전의 carla로 구축이 되기 때문에, 위 커맨드가 아닌,
  ```
  {**carla설치폴더**}$ git lfs clone -b 0.9.12 https://bitbucket.org/carla-simulator/carla-content Unreal/CarlaUE4/Content/Carla
  ```
  
  
  3. bashrc파일에 UnrealEngine 폴더 경로 기입 후 터미널 리셋
  ```
  gedit ~/.bashrc
    export UE4_ROOT=~/UnrealEngine_4.26 기입 (UnrealEngine 다운받은 공간 경로 기입)
  source ~/.bashrc
  ```
  
  4. carla root 폴더에 들어간 후 Python API client 컴파일
  ```
  make PythonAPI
  (만약 특정 파이썬 버전에 맞게 컴파일 하고 싶다면 make PythonAPI ARGS="--python-version=3.7 3.8")
  ```
  
  5. 서버 컴파일
  ```
  make launch
  ```
  
  6.
  ```
  make package
  ```
  
  -----------------------------------------------------------------------------
 
 ## Part Three: Play CARLA 
 ```
 cd ~/carla/Dist/CARLA_Shipping_0.9.12/LinuxNoEditor && ./CarlaUE4.sh 
 ```

  
