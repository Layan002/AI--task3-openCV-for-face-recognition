# start
Here I will use raspberry pi to complete this task. <br>
If you are not familiar with this microcontroller I recommend you to watch videos on youtube to get start with it

## The operating system and getting started

Use the following website as a reference for you to download "Raspain Buster". <br>
[How to Flash the Old 'Buster' Raspberry Pi OS to a Micro-SD](https://core-electronics.com.au/guides/flash-buster-os-pi/) 

# Downloading OpenCV library. 
Follow the instructions in this link to download OpenCV library: [Object and Animal Recognition With Raspberry Pi and OpenCV](https://core-electronics.com.au/guides/object-identify-raspberry-pi/)<br>

# Starting with the Raspberry pi 
After successfully of OpenCV instillation, follow these steps.

- Make sure that the camera is enable: <br>
![Capture](https://github.com/user-attachments/assets/45a6a621-289f-4e96-9f66-a90735ccbefa)

- Follow the steps in this website: [Face Recognition With Raspberry Pi and OpenCV](https://core-electronics.com.au/guides/face-identify-raspberry-pi/)

## Troubleshooting
Since I am using a **webcam** not a **PiCam**, I will change the following code: 
``` PYTHON
import cv2
from picamera import PiCamera
from picamera.array import PiRGBArray

name = 'Caroline' #replace with your name

cam = PiCamera()
cam.resolution = (512, 304)
cam.framerate = 10
rawCapture = PiRGBArray(cam, size=(512, 304))
    
img_counter = 0

while True:
    for frame in cam.capture_continuous(rawCapture, format="bgr", use_video_port=True):
        image = frame.array
        cv2.imshow("Press Space to take a photo", image)
        rawCapture.truncate(0)
    
        k = cv2.waitKey(1)
        rawCapture.truncate(0)
        if k%256 == 27: # ESC pressed
            break
        elif k%256 == 32:
            # SPACE pressed
            img_name = "dataset/"+ name +"/image_{}.jpg".format(img_counter)
            cv2.imwrite(img_name, image)
            print("{} written!".format(img_name))
            img_counter += 1
            
    if k%256 == 27:
        print("Escape hit, closing...")
        break

cv2.destroyAllWindows()

```

TO:

``` PYTHON
import cv2

name = 'Layan'  # replace with your name

cam = cv2.VideoCapture(0)  # 0 is the default camera, change if necessary
cam.set(cv2.CAP_PROP_FRAME_WIDTH, 512)
cam.set(cv2.CAP_PROP_FRAME_HEIGHT, 304)

img_counter = 0

while True:
    ret, frame = cam.read()
    if not ret:
        print("Failed to grab frame")
        break
    
    cv2.imshow("Press Space to take a photo", frame)
    
    k = cv2.waitKey(1)
    if k % 256 == 27:  # ESC pressed
        print("Escape hit, closing...")
        break
    elif k % 256 == 32:  # SPACE pressed
        img_name = "dataset/" + name + "/image_{}.jpg".format(img_counter)
        cv2.imwrite(img_name, frame)
        print("{} written!".format(img_name))
        img_counter += 1

cam.release()
cv2.destroyAllWindows()
```

> [!CAUTION]
> If you did not change your code while using a webcam the following error will appear:
```
Traceback (most recent call last):
  File "/home/fruitopia/facial-recognition/headshots_picam.py", line 7, in <module>
    cam = PiCamera()
  File "/usr/lib/python3/dist-packages/picamera/camera.py", line 431, in __init__
    self._init_camera(camera_num, stereo_mode, stereo_decimate)
  File "/usr/lib/python3/dist-packages/picamera/camera.py", line 460, in _init_camera
    "Camera is not enabled. Try running 'sudo raspi-config' "
picamera.exc.PiCameraError: Camera is not enabled. Try running 'sudo raspi-config' and ensure that the camera has been enabled.
```

