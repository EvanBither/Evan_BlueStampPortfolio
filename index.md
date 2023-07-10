# Security Camera
My project is a digital security camera that records live at 1080p 30fps. It uses Rasberry Pi and an HDMI connection to operate. It can hold 64gb of video via a micro SD chip and has two micro-usb ports. The camera case is small, roughly 3x1x1 in inches. The camera detects motion within 25 feet and immediately alerts the user via an email. This email consists of a screenshot of the moment when motion was detected, as well as a green box drawn around where the presumed object was in the frame.  <!-- Replace this text with a brief description (2-3 sentences) of your project. This description should draw the reader in and make them interested in what you've built. You can include what the biggest challenges, takeaways, and triumphs from completing the project were. As you complete your portfolio, remember your audience is less familiar than you are with all that your project entails!-->

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Evan B | Burlingame High School | Data Engineering | Incoming Senior

<!--**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**-->

<!---![Headstone Image](logo.svg)-->
  
# Third Milestone

My third milestone was to complete the smart security camera set up. This milestone included finishing the motion detection system, and the automated email system. The project now detects movement in the direction the camera is pointed, takes a screenshot of the object that the camera decided was moving, and sends the screenshot with a box drawn around the object to my email. 

The biggest challenges I faced when completing this milestone were the many instances of troubleshooting and issues with code and hardware. A lot of small problems branched out and unveiled even larger ones that took lots of time to fix. The raspberry pi's had to be swapped so that the faster ones could help me install updates quicker, but the switching between versions corrupted the SD cards and I had to restart many times. 

Next, I will be adding my modifications to mr project which are to add audio to the security reports I receive. Instead of a screenshot the pi will send a short video to my email with audio too. This will be close to a ring doorbell camera without the two way audio and video. 


<iframe width="560" height="315" src="https://www.youtube.com/embed/tPb56sLVS1w" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


# Second Milestone


For my second milestone, I accomplished video output from my pi camera. This video was livestreamed to a website run on the Raspberry Pi. I could see the live feed on a web browser on my Raspberry Pi. When the code is run, a link to the website is added to the interpreter. On the site, the camera feed is in the top left with the title, "Raspberry Pi Security Feed".


What has been surprising about the project so far is how many different sources there were for problems, which made troubleshooting incredibly hard. The code has multiple classes, and being foreign to python made diagnosing errors quite hard for me. In addition, the versions of OpenCV and python were incorrect, and needed to be changed in order for the code to work. This took many installations and lots of time. Also, there was hardware that had to be switched, some camera didn't work, and the older rapsberry Pi's couldn't display the website so I had no idea that the camera was working. Unfortunately, drastically switching versions of raspberry pi's lead to corruption in the MicroSD, which meant I had to completely restart a few times.


Before my final milestone, I need to create and fix the code that detects the movement, draws a box around the object or person, and sends me an email. After all of that is finished, I need to move it from the raspberry pi 4, to the raspberry pi zero, so that it fits in the camera case and can stand up on its own. 


<iframe width="560" height="315" src="https://www.youtube.com/embed/Qga3blWhqeU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# First Milestone
<iframe width="560" height="315" src="https://www.youtube.com/embed/9DHfboT22uo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

My first milestone was completing the construction of my main project. I have finished building the security camera and need to plug it into my computer and do the more technical things such as programming it and making sure the camera works. While building the camera, I connected the camera module to the Rasberry Pi controller via a ribbon cable. I assembled the case for the camera, as well as the plastic shielded viewing point that protects the lens and gives the camera a wide enough opening to record. I installed the memory card into the side port of the camera case and made sure that the two micro USB ports and the HDMI port work and can be connected.

  The challenges I faced were staying organized and figuring out how to assemble the camera. The project came with a lot of extra parts that I didn’t need, and instructions for accessories that did not work with the variation I wanted to build. It was hard to figure out which pieces I needed for the case variation compared to the stand variation for example. 
  
  My plan to complete the project is to make sure that the electrical components in my camera work, by plugging them in and using the software. After that, I will try videoing with the camera and then think of modifications for my project.
  
 

# Starter Project
<iframe width="560" height="315" src="https://www.youtube.com/embed/d2xeVi4H5YE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

  My starter project was a digital clock that displays the accurate time, date, and temperature of the room. The clock is powered by a 3-volt battery that allows the internal mechanisms to keep track of the time and date, but the display is powered by a micro-USB cord. The clock sits in a clear box that allows the user to press the two operational buttons that control the display. In order to assemble this project, I needed to solder over 30 components and make sure they were in their correct spots and solder correctly so that there were no electrical shorts. 
  
  While building my project, it took me many attempts to solder every component correctly and get the clock to work as intended. 
 
  This project taught me how to solder correctly, and how to de-solder when necessary. I have learned how to stay organized, manage my time efficiently, and when to ask for help.



<iframe width="560" height="315" src="https://www.youtube.com/embed/d2xeVi4H5YE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

<!---# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. -->

<!--- # Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. -->
Main.py
```import cv2
import sys
from mail import sendEmail
from flask import Flask, render_template, Response
from camera import VideoCamera
from flask_basicauth import BasicAuth
import time
import threading
email_update_interval = 600 # sends an email only once in this time interval
video_camera = VideoCamera(flip=True) # creates a camera object, flip vertically
object_classifier = cv2.CascadeClassifier("models/fullbody_recognition_model.xml") # an opencv classifier
app = Flask(__name__)
app.config['BASIC_AUTH_USERNAME'] = 'CHANGE_ME_USERNAME'
app.config['BASIC_AUTH_PASSWORD'] = 'CHANGE_ME_PLEASE'
app.config['BASIC_AUTH_FORCE'] = True
basic_auth = BasicAuth(app)
last_epoch = 0
def check_for_objects():
	global last_epoch
	while True:
		try:
			frame, found_obj = video_camera.get_object(object_classifier)
			if found_obj and (time.time() - last_epoch) > email_update_interval:
				last_epoch = time.time()
				print "Sending email..."
				sendEmail(frame)
				print "done!"
		except:
			print "Error sending email: ", sys.exc_info()[0]

@app.route('/')
@basic_auth.required
def index():
    return render_template('index.html')
def gen(camera):
    while True:
        frame = camera.get_frame()
        yield (b'--frame\r\n'
               b'Content-Type: image/jpeg\r\n\r\n' + frame + b'\r\n\r\n')
@app.route('/video_feed')
def video_feed():
    return Response(gen(video_camera),
                    mimetype='multipart/x-mixed-replace; boundary=frame')
if __name__ == '__main__':
    t = threading.Thread(target=check_for_objects, args=())
    t.daemon = True
    t.start()
    app.run(host='0.0.0.0', debug=False)```

    
Mail.py
```import smtplib
from email.MIMEMultipart import MIMEMultipart
from email.MIMEText import MIMEText
from email.MIMEImage import MIMEImage
fromEmail = 'email@gmail.com'
fromEmailPassword = 'password'
toEmail = 'email2@gmail.com'
def sendEmail(image):
	msgRoot = MIMEMultipart('related')
	msgRoot['Subject'] = 'Security Update'
	msgRoot['From'] = fromEmail
	msgRoot['To'] = toEmail
	msgRoot.preamble = 'Raspberry pi security camera update'
	msgAlternative = MIMEMultipart('alternative')
	msgRoot.attach(msgAlternative)
	msgText = MIMEText('Smart security cam found object')
	msgAlternative.attach(msgText)
	msgText = MIMEText('<img src="cid:image1">', 'html')
	msgAlternative.attach(msgText)
	msgImage = MIMEImage(image)
	msgImage.add_header('Content-ID', '<image1>')
	msgRoot.attach(msgImage)
	smtp = smtplib.SMTP('smtp.gmail.com', 587)
	smtp.starttls()
	smtp.login(fromEmail, fromEmailPassword)
	smtp.sendmail(fromEmail, toEmail, msgRoot.as_string())
	smtp.quit()```

 
camera.py
```import cv2
from imutils.video.pivideostream import PiVideoStream
import imutils
import time
import numpy as np
class VideoCamera(object):
    def __init__(self, flip = False):
        self.vs = PiVideoStream().start()
        self.flip = flip
        time.sleep(2.0)
    def __del__(self):
        self.vs.stop()
    def flip_if_needed(self, frame):
        if self.flip:
            return np.flip(frame, 0)
        return frame
    def get_frame(self):
        frame = self.flip_if_needed(self.vs.read())
        ret, jpeg = cv2.imencode('.jpg', frame)
        return jpeg.tobytes()
    def get_object(self, classifier):
        found_objects = False
        frame = self.flip_if_needed(self.vs.read()).copy() 
        gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
        objects = classifier.detectMultiScale(
            gray,
            scaleFactor=1.1,
            minNeighbors=5,
            minSize=(30, 30),
            flags=cv2.CASCADE_SCALE_IMAGE
        )
        if len(objects) > 0:
            found_objects = True
        # Draw a rectangle around the objects
        for (x, y, w, h) in objects:
            cv2.rectangle(frame, (x, y), (x + w, y + h), (0, 255, 0), 2)
        ret, jpeg = cv2.imencode('.jpg', frame)
        return (jpeg.tobytes(), found_objects)```


# Bill of Materials


|Camera Case for Raspberry Pi zero| This is used as the case that holds the raspberry pi module and the camera|$9.95|<https://www.pishop.us/product/camera-case-for-raspberry-pi-zero-updated-for-v3/>|

| Raspberry Pi Camera Module| This captures pictures at 1080p 30fps and relays the information to the raspberry pi control board.| $25| <https://chicagodist.com/products/raspberry-pi-camera?src=raspberrypi>|

|Rii RKM709 2.4 Gigahertz Ultra-Slim Wireless Keyboard and Mouse Combo|Mouse and Keyboard to program the camera and use my computer|$18.99 |<https://www.amazon.com/Rii-Ultra-slim-Wireless-Multimedia-Raspberry/dp/B07BF3LFN3>|

| HDMI Video Capture Card| This is a converter that converts HDMI to USB so that it can be used on computers without HDMI ports  | $16.98 |<https://www.amazon.com/Capture-Streaming-Broadcasting-Conference-Teaching/dp/B09FLN63B3/ref=sr_1_3?keywords=hdmi+video+capture&qid=1687198760&sr=8-3> |

|Raspberry Pi 3 Power Supply| This supplies the camera with power via a micro USB port, and connects to a wall outlet|$9.95|<https://www.canakit.com/raspberry-pi-adapter-power-supply-2-5a.html>|

|HDMI to Mini HDMI Cable|This cable connects the mini HDMI port on the camera box to the HDMI port on the adapter| $7.59 | <https://www.amazon.com/AmazonBasics-High-Speed-Mini-HDMI-Adapter-Cable/dp/B014I8UEGY> |


<!---# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here. -->
