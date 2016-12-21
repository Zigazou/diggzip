Diggzip
=======

Diggzip is a Bash script that is able to extract gzip files embedded in image
files (like firmware, updates etc.)

Requirements
------------

Diggzip requires the Bash interpreter and the Gnu versions of grep, dd, gzip.

That’s all!

Usage
-----

Diggzip is very simple. It runs by giving it a path to a regular file:

    $ diggzip somefile
    Looking for GZip files in somefile...
    - GZip file at 7639222
      recompressed as diggzip.7639222.gz
    - GZip file at 10395938
      recompressed as diggzip.10395938.gz
    - GZip file at 17543478
      recompressed as diggzip.17543478.gz
    - GZip file at 20110194
      recompressed as diggzip.20110194.gz
    - GZip file at 44374735
      recompressed as diggzip.44374735.gz

If gzip files are found to be in `somefile`, it generates files named on the
pattern `diggzip.<offset>.gz` in the current directory.

How it works
------------

It works similarly to the Photorec utility, it doesn’t need to know the
format of the containing file to find gzip files. It looks for the magic
signature of gzip file and then tries to decompress it.

Produced files are not verbatim of the original embedded files. They are
decompressed and recompressed on the fly because it uses the ability of gzip
to discard extra data at the end of a stream. Therefore the script has only to
find the start of the gzip file, not the end.

