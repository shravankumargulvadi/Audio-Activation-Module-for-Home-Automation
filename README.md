# Audio-Activation-Module-for-Home-Automation
The Project is split into 2 parts. Part I aims at developing a stand alone Audio Activation Module that can be used as plug in module in any application that requires audio activation like robots, task automation, toys etc. The Part II of the project focuses specifically on interfacing our module with the existing industry standard home automation hardware and making it work.

The inspiration for this project came from the Trigger word detection assignment (last assignment of the Sequence Modelling Module) of the Deep learning specialization on Coursera. The implementation hardware is Raspberry Pi 3 Model B and I make use of platform Deeplearning frame work; Tensorflow lite for our application.
I have created a virtual environment for this project with the necessary modules, the following points are worth noting in this regard:

Operating System-Windows 8.1

Tensorflow Version-2.0.0(incompatible on higher versions)

Python Version-3.7

Matplotlib version-3.1(incompatible on higher versions)

The following are some of the commands that may come in handy while working with virtual environments:

to create a new conda env

	- open anconda prompt
  
	- conda create --name env_name python=python_version
  
download necessary packages

 	- conda create --prefix ./envs jupyterlab=0.35 matplotlib=3.1 numpy=1.16
  
to activate an env
	
	- open anconda prompt
	
  - conda activate env_name

to open jupyter-notebook	

	- open anconda prompt
  
	- cd to required dir
  
	- jupyter-notebook
  
The Audio Activation code takes a recorded audio track as input looks for the word ‘Activate’, the detection of the trigger word is demonstrated as an output of ‘1’ in the sequence model. We use this output to activate specific pins of our Pi which we use inturn to interface with other modules (like our home automation controller).
The Home Automation Module has a System Controller that receives command signals from Mobile Phones, Touch interfaces etc these commands are interpreted by the controller and based on the commands operates the different components of home automation via switching modules like lighting, AC, Heater etc. We interface our Audio Activation Module to the Controller through an OR operation with commands from other modes like Mobile phones, touch screens etc. Thus an audio-verbal command of ‘Activate’ given is successfully translated into an activation command to the controller, which inturn controls the components of the home automation. 
 
 ![Capture](https://user-images.githubusercontent.com/19910970/93505997-41c36d00-f939-11ea-8117-e4e45c978ea6.JPG)
 
 ## Implementation of Trigger Word Detection Module:
	Trigger word detection is the mechanism used in systems such as Amazon eco, Google Home, apple siri etc where they are activated by a specific word instantaneously. The literature for Trigger word detection is still evolving and there isn't clear consensus regarding an optimal architecture for this application. However we implement this on a Unidirectional GRU model. (We have not used bidirectional implementation here as it would require the entire audio track to be processed before we get an output, but the whole point of trigger word detection is an instantaneous response).
 	I have used the final assignment of the Deep learning Specialization on coursera as my starting point of the course, and used its pretrained model as the initial step through tranfer learning. Training data can be generated through data synthesis, ie, we overlay both positive(in our case the word 'ACTIVATE') and negative words over a background noise track which represents the most probable application conditions. We maintain a standard audio track of 10 seconds as our input and convert it into a spectrogram ie Frequency Vs Time representation with standard discretization of time followed through out. We use this as the input to our model. 
	
![IMG_20200921_211358](https://user-images.githubusercontent.com/19910970/93789549-9e7f9a00-fc4f-11ea-8c79-ae056b1cbe9a.jpg)

![Model](https://user-images.githubusercontent.com/19910970/93789240-3cbf3000-fc4f-11ea-8188-86b51364b0ea.JPG)

## Hardware Details:
1.Raspberry Pi 3 Model B:
Raspberry Pi is a small single board computer, optimal for mobile applications.
Specs:
Quad Core 1.2GHz Broadcom BCM2837 64bit CPU
1GB RAM
BCM43438 wireless LAN and Bluetooth Low Energy (BLE) on board
100 Base Ethernet
40-pin extended GPIO
4 USB 2 ports
4 Pole stereo output and composite video port
Full size HDMI
CSI camera port for connecting a Raspberry Pi camera
DSI display port for connecting a Raspberry Pi touchscreen display
Micro SD port for loading your operating system and storing data
Upgraded switched Micro USB power source up to 2.5A

![raspberry](https://user-images.githubusercontent.com/19910970/93791771-49915300-fc52-11ea-9d83-ad7bebd52d44.jpg)

2. System Controller-Elan G1:
Features:
Complete single-package solution – includes everything needed to control an average media room system.
Compatible with remote, touch panels and keypads as well as iOS and Android mobile devices and PC and Mac computers.
Sense input – automation based on voltage, light, contact closure, or audio signals.
PoE or Wi-Fi connection 

Connections:
Serial RS-232 (1) 3.5mm Connector (Stereo)
ELAN Sense (1) 3.5mm Connector (Stereo)
IR Input (1) 3.5mm Connector (Stereo) 12V DC
IR Output (3) 3.5mm Connector (Mono) 12V DC
Audio (1) 3.5mm Connector (Stereo)
On-Screen Display (1) HDMI Female Connector
USB (1) USB-A Connector
Ethernet (1) RJ-45 PoE Compatible
Power (1) Coaxial Type-A – 2.5mm inside dimensions

![Elan-G1-Controller](https://user-images.githubusercontent.com/19910970/93791727-38484680-fc52-11ea-9d85-d0f39917dda2.jpg)
