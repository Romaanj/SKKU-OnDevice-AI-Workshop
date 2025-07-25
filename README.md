# On-Device ResNet 모델 경량화 및 가속 실습 자료

이 저장소는 ResNet18 모델을 효율적으로 경량화하고 가속화하기 위한 실습 코드 및 관련 유틸리티를 제공합니다. 양자화(Quantization)와 희소화(Sparsity) 기법을 적용하여 모델의 크기를 줄이고 추론 속도를 개선하는 방법을 다룹니다.

## 🚀 Colab에서 시작하기

Google Colaboratory 환경에서 이 실습 자료를 가장 쉽고 빠르게 시작할 수 있습니다. 별도의 Google Drive 마운트 없이 GitHub에서 직접 파일을 클론하여 사용할 수 있습니다.

1.  **리포지토리 클론**:
    Colab 노트북의 첫 번째 셀에서 다음 명령어를 실행하여 이 저장소를 클론합니다.
    ```bash
    !git clone [여기에 본인의 GitHub 리포토리 URL을 입력하세요]
    ```

2.  **작업 디렉토리로 이동**:
    클론된 리포지토리 폴더로 작업 디렉토리를 변경합니다. (예: `your_repo_name`을 실제 리포지토리 이름으로 변경)
    ```bash
    %cd [your_repo_name]
    ```

3.  **필요한 라이브러리 설치**:
    `requirements.txt` 파일에 명시된 모든 Python 라이브러리를 설치합니다.
    ```bash
    !pip install -r requirements.txt
    ```

이제 모든 준비가 완료되었습니다! 클론된 파일들을 Colab 환경에서 바로 사용할 수 있습니다.

## 📁 프로젝트 파일 구성

* `resnet_sequential.py`: ResNet 모델의 각 레이어에 대해 순차적으로 압축(양자화 및 희소화)을 적용하는 핵심 로직을 포함합니다.
* `Quantizer.py`: 모델의 가중치를 양자화하는 기능을 담당하는 클래스입니다. 비트 단위 양자화를 위한 파라미터 검색 및 적용을 수행합니다.
* `CombinedCompressor.py`: 주어진 레이어에 대해 입력(`Hessian`) 정보를 수집하고, 이를 기반으로 프루닝(Pruning) 및 양자화(Quantization)를 효율적으로 수행하는 주요 압축 클래스입니다.
* `utils.py`: 모델 레이어를 찾는 `find_layers_resnet` 함수, 시드 설정(`set_seed`), 장치(`device`) 설정, CIFAR 전용 ResNet18 정의, 모델의 정확도 측정(`get_acc`) 등 유틸리티 함수들을 포함합니다.
* `requirements.txt`: 이 프로젝트를 실행하는 데 필요한 모든 Python 라이브러리 목록이 포함되어 있습니다. [cite_start](`pip install -r requirements.txt` 명령어로 설치 가능) [cite: 1]
