# This is OTW Bandit Walkthrough

> Mayank Yadav Jan 30, 2022

>Level 0:
>------------------------------------------------------------------


Login via SSH on port 2220 as user bandit0:

```
ssh bandit0@bandit.labs.overthewire.org -p 2220
```


>We can see password for any level at ***/etc/bandit_pass/< user >***

Here we get the password using

```
cat /etc/bandit_pass/bandit0
```
viz _bandit0_


>Level 0 -> 1:
>------------------------------------------------------------------


password for Bandit1 is in readme file in home, so

```
cat ~/readme
```

which gives the password for _bandit1_::_boJ9jbbUNNfktd78OOpsqOltutMc3MY1_

>Level 1 -> 2:
>------------------------------------------------------------------

passowrd for bandit2 is in file _-_, so

```
cat ~/-
```
and the passsword is _bandit2_::_CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9_


>Level 2 -> 3:
>------------------------------------------------------------------

The password is in a file called __spaces in filename__, so we use:

```
cat ./"spaces in this filename"
```
We get the password _bandit3_::_UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK_


>Level 3 -> 4:
>------------------------------------------------------------------

the password for next user is stored in .hidden file in inhere directory in home, 

```
cat ./inhere/.hidden
```

This gave me the password _bandit4_ :: _pIwrPrtPN36QITSp3EQaw936yaFoFgAB_

>Level 4 -> 5
>-----------------------------------------------------------------

The password for next level is stored in the only human readable file in _inhere_ directory in home.

```
cat ./inhere/*
```

This gave us a lot of gibbrish, and the password _bandit5_ :: _koReBOKuIDDepwhWk7jZC0RTdopnAYKh_

>Levl 5 -> 6
>-----------------------------------------------------------------

The file is somwhere in _inhere_ directory, 
properties :
1. 1033 B
2. readable
3. NON EXE

```
find ~/inhere/ -size 1033c
```
The file  ***./maybehere07/.file2*** contains out password _bandit6_ :: _DXjZPULLxYr17uwoI01bNLQbtFemEgo7_

>Level 6 -> 7
>---------------------------------------------------------------

Password for next user is to be found, we dont know the filename, but we know these 3 properties about the file:
1. Size 33B
2. User bandit7
3. Group bandit6

so, i did a `find` for a file having these properties.

```
find / -user bandit7 -size 33c
```

This gave back 2 files, one of them is _/etc/bandit_pass/bandit7_ viz denied to access, the second file we got was _/var/lib/dpkg/info/bandit7.password_

and we get the password _bandit7_::_HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs_

>Level 7 -> 8
>----------------------------------------------------------

The password for next level is stored in a file called _data.txt_ in home of _bandit7_
, the password is next to the word "millionth",
so

```
cat data.txt | grep "millionth"
```

This gave me the password : _bandit8_::_cvX2JJa4CFALtqS87jk27qwqGhBM9plV_

>Level 8 -> 9
>---------------------------------------------------------

the password for next level is in the file _data.txt_ in the home directory, it is the only line viz **NOT** repeating,

So i sorted `data.txt ` in `filter1.txt` and kept the uniques in `filter2.txt`.
then I took the differences

```
sdiff filter1.txt filter2.txt
```
This gave me the line viz not repeating, so the password _bandit9_::_UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR_

>Level 9 -> 10
>---------------------------------------------------------

The password is in _data.txt_ file in home directory and it is preceeded with many _=='s_
so i did
`
strings ~/data.txt | grep "=="
`

This gave the password : _bandit10_ :: _truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk_

>Level 10 -> 11
>---------------------------------------------------------

The password is stored as base64 encoded text in _data.txt_, 
`
cat ~/data.txt | base64 -d
`
This gave us the password  _bandit11_ :: _IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR_

>Level 11 -> 12
>--------------------------------------------------------
The password is Caesar Ciphertext, with key = 13, in _data.txt_ in home directory.
so 
`
cat ~/data.txt
`
So, I used [Dcode_Fr](https://www.dcode.fr/caesar-cipher) for decryption, and got the password _bandit12_::_5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu_

>Level 12 -> 13
>----------------------------------------------------------

goto `/tmp/bandit12`, there cat all the files you can and you'll get the password

_bandit13_ :: _8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL_

>Proper Method:
>Here, we'll do 
>`
>xxd -r ~/data.txt
>`
>1. then we figure out the compresession, 
>2. change the extension accordingly,
>3. and decompress again
>
>we repeat these steps until we get the ASCII Text

>Level 13 -> 14:
>----------------------------------------------------------
There's a SSH PrivateKey in the home folder and we can use that to connect to localhost using SSH.

The Syntax is : `ssh -i <PRIVATE_KEY> <USERNAME>@localhost`
So, I did : `ssh -i ~/sshkey.private bandit14@localhost`

then we'll be logged in as _bandit14_ then we can just `cat /etc/bandit_pass/bandit14`, which gives the password _bandit14_::_4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e_

>Level 14 -> 15
>---------------------------------------------------------

We're supposed to submit password of _bandit14_ to port 30000, 
so
`
nc localhost 30000
`
and submit password of _bandit14_ viz _BfMYroe26WYalil77FoDi9qh59eK5xNr_
then we get the next passsword _bandit15_ :: _BfMYroe26WYalil77FoDi9qh59eK5xNr_

>Level 15 -> 16
>----------------------------------------------------------

We connect to port 30001 on localhost using openssl

`openssl s_client -connect localhost:30001`

then we supply _bandit15_'s password, and get the next password
_bandit16_ :: _cluFn7wTiGryunymYOu4RcffSxQluehd_

>Level 16 -> 17
>---------------------------------------------------------
A server is running on a port from 31000 to 32000, we need to figure out that port and then do the same process as _Level 15 -> 16_,

So, I did a `nmap` scan for the port range:

```
nmap -T4 localhost -p 31000-32000 -sV
```
which gave me:

```
Not shown: 996 closed ports
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo
```

I can see that port `31790` is what we needed, 

connecting to this using `openssl s_client -connect localhost:31790`, we provide the password from previous level and get a RSA Pvt. Key :

```
---BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----
```

Now we can use this key as SSH Private Key for logging in as _bandit17_

Now, to save this private key, goto `/tmp` and create a directory `mkdir lol`,
save this as `key.private`, in `lol ` , 

Now we SSH as _bandit17_ using this private key.

`
ssh -i key.private bandit17@localhost
`
Then we can go to the `/etc/bandit_pass/badit17` to get the password viz
_bandit17_ :: _xLYVMN9WE5zQ5vHacb0sZEVqbrp7nBTn_

>Level 17 -> 18
>------------------------------------------------------------

