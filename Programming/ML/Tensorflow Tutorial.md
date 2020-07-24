# 2020/05/22

## TensorFlow Tutorial ([Tensorflow Korea](https://tensorflowkorea.gitbooks.io/tensorflow-kr/content/g3doc/tutorials/))

### 1. 목표 
Tensorflow 를 통해 LOL 경기 영상에서 해당 경기 동안 각 챔피언들의 동선, 각 팀간의 시간별 골드 차이 등을 분석하는 프로그램 개발

### 2. 설치

1. Pip 설치
2. Virtualenv 설치
3. Anaconda 설치
4. Docker 설치
5. 소스에 설치

    Pip : 파이썬 패키지 설치 및 관리하는 패키지 매니저 프로그램
    Virtualenv : 각기 다른 파이썬 프로젝트에서 필요한 패키지들의 버전이 충돌되지 않도록 다른 공간에서 운영되도록 하는 툴
    Anaconda : 여러 수학, 과학 패키지를 기본적으로 포함하고 있는 파이썬 배포판
    Docker : 로컬 컴퓨터에서 컨테이너로 리눅스 운영체제를 운영할 수 있는 시스템

    [Conda:"command not found" error](https://antilibrary.org/2098)

** 텐서플로우 데모 모델 실행까지 진행
~~
$ python /usr/local/lib/python2.7/site-packages/tensorflow/models/image/mnist/convolutional.py
~~

### 3. MNIST 초급

    MNIST는 간단한 컴퓨터 비전 데이터셋입니다. 
