# Nice Cat... CTF Challenge Write-Up

This challenge, titled "Nice Cat...", involves interacting with a program through a shell command to uncover a message encoded in a sequence of numbers. The challenge demonstrates how to convert ASCII values to their character counterparts to reveal a hidden flag.

## Challenge Overview

The task is to communicate with a specific program by using the command `$ nc mercury.picoctf.net 22902` in a shell. However, the catch is that the program communicates back not in English, but in a series of ASCII values. The objective is to decode these ASCII values to uncover a hidden message or flag.

<br>

## Tools Utilized

**Netcat (nc)**: A networking utility for reading from and writing to network connections using TCP or UDP.
**awk**: A programming language and utility used for text processing. In this challenge, it's used to convert ASCII values to their character representations.

<br>

## ASCII Decoding

<br>

The initial interaction with the program using `nc` command returned a sequence of ASCII values:

```bash
┌──(kali㉿kali)-[~/picoCTF]
└─$ nc mercury.picoctf.net 22902
```

### Output:

```bash
112
105
99
111
67
84
70
123
103
48
48
100
95
107
49
116
116
121
33
95
110
49
99
51
95
107
49
116
116
121
33
95
100
51
100
102
100
54
100
102
125
10
```

<br>

### Decoding ASCII to Text
To decode the ASCII values to text, an awk script was employed to convert each ASCII value to its corresponding character:

<br>

```bash
┌──(kali㉿kali)-[~/picoCTF]
└─$ nc mercury.picoctf.net 22902 | awk '{for(i=1;i<=NF;i++) printf "%c", $i; print ""}'
```

### Output:
```bash
p
i
c
o
C
T
F
{
g
0
0
d
_
k
1
t
t
y
!
_
n
1
c
3
_
k
1
t
t
y
!
_
d
3
d
f
d
6
d
f
}
```

To properly use the text, I needed to flip the text in some way.

```bash
┌──(kali㉿kali)-[~/picoCTF]
└─$ nc mercury.picoctf.net 22902 | awk '{for(i=1;i<=NF;i++) printf "%c", $i;}'
```

<br>

The loop for(i=1;i<=NF;i++) printf "%c", $i iterates over each field (i.e., each ASCII value) in the input and converts it to the corresponding character without printing a newline after each character.

<br>

The removal of print "" from inside the loop means that awk will not automatically print a newline after processing each field. This will result in all characters being printed horizontally in a continuous line.

<br>


### Output:

```bash
picoCTF{g00d_k1tty!_n1c3_k1tty!_d3dfd6df}
```


<br>

### Uncovered Flags
The final decoded message, which is also the flag for this challenge, is:

<br>

**picoCTF{g00d_k1tty!_n1c3_k1tty!_d3dfd6df}**

<br>

This challenge showcases the importance of understanding basic data encoding schemes such as ASCII and the use of common networking and text processing tools to uncover hidden messages or flags in cybersecurity challenges.
