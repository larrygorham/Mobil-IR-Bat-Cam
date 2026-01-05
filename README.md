MobiBatCam
1.	Introduction

The MotiBatCam system was an addon to an existing little brown bat colony consisting of a 4” x 6” pole 16’ tall with two attached “Bat Bunker” bat boxes from batmanagement.com.  The recording system consists of the solar panel, camera, IR lights, control box, battery box and connection wires.  Recording is automatically performed each day according to sunset and sunrise times stored in a text file in the control box computer. Video is stored on a uSD card in the control box that is switched every few days with a fresh card.  The video files and an info file for each event are taken off the uSD card and stored in the cloud. This recorder can accommodate many more videos. Using a low-res camera an entire season can fit on one terabyte card.

   
A Raspberry Pi 4b is the central processing unit (CPU) for MobiBatCam and only runs when actually recording video. A WittyPi microprocessor scheduling unit runs continuously to power up the CPU at the correct time for morning and evening runs on each day.   During normal running the WittyPi reads the next run number from runCount.txt (located in the wittypi directory), extracts that run time (Unix epoch time) from beginTimes.txt and if it is greater than the current time it continues. If not, it continues to read subsequent start times, comparing that time with the current time until the next appropriate one is reached. The wittypi boots the Raspberry Pi when its onboard real time clock reaches that scheduled time. The Raspberry Pi records video and status data to the uSD card for two hours, increments the current run number and powers down the Raspberry Pi, thereby returning control to the WittyPi.

2.	Start Up
   
When starting the system after a total shutdown or for the first time the runCount.txt should be set to 1. Then WittyPi will step through the beginTimes.txt until the next appropriate epoch time is reached and boot the Raspberry Pi for the normal startup. 

From a cold start:
Push start button on the WittyPi ,
Open a command line window and kill all pending stuff.
./kl
./kl
sudo killall fpsA

cd wittypi
make sure runSettings.txt has 490 7200 28800
make sure runNumber.txt is 1
./WMCCrun.sh will shut down the Raspberry Pi and restart it at the correct time

3.	Comments
   
Actual start times in beginTimes.txt are 30 minutes before sunset and 90 minutes before sunrise. The beginTimes.txt should be recomputed each year to compensate for the Earth's orbit and the leap year cycle.


4. Detailed installation and testing instructions are in the Wiki.

