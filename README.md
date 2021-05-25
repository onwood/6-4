# 작업하시다가
test라고 붙어있는건 제가 연습용으로 원본을 복사한거니 무시하셔도 됩니다.




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
