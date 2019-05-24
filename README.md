
# ChameleonMini Rev.G #


![alt text](chameleonmini.jpg "ChameleonMini")<br>



### This is a user friendly documentation for the [ChameleonMini](https://github.com/emsec/ChameleonMini/wiki)  (RevG 180125) from Kasper & Oswald GmbH.<br>
### Feel free to add or adapt the documentation 




<a id="top">

__Table of content__

- [VERSION](#version)
- [CONFIG](#config)
- [UID](#uid)
- [READONLY](#readonly)
- [UPLOAD](#upload)
- [DOWNLOAD](#download)
- [RESET](#reset)
- [UPGRADE](#upgrade)
- [MEMSIZE](#memsize)
- [UIDSIZE](#uidsize)
- [RBUTTON](#rbutton)
- [RBUTTON_LONG](#rbutton_long)
- [LBUTTON](#lbutton)
- [LBUTTON_LONG](#lbutton_long)
- [LEDGREEN](#ledgreen)
- [LEDRED](#ledred)
- [LOGMODE](#logmode)
- [LOGMEM](#logmem)
- [LOGDOWNLOAD](#logdownload)
- [LOGSTORE](#logstore)
- [LOGCLEAR](#logclear)
- [SETTING](#setting)
- [CLEAR](#clear)
- [STORE](#store)
- [RECALL](#store)
- [CHARGING](#charging)
- [HELP](#help)
- [RSSI](#rssi)
- [SYSTICK](#systick)
- [SEND_RAW](#send_raw)
- [SEND](#send)
- [GETUID](#getuid)
- [DUMP_MFU](#dump_mfu)
- [IDENTIFY](#identify)
- [TIMEOUT](#timeout)
- [THRESHOLD](#threshold)
- [AUTOCALIBRATE](#autocalibrate)
- [FIELD](#field)
- [CLONE](#clone)

Annex
----
- [Abbreviation](#abbr)
- [MIFARE Classic command overview](#mfc_commands)
- [MIFARE Classic ACK and NAK](#acknak)
- [ATQA and SAK responses](#atqasak)
- [How to customize the Firmware](#customize)


----





VERSION<a id="version">
----
^[Top](#top)


Print the current version of ChameleonMini.<br>

**Syntax:** `version?`
*101:OK WITH TEXT
ChameleonMini RevG 180125 using LUFA 151115 compiled with AVR-GCC 5.4.0. Based on the open-source NFC tool ChameleonMini. https://github.com/emsec/ChameleonMini commit c6d2968*

CONFIG<a id="config">
----
^[Top](#top)

Get/Set the configuratopn of the current slot. The "slot" includes the behavior of the Card. The ChameleonMini can emulate differend Cards, and each slot contains one Card.
The slot 8 is configured as "READER" in the default configuration.<br>
*Note: The ChameleonMini has 8 possible slots (1-8)*

**Syntax:** `config=?`<br>
*101:OK WITH TEXT
NONE,MF\_ULTRALIGHT,MF\_ULTRALIGHT|_EV1\_80B,MF\_ULTRALIGHT|_EV1\_164B,MF\_CLASSIC\_1K,MF\_CLASSIC\_1K\_7B,MF\_CLASSIC\_4K,MF\_CLASSIC\_4K\_7B,ISO14443A\_SNIFF,ISO14443A\_READER*

Set current slot as a MIFARE classic 4K emulation.<br>
**Syntax:** `config=MF_CLASSIC_4K`<br>
*101:OK WITH TEXT<br>*

Get the value of the current slot<br>
**Syntax:** `config?`<br>
*101:OK WITH TEXT<br>
MF\_CLASSIC\_4K<br>*


UID<a id="uid"></a>
----
^[Top](#top)

Print the current uid of the emulated card(slot).<br>
**Syntax:** `uid?`<br>
*101:OK WITH TEXT<br>
9E63BC03A<br>*


READONLY<a id="readonly"></a>

Configures the read-only mode to the internal memory. Activates (1) or deactivates (0) the read-only mode (***Any writing to the memory is silently ignored.***)<br>

Print the possible states.<br>
**Syntax:** `readonly=?`<br>
*101:OK WITH TEXT<br>
1,0<br>*

Print the current state of the accessrights<br>
**Syntax:** `readonly?`<br>
*101:OK WITH TEXT<br>
0<br>*

Activate the read-only mode<br>
**Syntax:** `readonly=1`<br>
*100:OK<br>*


UPLOAD<a id="upload"></a>
----
^[Top](#top)

Waits for an XModem connection in order to upload a new virtualized card into the currently selected slot, with a size up to the current memory size. 

**Syntax:** `upload`\<ENTER\><br>

DOWNLOAD<a id="download"></a>
----
^[Top](#top)

Waits for an XModem connection in order to download a virtualized card with the current memory size.

**Syntax:** `download`\<ENTER\><br>


RESET<a id="reset"></a>
----
^[Top](#top)

Reboots the Chameleon, i.e., power down and subsequent power-up. Note: A reset usually requires a new Terminal session. 

**Syntax:** `reset`\<ENTER\><br>


UPGRADE<a id="upgrade"></a>
----
^[Top](#top)

Sets the Chameleon into firmware upgrade mode (DFU). This command can be used instead of holding the RBUTTON while power-on to trigger the bootloader.<br>

After run the `upgrade` command, you can now start the upgrade process described on [Getting Started](https://rawgit.com/emsec/ChameleonMini/master/Doc/Doxygen/html/_page__getting_started.html)

**Syntax:** `upgrade`\<ENTER\><br>


MEMSIZE<a id="memsize"></a>
----
^[Top](#top)

Returns the memory size occupied by the current configuration in Byte.

**Syntax:** `memsize?`<br>
*101:OK WITH TEXT<br>
4096<br>*


UIDSIZE<a id="uidsize"></a>
----
^[Top](#top)

Print the size in bytes of the current uid on the emulated card.<br>

**Syntax:** `uidsize?`<br>
*101:OK WITH TEXT<br>
4<br>*


CHARGING<a id="charging"></a>
----
^[Top](#top)

Returns if the battery is currently being charged (TRUE) or not (FALSE).

**Syntax:** `charging?`<br>
*120:FALSE*


HELP<a id="help"></a>
----
^[Top](#top)

Returns a comma-separated list of all commands supported by the current firmware.

**Syntax:** `help`<br>
*101:OK WITH TEXT<br>
VERSION,CONFIG,UID,READONLY,UPL....*


RSSI<a id="rssi"></a>
----
^[Top](#top)

Returns the voltage measured at the antenna of the Chameleon, e.g., to detect the presence of an RF field or compare the field strength of different RFID readers.

**Syntax:** `help`\<ENTER\><br>
*101:OK WITH TEXT<br>
2648 mV*

SYSTICK<a id="systick"></a>
----
^[Top](#top)

Print the value of the left system tick **in ms** since PowerOn.<br>
*Note: An overflow occurs every 65,536 ms.*<br>

**Syntax:** `systick?`<br>
*101:OK WITH TEXT<br>
9C30<br>*

LEDGREEN<a id="ledgreen"></a>
----
^[Top](#top)

Set/Get the behavior of the green LED.

Possible values are:<br>
**Syntax:** `ledgreen=?`<br>
*101:OK WITH TEXT<br>
NONE,POWERED,TERMINAL\_CONN,TERMINAL\_RXTX,SETTING\_CHANGE,MEMORY\_STORED,MEMORY\_CHANGED,CODEC\_RX,CODEC\_TX,FIELD\_DETECTED,LOGMEM\_FULL*

Get current state:<br>
**Syntax:** `ledgreen?`<br>
*101:OK WITH TEXT<br>
POWERED<br>*

Set value for example:<br>
**Syntax:** `ledgreen=terminal_rxtx`\<ENTER\><br>
*100:OK*

LEDRED<a id="ledred"></a>
----
^[Top](#top)

Set/Get the behavior of the red LED.

Possible values are:<br>
**Syntax:** `ledred=?`<br>
*101:OK WITH TEXT<br>
NONE,POWERED,TERMINAL\_CONN,TERMINAL\_RXTX,SETTING\_CHANGE,MEMORY\_STORED,MEMORY\_CHANGED,CODEC\_RX,CODEC\_TX,FIELD\_DETECTED,LOGMEM\_FULL*

Get current state:<br>
**Syntax:** `ledred?`<br>
*101:OK WITH TEXT<br>
FIELD_DETECTED<br>*

Set value for example:<br>
**Syntax:** `ledred=powered`\<ENTER\><br>
*100:OK*


RBUTTON<a id="rbutton"></a>
----
^[Top](#top)

Set/Get the behavior of a right button with "short push".<br>

Possible values are:<br>
**Syntax:** `rbutton=?`<br>
*101:OK WITH TEXT<br>
NONE,UID_RANDOM,UID\_LEFT\_INCREMENT,UID\_RIGHT\_INCREMENT,UID\_LEFT\_DECREMENT,UID\_RIGHT\_DECREMENT,CYCLE\_SETTINGS,STORE\_MEM,RECALL\_MEM,TOGGLE\_FIELD,STORE\_LOG,CLONE*

Get current value:<br>
**Syntax:** `rbutton?`<br>
*101:OK WITH TEXT<br>
CYCLE_SETTINGS<br>*

Set value for example:<br>
**Syntax:** `rbutton=ui_random`


RBUTTON\_LONG<a id="rbutton_long"></a>
----
^[Top](#top)

Set/Get the behavior of a right button with "long push".<br>

Possible values are:<br>
**Syntax:** `rbutton_long=?`<br>
*101:OK WITH TEXT<br>
NONE,UID_RANDOM,UID\_LEFT\_INCREMENT,UID\_RIGHT\_INCREMENT,UID\_LEFT\_DECREMENT,UID\_RIGHT\_DECREMENT,CYCLE\_SETTINGS,STORE\_MEM,RECALL\_MEM,TOGGLE\_FIELD,STORE\_LOG,CLONE*

Get current value:<br>
**Syntax:** `rbuttton_long?`<br>
*101:OK WITH TEXT<br>
CYCLE_SETTINGS<br>*

Set value for example:<br>
**Syntax:** `rbutton_long=uid_random`<br>
*100:OK*

LBUTTON<a id="lbutton"></a>
----
^[Top](#top)

Set/Get the behavior of a left button with "short push".<br>

Possible values are:<br>

**Syntax:** `lbutton_long=?`<br>
*101:OK WITH TEXT<br>
NONE,UID_RANDOM,UID\_LEFT\_INCREMENT,UID\_RIGHT\_INCREMENT,UID\_LEFT\_DECREMENT,UID\_RIGHT\_DECREMENT,CYCLE\_SETTINGS,STORE\_MEM,RECALL\_MEM,TOGGLE\_FIELD,STORE\_LOG,CLONE*

Get current value:<br>
**Syntax:** `lbutton?`<br>
*101:OK WITH TEXT<br>
CYCLE_SETTINGS<br>*

Set value for example:<br>
**Syntax:** `lbutton=uid_random`<br>
*100:OK*

LBUTTON\_LONG<a id="lbutton_long"></a>
----
^[Top](#top)

Set/Get the behavior of a left button with "long push".<br>

Possible values are:<br>
**Syntax:** `lbutton_long=?`<br>
*101:OK WITH TEXT<br>
NONE,UID_RANDOM,UID\_LEFT\_INCREMENT,UID\_RIGHT\_INCREMENT,UID\_LEFT\_DECREMENT,UID\_RIGHT\_DECREMENT,CYCLE\_SETTINGS,STORE\_MEM,RECALL\_MEM,TOGGLE\_FIELD,STORE\_LOG,CLONE*

Get current value:<br>
**Syntax:** `lbuttton_long?`<br>
*101:OK WITH TEXT<br>
CYCLE_SETTINGS<br>*

Set value for example:<br>
**Syntax:** `lbutton_long=ui_random?`<br>
*100:OK*


LOGMODE<a id="logmode"></a>
----
^[Top](#top)

The 'logmode' command set the behavior of the datalogging.<br>
 
Possible values are:<br>
**Syntax:** `logmode=?`<br>
*101:OK WITH TEXT<br>
OFF,MEMORY,LIVE<br>*

- **off** -> logging disabled
- **LIVE** -> log events are written directly to the terminal
- **MEMORY** -> log events are written to SRAM (uC RAM)

Get current value:<br>
**Syntax:** `logmode?`<br>
*101:OK WITH TEXT<br>
LIVE<br>*

Set logging mode:<br>
**Syntax:** `logmode=MEMORY`<br>
*100:OK<br>*

####Log Entry Format####
The log entries use a TLV (Type Length Value)-like format:

- **Entry type** -> 1 byte, see possible types on [GitHub](*https://rawgit.com/emsec/ChameleonMini/master/Doc/Doxygen/html/_log_8h.html#a34112fbd78128ae58dc7801690dfa6e0)
- **Data length** -> 1 byte, the length of the appended data
- **Timestamp** -> 2 bytes, current systick timestamp value (ms) 
- **Data** -> Data length bytes, it's also possible that no data is appended, then the Data length field is zero


LOGMEM<a id="logmem"></a>
----
^[Top](#top)

Returns the remaining free space for logging data to the SRAM (max. 2048 byte).

**Syntax:** `logmem?`<br>
*101:OK WITH TEXT<br>
18430 (from which 16382 non-volatile)*


LOGDOWNLOAD<a id="logdownload"></a>
----
^[Top](#top)

Waits for an XModem connection and then downloads the binary log - including any log data in FRAM. 

**Syntax:** `logdownload`\<ENTER\><br>


LOGSTORE<a id="logstore"></a>
----
^[Top](#top)

Writes the current log from SRAM to FRAM and clears the SRAM log. 

**Syntax:** `logstore?`<br>
*100:OK<br>*

***Warning***<br>
If the FRAM is full, currently no error message is shown.<br>
If calling `LOGMEM?` after executing this command returns any other value than the maximum SRAM log size, there was not sufficient space in the FRAM and nothing has been done. 


LOGCLEAR<a id="logclear"></a>
----
^[Top](#top)

Clears the log memory (SRAM on ATMega and FRAM on external RAM IC5) 

**Syntax:** `logclear`<ENTER\><br>
*100:OK<br>*

SETTING<a id="setting"></a>
----
^[Top](#top)

Get/Set the current slot (slot 1-8) for the card/reader emulation.

Get the current slot number<br>
**Syntax:** `setting?`<br>
*101:OK WITH TEXT<br>
1*

Switch to slot 2<br>
**Syntax:** `setting=2`<br> 
*100:OK*

CLEAR<a id="clear"></a>
----
^[Top](#top)

Clears the content of the current slot.

**Syntax:** `clear`\<ENTER\><br>
*100:OK<br>*

STORE<a id="store"></a>
----
^[Top](#top)

Stores the content of the current slot from the external FRAM into the Flash memory.

**Syntax:** `store`\<ENTER\><br>
*100:OK*


RECALL<a id="recall"></a>
----
^[Top](#top)

Recalls/restores the content of the current slot from the Flash memory into the external FRAM.

**Syntax:** `recall`\<ENTER\><br>
*100:OK*


SEND\_RAW<a id="send_raw"></a>
----
^[Top](#top)

Adds parity bits, sends the given byte string <BYTEVALUE>, and returns the cards answer.

Request type A<br>
**Syntax:** `send 26`\<ENTER\><br>
*101:OK WITH TEXT<br>
0400<br>
0010<br>
PARITY OK*<br>

Select card<br>
**Syntax:** `send 9320'\<enter\><br>
*101:OK WITH TEXT<br>
BA46A1B2EF<br>
0028<br>
PARITY OK<br>*


SEND<a id="send"></a>
----
^[Top](#top)

Does NOT add parity bits, sends the given byte string <BYTEVALUE> and returns the cards answer.

**Syntax:** `send 26`\<ENTER\><br>
*101:OK WITH TEXT<br>
0400<br>
0010<br>
PARITY OK*<br>


GETUID<a id="getuid"></a>
----
^[Top](#top)

Obtains the UID of a card that is in the range of the antenna and returns it. This command is a Timeout command.<br>

**Valid only in 'ISO14443A\_READER' mode**

**Syntax:** `getuid`\<ENTER\><br>
*101:OK WITH TEXT<br>
BA46A1B2*


DUMP\_MFU<a id="dump_mfu"></a>
----
[Top](#top)

Reads the whole content of a Mifare Ultralight card that is in the range of the antenna and returns it. This command is a Timeout command.

**Valid only in 'ISO14443A\_READER' mode**

**Syntax:** `dump_mfu`\<ENTER\><br>
*101:OK WITH TEXT<br>
04A8DEFAE2B54C809B48000000000000<br>
FFFFFFFF000000000000000000000000<br>
00000000000000000000000000000000<br>
00000000000000000000000000000000<br>*


IDENTIFY<a id="identify"></a>
----
^[Top](#top)

Identifies the type of a card in the range of the antenna and returns it. This command is a Timeout command.

**Valid only in 'ISO14443A\_READER' mode** (`config=iso14443a_reader`)

**Syntax:** `identify`\<ENTER\><br>
*101:OK WITH TEXT<br>
MIFARE Classic 1k<br>
ATQA:.0400<br>
UID:.BA46A1B2<br>
SAK: 08<br>*

TIMEOUT<a id="timeout"></a>
----
^[Top](#top)

Get/Set the timeout for the current slot in multiples of 128 ms. If set to zero, there is no timeout. See also Timeout commands. 

Get the possible range<br>
**Syntax:** `timeout=?`<br> 
*101:OK WITH TEXT<br>
0 = no timeout<br>
1-600 = 100 ms - 60000 ms timeout<br>*

Get the current value<br>
**Syntax:** `timeout?`<br> 
*101:OK WITH TEXT<br>
5000 ms<br>*


THRESHOLD<a id="threshold"></a>
----
^[Top](#top)

Get/Set the possible number for the reader threshold.

Get the possible range<br>
**Syntax:** `threshold=?`<br>
*101:OK WITH TEXT<br>
Any integer from 0 to 4095. Reference voltage will be (VCC \* THRESHOLD / 4095) mV*


Set the reader threshold. The *\<NUMBER\>* influences the reader function and range. Setting a wrong value may result in malfunctioning of the reader. **DEFAULT: 400**

**Syntax:** `threshold=300`\<ENTER\><br>
*100:OK*

AUTOCALIBRATE<a id="autocalibrate"></a>
----
^[Top](#top)

Automatically finds a good threshold for communicating with the card that currently is on top of the Chameleon. This command is a Timeout command.

**Valid only in 'ISO14443A\_READER' mode**

**Syntax:** `autocalibrate`\<ENTER\><br>
*101:OK WITH TEXT<br>
 128: -<br>
 136: -<br>
 144: -<br>
 .<br>
 .<br>
 .<br>
1000: +<br>
1008: +<br>
1016: -<br>*


FIELD<a id="field"></a>
----
^[Top](#top)

Get/Set the state of the reader field.

Get the possible values<br>
**Syntax:** `field=?`<br>
*101:OK WITH TEXT<br>
1,0*

Switch the reader field on<br>
**Syntax:** `field=1`<br>
*100:OK*


CLONE<a id="clone"></a>
----
^[Top](#top)

Change `config` and `uid` to the identified card (mifare classic 1k/4k or ultralight).
To check the progress, you can set the mod of the LEDs to *FIELD\_DETECTED* (`ledred=field_detected`) 

(*In fact, it's not a really full clone of a card. It will be clone the Card-ID and switch the ChameleonMini in to the same cardtype as the "master". Nevertheless, this is enough to make penetration tests to low level systems, based only of Card-ID and/or Card-Type.*)


**Syntax:** `clone`\<ENTER\><br>
Hold then the card to be clone on the readers field.

See [ISSUE #165](https://github.com/emsec/ChameleonMini/issues/165)


Annex
----

Abbreviation<a id="abbr"></a>
----

| |Description|
|---|---|
|**PICC**|Proximity Integrated Circuit Card (MIFARE Card)|
|**PCD**|Proximity Coupling Device (Cardreader)|
|**ACK**|ACKnowledge|
|**NAK**|Not AcKnowledge|
|**ATQA**|Answer To reQuest, Type A|
|**NUID**|Non-Unique IDentifier|
|**REQA**|REQuest command, Type A|
|**SAK**|Select AcKnowledge, type A|
|**UID**|Unique IDentifier|
|**WUPA**|Wake-Up Protocol type A|



MIFARE Classic command overview<a id="mfc_commands"></a>
----

[NXP Datasheet 4K](https://www.nxp.com/docs/en/data-sheet/MF1S70YYX_V1.pdf)


|Command|ISO/IEC 14443|Command code (hexadecimal)|
|---|---|---|
|Request|REQA|26h (7 bit)|
|Wake-up|WUPA|52h (7 bit)|
|Anticollision CL1|Anticollision CL1|93h 20h|
|Select CL1|Select CL1|93h 70h|
|Anticollision CL2|Anticollision CL2|95h 20h|
|Select CL2|Select CL2|95h 70h|
|Halt|Halt|50h 00h|
|Authentication with Key A|-|60h|
|Authentication with Key B|-|61h|
|Personalize UID Usage|-|40h|
|SET\_MOD\_TYPE|-|43h|
|MIFARE Read|-|30h|
|MIFARE Write|-|A0h|
|MIFARE Decrement|-|C0h|
|MIFARE Increment|-|C1h|
|MIFARE Restore|-|C2h|
|MIFARE Transfer|-|B0h


MIFARE Classic ACK and NAK<a id="acknak"></a>
----

|Code (4-bit)|Transfer Buffer Validity|Description|
|---|---|---|
|Ah||Acknowledge (ACK)|
|0h|valid|invalid operation|
|1h|valid|parity or CRC error|
|4h|invalid|invalid operation|
|5h|invalid|parity or CRC error|



ATQA and SAK responses<a id="atqasak"></a>
----

**ATQA response of the MF1S70yyX/V1**

|Sales Type|Hex Value|
|---|---|
|MF1S00yX|00 44h|
|MF1S03yX|00 04h|
|MF1S700yX|00 42h|
|MF1S703yX|00 02h|


**SAK response of the MF1S70yyX/V1**

|Sales Type|Hex Value|
|---|---|
|MF1S70yyX/V1|18h|


How to customize the Firmware<a id="customize"></a>
----

The asiest way is to setup a toolchain with UBUNTU (Physical or as VM). This example use UBUNTU as a VirtualBox VM.<br>

1. Download the [UBUNTU Desktop](https://www.ubuntu.com/download/desktop) as ISO (i used the Ubuntu 16.04.3 LTS) and create a VM.

 ![alt text](VBox_UBUNTU.png "VirtualBox UBUNTU VM")

2. Install the [The AVR GCC Toolchain](http://avr-eclipse.sourceforge.net/wiki/index.php/The_AVR_GCC_Toolchain):

    **Syntax:** `sudo apt-get install gcc-avr binutils-avr gdb-avr avr-libc avrdude`\<ENTER\><br>

3. Install [git](https://git-scm.com) ([HowTo](https://www.liquidweb.com/kb/install-git-ubuntu-16-04-lts)\):
    
   **Syntax:** `apt-get update`\<ENTER\><br>
   **Syntax:** `apt-get install git-core`\<ENTER\><br>
   
4. Clone the ChameleonMini repo to local machine.
   
   - create a target directory like '~git' **Syntax:** `mkdir ~/git`\<ENTER\><br>
   - change into the new drectory: **Syntax:** `cd ~/git`\<ENTER\><br>
   - clone the original repository to the current directory:<br>
     **Syntax:** `git clone https://github.com/emsec/ChameleonMini.git`\<ENTER\><br>

5. For remote access to the VM install [ssh](http://ubuntuhandbook.org/index.php/2016/04/enable-ssh-ubuntu-16-04-lts)

   **Syntax:** `sudo apt-get install openssh-server`\<ENTER\><br>
   
6. Edit the ChameleonMini source files:

   After cloning the git repository, you will find the firmwarefiles under `~/git/ChameleonMini/Firmware/Chameleon-Mini`
   
7. Compile the changes

   **Syntax:** `make`\<ENTER\><br>
   `../LUFA/Build/lufa_build.mk:131: The XMEGA device support is currently EXPERIMENTAL (incomplete and/or non-functional), and is included for preview purposes only.`
 `[INFO]    : Begin compilation of project "Chameleon-Mini"...`<br>
` `<br>
`avr-gcc (GCC) 4.9.2`<br>
*`Copyright (C) 2014 Free Software Foundation, Inc.`<br>
`This is free software; see the source for copying conditions.  There is NO`<br>
`warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.`<br>
` `<br>
` [OBJCPY]  : Extracting HEX file data from "Chameleon-Mini.elf"`br>
`avr-objcopy -O ihex -R .eeprom -R .fuse -R .lock -R .signature --set-section-flags=.flashdata="alloc,load" Chameleon-Mini.elf Chameleon-Mini.hex`<br>
` [OBJCPY]  : Extracting EEP file data from "Chameleon-Mini.elf"`<br>
`mavr-objcopy -O ihex -j .eeprom --set-section-flags=.eeprom="alloc,load" --change-section-lma .eeprom=0 --no-change-warnings Chameleon-Mini.elf Chameleon-Mini.eep || exit 0`<br>
` [SIZE]    : Determining size of "Chameleon-Mini.elf"`<br>
` `<br>
`avr-size --mcu=atxmega128a4u --format=avr Chameleon-Mini.elf`<br>
`AVR Memory Usage`<br>
`----------------`<br>
`Device: atxmega128a4u`<br>
` `<br>
`Program:   49218 bytes (35.3% Full)`<br>
`(.text + .data + .bootloader)`<br>
` `<br>
`Data:       5537 bytes (67.6% Full)`<br>
`(.data + .bss + .noinit)`<br>
` `<br>
`EEPROM:      100 bytes (4.9% Full)`<br>
`(.eeprom)`<br>
` `<br>
` `<br>
` [INFO]    : Finished building project "Chameleon-Mini".`*<br>

  Now, you will get the needed two compiled files `Chameleon-Mini.eep` and `Chameleon-Mini.hex`.

8. Upgrade the Firmware

   Start the upgrade process descripted on [Getting Started](https://rawgit.com/emsec/ChameleonMini/master/Doc/Doxygen/html/_page__getting_started.html) with both compiled files `Chameleon-Mini.eep` and `Chameleon-Mini.hex`.   
    
  That's it. Now, you have your own code :-)

   
