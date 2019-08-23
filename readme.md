## Hand Movement Tracking

### Code Requirements
The example code is in Python ([version 2.7](https://www.python.org/download/releases/2.7/) or higher will work). 
You need to install opencv library


### Description

To perform video tracking an algorithm analyzes sequential video frames and outputs the movement of targets between the frames. There are a variety of algorithms, each having strengths and weaknesses. Considering the intended use is important when choosing which algorithm to use. There are two major components of a visual tracking system: target representation and localization, as well as filtering and data association.

Video tracking is the process of locating a moving object (or multiple objects) over time using a camera. It has a variety of uses, some of which are: human-computer interaction, security and surveillance, video communication and compression, augmented reality, traffic control, medical imaging and video editing.

The video is live streamed from Agora.io's RTC. Currently the live stream is done only from client to server. Streaming back from server to client is remaining.

For more information, [see](http://opencv-python-tutroals.readthedocs.io/en/latest/)

### Working Example

<img src="Hand tracking agora streaming.flv">



### Execution
Go to `https://agora-source.netlify.com/` 

Paste the app id: `49c2343ef91c4517a6c6a93a445e0a43` (its mentioned in `client=AgoraRTC.create_watcher("49c2343ef91c4517a6c6a93a445e0a43", str(c_path))`). 

Add channel as `gesture` (mentioned in`client.join_channel("gesture")`). 

You can change id and gesture as per your need. But remember to enter same in the browser (client side).


Then run the code, type `python live webcam network streaming hand tracking.py` for agora live webcam streaming hand movement tracking 

```
python live webcam network streaming hand tracking.py
```

Run `python live webcam network streaming hand tracking.py` for hand movement tracking on local system.
