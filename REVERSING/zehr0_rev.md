# FIRMWARE REVERSING

## Zehr0_rev

### Challenge description:

 Find the flag from the firmware dump [zehr0_rev]([zehro_rev - Google Drive](https://drive.google.com/file/d/1dO3__bGhWKPLOCe6r2yD8vTuMNjn-jCK/view?usp=drive_link))

### Solution:

The downloaded executable was loaded onto IDA Freeware

```c
 v7 = __readfsqword(0x28u);
  if ( argc == 1 )
  {
    puts("Usage: ./crackme FLAG");
    return 1;
  }
  else if ( strlen(argv[1]) == 21 )
  {
    for ( i = 0; i <= 20; ++i )
      *((_BYTE *)&v6[24] + i) = aSup3rS3cr3tK3y[i] - 34;
    v6[0] = 55;
    v6[1] = 63;
    v6[2] = 47;
    v6[3] = 118;
    v6[4] = 43;
    v6[5] = 98;
    v6[6] = 40;
    v6[7] = 33;
    v6[8] = 52;
    v6[9] = 15;
    v6[10] = 119;
    v6[11] = 98;
    v6[12] = 72;
    v6[13] = 39;
    v6[14] = 117;
    v6[15] = 8;
    v6[16] = 86;
    v6[17] = 106;
    v6[18] = 104;
    v6[19] = 78;
    v6[20] = 104;
    for ( j = 0; j <= 20; ++j )
    {
      if ( (char)(argv[1][j] ^ *((_BYTE *)&v6[24] + j)) != v6[j] )
      {
        puts("Wrong flag");
        return 1;
      }
    }
```

- In this we can see the input (aSupersecretkey) is converted into ascii and *34* is subtracted from it

- And that value is xored with the values stored in the list v[6]

- While using *strings* command on the executable we'll get to know that the super secretkey is **sup3r_s3cr3t_k3y_1337**
  
  ### Solve Script:
  
  ```py
  x="sup3r_s3cr3t_k3y_1337"
  l=[55,63,47,118,43,98,40,33,52,15,119,98,72,39,117,8,86,106,104,78,104]
  j=[]
  for i in range (20):
     k= chr(l[i]^(ord(x[i])-34))
     j.append(k)
  print(j)
  ```

### Flag:

**['f', 'l', 'a', 'g', '{', '_', 'y', '0', 'u', '_', 'f', '0', 'u', 'n', 'd', '_', 'k', 'e', 'y', '_']** 
