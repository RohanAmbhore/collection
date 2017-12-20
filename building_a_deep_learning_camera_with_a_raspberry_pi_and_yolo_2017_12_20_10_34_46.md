<a href="https://www.makeartwithpython.com/blog/poor-mans-deep-learning-camera/">https://www.makeartwithpython.com/blog/poor-mans-deep-learning-camera/</a><div id="articleHeader"><h1>Building a Deep Learning Camera with a Raspberry Pi and YOLO</h1></div>

<p><div class="readableLargeImageContainer"><img src="/blog/assets/images/deep-lens/deep-learning-camera.jpg" /></div></p>

<p>Amazon has just announced <a href="https://aws.amazon.com/deeplens/" target="_blank">DeepLens</a>, a smart webcam that uses machine learning to detect objects, faces, and activities like playing a guitar on the camera itself. The DeepLens isn’t available yet, but the idea of a smart camera is exciting.</p>

<p>Imagine being able to use a camera that’s able to tell when you’re playing a guitar, or creating a new dance, or just learning new skateboard tricks. It could use the raw image data to tell if you landed a trick or not. Or if you’re doing a new dance routine, what the series of poses are, and how they fit to the music.</p>

<p>Today, we’ll build a deep learning camera that detects when there are birds present in the webcam image, and then saves a photo of the bird. The end result gives us images like this:</p>

<figure>
  
    
      <a href="/blog/assets/images/deep-lens/1.jpg" title="Detected Bird Image" target="_blank" class="readableLinkWithMediumImage">
        <img src="/blog/assets/images/deep-lens/1.jpg" />
      </a>
    
  
    
      <a href="/blog/assets/images/deep-lens/2.jpg" title="Detected Bird Image" target="_blank" class="readableLinkWithMediumImage">
        <img src="/blog/assets/images/deep-lens/2.jpg" />
      </a>
    
  
    
      <a href="/blog/assets/images/deep-lens/3.jpg" title="Detected Bird Image" target="_blank" class="readableLinkWithMediumImage">
        <img src="/blog/assets/images/deep-lens/3.jpg" />
      </a>
    
  
  
    <figcaption>Detected images including birds from the deep learning camera
</figcaption>
  
</figure>

<p>Deep learning cameras are the beginning of a whole new platform for machine learning computers.</p>

<p>The DeepLens has 100 GFlops of computational power available for inference, which is just the beginning of the computational power necessary for an interesting deep learning camera computer. In the future, these devices will get much more powerful, and allow for inferring hundreds of images a second.</p>

<p>But who wants to wait for the future?</p>

<h2 id="dumb-camera-smart-inference">Dumb Camera, Smart Inference</h2>

<p>Instead of building a deep learning model into our camera, we’ll use a “dumb” camera computer at the edge (like a $9 Raspberry Pi), hook it up to a webcam, and then send the images over WiFi. At the tradeoff of a bit more latency, we can build a prototype of the same DeepLens concept today, much cheaper.</p>

<p>So in today’s post, we’ll do just that. We’ll write a web server in Python to send images from a Raspberry Pi to another computer for inference, or image detection.</p>

<p><div class="readableLargeImageContainer"><img src="/blog/assets/images/deep-lens/deeplens.png" /></div></p>

<p>The other computer with more processing power will then use a neural network architecture called <a href="https://pjreddie.com/darknet/yolo/" target="_blank">“YOLO”</a> to do detection on that input image, and tell if there’s a bird in the camera frame.</p>

<p>We’ll start with the YOLO architecture, because it’s one of the fastest detection models around. And there is a port of its model to Tensorflow, which is very easy to install and get running on many different platforms. As a bonus, if you use the Tiny model we use in this post, you’ll also be able to do detection on a CPU, no expensive GPU needed.</p>

<p>Going back to our prototype. If there is a bird detected in the camera frame, we’ll save that image for later analyses.</p>

<p>This is just the beginning of a truly intelligent deep learning camera, and terribly basic, but you’ve got to start from somewhere. So let’s jump in, and get the first version of our prototype our the door.</p>

<h2 id="detection-vs-imaging">Detection vs Imaging</h2>

<figure>
  
    
      <a href="/blog/assets/images/deep-lens/1.jpg" title="Detected Bird Image" target="_blank" class="readableLinkWithLargeImage">
        <div class="readableLargeImageContainer"><img src="/blog/assets/images/deep-lens/1.jpg" /></div>
      </a>
    
  
    
      <a href="/blog/assets/images/deep-lens/labeled/0.jpg" title="Labeled Bird Image. Notice the wrong label 'bicycle'." target="_blank" class="readableLinkWithLargeImage">
        <div class="readableLargeImageContainer"><img src="/blog/assets/images/deep-lens/labeled/0.jpg" /></div>
      </a>
    
  
  
    <figcaption>Detected and Labeled Birds
</figcaption>
  
</figure>

<p>As we’ve already said, the DeepLens’ imaging is built right into the computer. So it can do base level detection, and determine if the images coming in match your criteria or not with the onboard computational power.</p>

<p>But with something like a Raspberry Pi, we won’t necessarily have the computational power necessary to do onboard detection in real time. So instead, we’re going to use another computer to do the inference of what’s in the image.</p>

<p>In my case, I used a base, simple Linux computer with a webcam and wifi access (<a href="http://amzn.to/2B1ZEV2" target="_blank">Raspberry Pi 3</a> and a <a href="http://amzn.to/2Crwtqv" target="_blank">cheap webcam</a>), to act a server for my deep learning machine to do inference from.</p>

<p>This is a good stack, because it allows for keeping many cheaper cameras in the wild, and doing all my computation in one place, on my desktop machine.</p>

<h2 id="webcam-image-server-stack">Webcam Image Server Stack</h2>

<p>If you don’t want to use the Raspberry Pi camera, you can install OpenCV 3 on your Raspberry Pi <a href="https://www.pyimagesearch.com/2017/09/04/raspbian-stretch-install-opencv-3-python-on-your-raspberry-pi/" target="_blank">using these instructions</a>, although substitute OpenCV version 3.3.1 for 3.3.0 in the instructions to get the latest version installed locally.</p>

<p>As a sidenote, I had to disable CAROTENE compilation in order to get 3.3.1 on my Raspberry Pi. You may need to do the same.</p>

<p>Once that’s done, we just need to set up our web server in Flask, so we can load the images from the webcam.</p>

<p>I’ve used <a href="https://blog.miguelgrinberg.com/post/flask-video-streaming-revisited" target="_blank">Miguel Grinberg’s</a> excellent <a href="https://github.com/miguelgrinberg/flask-video-streaming" target="_blank">webcam server code</a> as a starting place, and created just a simple jpg endpoint instead of a motion jpeg endpoint:</p>

<div><div><pre><code>#!/usr/bin/env python
from importlib import import_module
import os
from flask import Flask, render_template, Response

# uncomment below to use Raspberry Pi camera instead
# from camera_pi import Camera

# comment this out if you're not using USB webcam
from camera_opencv import Camera

app = Flask(__name__)

@app.route('/')
def index():
    return "hello world!"

def gen2(camera):
    """Returns a single image frame"""
    frame = camera.get_frame()
    yield frame

@app.route('/image.jpg')
def image():
    """Returns a single current image for the webcam"""
    return Response(gen2(Camera()), mimetype='image/jpeg')

if __name__ == '__main__':
    app.run(host='0.0.0.0', threaded=True)

</code></pre></div>

<p>If you want to use the Raspberry Pi video camera, make sure you uncomment the <code>from camera_pi</code> line, and comment out the <code>from camera_opencv</code> line.</p>

<p>You can get this server running with just a <code>python3 app.py</code>, or using <code>gunicorn</code>, the same as is mentioned in Miguel’s post.</p>

<p>It just uses Miguel’s excellent camera management to turn off the camera when there aren’t requests coming in, and also manages threads, if we have more than one machine doing inference on the images coming in from the webcam.</p>

<p>Once we’ve started it on our Raspberry Pi, we can test and make sure the server works by first discovering it’s IP address, and then attempting to reach it via our web browser.</p>

<p>The URL should be something like <code>http://192.168.1.4:5000/image.jpg</code>:</p>

<figure>
<div class="readableLargeImageContainer"><img src="/blog/assets/images/deep-lens/success.png" /></div>
<figcaption>Load the web page of the Raspberry Pi to confirm the image server works.</figcaption>
</figure>

<h2 id="pulling-images-and-doing-inferences-from-the-camera-server">Pulling Images and Doing Inferences from the Camera Server</h2>

<p>Now that we’ve got an endpoint to load the webcam’s current image from, we can build the script to grab and run inference on those images.</p>

<p>We’ll use <code>requests</code>, the great Python library for grabbing files from URLs, along with <a href="https://github.com/thtrieu/darkflow/" target="_blank">Darkflow</a>, an implementation of the YOLO models on Tensorflow.</p>

<p>Unfortunately, there isn’t a pip wheel for installing <a href="https://github.com/thtrieu/darkflow/" target="_blank">Darkflow</a>, so we’ll need to clone the repo, and then build and install it ourselves on the computer that will be doing our inferences.</p>

<p>After installing the Darkflow repo, we’ll also need to download the weights and model of a version of YOLO we’ll be using.</p>

<p>In my case, I used the YOLO v2 tiny network, as I wanted to run my inference on a slower computer, using the onboard CPU, not the GPU in my main desktop. The tiny network comes with the tradeoff of less accuracy than the full YOLO v2 model.</p>

<p>With this built and downloaded, we’ll also need <code>Pillow</code>, <code>numpy</code>, and OpenCV installed on the detection computer.</p>

<p>Finally, we can finally write our code to run detection:</p>

<div><div><pre><code>from darkflow.net.build import TFNet
import cv2

from io import BytesIO
import time
import requests
from PIL import Image
import numpy as np

options = {"model": "cfg/tiny-yolo-voc.cfg", "load": "bin/tiny-yolo-voc.weights", "threshold": 0.1}

tfnet = TFNet(options)

birdsSeen = 0
def handleBird():
    pass

while True:
    r = requests.get('http://192.168.1.11:5000/image.jpg') # a bird yo
    curr_img = Image.open(BytesIO(r.content))
    curr_img_cv2 = cv2.cvtColor(np.array(curr_img), cv2.COLOR_RGB2BGR)

    result = tfnet.return_predict(curr_img_cv2)
    print(result)
    for detection in result:
        if detection['label'] == 'bird':
            print("bird detected")
            birdsSeen += 1
            curr_img.save('birds/%i.jpg' % birdsSeen)
    print('running again')
    time.sleep(4)
</code></pre></div>

<p>With this, we have a very basic first version of our detection running. We can see in the console for our Raspberry Pi what’s being detected, and we can also see each of the birds being seen saved on to our hard drive.</p>

<p>Later, we can run a program to do labeling on the images YOLO has detected birds in.</p>

<h2 id="balance-more-false-positives-or-more-false-negatives">Balance: More False Positives or More False Negatives?</h2>

<p>One thing to take note of, our <code>threshold</code> key in the options dictionary we created.</p>

<p>This threshold says what confidence level we need to have at a minimum to say we’ve detected what we’re looking for.</p>

<p>For testing purposes, I’ve set it to be 0.1. But this low of a threshold will give us a lot of false positives. Worse still, the Tiny YOLO model we’ve used for detection is less accurate than the real YOLO model, and so we’ll have a fair bit of wrong detections.</p>

<p>Lowering or raising the threshold can improve or lower the total output of your model, depending on what you’re trying to build. In my case, I’m fine with more false positives, but I really prefer to get more images of birds than less. You may need to tweak these parameters to match your needs.</p>

<h2 id="waiting-for-the-birds">Waiting for the Birds</h2>

<p>Getting birds into my bird feeder took a long time. I figured I’d have birds in the backyard for my feeder within hours of putting out food.</p>

<p>Instead, it took a few days. Squirrels kept eating the food I’d left out, and it seemed for the first few days I hardly saw a bird in the sky at all.</p>

<p>Finally, I broke down and got a second bird feeder, one that was a bit more visible and off the ground. With this, I finally started getting some images like the ones at the beginning of the post.</p>

<h2 id="where-to-go-from-here">Where to Go from Here</h2>

<p>The code for this post is <a href="https://github.com/burningion/poor-mans-deep-learning-camera" target="_blank">available at Github</a>, as always.</p>

<p>Because so much of this post itself was just combining other previous work, there isn’t really much to it. A huge debt is owed to both Miguel Grinberg’s <a href="https://blog.miguelgrinberg.com/post/flask-video-streaming-revisited" target="_blank">Flask streaming video example</a>, and to <a href="https://github.com/thtrieu/darkflow" target="_blank">Darkflow</a> and <a href="https://pjreddie.com/darknet/" target="_blank">Darknet</a> for the deep learning models used for detection.</p>

<p>This post is the beginning of a set of lessons where I will use deep learning cameras to try and interact with birds.</p>

<p>If you’re interested in following along, I encourage you to subscribe below, or <a href="https://www.makeartwithpython.com/signup" target="_blank">create an account</a> here on Make Art with Python.</p>

<p>Finally, feel free to share this post with your friends. It helps me to continue making these sort of tutorials.</p>






<div id="mc_embed_signup">
    
        <div id="mc_embed_signup_scroll">
	          <label>Enter Your Email to Receive More Posts Like This</label>
	          
            
            
            
        </div>
    





        
      