fdump
=====

A program to dump file contents in ASCII/HEX format.

Now and then you want to look at the data in a file in the rawest way -
just the HEX bytes.  *fdump* is a python program that dumps to stdout
the data in a file.  Each output line has the HEX offset of the byte at the
beginning of the line, followed by 16 HEX bytes of the file, followed by
the same 16 bytes presented as ASCII characters, followed by the decimal
offset of the byte at the start of the line.

If a file contained the data "The quick brown fox\\n\\tjumps over the lazy dog."
then the output would be:

::

    0000  54 68 65 20 71 75 69 63 6b 20 62 72 6f 77 6e 20  |The quick brown |  0
    0010  66 6f 78 0a 09 6a 75 6d 70 73 20 6f 76 65 72 20  |fox..jumps over |  16
    0020  74 68 65 20 6c 61 7a 79 20 64 6f 67 2e           |the lazy dog.|     32

Note that the non-printable characters in the ASCII part are replaced by the
"." character.  The "|" characters bracketing the ASCII characters show the
limits of the ASCII characters.  The characters considered "unprintable" are
controlled by the "-c" option.

Example
-------

Here's the output when dumping the source code of *fdump* using *fdump*
itself:

::

    $ fdump bin/fdump
    0000  23 21 2f 75 73 72 2f 62 69 6e 2f 65 6e 76 20 70  |#!/usr/bin/env p|  0
    0010  79 74 68 6f 6e 33 0a 0a 22 22 22 46 69 6c 65 20  |ython3.."""File |  16
    0020  68 65 78 64 75 6d 70 20 70 72 6f 67 72 61 6d 2e  |hexdump program.|  32
    0030  22 22 22 0a 0a 69 6d 70 6f 72 74 20 73 79 73 0a  |"""..import sys.|  48
    0040  69 6d 70 6f 72 74 20 67 65 74 6f 70 74 0a 69 6d  |import getopt.im|  64
    0050  70 6f 72 74 20 6f 73 2e 70 61 74 68 0a 0a 0a 48  |port os.path...H|  80
    0060  45 58 4c 45 4e 20 3d 20 34 38 0a 43 48 41 52 4c  |EXLEN = 48.CHARL|  96
    0070  45 4e 20 3d 20 31 36 0a 0a 0a 64 65 66 20 68 65  |EN = 16...def he|  112
    0080  78 64 75 6d 70 28 66 69 6c 65 6e 61 6d 65 29 3a  |xdump(filename):|  128
    0090  0a 20 20 20 20 22 22 22 41 20 66 75 6e 63 74 69  |.    """A functi|  144
    00A0  6f 6e 20 74 68 61 74 20 67 65 6e 65 72 61 74 65  |on that generate|  160
    00B0  73 20 61 20 27 68 65 78 20 64 75 6d 70 27 20 6f  |s a 'hex dump' o|  176
    00C0  66 20 61 20 66 69 6c 65 2e 0a 0a 43 61 6c 6c 69  |f a file...Calli|  192
    00D0  6e 67 20 74 68 69 73 20 66 75 6e 63 74 69 6f 6e  |ng this function|  208
    00E0  20 66 6f 72 20 61 20 66 69 6c 65 20 63 6f 6e 74  | for a file cont|  224
    00F0  61 69 6e 69 6e 67 0a 27 54 68 65 20 71 75 69 63  |aining.'The quic|  240
    0100  6b 20 62 72 6f 77 6e 20 66 6f 78 5c 6e 5c 74 6a  |k brown fox\n\tj|  256
    0110  75 6d 70 73 20 6f 76 65 72 20 74 68 65 20 6c 61  |umps over the la|  272
    0120  7a 79 20 64 6f 67 2e 27 0a 72 65 74 75 72 6e 73  |zy dog.'.returns|  288
    0130  20 61 20 73 74 72 69 6e 67 20 63 6f 6e 74 61 69  | a string contai|  304
    0140  6e 69 6e 67 3a 0a 30 30 30 30 20 20 35 34 20 36  |ning:.0000  54 6|  320
    0150  38 20 36 35 20 32 30 20 37 31 20 37 35 20 36 39  |8 65 20 71 75 69|  336
    0160  20 36 33 20 36 62 20 32 30 20 36 32 20 37 32 20  | 63 6b 20 62 72 |  352
    0170  36 66 20 37 37 20 36 65 20 32 30 20 20 7c 54 68  |6f 77 6e 20  |Th|  368
    0180  65 20 71 75 69 63 6b 20 62 72 6f 77 6e 20 7c 20  |e quick brown | |  384
    0190  20 30 0a 30 30 31 30 20 20 36 36 20 36 66 20 37  | 0.0010  66 6f 7|  400
    01A0  38 20 30 61 20 30 39 20 36 61 20 37 35 20 36 64  |8 0a 09 6a 75 6d|  416
    01B0  20 37 30 20 37 33 20 32 30 20 36 66 20 37 36 20  | 70 73 20 6f 76 |  432
    01C0  36 35 20 37 32 20 32 30 20 20 7c 66 6f 78 2e 2e  |65 72 20  |fox..|  448
    01D0  6a 75 6d 70 73 20 6f 76 65 72 20 7c 20 20 31 36  |jumps over |  16|  464
    01E0  0a 30 30 32 30 20 20 37 34 20 36 38 20 36 35 20  |.0020  74 68 65 |  480
    01F0  32 30 20 36 63 20 36 31 20 37 61 20 37 39 20 32  |20 6c 61 7a 79 2|  496
    0200  30 20 36 34 20 36 66 20 36 37 20 32 65 20 20 20  |0 64 6f 67 2e   |  512
    0210  20 20 20 20 20 20 20 20 7c 74 68 65 20 6c 61 7a  |        |the laz|  528
    0220  79 20 64 6f 67 2e 7c 20 20 20 20 20 33 32 0a 0a  |y dog.|     32..|  544
    ... lots of lines snipped
