# Butterbot
Home made Butterbot using google AIY Vision

Hi I am Butterbot.
My five year old son and I check out robots and robot toys all the time. One of our favorite robotics companies Digital Dreams Labs is releasing a version of Butterbot from the Rick and Morty TV show. We thought it was super cute and wanted to make our own. 

The original from the show (we have not watched):

Digital Dream Labs version:


Not yet released. Pre order price is around $150 and retail will be around $200.

Our Butterbot:
Google AIY Vision kit (ebay I picked up around $30), 2 arm servos ($5), Remote control car ($11), the body is made from the box that the vision kit comes with and some Aluminum duct tape. He speaks through a Jabba Bluetooth Speaker I received from work as a thank you gift, thoroughly disassembled and battery and switches are placed in the body and the speaker in the head. I also placed a USB battery in the base for the Vision Kit.

A little bit about the Vision kit. One of Google's first attempts at offloading inferencing onto a separate chip. The main computing component is a Pi Zero W..
CPU: ARM11 running at 1GHz.
RAM: 512MB.
Wireless: 2.4GHz 802.11n wireless LAN.
Bluetooth: Bluetooth Classic 4.1 and Bluetooth LE.
Power: 5V, supplied via micro USB connector.
Video & Audio: 1080P HD video & stereo audio via mini-HDMI connector.(no audio jack)
With some research I figured out that they are using the original Intel Movidius chip on a special Hat to do the inferencing. The hat also provides connections for a small speaker, the green light, and the multicolored lights and button unit on the top. The Vision kit is capable of running some of the small vision models like mobilenet.
One thing I struggled with was the Bluetooth. I had to thoroughly update everything and add the pulseaudio bluetooth module for Butterbot to connect. Future plans include having the bluetooth auto connect without the GUI starting so he can run headless. Right now it does not connect unless logged into. 

To generate speech in a light manner I used the python pyttsx3 package. I also had to install espeak to allow pyttsx3 to work.  To operate the  servos I installed the python gpiozero package.
I used the example program Joy detection demo that starts by default with AIY vision to run Butterbot.

#The Aiy pins have their own package and I bring them into gpiozero by:
from gpiozero import Servo
from gpiozero import AngularServo
from aiy.pins import PIN_A
from aiy.pins import PIN_B

servo_a = AngularServo(PIN_A, min_angle=-90, max_angle=90)
servo_b = AngularServo(PIN_B, min_angle=-90, max_angle=90)
#Then I tie their movement to the joy score:
def process(self, joy_score):
        if joy_score > 0:
            self._leds.update(Leds.rgb_on(Color.blend(JOY_COLOR, SAD_COLOR, joy_score)))
            try:
                servo_a.angle = ((joy_score*100) - 10)
                
            except:
                print('servo a error')
                

            try:
                servo_b.angle = -((joy_score*100) - 10)
            except:
                print('servo b error')

#Here I set up the speech engine’s properties by starting it, setting the words per minute and what voice I would like to use:
engine = pyttsx3.init()
engine.setProperty('rate', 140)
engine.setProperty('voice', 'english_rp')

# I tie the voice engine to the high joy variable in the joy detector:
def joy_detector()

if event == 'high':
                logger.info('High joy detected.')
                player.play(JOY_SOUND)
                try:
                    happy =['Is there anything more marvelous than butter?'
# This is an example from the list. I used some facts I found about butter and just some fun things to say about butter for this list.
happy_choice = random.choice(happy)
                    print('happy choice: '+happy_choice)
                    engine.say(happy_choice)
                    engine.runAndWait()
                except:
                        print('error speaking')

# For the silly phrases I attached to the button I use the original take photo that happens when you push the button and replace the actions and activate the speech engine with the list of phrases.:
silly = [" Nonsense. With my maps and my journals, a six-year-old could find the shrine."]
# This is an example of the silly list. Original is quite long. It is a combination of some scooby do dialogue and some output from my Cinder AI built with distilgpt2 a NLP model.
def take_photo():
            logger.info('Button pressed.')
            player.play(BEEP_SOUND)
            #photographer.shoot(camera)
            try:
                silly_choice = random.choice(silly)
                engine.say(silly_choice)
                engine.runAndWait()
                print(silly_choice)
            except:
                print('fail:' )

Here is a link to a short video I made with Butterbot and me smiling at him. 
https://youtu.be/ulvmUMsXL6k

The construction instructions and setup for the AIY Vision can be found here:
https://aiyprojects.withgoogle.com/vision
The design is great and very simple. The camera cables for it are hard to work with and I replaced one of them with a longer one because I kept pulling it out.  The other models and scripts are pretty easy to work with also. I found a custom model for the Vision kit that Identifies different types of dishes and foods. Might be something worth trying if I attached a motor controller to Butter bot so that he could actually serve butter.  The repo for the AIY Projects:
https://github.com/google/aiyprojects-raspbian
