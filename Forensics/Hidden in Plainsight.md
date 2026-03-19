Author: Yahaya Meddy

#### Description

You’re given a seemingly ordinary JPG image. Something is tucked away out of sight inside the file. Your task is to discover the hidden payload and extract the flag.


File. img.jpg

Used exitfool to extract metadata:

```bash
exiftool img.jpg 
```

Results

```bash
ExifTool Version Number         : 13.44
File Name                       : img.jpg
Directory                       : .
File Size                       : 73 kB
File Modification Date/Time     : 2026:03:19 02:48:55-04:00
File Access Date/Time           : 2026:03:19 02:48:55-04:00
File Inode Change Date/Time     : 2026:03:19 02:48:55-04:00
File Permissions                : -rw-rw-r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : None
X Resolution                    : 1
Y Resolution                    : 1
Comment                         : c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9
Image Width                     : 640
Image Height                    : 640
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 640x640
Megapixels                      : 0.410
```


Interesting String: Comment - c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9

This looked like encoded base64 string:

```bash
 echo -n "c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9" | base64 -d
```

Results

```bash
steghide:cEF6endvcmQ= 
```

This gave me a clue to use steghide tool:

```html
steghide` is a tool used in steganography to hide or extract data inside files like images or audio without visibly altering them.
```

The text looked like it was encode in base64:

```bash
echo -n "cEF6endvcmQ=" | base64 -d 
```

Results

```bash
pAzzword 
```

I used steghide tool against the image which asked for a paraphrase which I used as the above: pAzzword

```bash
 steghide extract -sf img.jpg
```

Results

```bash
Enter passphrase: 
wrote extracted data to "flag.txt"
```

```bash
cat flag.txt
```

Answer: picoCTF{h1dd3n_1n_1m4g3_1c55ccd0}