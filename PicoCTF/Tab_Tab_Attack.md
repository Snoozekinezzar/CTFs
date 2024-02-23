# Tab, Tab, Attack CTF Challenge Write-Up

This write-up explores the "Tab, Tab, Attack" challenge created by Syreal, emphasizing the utility of the tab-completion feature in terminal environments. The challenge involves navigating through a complex directory structure within a .zip file named Addadshashanammu.zip, using tab completion to streamline the process. The ultimate goal is to uncover hidden information or flags within the file's contents.

## Challenge Overview

The essence of "Tab, Tab, Attack" lies in efficiently utilizing the tab-completion feature commonly found in Unix and Linux terminals. This functionality significantly aids in handling lengthy and complicated directory and file names, making it a valuable skill in this challenge. The provided Addadshashanammu.zip file likely contains nested directories or files with intricate names, requiring participants to employ tab completion to navigate and locate the desired information or flags.

<br>

## Commands Utilized

**grep** : A command-line utility for searching plain-text data sets for lines matching a regular expression.

<br>

## Searching for the Flag

### Unzipping the File

<br>

```
┌──(kali㉿kali)-[~/picoCTF]
└─$ unzip Addadshashanammu.zip
```

### Output:
```bash
Archive:  Addadshashanammu.zip
   creating: Addadshashanammu/
   creating: Addadshashanammu/Almurbalarammi/
   creating: Addadshashanammu/Almurbalarammi/Ashalmimilkala/
   creating: Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/
   creating: Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/
   creating: Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/
   creating: Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku/
  inflating: Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku/fang-of-haynekhtnamet
```

<br>

The objective revolves around finding a specific string, presumably a flag formatted as "picoCTF{...}", within the files extracted from Addadshashanammu.zip. Utilizing the Linux command-line utilities `grep`, we delve into the file structure in search of this string.

<br>

### Using grep to Locate "picoCTF"

First, we employ `grep` with recursive searching:

```bash
┌──(kali㉿kali)-[~/picoCTF]
└─$ grep -R "picoCTF" .
```

### Output:
```bash
grep: ./Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku/fang-of-haynekhtnamet: binary file matches
```

<br>

This command searches through all files and directories within the current path, flagging the presence of "picoCTF". It indicates a binary file match but does not display the content directly due to the binary nature of the file.

<br>

Given the binary nature of the file containing the "picoCTF" string, we proceed to extract readable strings from it:

```bash
strings ./Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku/fang-of-haynekhtnamet | grep "picoCTF"
```

### Output:
```bash
*ZAP!* picoCTF{l3v3l_up!_t4k3_4_r35t!_d32e018c}
```

<br>

### Uncovered Flags
The meticulous application of grep and strings unveils the flag hidden within the binary data, showcasing the practical application of these commands in CTF challenges:

<br>
<br>

**Flag: picoCTF{l3v3l_up!_t4k3_4_r35t!_d32e018c}**
