# Steganography

#### General Tips

> * Start by determining the file type using the `file [filename]` command.
> * Search for hidden clues within the strings, metadata, or embedded data.
> * If the file appears corrupted, consider fixing its [header bytes](https://en.wikipedia.org/wiki/List\_of\_file\_signatures).

***

#### Image Steganography

1. &#x20;Extracts printable strings from files with `strings [filename]`
   * `strings [filename] | grep -i "flag{"`
2. Attempt file carving with the `foremost [filename]` command, Foremost supports all file types.
3. Use `binwalk [filename]` to check for hidden files.
   * Use `binwalk --dd=".*" [filename]` to recover all hidden files
4. View and modify file metadata using `exiftool [filename]`
   * Add or update metadata tags using `exiftool -Author="John Doe" [filename]`.
5. Check the file signature aka magic header if you see a corrupted file
   * use `hexedit` , `xxd` or online [hexed.it](https://hexed.it/)
   * files may hide other files inside. check for more headers in the hex data and copy from there to extract hidden files.
6. Use [stegsolve](https://github.com/zardus/ctf-tools/blob/master/stegsolve/install) to analyze images in different planes by taking off bits of the image.
   * place the image in the /bin folder and run `java -jar stegsolve.jar`
7. Extract hidden data in JPEG `steghide --extract -sf <filename>`
   * hidden data might be password protected. look for hints or bruteforce it with rockyou.txt
8. Fix blurry images with [**SmartDeblur**](http://smartdeblur.net/)

#### Audio Steganography

1. Use `binwalk` first. something might be embedded in the file.
2. Extract hidden data in audio file `steghide --extract -sf <filename>` works on `.wav` files
3. Use [**Audacity**](https://www.audacityteam.org/) or [**Sonic Visualizer**](https://www.sonicvisualiser.org/). Look at spectrogram and other few Pane.
4. Use [**Deepsound**](https://jpinsoft.net/deepsound/download.aspx) especially when the file size is very large
5. Use [**SilentEye**](https://achorein.github.io/silenteye/).

***

#### Online Steganography Tools

* [**AperiSolve**](https://www.aperisolve.com/) **-** All-in-one tool (zsteg, steghide, outguess, exiftool, binwalk, foremost and strings)
* [**StegOnline**](https://stegonline.georgeom.net/) **-** multiple stego tools
* [**Steghide Online**](https://futureboy.us/stegano/decinput.html) **-** use steghide online
* [**StegTool**](https://stegtool.net/) **-** encode/decode data in LSB and browse plan bits

***
