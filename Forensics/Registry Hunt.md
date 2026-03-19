Author: Prince Niyonshuti N.

#### Description

Hi, intrepid investigator! 📄🔍 You've stumbled upon a peculiar PDF filled with what seems like nothing more than garbled nonsense. But beware! Not everything is as it appears. Amidst the chaos lies a hidden treasure—an elusive flag waiting to be uncovered. Find the PDF file here [Hidden Confidential Document](https://challenge-files.picoctf.net/c_amiable_citadel/a8aa03694837741eed59c479749fc7f5bfd14fa66f4295b83776f16b2003a67d/confidential.pdf) and uncover the flag within the metadata.

Used the ExifTool to extract the Metadata

```bash
exiftool Downloads/confidential.pdf 
```


Results

```bash
ExifTool Version Number         : 13.44
File Name                       : confidential.pdf
Directory                       : Downloads
File Size                       : 183 kB
File Modification Date/Time     : 2026:03:19 02:10:48-04:00
File Access Date/Time           : 2026:03:19 02:10:48-04:00
File Inode Change Date/Time     : 2026:03:19 02:10:48-04:00
File Permissions                : -rw-rw-r--
File Type                       : PDF
File Type Extension             : pdf
MIME Type                       : application/pdf
PDF Version                     : 1.7
Linearized                      : No
Page Count                      : 1
Producer                        : PyPDF2
Author                          : cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9jMjA3MzY2OX0=
```

Text of interest: cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9jMjA3MzY2OX0=

Looked like a base64 encoded string:

```bash
echo -n "cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9jMjA3MzY2OX0=" | base64 -d
```


Results

```bash
picoCTF{puzzl3d_m3tadata_f0und!_c2073669} 
```

Alternative Tool: pdfinfo