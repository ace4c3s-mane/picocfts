Author: Prince Niyonshuti N.

#### Description

The SOC team discovered a suspiciously large log file after a recent breach. When they opened it, they found an enormous block of encoded text instead of typical logs. Could there be something hidden within? Your mission is to inspect the resulting file and reveal the real purpose of it. The team is relying on your skills to uncover any concealed information within this unusual log. Download the encoded data here: [Logs Data](https://challenge-files.picoctf.net/c_amiable_citadel/3c1d1fea48e203c9c5d64c32d94aa1f091a6b72b4cebd35a761b09d4f9c0f0d2/logs.txt). Be prepared—the file is large, and examining it thoroughly is crucial


File: Logs.txt

First  I decoded the whole file:

```bash
base64 -d logs.txt > decoded.txt
```

Results

```bash
                                                                                                                                                      w���żi�ɐ�<��"�ý��௛�ɦ�9�e�<ϯ.N�������!
i�RZ��N�m��>��-vP6�X�,)v���Z�x�p��|���[�x�S�u:�b�EQ�ݳ�/_����e9.��H���[E��"���'N.�>��#"J
                                                                                       ��y�T�bo��M|9@�LD!���L��e7�!rb۶-��Zɲ,H>�kr�ibD�·2]PJ��~�1F�1Fm�1f�\�C�������d0▒Lv�J)c��m#߮8c�x<^\�E���#!"%�bmaSOQD�sD��R(!3{ү(�▒�Ke��ᷙ���+��bE���Ra���▒IEND�B`�                                                                                                                                                                                            

```

The Presence of IEND indicates that this is a png file.

So, I renamed the file to decoded.png, whose output was this:

![[decoded.png]]

On the front, there's a long string of text. Used tesseract ocr to extract the text.

```bash
tesseract decoded.png decoded.txt
```

Results

```bash
vbw
7

ge

ry
PNW

7069636F4354467B666F72656E736963735F 616E616C797369735F69735F61 6D617A696E675F35646161346132667D

KS

“
i
         
```

The text was in Hex format, after a lot of research. Which I decoded to get the flag.

```bash
echo "7069636F4354467B666F72656E736963735F616E616C797369735F69735F616D617A696E675F35646161346132667D" | xxd -r -p
```

Flag: picoCTF{forensics_analysis_is_amazing_5daa4a2f} 