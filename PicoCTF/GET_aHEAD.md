# GET aHEAD CTF Challenge Write-Up

This challenge, named "GET aHEAD," was presented with a tag focus on understanding HTTP methods and exploring how different methods can reveal hidden information or flags. The goal was to find a flag on a server to get ahead of the competition.

## Challenge Overview

The challenge provided by MADSTACKS involves a server located at `http://mercury.picoctf.net:47967/`. The task is to explore the server and uncover the flag.

<br>

## Commands Utilized

**curl** : A command-line tool used for transferring data with URLs. It supports various protocols, including HTTP, HTTPS, FTP, and more. In this challenge, `curl` was used to make requests to the server.

<br>

### Initial Page Request

The initial step involved making a basic HTTP GET request to the server to understand the structure and content of the webpage.

```bash
┌──(kali㉿kali)-[~/picoCTF]
└─$ curl http://mercury.picoctf.net:47967/
```

<br>

### Output:

```
<!doctype html>
<html>
<head>
    <title>Red</title>
    <link rel="stylesheet" type="text/css" href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css">
        <style>body {background-color: red;}</style>
</head>
        <body>
                <div class="container">
                        <div class="row">
                                <div class="col-md-6">
                                        <div class="panel panel-primary" style="margin-top:50px">
                                                <div class="panel-heading">
                                                        <h3 class="panel-title" style="color:red">Red</h3>
                                                </div>
                                                <div class="panel-body">
                                                        <form action="index.php" method="GET">
                                                                <input type="submit" value="Choose Red"/>
                                                        </form>
                                                </div>
                                        </div>
                                </div>
                                <div class="col-md-6">
                                        <div class="panel panel-primary" style="margin-top:50px">
                                                <div class="panel-heading">
                                                        <h3 class="panel-title" style="color:blue">Blue</h3>
                                                </div>
                                                <div class="panel-body">
                                                        <form action="index.php" method="POST">
                                                                <input type="submit" value="Choose Blue"/>
                                                        </form>
                                                </div>
                                        </div>
                                </div>
                        </div>
                </div>
        </body>
</html>
```

<br>

### Discovering the Flag
As the name of the CTF has the word, *head* in it, I figured out it properly had something to do with the headers.
I then use the curl command with the -I option to fetch the headers of the HTTP response. This method revealed the flag within the headers, showing the importance of exploring not just the body of responses but also the headers for hidden information.

```bash
┌──(kali㉿kali)-[~/picoCTF]
└─$ curl -I http://mercury.picoctf.net:47967/
HTTP/1.1 200 OK
flag: picoCTF{r3j3ct_th3_du4l1ty_cca66bd3}
Content-type: text/html; charset=UTF-8
```

<br>

### Uncovered Flags
The flag was cleverly hidden within the response headers of the HTTP request, showcasing an unconventional method for flag storage.

<br>
<br>

**Flag: picoCTF{r3j3ct_th3_du4l1ty_cca66bd3}**

<br>
<br>
This challenge emphasized the significance of examining all aspects of HTTP requests and responses, demonstrating that sometimes, the information needed to succeed is not in plain sight.
