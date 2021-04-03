# Car Theft Detection using Face Recognition with Telegram API

## Description
The incident of vehicle theft has been increased enormously, especially in metropolitan cities. It becomes nearly impossible to locate the car when it was stolen and the thief escapes easily.\
To overcome this problem, A face recognition system developed and used to alert the owner when an unknown person tries to steal the car.\
`Histogram of Oriented Gradients` [HOG] algorithm is being used to detect and recognize the captured face of the driver.\
If the captured face is not recognized by the system, then a push notification will be sent to the owner’s telegram account through internet with the message contents of driver’s face and coordinates of the car. \
The system can be used to reduce the increased vehicle theft and allows the owner to identify the intruder. 

## Dependencies
***
> opencv-python==4.4.0.44

> opencv-contrib-python==4.4.0.44

> pip==21.0.1

> python-telegram-bot==13.4.1

> wheel==0.36.2

> telegram==0.0.1

> requests==2.25.1

> numpy==1.19.2

> gps==3.19

> face-recognition==1.3.0

> dlib==19.18.0

> cmake==3.17.2

> telethon==1.19.1

> pillow==8.1.0
***