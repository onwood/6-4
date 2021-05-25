# 작업하시다가
test라고 붙어있는건 제가 연습용으로 원본을 복사한거니 무시하셔도 됩니다.

- 진호님이 잡아주신 틀은
1. 1번 라즈베리 파이 카메라로 읽은 것을 별도의 파일로 저장
2. 저장된 파일을 1번 라즈베리 파이 LoRa로 읽어오기
3. 1번 라즈베리 파이 LoRa에서 읽어온 정보를 2번 라즈베리 파이 LoRa로 전송하기
- 입니다.



# Tensorflow - lite
https://github.com/tensorflow/examples/tree/master/lite/examples/object_detection/raspberry_pi
위에 링크에서 read.me 설명 읽어보시면 실행됩니다.

```
cd Tensorflow_lite/lite/examples/object_detection/raspberry_pi

# The script takes an argument specifying where you want to save the model files
bash download.sh /tmp

# bash download.sh는 뒤에 /tmp를 붙이지 않아도 tmp로 저장됩니다.(reboot하면 삭제됨)
```

실행하기
```
python3 detect_picamera.py --model /tmp/detect.tflite --labels /tmp/coco_labels.txt
```

특이사항 - 터미널에서 사람으로 인식하고 60%이상 맞추고 박스가 크게 잡힐 경우 출력되도록 수정한 구간

```
def annotate_objects(annotator, results, labels):
  """Draws the bounding box and label for each object in the results."""
  for obj in results:
    # Convert the bounding box figures from relative coordinates
    # to absolute coordinates based on the original resolution
    ymin, xmin, ymax, xmax = obj['bounding_box']
    xmin = int(xmin * CAMERA_WIDTH)
    xmax = int(xmax * CAMERA_WIDTH)
    ymin = int(ymin * CAMERA_HEIGHT)
    ymax = int(ymax * CAMERA_HEIGHT)

    # Overlay the box, label, and score on the camera preview
    annotator.bounding_box([xmin, ymin, xmax, ymax])
    annotator.text([xmin, ymin],
                   '%s\n%.2f' % (labels[obj['class_id']], obj['score']))
    
    detected_class_id = labels[obj['class_id']]
    detected_score = obj['score']
    detected_size = (xmax-xmin)*(ymax-ymin)
    blink(detected_class_id, detected_score, detected_size)

      
def blink(class_id, score, size):
  if (class_id == 'person') & (score >= 0.6) & (size >=30000):
    print(class_id, score, size)
    
```


# SX1262 915M LoRa
https://www.waveshare.com/wiki/SX1262_915M_LoRa_HAT
로라 통신 코드입니다.

라이브러리 설치
```
sudo apt-get install python-pip 
sudo pip install RPi.GPIO
sudo apt-get install python-smbus
sudo apt-get install python-serial
```

경로 이동 및 실행
```
cd 6-4/SX1262_915M_LoRa/transparent
python3 transparent.py BROADCAST_AND_MONITOR
```


# Security-cam
이건 책에 있는 코드입니다. 필요하시면 사용하시라고 참고용으로 넣었습니다.
