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
controlled by the "-8" option.

Do this to see the optiona available:

::

    $ fdump -h


Example
-------

Here's the output when dumping the source code of *fdump* using *fdump*
itself:

::

    $ fdump bin/fdump
    0000  23 21 2f 75 73 72 2f 62 69 6e 2f 65 6e 76 20 70  |#!/usr/bin/env p|  0
    0010  79 74 68 6f 6e 33 0a 0a 22 22 22 46 69 6c 65 20  |ython3.."""File |  16
    0020  68 65 78 64 75 6d 70 20 70 72 6f 67 72 61 6d 2e  |hexdump program.|  32
    0030  0a 0a 75 73 61 67 65 3a 20 66 64 75 6d 70 20 5b  |..usage: fdump [|  48
    0040  2d 68 5d 20 5b 2d 38 5d 20 5b 2d 6f 20 3c 6f 75  |-h] [-8] [-o <ou|  64
    0050  74 66 69 6c 65 3e 5d 20 3c 69 6e 66 69 6c 65 3e  |tfile>] <infile>|  80
    0060  0a 0a 77 68 65 72 65 20 3c 69 6e 66 69 6c 65 3e  |..where <infile>|  96
    0070  20 20 20 69 73 20 74 68 65 20 66 69 6c 65 20 74  |   is the file t|  112
    0080  6f 20 70 72 6f 64 75 63 65 20 74 68 65 20 68 65  |o produce the he|  128
    0090  78 64 75 6d 70 20 6f 66 2c 20 61 6e 64 0a 20 20  |xdump of, and.  |  144
    00A0  20 20 20 20 3c 6f 75 74 66 69 6c 65 3e 20 20 69  |    <outfile>  i|  160
    00B0  73 20 74 68 65 20 6f 75 74 70 75 74 20 66 69 6c  |s the output fil|  176
    00C0  65 20 6f 66 20 66 64 75 6d 70 2c 20 69 66 20 73  |e of fdump, if s|  192
    00D0  75 70 70 6c 69 65 64 2e 0a 0a 49 66 20 74 68 65  |upplied...If the|  208
    00E0  20 22 2d 38 22 20 6f 70 74 69 6f 6e 20 69 73 20  | "-8" option is |  224
    00F0  75 73 65 64 20 74 68 65 6e 20 22 70 72 69 6e 74  |used then "print|  240
    0100  61 62 6c 65 22 20 63 68 61 72 61 63 74 65 72 73  |able" characters|  256
    0110  0a 61 72 65 20 74 68 6f 73 65 20 70 72 69 6e 74  |.are those print|  272
    0120  61 62 6c 65 20 63 68 61 72 61 63 74 65 72 73 20  |able characters |  288
    0130  69 6e 20 74 68 65 20 66 75 6c 6c 20 38 2d 62 69  |in the full 8-bi|  304
    0140  74 20 73 65 74 2c 20 6e 6f 74 0a 6a 75 73 74 20  |t set, not.just |  320
    0150  74 68 65 20 6e 6f 72 6d 61 6c 20 37 2d 62 69 74  |the normal 7-bit|  336
    0160  20 41 53 43 49 49 20 70 72 69 6e 74 61 62 6c 65  | ASCII printable|  352
    0170  73 2e 0a 22 22 22 0a 0a 69 6d 70 6f 72 74 20 73  |s.."""..import s|  368
    0180  79 73 0a 69 6d 70 6f 72 74 20 6d 61 74 68 0a 69  |ys.import math.i|  384
    0190  6d 70 6f 72 74 20 67 65 74 6f 70 74 0a 69 6d 70  |mport getopt.imp|  400
    01A0  6f 72 74 20 73 74 72 69 6e 67 0a 69 6d 70 6f 72  |ort string.impor|  416
    01B0  74 20 6f 73 2e 70 61 74 68 0a 0a 0a 23 20 64 65  |t os.path...# de|  432
    01C0  74 65 72 6d 69 6e 65 73 20 77 68 61 74 20 61 72  |termines what ar|  448
    ... lots of lines snipped
