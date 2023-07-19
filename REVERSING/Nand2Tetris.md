# FIRMWARE REVERSING

## Nand2Tetris

### Task Description:

Complete project 1 of Nand2Tetris



### AND

```nand2tetris-hdl
CHIP And {
    IN a, b;
    OUT out;

    PARTS:
    Nand(a=a ,b=b , out=nandOut);
    Not(in=nandOut, out= out);
    
}

```

### OUTPUT

![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-17-21-10-25-Screenshot%20from%202023-06-28%2021-36-22.png)



### OR

```nand2tetris-hdl
CHIP Or {
    IN a, b;
    OUT out;

    PARTS:
    // Put your code here:
    Not(in=a, out=notAOut);
    Not(in=b, out=notBOut);
    Nand(a=notAOut , b= notBOut, out=out);
    
}

```

### OUTPUT

![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-17-21-12-20-Screenshot%20from%202023-06-28%2021-01-09.png)



### NOT

```nand2tetris-hdl
CHIP Not {
    IN in;
    OUT out;

    PARTS:
    // Put your code here:
    Nand(a=in,b=in,out=out);
}
```

### OUTPUT

![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-17-21-13-43-Screenshot%20from%202023-06-28%2019-35-09.png)



### XOR

```nand2tetris-hdl
CHIP Xor {
    IN a, b;
    OUT out;

    PARTS:
    And(a=a, b=b, out=andOut);
    Or(a=a, b=b, out=or1Out);
    Not(in=or1Out, out=not1Out);
    Or(a=andOut, b=not1Out, out=or2Out);
    Not(in=or2Out,out=out);
}
```

### OUTPUT

![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-17-21-14-40-Screenshot%20from%202023-06-28%2021-49-24.png)



### MUX

```nand2tetris-hdl
CHIP Mux {
    IN a, b, sel;
    OUT out;

    PARTS:
    Not(in=sel, out=notSel);
    And(a=a, b=notSel, out=and1Out);
    And(a=b, b=sel, out=and2Out);
    Or(a=and1Out, b=and2Out, out=out);

}
```

### OUTPUT

![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-17-21-15-36-Screenshot%20from%202023-06-28%2022-07-18.png)





### DMUX

```nand2tetris-hdl
CHIP DMux {
    IN in, sel;
    OUT a, b;

    PARTS:
   Not(in=sel, out=notSel);
   And(a=notSel, b=in, out=a);
   And(a=sel, b=in, out=b);
   
}

```

### OUTPUT

![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-17-21-16-47-Screenshot%20from%202023-06-28%2022-22-12.png)





### NOT16

```nand2tetris-hdl

CHIP Not16 {
    IN in[16];
    OUT out[16];

    PARTS:
    Not(in=in[0],out=out[0]);
    Not(in=in[1],out=out[1]);
    Not(in=in[2],out=out[2]);
    Not(in=in[3],out=out[3]);
    Not(in=in[4],out=out[4]);
    Not(in=in[5],out=out[5]);
    Not(in=in[6],out=out[6]);
    Not(in=in[7],out=out[7]);
    Not(in=in[8],out=out[8]);
    Not(in=in[9],out=out[9]);
    Not(in=in[10],out=out[10]);
    Not(in=in[11],out=out[11]);
    Not(in=in[12],out=out[12]);
    Not(in=in[13],out=out[13]);
    Not(in=in[14],out=out[14]);
    Not(in=in[15],out=out[15]);
   
    
}
```

### OUTPUT

![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-17-21-18-03-Screenshot%20from%202023-06-28%2022-32-42.png)





### AND16

```nand2tetris-hdl
CHIP And16 {
    IN a[16], b[16];
    OUT out[16];

    PARTS:
    And(a=a[0], b=b[0], out=out[0]);
    And(a=a[1], b=b[1], out=out[1]);
    And(a=a[2], b=b[2], out=out[2]);
    And(a=a[3], b=b[3], out=out[3]);
    And(a=a[4], b=b[4], out=out[4]);
    And(a=a[5], b=b[5], out=out[5]);
    And(a=a[6], b=b[6], out=out[6]);
    And(a=a[7], b=b[7], out=out[7]);
    And(a=a[8], b=b[8], out=out[8]);
    And(a=a[9], b=b[9], out=out[9]);
    And(a=a[10], b=b[10], out=out[10]);
    And(a=a[11], b=b[11], out=out[11]);
    And(a=a[12], b=b[12], out=out[12]);
    And(a=a[13], b=b[13], out=out[13]);
    And(a=a[14], b=b[14], out=out[14]);
    And(a=a[15], b=b[15], out=out[15]);
}
```

### OUTPUT

![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-17-21-28-03-Screenshot%20from%202023-06-28%2022-43-20.png)



### OR16

```nand2tetris-hdl
CHIP Or16 {
    IN a[16], b[16];
    OUT out[16];

    PARTS:
    // Put your code here:
    Or(a=a[0], b=b[0], out=out[0]);
    Or(a=a[1], b=b[1], out=out[1]);
    Or(a=a[2], b=b[2], out=out[2]);
    Or(a=a[3], b=b[3], out=out[3]);
    Or(a=a[4], b=b[4], out=out[4]);
    Or(a=a[5], b=b[5], out=out[5]);
    Or(a=a[6], b=b[6], out=out[6]);
    Or(a=a[7], b=b[7], out=out[7]);
    Or(a=a[8], b=b[8], out=out[8]);
    Or(a=a[9], b=b[9], out=out[9]);
    Or(a=a[10], b=b[10], out=out[10]);
    Or(a=a[11], b=b[11], out=out[11]);
    Or(a=a[12], b=b[12], out=out[12]);
    Or(a=a[13], b=b[13], out=out[13]);
    Or(a=a[14], b=b[14], out=out[14]);
    Or(a=a[15], b=b[15], out=out[15]);
}
```

### OUTPUT

![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-17-23-02-07-Screenshot%20from%202023-07-01%2015-27-17.png)



### MUX16

```nand2tetris-hdl
 CHIP Mux16 {
    IN a[16], b[16], sel;
    OUT out[16];

    PARTS:
    Mux(a=a[0], b=b[0], sel=sel, out=out[0]);
    Mux(a=a[1], b=b[1], sel=sel, out=out[1]);
    Mux(a=a[2], b=b[2], sel=sel, out=out[2]);
    Mux(a=a[3], b=b[3], sel=sel, out=out[3]);
    Mux(a=a[4], b=b[4], sel=sel, out=out[4]);
    Mux(a=a[5], b=b[5], sel=sel, out=out[5]);
    Mux(a=a[6], b=b[6], sel=sel, out=out[6]);
    Mux(a=a[7], b=b[7], sel=sel, out=out[7]);
    Mux(a=a[8], b=b[8], sel=sel, out=out[8]);
    Mux(a=a[9], b=b[9], sel=sel, out=out[9]);
    Mux(a=a[10], b=b[10], sel=sel, out=out[10]);
    Mux(a=a[11], b=b[11], sel=sel, out=out[11]);
    Mux(a=a[12], b=b[12], sel=sel, out=out[12]);
    Mux(a=a[13], b=b[13], sel=sel, out=out[13]);
    Mux(a=a[14], b=b[14], sel=sel, out=out[14]);
    Mux(a=a[15], b=b[15], sel=sel, out=out[15]);
}

```

### OUTPUT

![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-17-23-05-17-Screenshot%20from%202023-07-01%2015-31-18.png)





### OR8WAY

```nand2tetris-hdl
CHIP Or8Way {
    IN in[8];
    OUT out;

    PARTS:
    Or(a=in[0], b=in[1], out=or1Out);
    Or(a=in[2], b=in[3], out=or2Out);
    Or(a=in[4], b=in[5], out=or3Out);
    Or(a=in[6], b=in[7], out=or4Out);

    Or(a=or1Out, b=or2Out, out=or5Out);
    Or(a=or3Out, b=or4Out, out=or6out);
    Or(a=or5Out, b=or6out, out=out);

}
```

### OUTPUT

![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-17-23-08-54-Screenshot%20from%202023-07-01%2015-52-37.png)



### DMUX4WAY

```nand2tetris-hdl
CHIP DMux4Way {
    IN in, sel[2];
    OUT a, b, c, d;

    PARTS:
    DMux(in=in ,sel=sel[1],a=outDA, b=outDB);
    DMux(in=outDA ,sel=sel[0],a=a, b=b);
    DMux(in=outDB ,sel=sel[0],a=c, b=d);

}
```

### OUTPUT

![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-17-23-11-46-Screenshot%20from%202023-07-01%2016-08-31.png)



### MUX4WAY16

```nand2tetris-hdl
CHIP Mux4Way16 {
    IN a[16], b[16], c[16], d[16], sel[2];
    OUT out[16];

    PARTS:
    Mux16(a=a, b=b, sel=sel[0], out=mux1Out);
    Mux16(a=c, b=d, sel=sel[0], out=mux2Out);
    Mux16(a=mux1Out, b=mux2Out, sel=sel[1], out=out);
}
```

### OUTPUT

![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-17-23-14-05-Screenshot%20from%202023-07-01%2016-31-56.png)



### MUX8WAY16

```nand2tetris-hdl
CHIP Mux8Way16 {
    IN a[16], b[16], c[16], d[16],
       e[16], f[16], g[16], h[16],
       sel[3];
    OUT out[16];

    PARTS:
    Mux4Way16(a=a, b=b, c=c, d=d, sel=sel[0..1], out=mux1Out);
    Mux4Way16(a=e, b=f, c=g, d=h, sel=sel[0..1], out=mux2Out);
    Mux16(a=mux1Out, b=mux2Out, sel=sel[2], out=out);

}
```

### OUTPUT

![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-17-23-19-25-Screenshot%20from%202023-07-01%2016-37-37.png)



### DMUX8WAY

```nand2tetris-hdl
CHIP DMux8Way {
    IN in, sel[3];
    OUT a, b, c, d, e, f, g, h;

    PARTS:
    
    DMux(in=in, sel=sel[2], a=abcd, b=efgh);
    DMux4Way(in=abcd, sel=sel[0..1], a=a, b=b, c=c, d=d);
    DMux4Way(in=efgh, sel=sel[0..1], a=e, b=f, c=g, d=h);
}
```



### OUTPUT

  ![](/home/saiikishen/snap/marktext/9/.config/marktext/images/2023-07-17-23-47-49-Screenshot%20from%202023-07-17%2023-45-35.png)
