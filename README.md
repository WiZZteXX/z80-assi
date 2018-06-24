# Z80 Assistent
All-In-One Emulation, Assembling and Programming of Z80 processor code using minipro

## FEATURES
* All-In-One z-80 development program for assembly, emulation, chip programming
* All Programming steps can be accomplished with only one shell command
* Compatible with the MiniPro TL866xx series programmers using controlling software by Valentin Dudouyt (https://github.com/vdudouyt/minipro)
* Interactive chip selection
* Ability to created ROM-Images with user-provided size and code offset
* Automatic size detection upon specified chips
* Globally executable

## PREREQUISITS
* If chip programming is needed, you will need a MiniPro TL866xx Programmer (http://www.autoelectric.cn/en/tl866_main.html)

***The following be installed automatically upon calling *z80-assi[deu/eng] -I***
* Minipro controlling software (https://github.com/vdudouyt/minipro) --> needed for chip programming
* Emulation z80-mon from z80-asm package (http://wwwhomes.uni-bielefeld.de/achim/z80-asm/) --> needed for emulation
* z80asm (https://galera.ii.pw.edu.pl/sml3/PDF/Z80ASM.pdf) --> needed for code assembling


## FILES
* z80-assideu: German version
* z80-assieng: English version

## USAGE
    z80-assi SOURCEFILE [OPTIONS: { -l -c[chip name] -s[Image Size] (-n [Offset) }  { -o[Output Name] }  { -a -e -p }  { -O }  { -h }  { -y }]

## INSTALLATION
To globally install the script, download the appropiate language version and run "bash z80-assideu -I" or "z80-assieng -I".
The script will install itself and the three needed services (z80asm by Bas Wijnen, z80-mon by Brainsoft and minipro by Valentin Dudouyt) to **/usr/local/bin**.     
Afterwards it can be run with ***z80-assi -h*** to get further information. 

## BUGS: 
Tell me, if You find some! ;)

## HOW TO GET STARTED?
Create an empty file using Your favorite editor, name it however You want.       
Just for example purpose, it could be something like this (which... in fact does nothing):

***ORG 	$0000***   

***DI*** ; Disable Interrupts while Startup   

***LD  SP,$FF00***; Intialize stackPointer  

***IM	 2***; Set Interrupt Mode 2  

***MAIN: NOP***           *; write Your code here*

***JP MAIN***

and save it, e.g. as *test.asm*. Open a terminal in the containing directory and type 
```nohighlight
  z80-assi test.asm -e (will only emulate the code, no programmer needed)
```
to emulate the code.
On successful emulation, You can try to program the code. For now, better use the interactive chip selection.
Put a fitting ROM into Your programmer. The easiest way is to youse NVRAMS (e.g. DS1245) or EEPROMS (e.g. W27C512)
```nohighlight 
  z80-assi test.asm -lp (will start the interactive IC selection and program the chip)
```
Once You know the minipro name of Your IC, you could also run (for W27C512)
 ```nohighlight 
  z80-assi test.asm -p -C"W27C512 @DIP28".
```  
If you do not yet own a programmer and want somebody else to program it for You, you can also create an sized image. 
For example the 27C512's have a size of 65536 bytes (=64KB)  So You can run
```nohighlight  
  z80-assi test.asm -s64K
``` 
which will create a local file **bin/test.rom.bin**. The rest is self-explanive, I think. 

### HAVE FUN!
