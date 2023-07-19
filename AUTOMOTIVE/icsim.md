# AUTOMOTIVE SECURITY

## TASK DESCRIPTION:

Perform a Replay Attack on ICSim using Can-utils, Increase the speed above 100kmph in ICSim

## SOLUTION

- ICSIM has an inbult speed limiter of 95kmph

- We need to identify the `ID` of speed control upon checking the manual it is found to be `244`

- Then we can use the command `cansend vcan0 ID#package` to send the instruction to the simulator

- `cansend vcan0 244#000000A000` giving this command to the terminal we can get the simulator to a speed above 100kmph

- The packages that are sent are in hexadecimal 
  
  ![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-18-16-03-32-Screenshot%20from%202023-07-18%2015-16-56.png)

### REPLAY ATTACK IN ICSIM

- To save the log of the commands gives we need to use the command `candump -c vcan0 -l` it will log the traffic sent to the simulator and save it with date and tie stamps

- If candump command is not found we can get it with `sudo apt install can-utilis` 

- CANDUMP
  
  ![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-18-20-28-44-Screenshot%20from%202023-07-18%2015-05-41.png)

- This is the log of the traffic that was saved
  
  ![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-18-16-11-19-Screenshot%20from%202023-07-18%2015-06-40.png)

- To replay this log of traffic we can use the command  `canplayer -I "canlog"`

- The entire traffic which was saved in the log will be replayed

- 
