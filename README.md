# Andbot-Software-Development-Plan


# Introduction
This document describes Andbot software module list and development plan.

# High-Level User Scenarios

## Open Box
* Tablet app to guide the user to download mobile app and subsequent setup procedures
* Mobile app to connect to robot and provisioning WiFi configuration to Andbot
* Mobile app to command the robot's base movement
* Mobile app to command the robot's arms movement 

## Auto-Upgrade over the air
* Tablet as GUI 
** Robot automatically check latest updates and download firmware in background
** When firmware downloaded, prompt messages to user to confirm the upgrade
 

## Telepresence and Teleop
* User can use PC or mobile phone to call the robot to establish the telepresence session.
* When the session established, the two-way audio and video media are delivered.
* User can even remotely operate the robot movement via mobile app.

## Navigation to a goal
* User can use mobile phone app to display the map and command the robot to go to a goal.

## Speech command
* Dialog-based speech interactions
* TBD


# System Architecture
* Here is the proposed system architecture: 
* All the intelligent modules will be on tablet or on ROS board.

![](https://docs.google.com/drawings/d/1OLJy2XtJEqDVM9ngFmSA43X3o70QNqNm0j4HAXmmKoQ/pub?w=1514&h=1336)

[Proposed Architecture in google doc](https://docs.google.com/drawings/d/1OLJy2XtJEqDVM9ngFmSA43X3o70QNqNm0j4HAXmmKoQ/edit?usp=sharing)

# Technical Modules to be developed
* To achieve above user scenarios, the following features needs to be implemented.  
* Each feature should be formed as a software development project.  

## Open Box App
* Open Box app on tablet
* Open Box app on Mobile phone

## Auto-Upgrade OTA 
* Remotely auto-upgrade app on Tablet
* Remotely auto-upgrade app on ROS board
* Remotely auto-upgrade firmware on Arduino boards
* Auto-Upgrade server and web UI on AWS
* Each robot will be assigned an unique "robotId"
* Upgrade by specified "robotId"

## Control by Mobile App
* Android mobile app
* iOS mobile app
* GUI to control base movement
* GUI to control arms movement
* Taipei team will develop ROS API and Denis's team will develop mobile apps
 
## Telepresence and Teleop
* This is for remote participation scenario. 
* We MAY leverage "webrtc" technology to establish P2P video calls, which can penetrate most NATs/Firewalls.
* App on Tablet
* App on Mobile
* Refer to http://www.doublerobotics.com/ 
* Refer to KKuei's work: https://github.com/oudeis/therobot/tree/master/webrtcProject

## Navigation & Obstacle Avoidance
* This makes the robot to be able to go to a specified goal.
* We will leverage ROS navigation stack,
* Refer to: http://wiki.ros.org/navigation

## SLAM Module
* SLAM stands for "Simultaneous Localization and Mapping"
* The robot must be able to construct and update a map on an unknown environment while simultaneously keeping track its location.
* Must integrate with some sensors including:
 * LiDAR (the most important one)
 * Electronic compass
 * RGB-D sensors (ex. Kinect or XtionPro Live ...etc)
* We will leverage ROS gmapping module
 * http://wiki.ros.org/gmapping?distro=indigo
* We will develop a mobile app to display the map and user can specify where the robot to go.


## Speech Interactions
* This is something like "Siri" or "Okay, Google". We should make a "Okay, Andbot".
* We can leverage several Android's services
 * https://developer.android.com/reference/android/service/voice/VoiceInteractionService.html
 * http://developer.android.com/reference/android/speech/SpeechRecognizer.html
* Full speech conversation is too difficult. Instead, we can go dialog-based and retrieve limited commands by keywords 
* If necessary, the robot should respond with speech, e.g., "Yes, master".
 * We can leverage Android's TextToSpeech service 
 * Refer to: http://developer.android.com/reference/android/speech/tts/TextToSpeech.html


## Computer Vision and Object Recognition
* The robot should be able to recognized "who" so that it can try to close to the "right" person.
* We can leverage OpenCV template matching by preset face images
 * Refer to: http://docs.opencv.org/doc/tutorials/imgproc/histograms/template_matching/template_matching.html
* The robot also must be able to recognize several specific objects, e.g., cups, bowls, door knob ...etc
* Must be able to measure relative positions between the object and the robot.

## Arms Manipulation
* As above, once we know the relative positions, we can have wheels to move to close to the object or person.
* Then we can leverage the inverse kinematics technology to have the robot arms and grasp to rotated to desired angles to get the object.
* Even more, the robot can carry the object and put it to somewhere destinated. 
* We will leverage ROS MoveIt,  http://moveit.ros.org/





# Implementation Priorities & Schedules (draft)
* Auto Upgrade OTA (Taipei team)
* Control by Mobile App (Denis's team)
* Telepresence & Teleop (Denis's team)
* Navigation & Obstacles Avoidance  (Taipei team)
* SLAM (Taipei team)
* Computer Vision & Object Recognition (TBD)
* Speech Interaction (TBD)
* Arms Manipulation (TBD)


# References
* SLAM
 * http://en.wikipedia.org/wiki/Simultaneous_localization_and_mapping
 * http://wiki.ros.org/robotino_navigation/Tutorials/Mapping%20with%20Robotino
* Navigation
 * http://en.wikipedia.org/wiki/Mobile_robot_navigation
 * http://wiki.ros.org/navigation
* LiDAR
 * https://www.sparkfun.com/products/13167
* Object Recognition
 * http://docs.opencv.org/doc/tutorials/imgproc/histograms/template_matching/template_matching.html
 * http://docs.opencv.org/doc/tutorials/objdetect/table_of_content_objdetect/table_of_content_objdetect.html
* Inverse Kinematics
 * http://en.wikipedia.org/wiki/Inverse_kinematics
* Speech Interactions 
 * https://developer.android.com/reference/android/service/voice/VoiceInteractionService.html
 * http://developer.android.com/reference/android/speech/SpeechRecognizer.html
* Webrtc
 * http://www.webrtc.org/native-code/android
