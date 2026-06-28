### Solution
- Check the type of file using `file` command. This showed that it is a compressed file.
```
siddhanth@LAPTOP-THRNGN31:/mnt/c/users/Anvitha/OneDrive/Desktop$ file dds1-alpine.flag.img.gz
dds1-alpine.flag.img.gz: gzip compressed data, was "dds1-alpine.flag.img", last modified: Fri Dec 19 18:57:00 2025, from Unix, original size modulo 2^32 134217728
siddhanth@LAPTOP-THRNGN31:/mnt/c/users/Anvitha/OneDrive/Desktop$
```
- Since it is a `.gz` file use `gzip -d ` to unzip it, you will get a disk image file.
```
siddhanth@LAPTOP-THRNGN31:/mnt/c/users/Anvitha/OneDrive/Desktop$ gzip -d dds1-alpine.flag.img.gz
siddhanth@LAPTOP-THRNGN31:/mnt/c/users/Anvitha/OneDrive/Desktop$ exiftool dds1-alpine.flag.img
ExifTool Version Number         : 12.76
File Name                       : dds1-alpine.flag.img
Directory                       : .
File Size                       : 134 MB
File Modification Date/Time     : 2026:06:28 04:09:55+00:00
File Access Date/Time           : 2026:06:28 04:09:56+00:00
File Inode Change Date/Time     : 2026:06:28 04:10:54+00:00
File Permissions                : -rwxrwxrwx
Error                           : Unknown file type
siddhanth@LAPTOP-THRNGN31:/mnt/c/users/Anvitha/OneDrive/Desktop$ srch_strings dds1-alpine.flag.img | grep picoCTF
  SAY picoCTF{f0r3ns1c4t0r_n30phyt3_5e56e786}
siddhanth@LAPTOP-THRNGN31:/mnt/c/users/Anvitha/OneDrive/Desktop$
```
- In the description of the challenge, they told to use `srch_strings` so I used it. It gave too many strings.
- So I piped it to `grep picoCTF`. I got the flag.

### What I Learned
- strings is the standard Unix tool, available everywhere
- srch_strings is picoCTF-specific, basically strings with -a flag baked in (searches the entire file, not just initialized data sections)
