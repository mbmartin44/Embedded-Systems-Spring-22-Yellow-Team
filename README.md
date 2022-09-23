# S22_yellow

This is the repo for YELLOW TEAM, in the spring 2022 offering of ECE 4140.
The descriptions of each milestone are provided below.

## Instructions for Building

Before building the application, make sure the file paths for ESOS_DIR,
CM3_DIR, and GCC_PATH are set as shown below. ESOS_DIR is the
base location of the ESOS32 source tree on your hard disk drive (HDD).
CM3_DIR is the base location of the libOpenCM3 source tree on your HDD.
GCC_PATH is the bin directory of the GCC GNU compiler on your HDD.
Place the following code under the else statement in the section
that says "# ESOS, CM3, and GCC Paths" with your paths:
```bash
  ifeq ($(USER), awesomeeagle)
    ESOS_DIR = /home/awesomeeagle/Documents/GitHub/esos32
    CM3_DIR = /home/awesomeeagle/Documents/libopencm3/libopencm3
    GCC_PATH = /home/awesomeeagle/Documents/gcc-arm-none-eabi-10.3-2021.10/bin
  endif
```

In the m4_app directory (the current directory as this readme.txt file),
enter the following command in the Terminal
to build the application:
```bash
make
```
You should find the .hex file that you can upload onto your NUCLEO-L452RE
in the build directory.

To clear all application files in the build directory, enter the following
command in the Terminal in the m4_app directory:
```bash
make clean
```

# Milestone 4
### Overview 
The m4_app module encodes and decodes text provided via the PuTTY serial
monitor using the Vigenere cipher algorithm on the NUCLEO-L452RE
microcontroller board. The UART is set to 57.6k/8/N/1 parameters.
The Vigenere cipher key is "TENNESSEETECH". The blue button (B1)
on the L452RE is used to toggle between the encipher (B1 unpressed)
and decipher (B1 pressed) settings.

The LED on L452RE (LD2) will blink as the application runs.
The LED blink period in ms will be displayed on the screen if "!!!L"
is entered into the serial terminal (i.e., if the LED period is
1000 ms, then "1000" will appear on the screen).
The user can change the LED blink period by entering
"!!!Snnnn" in which "nnnn" is a 4-digit number representing
the new blink period in ms (i.e. "!!!S1528" will change
the blink period to 1528 ms).

This application utilizes the ESOS32 operating system developed
by Dr. J.W. Bruce for the ECE 4140/5140 Embedded Systems Design
course at Tennessee Technological University.

## m4_app

### Instructions

1. Connect your NUCLEO-L452RE board to your computer and upload the m4_app.hex
onto the NUCLEO-L452RE using the STM32CubeProgrammer application.

2. Enter the following command into your Terminal to open PuTTY:
```bash
putty
```

3. When the PuTTY Configurations page opens, set PuTTY to serial
with a baud rate of 57600 and the serial line to the directory
in which your NUCLEO-L452RE is attached (for Linux, it most
likely is /dev/ttyACM0). Make sure that in Serial page under SSH,
the serial line is configured to 8 data bits, no parity,
1 stop bit, and no parity or flow control. In the Terminal page,
make sure that the Force under Local Echo and Local Line Editing
is Auto or Off; do NOT turn on the force.

4. Once PuTTY has been set to 57.6k/8/N/1, press "Open" on the
PuTTY configurations page. Press the black reset button
on the NUCLEO-L452RE to restart your application.

5. Type in characters into the serial monitor. All
letters will be capitalized before encryption/decryption, and
non-alphabetic letters will not be encrypted/decrypted.
The user can perform one of the four following actions:

a) If the blue button (B1) on L452RE is unpressed, the characters
will be encrypted using the Vigenere cipher
(i.e. "AAAAAAAAAAAAA" -> "TENNESSEETECH").

b) If B1 is pressed, the characters will be decrypted
using the Vigenere cipher
(i.e. "TENNESSEETECH" -> "AAAAAAAAAAAAA").

c) Enter "!!!L" to display the length of the blink period of the
LED (LD2) on the L452RE in milliseconds
(i.e. "!!!L" -> "1000" for 1000 ms).

d) Enter "!!!Snnnn" in which "nnnn" is a 4-digit number between
0001 and 9999 (include the leading zeros) to set the
LD2 blink period to "nnnn" I.e. "!!!S2022" will set
LD2 to blink with a period of 2022 ms at a 50% duty cycle).

## Barrier

1. Connect your NUCLEO-L452RE board to your computer and upload the barrier.hex
onto the NUCLEO-L452RE using the STM32CubeProgrammer application.

2. Enter the following command into your Terminal to open PuTTY:
```bash
putty
```

3. When the PuTTY Configurations page opens, set PuTTY to serial
with a baud rate of 57600 and the serial line to the directory
in which your NUCLEO-L452RE is attached (for Linux, it most
likely is /dev/ttyACM0). Make sure that in Serial page under SSH,
the serial line is configured to 8 data bits, no parity,
1 stop bit, and no parity or flow control. In the Terminal page,
make sure that the Force under Local Echo and Local Line Editing
is Auto or Off; do NOT turn on the force.

4. Once PuTTY has been set to 57.6k/8/N/1, press "Open" on the
PuTTY configurations page. Press the black reset button
on the NUCLEO-L452RE to restart your application.

5. Watch the output of the application as multiple threads
encounter the barrier.

# Milestone 5
## Overview
The app module uses the NUCLEO-L452RE microcontroller board
attached to the EduBase-V2-L452 peripheral target board
to perform various text and LED manipulation functions.
The application uses the PuTTY serial monitor to send to
and receive text from the L452RE, and the UART is set to
57.6k/8/N/1 parameters. This application utilizes the
ESOS32 operating system developed by Dr. J.W. Bruce for
the ECE 4140/5140 Embedded Systems Design
course at Tennessee Technological University.

### Operation Modes:

* No Buttons are Pressed:
All text sent to the L452RE are echoed verbatim back to
the serial monitor if no buttons are pressed on either
the EduBase PTB or the L452RE.

* SW5 and SW4:
SW5 and SW4 encodes and decodes text using the Vigenere
cipher algorithm with the Vigenere cipher key "TENNESSEETECH".
Pressing SW4 on the EduBase-L452 encrypts text,
and pressing SW5 decrypts text.

* SW3:
Pressing SW3 converts all lowercase letters to uppercase.

* SW2:
Pressing SW2 removes any non-alphanumeric characters
(not 'A'-'Z', 'a'-'z', '0'-'9') from the text stream.

* B1 on Nucleo:
The LED on L452RE (LD2/LED4) and the LEDs on the L452RE
(LED0-LED3) will blink as the application runs.
An LED's blink period in ms will be displayed on the screen if "Lx",
in which x is the number of the LED (i.e. 0-4),
is entered into the serial terminal (i.e., if the LED period is
1000 ms, then "1000" will appear on the screen).
The user can change the LED blink period by entering
"Sx,nnn" in which "nnnn" is a 4-digit number representing
the new blink period in ms (i.e. "!!!S1528" will change
the blink period to 1528 ms).

The user can read the keypad by entering "Rhhhh" where
"hhhh" is four hex symbols that correspond to a bit mask
of keys (KEY0-KEY9, KEYA-D, KEY#, and KEY*) that
the user is interested in returning the on/off value of.
For the binary representation of "hhhh",
bits 0 to 9 correspond to keys 0 to 9, respectively.
Bits 10 to 13 correspond to keys A to D, respectively.
Bit 14 corresponds to key # (pound), and
bit 15 corresponds to key * (star).
(Ex. Entering "R4021" means that we want to return a 1
only for the bits that correspond to keys 1, 5, and #
and all other keys will be masked to 0 automatically).

## Instructions

1. Connect your NUCLEO-L452RE board to your computer and upload the m4_app.hex
onto the NUCLEO-L452RE using the STM32CubeProgrammer application.

2. Enter the following command into your Terminal to open PuTTY:
```bash
putty
```

3. When the PuTTY Configurations page opens, set PuTTY to serial
with a baud rate of 57600 and the serial line to the directory
in which your NUCLEO-L452RE is attached (for Linux, it most
likely is /dev/ttyACM0). Make sure that in Serial page under SSH,
the serial line is configured to 8 data bits, no parity,
1 stop bit, and no parity or flow control. In the Terminal page,
make sure that the Force under Local Echo and Local Line Editing
is Auto or Off; do NOT turn on the force.

4. Once PuTTY has been set to 57.6k/8/N/1, press "Open" on the
PuTTY configurations page. Press the black reset button
on the NUCLEO-L452RE to restart your application.

5. Type in characters into the serial monitor.
The user can perform one of the six following actions
by pressing the pushbutton switches on the L452RE
and the EduBase-L452 PTB (there is priority with
smallest integer 0 as highest priority):

a) If no buttons are pressed, the characters are
simply returned.

b) If SW5 is pressed, the characters will be decrypted
using the Vigenere cipher (i.e. "TENNESSEETECH" -> "AAAAAAAAAAAAA").
All characters will be automatically capitalized.

c) If SW4 is pressed, the characters will be encrypted
using the Vigenere cipher (i.e. "AAAAAAAAAAAAA" -> "TENNESSEETECH").
All characters will be automatically capitalized.

d) If SW3 is pressed, all lowercase letters will be
capitalized to uppercase (i.e. "HeLlo WoRlD" -> "HELLO WORLD").

e) If SW2 is pressed, all non-alphanumeric characters
(not 'A'-'Z', 'a'-'z', '0'-'9') will be removed from the text stream
(i.e. "!^@#!Hello)(World@" -> "HelloWorld").

f) If SW1 (B1 on the L452RE) is pressed, then you can
enter one of the following three commands:

Enter "Lx" with "x" being an integer from 0-4
to display the length of the blink period of the
LEDx on the L452RE or EduBase in milliseconds
(i.e. "L3" -> "1000" for 1000 ms on LED3).

Enter "Sx,nnnn" in which "nnnn" is a 4-digit number between
0001 and 9999 (include the leading zeros) to set
LEDx blink period to "nnnn" I.e. "S2,2022" will set
LED2 to blink with a period of 2022 ms at a 50% duty cycle).

Enter "Rhhhh" where "hhhh" is four hex symbols
that correspond to a bit mask of keys
(from Msb to Lsb: KEY*, KEY#, KEYD-A, KEY9-0)
that you are interested in returning the value of
(i.e. "F1A7" will returning a 1 for the bits
corresponding to keys 0, 1, 2, 5, 7, 8, C, D, #, *).
All other keys not included in the bit mask will
be automatically set to 0.

# Milestone 6
### Instructions
### [m6.pdf](https://github.com/mbmartin44/Embedded-Systems-Spring-22-Yellow-Team/files/9633786/m6.pdf)

# Milestone 7
### Instructions
1. Connect your NUCLEO-L452RE board to your computer and upload the m7_test.hex
onto the NUCLEO-L452RE using the STM32CubeProgrammer application.

2. Press the black Reset button on the NUCLEO-L452RE and watch the LCD
print text going through testing the following functions (which
all start with "esos_lcd44780_" which each mode on for 2-4 seconds:

a) clearScreen() - blank screen
b) writeChar() - writes message character by character
c) writeBuffer() - this one has a bug in which alternating characters are printed
in different rows (i.e. in the word "buffer," the "u", second "f", and "r" are seen
in row 0 than in row 1 with the rest of the word's letters). This could be a function issue?
d) setCursorDisplay() and setCursorBlink() - should go through three possibilities
for the cursor: blinking cursor, non-blinking cursor, then no cursor shown
e) setDisplayVisible() - no text should be printed for 2 s, then text will be
shown again afterwards

# Milestone 8
### Instructions
### [m8.pdf](https://github.com/mbmartin44/Embedded-Systems-Spring-22-Yellow-Team/files/9633793/m8.pdf)
