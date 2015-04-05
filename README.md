=======
# eurorack-with-binaries

This is a mirror repo of the Mutable Instrumetns Eurorack repo, but additionally it contains under the folder BUILD all the latest compiled programs for the modules (including some WAVs).

The reason why I pushed this repo was to provide compiled programs, since Its not super easy to setup all the libraries and binding in some platform (i.e. OSX), because I tried my self. I was quite easy on Ubuntu, so I pushed all this compiled programs for my personal use (and to share them).

=======


# Uploading
(From [flocked](http://mutable-instruments.net/forum/discussion/4344/mac-tutorial-how-to-compile-and-upload-the-firmware-of-mis-eurorack-modules/p1))

There are three ways of uploading a firmware to the modules:

1. Audio input via wav file (very slow, but no programmer is needed and it’s supported by every module, in order to use this method you must already have the "braids_bootloader" into the microcontroller, so a blank *new* microcontroller cannot use this method).
2. FTDI (slower than JTAG, but the programmer isn’t as expensive; 10-15$; Yarns has no FTDI port)
3. JTAG (fast, but the programmer is expensive; 50-60$)

## FTDI

If you want to upload a firmware via FTDI, you will need to get an FTDI programmer. I can recommend FTDI friend (you will need to cut the connection between the two 5v VCC pads and solder the pads for 3v). There are a few additional first steps, before you can compile and upload code via FTDI:

1. Download and install FTDI driver
2. Download Pyserial and unpack the tar.gz
3. Open Terminal and enter:
..* cd /PATHTOPYSERIALFOLDER/
..* sudo python setup.py install
..* Enter: ls /dev/cu.*
4. Copy the returned value that looks similar to: /dev/cu.usbserial-XXXX
8. Open /eurorack/stmlib/makefile.inc
9. Paste the copied value to PGM_SERIAL_PORT

Now you can upload via FTDI:

1. Connect FTDI friend to the 6 FTDI pins on your module (the module needs to be connected to your eurorack busboard for power).
2. Press and hold RESET. Press SYSBOOT simultaneously, then release reset while still holding SYSBOOT.
3. Open Terminal and enter: “cd /PATHTOEURORACKFOLDER/”
4. To upload: “make -f /MODULENAME/makefile upload_combo_serial”
