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
  
The Audio Activation code takes a recorded audio track as input looks for the word ‘Activate’, the detection of the trigger word is demonstrated as an output of ‘1’ in the sequence model. We use this output to activate specific pins of our hardware which we use inturn to interface with other modules (like our home automation controller).
The Home Automation Module has a System Controller that receives command signals from Mobile Phones, Touch interfaces etc these commands are interpreted by the controller and based on the commands operates the different components of home automation via switching modules like lighting, AC, Heater etc. We interface our Audio Activation Module to the Controller through an OR operation with commands from other modes like Mobile phones, touch screens etc. Thus an audio-verbal command of ‘Activate’ given is successfully translated into an activation command to the controller, which inturn controls the components of the home automation. 
 
