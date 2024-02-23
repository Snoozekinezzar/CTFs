# Obedient Cat CTF Challenge Write-Up

This write-up details the steps taken to solve the "Obedient Cat" challenge from picoCTF, which involves basic command-line operations to retrieve a flag from a provided file.

## Challenge Overview

"Obedient Cat" is a beginner-level challenge designed by Syreal to teach participants the fundamentals of file manipulation and command-line interface operations in Unix/Linux environments. The task requires participants to download a file that explicitly contains the flag.

<br>

## Commands Utilized

The challenge was solved using standard Unix/Linux command-line utilities:
- **mkdir**: To create a new directory.
- **cd**: To change the current directory.
- **wget**: To download files from the internet.
- **ls**: To list directory contents.
- **cat**: To display file contents.

<br>

### Setting up the Environment

The initial step was to create a directory for the challenge files and navigate into it:

```bash
┌──(kali㉿kali)-[~]
└─$ mkdir picoCTF

┌──(kali㉿kali)-[~]
└─$ cd picoCTF
```

<br>

### Downloading the Flag File

Using the wget command, the flag file was then downloaded from the provided URL:

```bash
┌──(kali㉿kali)-[~/picoCTF]
└─$ wget https://mercury.picoctf.net/static/fb851c1858cc762bd4eed569013d7f00/flag
```

<br>

### Revealing the Flag
After downloading, the ls command confirmed the presence of the flag file, and cat was used to display its content, revealing the flag:

```bash
┌──(kali㉿kali)-[~/picoCTF]
└─$ cat flag
```

### Output:

```bash
picoCTF{s4n1ty_v3r1f13d_28e8376d}
```
<br>

### Uncovered Flags
The process led directly to the discovery of the flag:

**Flag: picoCTF{s4n1ty_v3r1f13d_28e8376d}**

This challenge underscores the importance of being comfortable with basic file manipulation commands and the Unix/Linux command-line interface, serving as a foundation for more complex cybersecurity and CTF challenges.
