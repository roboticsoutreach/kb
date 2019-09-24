---
title: Camera Board
---

The Camera Board is a project that aims to find a hardware replacement for webcams.

The current Webcams have a slow shutter speed and the image quality is not great, this means that thr robots cannot take images while moving, and can lead to some big issues if the lighting is not right.

Using Raspberry pi camera's we can improve the shutter speed, which will hopefully allow for image processing on the move. We can also have a compute module 3 which deals with all of the image processing so that the robot "brain" doesn't have to. It will also allow for 2 cameras, one which can either be attached to the board directly or over a HDMI cable, and the other will be just over HDMI. This will allow for taking images in different directions, or having a forward facing camera and a turning camera, or could be used for stereo vision.

The first prototype for this board was made at the end of the 2018-2019 academic year, and did not work due to impedance matching issues on the HDMI lines, which meant we could not get a signal out of the Pi. This can likely be fixed by using a 4 layer stackup with a tuned impedance, this way we can ensure that the signal does not destructively interfere with itself in the cable by tuning the width of the PCB traces and the distance between the signals of a differential pair. 

The Schematic has currently been updated and is now licenced under CC by SA, where previously it didn't have a license. The next step is to reoute the PCB, and order it so that a second prototype can be tested, if that works, then some of the IO will be removed, and the PCB will be made as small as possible. At this point the PCB will be ready for manufacture.

Once we have a working prototype, work will start on the software which will allow the compute module to do the image processing, and send the data over USB to the "brain" of the computer when requested. The specification and architecture of the software are not yet decided.

This project is currently being lead by Joe Morton and Daniel Hobson, so if you would like to get involved with any aspect of this project, please speak to one of us.

