# NETWORK FORENSICS

## CHALLENGE DESCRIPTION:

Bob and Charlie were sending some messages among themselves,and I planned to intercept their secrecy and get something out of it, however they are clever enough that no one gets anything. Please help me out to get the secret!!

In [`this`](https://drive.google.com/drive/folders/19ye_jvf93SzScmoMcuZ3cfU471aY80gj?usp=share_link) Challenge we are given a **Dcrypt.pcap** file which contains packet data of Networks. We are going to use `Wireshark` to analyse these Packets .

## SOLUTION

- `binwalk` is done on the pcap file
  
  ![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-18-01-21-57-Screenshot%20from%202023-07-18%2001-21-23.png)

- As we can see the pcap file contains a PGP message and a PNG image

- The PGP message can be extracted by giving the following filter `frame contains “MESSAGE`
  
  ![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-18-01-31-54-Screenshot%20from%202023-07-18%2001-30-16.png)

- `aGVsbG93b3JsZA` is a base64 encryption of the passphrase which is `helloworld`

- The above diagram contains the **Public Key** 

- To get the PNG image `frame contains “PNG”` filter is used
  
  ```
  0000   d2 94 4d 79 6f e8 32 c2 f7 c1 f7 8e 08 00 45 00   ..Myo.2.......E.
  0010   01 e7 93 5b 40 00 40 11 cf a5 c0 a8 2a 81 c0 a8   ...[@.@.....*...
  0020   2a 33 00 35 70 36 00 39 33 76 2d 9f 81 80 00 01   *3.5p6.93v-.....
  0030   00 01 00 00 00 00 03 73 73 6c 07 67 73 74 61 74   .......ssl.gstat
  0040   69 63 03 63 6f 6d 00 00 01 00 01 c0 0c 00 01 00   ic.com..........
  0050   01 00 00 00 15 00 04 ac d9 a3 a3 00 00 00 00 00   ................
  0060   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
  0070   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
  0080   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
  0090   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
  00a0   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
  00b0   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
  00c0   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
  00d0   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
  00e0   89 50 4e 47 0d 0a 1a 0a 00 00 00 0d 49 48 44 52   .PNG........IHDR
  00f0   00 00 00 c8 00 00 00 c8 08 06 00 00 00 ad 58 ae   ..............X.
  0100   9e 00 00 17 e4 49 44 41 54 78 9c ed 56 db 8e ec   .....IDATx..V...
  0110   3c ab 5c ef ff d2 b3 af fa 97 37 aa 13 e9 6f 4c   <.\.......7...oL
  0120   a4 a1 a4 56 12 07 43 81 29 d2 ff 7e 16 8b 05 c5   ...V..C.)..~....
  0130   bf 69 02 8b c5 9b b1 02 59 2c 04 56 20 8b 85 c0   .i......Y,.V ...
  0140   0a 64 b1 10 58 81 2c 16 02 2b 90 c5 42 60 05 b2   .d..X.,..+..B`..
  0150   58 08 ac 40 16 0b 81 15 c8 62 21 b0 02 59 2c 04   X..@.....b!..Y,.
  0160   56 20 8b 85 c0 0a 64 b1 10 58 81 2c 16 02 2b 90   V ....d..X.,..+.
  0170   c5 42 60 05 b2 58 08 ac 40 16 0b 81 15 c8 62 21   .B`..X..@.....b!
  0180   b0 02 59 2c 04 56 20 8b 85 c0 0a 64 b1 10 58 81   ..Y,.V ....d..X.
  0190   2c 16 02 2b 90 c5 42 60 05 b2 58 08 ac 40 16 0b   ,..+..B`..X..@..
  01a0   81 15 c8 62 21 b0 02 59 2c 04 56 20 8b 85 c0 0a   ...b!..Y,.V ....
  01b0   64 b1 10 18 11 c8 bf 7f ff e8 af da d5 7b 64 8b   d............{d.
  01c0   f6 9d f6 2c a6 f2 5d d7 ba ef 15 37 95 23 db 8b   ...,..]....7.#..
  01d0   e2 22 fe 28 1f c5 4d d5 87 ed 65 36 28 bf 24 4f   .".(..M...e6(.$O
  01e0   94 a3 ea 8b 9b 18 13                              .......
  ```

- To extract the PNG from the pcap file `scapy` is used
  
  ```python
  from scapy.all import*
  from scapy.layers.inet import IP
  from scapy.layers.dns import DNS
  
  file =rdpcap('/home/saiikishen/Desktop/bi0s_hardware/Decrypt.pcap')
  t=bytes()
  for i in range(len(file)):
      if file[i].haslayer("DNS") and len(file[i]) > 450 :#PNG packet size > 450
          t+=bytes(file[i])[224:]#224 is the starting byte index of PNG data
  with open('/home/saiikishen/Desktop/bi0s_hardware/imag1.png', 'wb') as f:
      f.write(t)
  ```

![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-18-01-50-33-imag1.png)

- We get this **QR Code** 

- Using `zbarimg imag1.png` we get acess to the **Private Key** 
  
  ![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-18-01-52-42-Screenshot%20from%202023-07-18%2001-52-30.png)

- We got the **Private key, Public Key , Passphrase** 

- And using an online PGP decryption tool we can get the flag (https://8gwifi.org/pgpencdec.jsp)
  
  ![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-18-01-57-56-Screenshot%20from%202023-07-18%2001-57-08.png)
  
  ### FLAG
  
  `flag{eNcryP7!ng_t0_PgP_1s_r34LLy_Pre3tY_g00D_pr1V4cY}`
  
  
