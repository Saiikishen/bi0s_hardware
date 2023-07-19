# AUTOMOTIVE SECURITY

## TASK DESCRIPTION:

Perform a Replay Attack on ICSim using Can-utils, Increase the speed above 100kmph in ICSim

## SOLUTION

- ICSIM has an inbult speed limiter of 95kmph

- We need to identify the `ID` of speed control upon checking the manual it is found to be `244`

- Then we can use the command `cansend vcan0 ID#package` to send the instruction to the simulator

- `cansend vcan0 244#000000A000` giving this command to the terminal we can get the simulator to a speed above 100kmph

- The packages that are sent are in hexadecimal

  
![Screenshot from 2023-07-18 15-16-56](https://github.com/Saiikishen/bi0s_hardware/assets/128302556/79523bee-c20f-4f37-87f6-846d2f8e5e6e)

  
### REPLAY ATTACK IN ICSIM

- To save the log of the commands gives we need to use the command `candump -c vcan0 -l` it will log the traffic sent to the simulator and save it with date and tie stamps

- If candump command is not found we can get it with `sudo apt install can-utilis` 

- CANDUMP
- 
  ![Screenshot from 2023-07-18 15-05-41](https://github.com/Saiikishen/bi0s_hardware/assets/128302556/2410e77a-b2b4-4cc3-b3b3-19f41d143d77)



- This is the log of the traffic that was saved

- 
  ![Screenshot from 2023-07-18 15-06-40](https://github.com/Saiikishen/bi0s_hardware/assets/128302556/b7e1e832-5af8-4507-9363-1cb6d804af14)

 

- To replay this log of traffic we can use the command  `canplayer -I "canlog"`

- The entire traffic which was saved in the log will be replayed


