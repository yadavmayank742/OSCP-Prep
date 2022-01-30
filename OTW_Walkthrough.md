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


