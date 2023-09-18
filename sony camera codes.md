# sory dslr codes

#### authors note

If you require controlling multiple cameras, or want to do more complex things.
Have a look at sony remote camera API.
https://developer.sony.com/cameras

This is the same api that the remote app uses for shooting.

The reason why I'm going IR route instead, is that opening the remote camera app resets all of my configuration, and for star photography that is a major pain point :D

#### preface

These codes were obtained by repeatedly sending codes from a custom remote (stm32 and an IR led), and watching what changes on the display.

This list might be incomplete, or might be missing aditional features

Also if any codes require continuous sending they aren't being tested YET.

#### protocol

Sirc protocol is used here.

7bit command and 13bit address. (7 + 5 and 7 + 8 are also possible combinations)
the carry signal is 40 khz, 50% square wave.

While everyone uses a pulse length modulation, my approach is to simply count the pulses.

there's a 42 pulses in a chirp.
there's 4 on chirps and 1 off chirp in start.
there's 1 on chirp and 1 off chirp in 0.
there's 2 on chirps and 1 off chirp in 1.

Each message starts with start chirp (4+1 chirps), this doesn't count towards bit length

Data is LSB first and the entire signal needs to repeat 3 times every 45ms, for the command to be accepted.

#### shooting screens

address used is 0x1e3a

these codes were discovered on sony a6300 while on shooting screen

0x14 - change view
0x29 - nfc symbol blinked (further investigation needed)
0x2d - shutter (in bulb mode opens shutter, sending it 2nd tine closes the shutter)
0x37 - delayed shutter
0x38 - menu??
0x47 - plyas trough images in galery
0x48 - starts video recording
0x4a - zoom in - mildly
0x4b - zoom out - mildly

0x4c - zoom in - fast
0x4d - zoom out - fast

0x65 - shutter (in bulb mode takes picture immediately) - it's similar to 0x2d
0x66 - shutter, but doesn't repeat 

speculation:
0x66 - open shutter
0x65 - close shutter


