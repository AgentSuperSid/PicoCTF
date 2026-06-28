### Solution
- Check the type of file using `file` command. This showed that it is a compressed file.
- Since it is a `.gz` file use `gzip -d ` to unzip it, you will get a disk image file.
- In the description of the challenge, they told to use `srch_strings` so I used it. It gave too many strings.
- So I piped it to `grep picoCTF`. I got the flag.
