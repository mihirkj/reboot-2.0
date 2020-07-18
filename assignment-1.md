<b>Problem #1 : Block System call : </b>
 <ul>
   <li> block system call for date command </li>
   <li> that means you don't have to uninstall date command but if you run kernel must not accept </li>
   <li> do the same Firefox as well </li>
  </ul>
  <br/>
  
In bash there is a builtin error handling function called command_not_found(). This function can be used to solve this problem. The function body can be defined inside the bashrc file in such a way to do nothing whenever 'date' or 'firefox' command is entered. The following lines need to be added to the bashrc file (the PATH to be entered as per the user's home directory):

```bash
realpath="$PATH"
PATH="/home/mihir"

command_not_found_handle() (
  if [[ "$1" == 'date' ]] || [[ "$1" == 'firefox' ]]
  then
    :
    return 1
  else
    PATH="$realpath" 
    unset command_not_found_handle
    "$@"
  fi
)
```
In the situation when either 'date' or 'firefox' command is encountered ':' will be executed, which does nothing.

![alt  text](https://github.com/mihirkj/reboot-2.0/blob/master/resources/block?raw=true)

Here it can be seen that 'date' and 'firefox' commands don't do anything while others work as usual.

<br/>
<br/>

<b>Problem #2 :  play with directory</b> 

<b>1)</b> create a directory without name from command line

For creating a directory without name I thought of naming it with a blank character which does not takes any space. I used a UTF-8 character named "ZERO WIDTH SPACE" (U+200B), for which no name of the directory is displayed in file explorer applications and also in the terminal by using the 'ls' command.

The commands used:

```bash
mkdir -v ​
```

(used "-v" to see the verbose output of the operation)

TO verify this I created a new directory inside the one without name, changed the path into it and showed the present working directory:

![alt text](https://github.com/mihirkj/reboot-2.0/blob/master/resources/NoNameDir?raw=true)

(Here the directory without name under the reboot directory can be seen.)
<br/>
<br/>

<b>2)</b> create a directory with name "-okgoogle"

This task seemed straightforward but the presence of the hyphen before okgoogle caused problems. That hyphen was being regarded as the start of one of the command options for the 'mkdir' command. To tackle this double hyphens (--) can be used which signify the end of the command options and thus the beginning of the arguments. In this case the aurgument is the name of the directory to be created.

```bash
mkdir -v -- -okgoogle
```
![alt text](https://github.com/mihirkj/reboot-2.0/blob/master/resources/-okgoogle%20dir?raw=true)
<br/>
<br/>

<b>Problem #3 :  create a directory structure</b> (You are only allowed to use a single command and only one time)

![alt text](https://1.bp.blogspot.com/-x6vLWgVIU7Q/XvjlJyKJsnI/AAAAAAAAU0M/lmH8ddGkm90gXPNwUZCUvwCTN6XfJINZgCLcBGAsYHQ/s320/Screenshot%2B2020-06-29%2Bat%2B12.12.55%2BAM.png)

To create a directory structure like this the mkdir command can be used with curly braces to make muliple directories at the same location. Also, to be able to create it at once the parents tag (-p) is needed to avoid the need to first create directories at one level, and then changing the path to those directories to make directories further down. the final command looks like this:

```
mkdir -p A/{B/{G/K/Reboot.txt,H/J/Reboot.txt},C/{I/J/Reboot.txt,J/L/Reboot.txt},D/{F/L/Reboot.txt,E/M/Reboot.txt}}
```

Further, the tree command can be used to view the directory structure of A in a tree like format for easy visualisation.

```
tree A
```

It shows the following output:

![alt text](https://github.com/mihirkj/reboot-2.0/blob/master/resources/tree%20output?raw=true)
<br/>
<br/>

<b>Problem #4 : share files and folders </b>
<ul>
 <li>create two users name jack and Jill  from command line </li>
 <li>create all the data under home directory of each users </li>
 <li>login with jack user and create a file name  jack.txt using vim editor and write "hello jack" </li>
 <li>from jack user also create two directories name jack1 & jack2 </li>
 <li>now login from Jill user and create a file. Jill.txt using vim editor and write "hey jiil" </li>
 <li>from Jill also create two directoires named jill1 & jill2 </li>
</ul>
(swap these files and directories in between users  and to swap don't use root account.)

<br/>
<br/>
It is required to swap the files across these two users without using the root account. To acheive this 'tmp' directory can be used which is accessible by any user and does not requires root password.
Firstly the required files and directories can be generated under the respective accounts and then moved to the '/tmp' directory. From there those files can be copied to the required home directories. 
<br/>

Creation of the user jack: `sudo useradd jack`

Setting password for user jack: `sudo passwd jack`

Logging into the user jack: `su - jack`

To make jack.txt using vim: `vim jack.txt`

After running the above command pressed 'i' to enter Insert mode, wrote 'hello jack', then Esc -> : (semicolon) -> wq -> Enter

Creation of jack1 and jack2 directories: `mkdir jack1 jack2`

Similar steps can be taken to create the user jill and generate the required files.

To move jack.txt, jack1 and jack2 (logged in as jack): `mv jack.txt jack1 jack2 /tmp/`

To move jill.txt, jill1 and jill2 (logged in as jill): `mv jill.txt jill1 jill2 /tmp/`

To move files of jill to jack (logged in as jack):
```
cd /tmp
cp -r jill.txt jill1 jill2 /home/jack
```
To move files of jack to jill (logged in as jill):
```
cd /tmp
cp -r jack.txt jack1 jack2 /home/jill
```
Hence, all the files have been swapped between the users without the use of root account.

![alt text](https://github.com/mihirkj/reboot-2.0/blob/master/resources/swap-1?raw=true)

![alt text](https://github.com/mihirkj/reboot-2.0/blob/master/resources/swap-2?raw=true)

<br/>
<br/>

<b> Problem #5: play with files and directories </b>
<ul>
  <li> create  3 files named   abc.txt  ok  fine  g.txt under /tmp directory </li> 
  <li> create  4  directories   aa aaa aaaa  under  /tmp directory </li>
  <li> give ls command to  list the contents of  /tmp directory </li> 
  <li> make sure it will only list the content (file|directory)  having 2 char in their name. </li>
</ul>
<br/>
First we need to change the present working directory to the /tmp
`cd /tmp`
Creation of files:
`touch abc.txt "ok fine" g.txt`
Creation of directories:
`mkdir aa aaa aaaa`
Listing of files/directories having 2 characters in their name:
`ls -d ??`
('?' is a wilcard for a single charcter in file globbing, and '-d' is used with the ls command to "list directories themselves, not their contents")
<br/>

![alt text](https://github.com/mihirkj/reboot-2.0/blob/master/resources/prob5?raw=true)

<br/>
<br/>
