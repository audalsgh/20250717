# 19일차

## 어제에 이어서 YOLOv8에 사진이 아닌 비디오를 넣어보자.
[미션3개가 담긴 코드](0717_YOLOv8_video.ipynb) : 마지막 코드는 YOLOv11 설치 오류라 그런것.<br>

동영상을 직접 업로드, 교수님의 주행영상 19초 짜리를 업로드해서 runs/detect/predict 폴더에 같은 이름의 .avi 결과영상이 나온다.<br>
temp_video.avi는 유튜브 링크로만 영상을 업로드해서, 제목이 temp로 붙혀진 것일뿐.<br>
<img width="343" height="484" alt="image" src="https://github.com/user-attachments/assets/b2ff10f0-33cf-45e7-9dea-c6a0a262f6e7" /><br>
<img width="1184" height="637" alt="image" src="https://github.com/user-attachments/assets/29ebfc31-da2c-4be6-b8dc-342491c644e8" /><br>
-결과영상

## 추가적으로 YOLOv11도 사용해보자.
[Ultralytics YOLOv11 공식 문서](https://docs.ultralytics.com/ko/models/yolo11/)
- 기존 YOLOv8 대비 더 높은 정확도와 속도를 제공
- RepNCSPELAN4C, CBLinearNeck, DConvHead 등의 아키텍처 향상이 있음
- 기존 API와 완전히 호환됨

| 모델            | 설명                       |
| ------------- | ------------------------ |
| `yolov11n.pt` | nano: 가장 가볍고 빠름          |
| `yolov11s.pt` | small: 기본 사용             |
| `yolov11m.pt` | medium: 속도-정확도 균형        |
| `yolov11l.pt` | large: 더 높은 정확도          |
| `yolov11x.pt` | xlarge: 최고 정확도 (성능 비용 큼) |
