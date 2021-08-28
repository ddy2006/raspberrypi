### 摄像头人脸识别

```sh
docker run -it \
    --name face_recognition \
    --device /dev/vchiq \
      registry.cn-hangzhou.aliyuncs.com/denverdino/face_recognition \
      bash

docker run -it --name face_recognition --privileged -e DISPLAY=191.168.1.63:0.0  --device /dev/vchiq  --network=host --rm registry.cn-hangzhou.aliyuncs.com/denverdino/face_recognition bash -c 'cd /face_recognition/examples/ && python digital_makeup.py'

docker run -it --name face_recognition --privileged -e DISPLAY=191.168.1.63:0.0  --device /dev/vchiq  --network=host --rm registry.cn-hangzhou.aliyuncs.com/denverdino/face_recognition bash -c 'cd /face_recognition/examples/ && python recognize_faces_in_pictures.py'

docker run -it --name face_recognition --privileged -e DISPLAY=191.168.1.63:0.0  --device /dev/vchiq  --network=host --rm ddy2006/face_recognition bash -c 'cd /face_recognition/examples/ && python digital_makeup.py'

```
