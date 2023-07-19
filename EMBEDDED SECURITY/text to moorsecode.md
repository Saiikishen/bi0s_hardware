# EMBEDDED SECURITY

## Text to Morse Code

### Challenge Description:

Make a text to Moorse code converter

### Code:

```py
morse_code_mapping = {
    'A': '.-',
    'B': '-...',
    'C': '-.-.',
    'D': '-..',
    'E': '.',
    'F': '..-.',
    'G': '--.',
    'H': '....',
    'I': '..',
    'J': '.---',
    'K': '-.-',
    'L': '.-..',
    'M': '--',
    'N': '-.',
    'O': '---',
    'P': '.--.',
    'Q': '--.-',
    'R': '.-.',
    'S': '...',
    'T': '-',
    'U': '..-',
    'V': '...-',
    'W': '.--',
    'X': '-..-',
    'Y': '-.--',
    'Z': '--..',
    '1': '.----',
    '2': '..---',
    '3': '...--',
    '4': '....-',
    '5': '.....',
    '6': '-....',
    '7': '--...',
    '8': '---..',
    '9': '----.',
    '0': '-----',
    '.': '.-.-.-',
    ',': '--..--',
    '?': '..--..',
    '\'': '· − − − − ·',
    '!': '− · − · − −',
    '/': '− · · − ·',
    '(': '− · − − ·',
    ')': '− · − − · −',
    '&': '· − · · ·',
    ':': '− − − · · ·',
    ';': '− · − · − ·',
    '=': '− · · · −',
    '+': '· − · − ·',
    '-': '− · · · · −',
    '_': '· · − − · −',
    '"': '· − · · − ·',
    '$': '· · · − · · −',
    '@': '· − − · − ·',
}

def to_morse_code(text):
    morse_code = ''
    for char in text:
        if char == ' ':
            morse_code += '  '
        else:
            morse_code += morse_code_mapping[char.upper()] + ' '
    return morse_code
x=input("Enter the text: ")
morse_code = to_morse_code(x)
print(morse_code)
```

### Code Explanation:

- An input is taken and stored in in the variable **x** 

- Then this is passed onto a function **to_morse_code** 

- A string *'morse_code'* is initialised

- A for loop is made and the characters on the input string is compared

- If the input string has spaced then double spaces appended to the string (the standard spacing for morse code is double the spacing of normal text)

- When the for loop comes across a character it converts it to upper case and then compares it with the values in the dictionary **morse_code_mapping** 

- It the appends the appropriate value to the string *morse_code*

- Then the string is returned and printed as output 
