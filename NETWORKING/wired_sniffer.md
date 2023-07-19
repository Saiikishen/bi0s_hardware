# WIRELESS AND ICS SECURITY

## Challenge Description:

[wired.pcap](https://gitlab.com/bi0s-hardware/illuminati/wiredctf/-/blob/Xavi0r_patch/wireless/Wire%205niffer/wired.pcap)  from this pcap file we need to get the flag

## Solution:

-`binwalk` is done on the given pcap file 
![Screenshot from 2023-07-17 15-52-46](https://github.com/Saiikishen/bi0s_hardware/assets/128302556/f421e376-5ce8-4c8c-b94e-9eb74c5305da)


-The `pcap` file is the loaded into **wireshark** 

-`http` objects are oexported

![Screenshot from 2023-07-17 16-11-11](https://github.com/Saiikishen/bi0s_hardware/assets/128302556/271233b8-d460-43ef-bcc8-631a4fade5cd)


-from `Jarvis.txt` we get a clue

**Hey Have you heard about hiding texts inside images????!!!**

-s0m3_r4andom3_1mg.png must contain the flag

-We must use image steganography methods to find the flag

-Most common method of image steganography is LSB method

-`zsteg` commad is used to extract the flag from the image in terminal

![Screenshot from 2023-07-17 16-21-07](https://github.com/Saiikishen/bi0s_hardware/assets/128302556/09d1a13c-1a86-4da0-a688-41e893507eac)



### FLAG:

**wired{b1g_m4n_1n_a_su1t3_0f_4rm0r}**


