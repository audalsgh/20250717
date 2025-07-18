# 19일차

## 어제에 이어서 YOLOv8에 사진이 아닌 비디오를 넣어보자.
[미션3개가 담긴 코드](0717_YOLOv8_video.ipynb) : 마지막 코드는 YOLOv11 설치 오류라 그런것.<br>
(colab의 ram사용가능량 제한 문제로 0717 오늘자는 나의 구글계정으로 진행함.)<br>

미션1. 교수님의 주행영상 19초 짜리를 직접 업로드해서 runs/detect/predict 폴더에 같은 이름의 .avi 결과영상이 나온다.<br>
미션2. temp_video.avi는 유튜브 링크로만 영상을 업로드해서, 제목이 temp로 붙혀진 것일뿐. 내용은 동일하다.<br>
<img width="343" height="484" alt="image" src="https://github.com/user-attachments/assets/b2ff10f0-33cf-45e7-9dea-c6a0a262f6e7" /><br>
(결과영상 다운로드 오류가 뜨긴하지만, 왼쪽 메뉴에서 다운받으면 결과영상 확인가능)
<img width="1184" height="637" alt="image" src="https://github.com/user-attachments/assets/29ebfc31-da2c-4be6-b8dc-342491c644e8" /><br>
-결과영상1
<img width="1189" height="671" alt="image" src="https://github.com/user-attachments/assets/e1de854d-7df0-4455-9e49-37aba7b0d201" /><br>
-결과영상2

## 3번째 문제, 추가적으로 YOLOv11도 사용해보자.
[Ultralytics YOLOv11 공식 문서](https://docs.ultralytics.com/ko/models/yolo11/) : **YOLOv11은 YOLOv8 대비 성능·속도 모두 개선된 차세대 모델**<br>
<br>
YOLO의 Backbone은 이미지에서 기본 특징(edges, textures 등)을 추출하는 앞단.<br>
YOLO의 Neck은 다양한 스케일의 특징 맵(feature maps)을 융합하여 작은/중간/큰 객체를 모두 감지할 수 있게 하는 중간단.<br>
YOLO의 Head는 객체의 위치, 클래스, 크기 등을 최종 예측하는 마지막 단.<br>

- 기존 YOLOv8 대비 더 높은 정확도와 속도를 제공
- 모델 아키텍쳐 : (C2f, Conv, RepConv 등) -> (RepNCSPELAN4C, CBLinearNeck, DConvHead 등)으로 향상이 있음
- 백본 구조 : ELAN-CSP 기반 ->	더 깊고 가볍게 최적화된 CSP 구조
- 헤드 구조 : YOLOHead (Conv 기반)	-> DConvHead (Depthwise Conv 기반, 연산 효율 ↑)
- 활성화 함수 : (SiLU) -> (SiLU, Swish 등) 선택 가능
- 기존 API와도 완전히 호환됨

**모델 아키텍쳐 용어 정리**
1. RepNCSPELAN4C<br>
YOLOv8의 CSP 구조를 개선한 백본<br>
연산량 감소 + 표현력 향상<br>
모델 경량화 + 정확도 향상 동시에 달성<br>

2. CBLinearNeck<br>
PANet과 FPN 구조보다 더 간결<br>
빠른 속도, 작은 크기, 낮은 메모리 사용량<br>

3. DConvHead<br>
Depthwise Convolution 기반의 경량화된 Detection Head<br>
Mobile 환경이나 Edge 추론에 최적화<br>

<img width="813" height="484" alt="image" src="https://github.com/user-attachments/assets/1adbd9f7-c88c-47ce-b858-29e03341805c" />

| 모델 종류     | 설명                       |
| ------------- | ------------------------ |
| `yolov11n.pt` | nano: 가장 가볍고 빠름          |
| `yolov11s.pt` | small: 기본 사용             |
| `yolov11m.pt` | medium: 속도-정확도 균형        |
| `yolov11l.pt` | large: 더 높은 정확도          |
| `yolov11x.pt` | xlarge: 최고 정확도 (성능 비용 큼) |

단점 : 오래된 코드/모델와 호환이 필요할때, YOLOv5 이전과는 호환이 되지않음.
