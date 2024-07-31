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

## Important steps:
Here how I trained the model:<br>

<img src="https://github.com/user-attachments/assets/fa422d53-d8d4-4edc-8a95-c21162db0470" alt="img" width= 500>


# Training

![image](https://github.com/user-attachments/assets/16ec4d69-806d-4635-a383-de755fe268ec)
![image](https://github.com/user-attachments/assets/24016895-9bf4-49bc-b661-146a55ce01cf)




# Troubleshooting
Here I will show you the errors I've encountered and how I solved them:

## Problem 1: picamera.exc.PiCameraError: Camera is not enabled
Since I am using a **webcam** not a **PiCam**, I will run 'headshot.py' instead of 'headshotPiCam.py': 

> [!CAUTION]
> If you did not change the code to run and take you photos for your face while using a webcam, the following error will appear:
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

## Problem 2: No module named imutils

when I tried to train my face using the follwing command:<br>
```
 cd facial_recognition
 python train_model.py

```
I got this error:<br>
<img src="https://github.com/user-attachments/assets/37bb14b2-e4a5-44d3-9d66-e9c920485f4d" alt="img" width= 500>

I solved it by installing this library:
```
pip install imutils
```

## Problem 3: No module named face_recognition

To solve this problem I've run the following command:
```
pip install face-recognition --no-cache-dir
```
If it doesn't work, run the following command:<br>
```
sudo systemctl restart dphys-swapfile
```

then rerun: 
```
pip install face-recognition --no-cache-dir
```

## Problem 4: Can't open camera by index / AttributeError: 'NoneType' object has no attribute 'shape'

![image](https://github.com/user-attachments/assets/d79c5068-295d-4d11-a9e3-8b46cc503087)

What I did to solve this problem is very simple:<br>
I just changed the src= 2 to src= 0 and it works appropriately. <br>

![image](https://github.com/user-attachments/assets/c51ed806-99f2-42cc-ace8-41af7cfa6b8d)









