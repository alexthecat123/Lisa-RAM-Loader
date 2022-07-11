# Lisa RAM Loader
A program that lets you load code straight into the Lisa's memory over serial.<br><br>

![IMG_6015](https://user-images.githubusercontent.com/16897189/178361366-109347f6-1409-4f3e-89c2-da8d611dfba6.png)



# Introduction

This program was inspired by another one that I wrote that allows you to program F-RAM chips on Lisa expansion cards without having to remove them from the Lisa. If that sounds interesting, you can find it [here](https://github.com/alexthecat123/Lisa-Expansion-ROM-Programmer).

When writing code for the Lisa, it's really annoying to have to type your long programs into service mode or to make floppy disks for loading your programs, so I wrote this little application to make things way easier. It's pretty simple; it just accepts your program over serial, loads it into memory, and jumps to it.

# Using the RAM Loader
To use the serial loader, just write the RAMLoader.dc42 file to a 400K floppy or copy it over to your Floppy Emu. When you boot your Lisa from this floppy, it will ask you to start sending your program over the serial port. Connect a serial cable between your modern computer and the Lisa's serial port B and set your modern computer's terminal software to 57600 baud. Then send your code over as raw binary (no XMODEM or anything fancy like that) and the Lisa should load it into memory starting at address $1000. Of course, you can change this address to anything you want by editing the source code. After receiving the entire program, you'll see a "Jumping to Program..." message and your program will begin execution.

This program uses a timeout to determine when you're done sending your code over to the Lisa; if around a second has passed since the last byte has been received, the computer will assume that you've finished sending your program and will go ahead and jump to it.

Note that the Lisa doesn't eject the floppy after reading the loader program from it; I made this decision because it's a pain to have to reinsert the floppy each time you want to test a new program if you're making changes really often. If you don't like this feature, it should be pretty easy to modify the source code to eject the disk after booting from it.


# Modifications
All of the code can be found in RAMLoader.x68 and was written for the EASy68K assembler, but it can probably be adapted to other assemblers pretty easily. Keep in mind that I'm still a novice when it comes to assembly language, so it's probably kind of sloppy in places, but it certainly gets the job done!

