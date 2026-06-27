- Since the name itself was close to **Trivial File Transfer Protocol** I filtered the file with `tftp`.
- First few packets looked like they had something, later on the packets looked same and I didnt feel like anything interesting was there later on.
- While looking at them I found this text in one of them- `VHFRQGURCEBTENZNAQUVQVGJVGU-QHRQVYVTRAPR.PURPXBHGGURCUBGBF`.
- Usually the packets will have some random charecters and then some dot spaces between them. This whole text was together.
- I put this to cyberchef and to my luck the ROT13 converter which I forgot to remove after the previous challenge was still there.
- It automatically converted it to `IUSEDTHEPROGRAMANDHIDITWITH-DUEDILIGENCE.CHECKOUTTHEPHOTOS`. Which was a hint.
- I had found some png files and some program files exchanged in some packets before.
- TO find that packet containing image I did `File -> Export Objects -> TFTP`. THis will show all the transferred files(even images).
- There were 3 `.bmp` image files.
- I downoladed them and opened them to see if they had an image of the flag. They just had photos of some good sceneries.
- So as the hint said, the flag is hidden inside the images.
- Tried using `strings` for each of them and piped it to `grep` pico. But didnt find anything.
- When using `steghide` it was asking for passphrase, so I tried **DUEDILIGENCE**(So they used steghide to hide it).
- Then I tried `steghide extract -sf picture1.bmp -p "DUEDILIGENCE"` (`-sf` means the file you are trying to read and `-p` means passphrase).
- For the third image I got a `flag.txt` file
```
  siddhanth@LAPTOP-THRNGN31:/mnt/c/Users/Anvitha/OneDrive/Desktop$ steghide extract -sf picture3.bmp -p "DUEDILIGENCE"
  wrote extracted data to "flag.txt".
```
- This txt file had the flag `picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}`

### What I learnt
 - Binwalk looks for:
- Files appended or embedded inside another file
- Recognizable file signatures (magic bytes like PK, %PDF, \x89PNG)
- Basically "is there a whole separate file hiding in here"
- Files hidden with `steghide` wont be visible here

- Steghide works differently:
- It doesn't append a file, it scatters the data across pixel bytes of the image
- The hidden data is spread throughout the BMP pixel values as tiny LSB tweaks
- There's no recognizable file signature for binwalk to detect
