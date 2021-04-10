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

> pyrebase==3.0.27

<br/>

## MODULES
---
<br/>

> User Module

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In user module, there are mainly five sections,
* New User
* Existing User
* Set Password
* Change Chat ID
* Change Password
<br/>
1) New User<br/>

* Username Textfield -
    <br/>
    In username textfeild, the user will enter his/her
    name. This username will be the file name used to store his/her image.
    At this stage, the system will check if the entered username is already
    present in the database. If yes, then it will show the message as you are
    an existing user and the process will not be carried out further.
    <br/>
    * Get Started Button -
    <br/>After hitting Get Started button, the application
    will open up the camera to capture the user’s face.<br/>
        * Case 1: At first, the algorithm will look for multiple faces. If
        the current frame contains more than one face, then the system
        will not capture and store the current user’s face.

        * Case 2: Also, the algorithm will detect and retrieve the face
        encodings of the current user’s face and compare it with
        already existing user’s face encodings. If it matches, the
        process will not be carried further.

        * Case 3: Only if the above two conditions satisfy, the system
        will store the image of the current user with username as the
        file name.
<br/><br/>
2) Existing User

    * Existing user Button -
    <br/>
        If the user already presents in the database,
        he/she can simply click on the Existing User button to get into the
        Dashboard.
    * Dashboard -<br/>
    In Dashboard layout, user can be able to view or delete
    the already existing users in the system.

        * Back - Back button is used to return to the first layout which is
        the startup page by leaving Dashboard layout.
        * Refresh - Refresh button is used to dynamically update the
        database with the newly added users.
        * Delete - Delete button is used to remove the selected user from
        the system permanently.
---
<br/>

> Face Recognition Module


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In Face recognition module,<br/>

* At first the Histogram of Oriented Gradients algorithm will be executed and detect the driver’s face.


* From the captured face image, the image will be converted into BGR to RGB. Then the algorithm will extract the encodings from the face by creating gradients for each pixel. After that, the extracted face encodings will be compared with the pre-trained data.

    * Case 1: Face Matched

        * Encodings of the pre-trained face will be compared with the driver’s face encodings using HOG algorithm and if the face encodings match, then the system will send a entry log of the user to the user’s telegram account.


    * Case 2: Face Not Matched
        * Encodings of the pre-trained face will be compared with the driver’s face encodings using HOG algorithm.
        * If the face encodings don’t match with pre-trained face data for more than five seconds, then the algorithm will capture the unknown driver’s image.
        * Then, the system will send an Alert message along with the five images of the driver to the user’s telegram account.

        <br/>

> Telegram Module
&nbsp;
* At first telegram Bot has been created to send information to the user’s telegram account. The Bot can be created with help of BOTFATHER which is an in-built Telegram bot for creating the bot.


* Then we have retrieved the bot’s BOT_TOKEN from the telegram API website.


* BOT_TOKEN - The token is a string that is required to authorize the bot and send requests to the Bot API.


* For sending messages by the bot to user’s telegram account, we need to get the chat id of the user.


* CHAT_ID - On Telegram, chat ID is a numeric value that identifies each and every user uniquely. This is not the same as the username, but the user needs to have a username set in order to find the chat ID.


* If the driver’s face is not recognized, then the system will call the telegram method.


* Telegram URL has been used to send messages and images by using the user’s chat ID through bot.
&nbsp;
#### URL Syntax –
    * For sending message -https://api.telegram.org/bot[BOT_API_KEY]/sendMessage?chat_id=[chat_id]&text=[MESSAGE_TEXT]

    * For sending image -https://api.telegram.org/bot[BOT_API_KEY]/sendPhoto?chat_id=[chat_id]&files=[filename]
* Inside the telegram method, request module has been used.

* The GET method is used to request the resource specified in the URL and then send the Alert message and images of a thief to the mentioned chat ID.

<br/>

#### Message Format to be sent to the user -
    ➔ If Face matched:
        Welcome Akhash!
        Login details -
        03/08/21 Monday 11:28 AM

    ➔ If Face not matched:
        Alert! Car is not SAFE!!!

&nbsp;
> GPS Module
&nbsp;
* At first, location can be get by mobile GPS which will stream the NMEA data (GPSD) to the raspberry Pi’s IP address and port through Wi-Fi.
* Then at other end, Raspberry Pi will receive the NMEA data streaming by the mobile phone as a Datagram using UDP protocol.
* By using the GPS python package, latitude and longitude of the car can be easily extracted from the NMEA data.
* Extracted latitude and longitude will be send to the user’s telegram account when there is a CommandHandler receives a command from the bot.
* Location of the car will be recursively updated on the firebase, which will be useful to determine the last known location of the car when the car stops.

    ### Commands:
    * `/location` &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;– &nbsp;to get the current location of the lost car.


    * `/lastknownlocation` – &nbsp;to get the last known location of the car from the firebase.
