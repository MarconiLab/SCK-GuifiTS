SCK-GuifiTS
===========
Modification of SmartCitizen code to use SCK in ThingSpeak.

Source https://github.com/fablabbcn/Smart-Citizen-Kit

Getting Started
=====

### Adding a Smart Citizen Kit to ThingSpeak. Manual set up

Setting Smart Citizen Kit (SCK) by editing directly the source code. As the code is Open Source, one way of setting the Wi-Fi of your SCK is to download the firmware, edit some lines of code, recompile it and upload it to the kit. 
 
One advantage of this system is that it gives you the opportunity to register multiple Wi-Fi networks at the same time. This is useful if your SCK is traveling from one location to another where the Wi-Fi credentials are known. 

#### STEP 1: Getting the Firmware

You can download the latest firmware on our Github : 
https://github.com/MarconiLab/SCK-GuifiTS/tree/master/sck_beta_v0_9
As you may know, the hardware and software are based on the arduino project. we will use the Arduino IDE to edit the firmware and upload it to the kit. This tutorial have been tested with arduino 1.0.5. Get the Arduino IDE at http://arduino.cc/en/Main/Software.

Open the file https://github.com/MarconiLab/SCK-GuifiTS/blob/master/sck_beta_v0_9/sck_beta_v0_9.ino

#### STEP 2: Editing the code

If you want to set the network configuration manually, you should go to the Constant.h or
https://github.com/MarconiLab/SCK-GuifiTS/blob/master/sck_beta_v0_9/Constants.h
and modify the lines you see below (line 31):
 
```Arduino
#define networks 0
#if (networks > 0)
char* mySSID[networks]      = { 
  "Red1"        , "Red2"        , "Red3"             };
char* myPassword[networks]  = { 
  "Pass1"      , "Pass2"       , "Pass3"            };
char* wifiEncript[networks] = { 
  WPA2         , WPA2          , WPA2               };
char* antennaExt[networks]  = { 
  INT_ANT      , INT_ANT       , INT_ANT            }; //EXT_ANT
#endif
 ```
 
The easiest way would be to write "#define redes X" (where X is the number of WI-FI networks you are going to use),  add the name of your network in "RedX" and the corresponding password in "PassX". You could also choose the encryption mode that fits with your network's configuration (OPEN, WEP, WPA1, WPA2, WEP64) or the type of antenna you are using (*INT_ANT* for internal antenna (default) or *EXT_ANT* for external antenna).
 
If you register only one wifi credential, you should obtain something like:
 
 ```Arduino 
#define networks 1
#if (networks > 0)
char* mySSID[networks]      = { 
  "MyWifiSSID"    };
char* myPassword[networks]  = { 
  "MyPassword"    };
char* wifiEncript[networks] = { 
  WPA2            };
char* antennaExt[networks]  = { 
  INT_ANT         }; //EXT_ANT
#endif
 ```
 
#### STEP 3: Creating an account on ThingSpeak

In order to get started, you will need to have a free ThingSpeak User Account. If you have a user account, sign in and move to the next step.

Visit ThingSpeak server in the Cloud, for example TS server installed in a BeagleBoneBlack in Italy
10.95.0.25:3000
To create a new ThingSpeak User Account, click Sign Up
Sign into ThingSpeak
Step 2: Create ThingSpeak Channel
ThingSpeak Channels are were data from SCK will be stored. This procedure will create a blank channel ready for data from SCK module.

Sign into ThingSpeak
Select Channels
Click “Create New Channel”
Enter a name for your channel, “SCK ambient board”
Enter a name for Field 1, “Temperature” 
Enter a name for Field 2, “Humidity” 
Enter a name for Field 3, “Light” 
Enter a name for Field 4, “Battery” 
Enter a name for Field 5, “Solar Panel” 
Enter a name for Field 6, “Carbon Monoxide” 
Enter a name for Field 7, “Nitrogen Dioxide” 
Enter a name for Field 8, “Noise” 

Click “Update Channel”

Go to Api Key tab and copy channel API Key (ex. JA1SBQKH0T2SNB9U)

#### STEP 4: Updating ThingSpeak API keys on the code

Go back to Constant.h or
https://github.com/MarconiLab/SCK-GuifiTS/blob/master/sck_beta_v0_9/Constants.h
and modify the lines you see below (line 226):

static char* WEBTS[2]={
                   "10.95.0.25",		        //with the address of TS
                   "RX8HGPW4WCIGYHQS "};    //Channel Api key  

#### STEP 5: Downloading firmwatre to SCK
Now you are ready to download the file to SCK board!

EP 1: Configuring the Wi-Fi settings

Open Arduino IDE.
Connect your SCK via USB.
Open firmware sck_beta_v0_9.ino
From the Tools > Board menu, choose the right USB port (generally the last one).
From the Tools > Serial port menu, select the right board. This is LilyPad Arduino USB for SCK v1.1.
Upload firmware and ready!!
