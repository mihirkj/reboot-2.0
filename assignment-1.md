Problem #2 :  play with directory 

1) create a directory without name from command line

For creating a directory without name I thought of naming it with a blank character which does not takes any space. I used a UTF-8 character named "ZERO WIDTH SPACE" (U+200B), for which no name of the directory is displayed in file explorer applications and also in the terminal by using the 'ls' command.

The commands used:

> mkdir -v ​

(used "-v" to see the verbose output of the operation)

2) create a directory with name "-okgoogle"

This task seemed straightforward but the presence of the hyphen before okgoogle caused problems. That hyphen was being regarded as the start of one of the command options for the 'mkdir' command. To tackle this double hyphens (--) can be used which signify the end of the command options and thus the beginning of the arguments. In this case the aurgument is the name of the directory to be created.

> mkdir -v -- -okgoogle



Problem #3 :  create a directory structure

![alt text](https://1.bp.blogspot.com/-x6vLWgVIU7Q/XvjlJyKJsnI/AAAAAAAAU0M/lmH8ddGkm90gXPNwUZCUvwCTN6XfJINZgCLcBGAsYHQ/s320/Screenshot%2B2020-06-29%2Bat%2B12.12.55%2BAM.png)

To create a directory structure like this the mkdir command can be used with curly braces to make muliple directories at the same location. Also, to be able to create it at once the parents tag (-p) is needed to avoid the need to first create directories at one level, and then changing the path to those directories to make directories further down. the final command looks like this:

> mkdir -p A/{B/{G/K/Reboot.txt,H/J/Reboot.txt},C/{I/J/Reboot.txt,J/L/Reboot.txt},D/{F/L/Reboot.txt,E/M/Reboot.txt}}

Further, the tree command can be used to view the directory structure of A in a tree like format for easy visualisation.

> tree A

It shows the following output:

![alt text](https://github.com/mihirkj/reboot-2.0/blob/master/tree%20output?raw=true)
