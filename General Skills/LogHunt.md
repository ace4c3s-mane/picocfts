
Description:

Our server seems to be leaking pieces of a secret flag in its logs. The parts are scattered and sometimes repeated. Can you reconstruct the original flag? Download the [logs](https://challenge-files.picoctf.net/c_amiable_citadel/49cec6157142f24a599f4164d5b63322c2494f801390d6f22eb91b3aa592bc66/server.log) and figure out the full flag from the fragments.


Log File: server.log

```bash
grep { server.log 
```

Results:

```bash
[1990-08-09 10:00:10] INFO FLAGPART: picoCTF{us3_
[1990-08-09 11:04:27] INFO FLAGPART: picoCTF{us3_
[1990-08-09 11:04:29] INFO FLAGPART: picoCTF{us3_
[1990-08-09 11:04:37] INFO FLAGPART: picoCTF{us3_
[1990-08-09 12:19:23] INFO FLAGPART: picoCTF{us3_
[1990-08-09 12:19:29] INFO FLAGPART: picoCTF{us3_
[1990-08-09 12:19:32] INFO FLAGPART: picoCTF{us3_
```

Grepped the 'FLAGPART KEYWORD'

```bash
cat server.log | grep "FLAGPART" > flagsparts.txt
```

Results

```bash
[1990-08-09 10:00:10] INFO FLAGPART: picoCTF{us3_
[1990-08-09 10:02:55] INFO FLAGPART: y0urlinux_
[1990-08-09 10:05:54] INFO FLAGPART: sk1lls_
[1990-08-09 10:05:55] INFO FLAGPART: sk1lls_
[1990-08-09 10:10:54] INFO FLAGPART: cedfa5fb}
[1990-08-09 10:10:58] INFO FLAGPART: cedfa5fb}
[1990-08-09 10:11:06] INFO FLAGPART: cedfa5fb}
[1990-08-09 11:04:27] INFO FLAGPART: picoCTF{us3_
[1990-08-09 11:04:29] INFO FLAGPART: picoCTF{us3_
[1990-08-09 11:04:37] INFO FLAGPART: picoCTF{us3_
[1990-08-09 11:09:16] INFO FLAGPART: y0urlinux_
[1990-08-09 11:09:19] INFO FLAGPART: y0urlinux_
[1990-08-09 11:12:40] INFO FLAGPART: sk1lls_
[1990-08-09 11:12:45] INFO FLAGPART: sk1lls_
[1990-08-09 11:16:58] INFO FLAGPART: cedfa5fb}
[1990-08-09 11:16:59] INFO FLAGPART: cedfa5fb}
[1990-08-09 11:17:00] INFO FLAGPART: cedfa5fb}
[1990-08-09 12:19:23] INFO FLAGPART: picoCTF{us3_
[1990-08-09 12:19:29] INFO FLAGPART: picoCTF{us3_
[1990-08-09 12:19:32] INFO FLAGPART: picoCTF{us3_
[1990-08-09 12:23:43] INFO FLAGPART: y0urlinux_
[1990-08-09 12:23:45] INFO FLAGPART: y0urlinux_
[1990-08-09 12:23:53] INFO FLAGPART: y0urlinux_
[1990-08-09 12:25:32] INFO FLAGPART: sk1lls_
[1990-08-09 12:28:45] INFO FLAGPART: cedfa5fb}
[1990-08-09 12:28:49] INFO FLAGPART: cedfa5fb}
[1990-08-09 12:28:52] INFO FLAGPART: cedfa5fb}                                           
```


Contents  of flagsparts.txt

```bash
[1990-08-09 10:00:10] INFO FLAGPART: picoCTF{us3_
[1990-08-09 10:02:55] INFO FLAGPART: y0urlinux_
[1990-08-09 10:05:54] INFO FLAGPART: sk1lls_
[1990-08-09 10:05:55] INFO FLAGPART: sk1lls_
[1990-08-09 10:10:54] INFO FLAGPART: cedfa5fb}
[1990-08-09 10:10:58] INFO FLAGPART: cedfa5fb}
[1990-08-09 10:11:06] INFO FLAGPART: cedfa5fb}
[1990-08-09 11:04:27] INFO FLAGPART: picoCTF{us3_
[1990-08-09 11:04:29] INFO FLAGPART: picoCTF{us3_
[1990-08-09 11:04:37] INFO FLAGPART: picoCTF{us3_
[1990-08-09 11:09:16] INFO FLAGPART: y0urlinux_
[1990-08-09 11:09:19] INFO FLAGPART: y0urlinux_
[1990-08-09 11:12:40] INFO FLAGPART: sk1lls_
[1990-08-09 11:12:45] INFO FLAGPART: sk1lls_
[1990-08-09 11:16:58] INFO FLAGPART: cedfa5fb}
[1990-08-09 11:16:59] INFO FLAGPART: cedfa5fb}
[1990-08-09 11:17:00] INFO FLAGPART: cedfa5fb}
[1990-08-09 12:19:23] INFO FLAGPART: picoCTF{us3_
[1990-08-09 12:19:29] INFO FLAGPART: picoCTF{us3_
[1990-08-09 12:19:32] INFO FLAGPART: picoCTF{us3_
[1990-08-09 12:23:43] INFO FLAGPART: y0urlinux_
[1990-08-09 12:23:45] INFO FLAGPART: y0urlinux_
[1990-08-09 12:23:53] INFO FLAGPART: y0urlinux_
[1990-08-09 12:25:32] INFO FLAGPART: sk1lls_
[1990-08-09 12:28:45] INFO FLAGPART: cedfa5fb}
[1990-08-09 12:28:49] INFO FLAGPART: cedfa5fb}
[1990-08-09 12:28:52] INFO FLAGPART: cedfa5fb
```

**Separated the fields using awk, using space separator**

```bash
awk -F ' ' '{print $5}' flagsparts.txt | tee flags.txt
```


Results

```bash
picoCTF{us3_
y0urlinux_
sk1lls_
sk1lls_
cedfa5fb}
cedfa5fb}
cedfa5fb}
picoCTF{us3_
picoCTF{us3_
picoCTF{us3_
y0urlinux_
y0urlinux_
sk1lls_
sk1lls_
cedfa5fb}
cedfa5fb}
cedfa5fb}
picoCTF{us3_
picoCTF{us3_
picoCTF{us3_
y0urlinux_
y0urlinux_
y0urlinux_
sk1lls_
cedfa5fb}
cedfa5fb}
cedfa5fb}
```

Duplicate values found, sorted the contents of flags.txt

```bash
sort flags.txt | uniq
```

Results

```bash
cedfa5fb}
picoCTF{us3_
sk1lls_
y0urlinux_
```

Manually concatenated the strings:

```bash
echo "picoCTF{us3_y0urlinux_sk1lls_cedfa5fb}" > answer.txt
```


### Answer

```bash
picoCTF{us3_y0urlinux_sk1lls_cedfa5fb}
```

