# WIRELESS AND ICS SECURITY

## Challenge Description:

[wired.pcap](https://gitlab.com/bi0s-hardware/illuminati/wiredctf/-/blob/Xavi0r_patch/wireless/Wire%205niffer/wired.pcap)  from this pcap file we need to get the flag

## Solution:

-`binwalk` is done on the given pcap file 

![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-17-16-00-19-Screenshot%20from%202023-07-17%2015-52-46.png)

-The `pcap` file is the loaded into **wireshark** 

-`http` objects are oexported

![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-17-16-11-24-Screenshot%20from%202023-07-17%2016-11-11.png)

-from `Jarvis.txt` we get a clue

**Hey Have you heard about hiding texts inside images????!!!**

-s0m3_r4andom3_1mg.png must contain the flag

-We must use image steganography methods to find the flag

-Most common method of image steganography is LSB method

-`zsteg` commad is used to extract the flag from the image in terminal

![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-17-16-22-45-Screenshot%20from%202023-07-17%2016-21-07.png)



### FLAG:

**wired{b1g_m4n_1n_a_su1t3_0f_4rm0r}**


