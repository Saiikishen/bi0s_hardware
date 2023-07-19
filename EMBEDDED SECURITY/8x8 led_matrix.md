# EMBEDDED SECURITY

## 8x8 LED Matrix

### Task description:

Make an 8x8 programmable led matrix

### CODE:

```cpp
#define ROW1 13
#define ROW2 12
#define ROW3 11
#define ROW4 10
#define ROW5 9
#define ROW6 8
#define ROW7 7
#define ROW8 6

#define COL1 5
#define COL2 4
#define COL3 3
#define COL4 2
#define COL5 A4
#define COL6 A3
#define COL7 A2
#define COL8 A1

const int row[] = {ROW1, ROW2, ROW3, ROW4, ROW5, ROW6, ROW7, ROW8};
const int col[] = {COL1,COL2, COL3, COL4, COL5, COL6, COL7, COL8};

int H[8][8] = {{1,0,0,1,1,0,0,1},
               {1,0,0,1,1,0,0,1},
               {1,0,0,1,1,0,0,1},
               {1,0,0,0,0,0,0,1},
               {1,0,0,0,0,0,0,1},
               {1,0,0,1,1,0,0,1},
               {1,0,0,1,1,0,0,1},
               {1,0,0,1,1,0,0,1}};
int E[8][8] = {{1,0,0,0,0,0,0,1},
               {1,0,0,0,0,0,0,1},
               {1,0,0,1,1,1,1,1},
               {1,0,0,0,0,0,0,1},
               {1,0,0,0,0,0,0,1},
               {1,0,0,1,1,1,1,1},
               {1,0,0,0,0,0,0,1},
               {1,0,0,0,0,0,0,1}};

void setup() {
  Serial.begin(9600);
  for (int i = 2; i <= 13; i++) {
    pinMode(i, OUTPUT);
    digitalWrite(i, LOW);
  }
  pinMode(A1, OUTPUT);
  digitalWrite(A1, LOW);
  pinMode(A2, OUTPUT);
  digitalWrite(A2, LOW);
  pinMode(A3, OUTPUT);
  digitalWrite(A3, LOW);
  pinMode(A4, OUTPUT);
  digitalWrite(A4, LOW);
}

void loop() {
  drawScreen(H);
}

void drawScreen(int letter[8][8]){
  for (int c = 0; c < 8; c++){
    digitalWrite(col[c], HIGH);
    for (int r = 0; r < 8; r++){
      digitalWrite(row[r], HIGH*letter[r][c]);
      delay(1);
    }
    for (int r = 0; r < 8; r++){
      digitalWrite(row[r], HIGH);
      delay(1);
    }
    digitalWrite(col[c], LOW);
  }
}
```

### CODE EXPLANATION:

- **VOID SETUP**    
  
  - Serial.begin(9600) initialises the baud rate to 9600
  
  - All the pins from 2 to 13 and analogue pins A1-A4 are set as output pins
  
  - The initial states of these pins are set to **LOW**

- **VOID LOOP**
  
  - Here we can choose to print H or E 
  
  - It passes the argument to *void drawscreen*

- **VOID DRAWSCREEN**
  
  - Takes the 2D array H or E as an input
  
  - The outter for loops controls the columns **digitalWrite(col[c], HIGH)**  sets the the column c to high
  
  - The 1st inner for loop sets row[r] to high or low based on the value present at letter[r][c] (HIGH*letter[r][c] does this)
  
  - delay(1) introduces a delay of 1ms
  
  - The second for loop iterates over the rows and sets everything to HIGH to turn off previous row
  
  - digitalWrite(col[c], LOW) sets the **c** column to low after displaying the current column.This deactivates the column

### TINKERCAD SETUP

Circuit design 8x8 led matrix | Tinkercad

https://www.tinkercad.com/things/2WxkyZKHli0?sharecode=ADtORvNz9BpKNUmZQxWUOC0Vrk8VJjHJVQlMJzfTZZc


