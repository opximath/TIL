# YOLO 개발 환경 구축(Darknet)
**Darknet github** : https://github.com/AlexeyAB/darknet

## SW/HW 환경  
**OS : Window 10**  
**GPU : 3080Ti, 3090**  
**CUDA : 11.1**  
**cuDNN : 8.0.5**  
**OpenCV : 4.5.0**  
**Cmake : 3.20.5**  
**Visual Studio : '17, '19 Community(English)**  

## CUDA 설치 및 cuDNN 포팅  
- https://developer.nvidia.com/cuda-gpus 링크를 통해 사용하는 그래픽의 연산능력을 체크  
- 3080Ti, 3090의 경우 8.6에 속함  
- https://developer.nvidia.com/cuda-toolkit-archive 링크를 통해 CUDA 11.1 설치(그래픽과 매칭 필요)  
- https://developer.nvidia.com/rdp/cudnn-archive 링크를 통해 cuDNN 8.0.5 for CUDA 11.1 설치
- CUDA 11.1이 깔린 경로 (~/NVIDIA GPU Computing Toolkit/CUDA/v11.1/)의 bin, include, lib 폴더에 매칭하여 cuDNN 항목 붙여넣기  
- 환경 변수 설정의 '사용자 명'에 대한 사용자 변수 항목 중, "Path" 편집 선택
- 설치한 CUDA 경로의 bin, include, lib 환경 변수 추가(예. ~/CUDA/v11.1/bin)

## Darknet Build 파일 수정  
- 위의 **darknet github**에서 프로젝트 파일 다운로드
- darknet/build/darknet 경로에 있는 **darknet.vcxproj** 파일 Notepad ++ 로 편집 실행
- 상단의 2번째 줄, <Project DefaultTargets="Build" ToolsVersion=**"16.0"** 으로 수정  
- 55번째 줄, <Import Project="$(VCTargetsPath)\BuildCustomizations\ **CUDA 11.1.props**" 으로 수정
- 마지막 줄(308), 위와 같이 **CUDA 11.1.targets**로 수정

## Darknet Build를 위한 OpenCV, CUDA 설정
- darknet.sln 파일을 앞서 정의한 버전으로 실행(VS19)
- VS 19가 영문으로 실행되는지 체크 후, Release, x64로 변경(모든 항목에 대해서 Release와 x64 정의 필요)
- darknet 프로젝트 우측 클릭 후, Properties 클릭
- C/C++ 항목의 General 카테고리 클릭 후, Additional Include Directories 수정(OpenCV, CUDA 경로 확인)  

<img src="https://github.com/opximath/TIL/blob/main/Deep%20Learning/CNN/YOLO/Image/YOLO_SetUp1.png" width="500">  

- CUDA C/C++ 항목의 Device 카테고리 클릭 후, Code Generation 수정(그래픽 연산능력 확인 필요)  
<img src="https://github.com/opximath/TIL/blob/main/Deep%20Learning/CNN/YOLO/Image/YOLO_SetUp2.png" width="500">   

- Linker 항목의 General 카테고리 클릭 후, Additional Library Directories 수정(OpenCV 경로 확인)
<img src="https://github.com/opximath/TIL/blob/main/Deep%20Learning/CNN/YOLO/Image/YOLO_SetUp3.png" width="500">   

- 편집이 완료되었으면, YOLO에서 OpenCV와 CUDA를 사용할 수 있게하는 .dll 파일을 옮겨야함
- darknet/build/darknet/x64 경로에 **OpenCV**(opencv_world450.dll, opencv_world450d.dll, opencv_videoio_ffmpeg450_64.dll)와 **CUDA**(curand64_10.dll, cusolver64_11.dll, cudart64_110.dll, cublas64_11.dll)을 옮겨준다.
- CTRL + F5를 눌러 빌드 수행
- 빌드가 성공적으로 수행됐다면 YOLO 환경 셋팅이 완료된 것임

