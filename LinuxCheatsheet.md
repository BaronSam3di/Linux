# Cheat sheet of Snippets

This is a cheat sheet of lots of useful linux commands. The way I use is to pull it up in my browser and run command F to search for what I am interested in. Enjoy!


### mactroubleshooting 
```
sudo dscacheutil -flushcache && sudo killall -HUP mDNSResponder && sudo ipconfig set en0 DHCP
```

### Useful BASH installs
```sh

MAC
brew install gnu-sed		                # gnu version of sed or MAC
brew install sslscan				# https://github.com/rbsec/sslscan
brew install cfr-decompiler			# Modern decompiler for Java 5 and beyond
brew install lynx				# Text-based web browser	
brew install pyenv 				# from https://opensource.com/article/19/5/python-3-default-mac
brew install semgrep				# Code scanning tool to find vulns
brew tap caffix/amass
brew install amass
brew install ngrok				# creates an internet viewable webserver, like python http.server but more.
brew install mitmproxy
brew install proxychains
brew install ffmpeg
brew install --cask 1password-cli		# 1pasword cli tool
brew install jython				# java python ?? for Burp suite
brew install doctl				# digital ocean cli tool fo spinning up things via the terminal
brew install ripgrep				# rust faster than grep
brew install html2text
```

### Installs Docker on Kali
```sh
sudo  apt update
sudo apt install -y docker.io				# Installs docker 
sudo systemctl enable docker --now			# Boots docker automatically after reboot.
sudo usermod -aG docker $USER				# adds non root user to the docker group
newgrp docker						# persist user reboot to new group applies

```

## Shell Commands

```sh
# Standard input (0) : \<
sort \< /etc/services  # gets the output of /etc/services and sorts it 

# Standard output (1) : \>
ls \> ~/myfile        # sends Standard output (1) new file and overwrites what was there before 
whoami \>\> ~/myfile  # appends Standard output (1) to the existing file

# Standard Error (2)
grep -R root /proc 2>/dev/null         # this sends the Standard Error (2) to the null device ( nowhere)
grep -R root /etc &> ~/myfile         # this sends Standard Error (2) and all to myfile
alias foo='echo hello'              # Set an alias command foo that will echo hello to the terminal , or whatever you want. Set by default in the /etc/profile
 <COMMAND_1> ; <COMMAND_2> ; <COMMAND_3> ; # run sequential commands split with a semi-colon
```

### Commands run together 

```sh
A; B    			# Run A and then B, regardless of success of A
A && B  			# Run B if and only if A succeeded
A || B  			# Run B if and only if A failed
A &     			# Run A in background.

command1 && command2 		# that will run command2 if command1 succeeds.
command1 || command2 		# that will run command2 if command1 fails.
command1 ; command2 		# that will run command1 then command2.
command1 | command2 		# that will run command1 and send the output of command1 to command2.
```

## List all available commands: compgen (Programmable Completion Builtins)
```sh
compgen -c              # will list all the commands you could run.
compgen -a              # will list all the aliases you could run.
compgen -b              # will list all the built-ins you could run.
compgen -k              # will list all the keywords you could run.
compgen -A              # function will list all the functions you could run.
compgen -A              # function -abck will list all the above in one go.
```

## Shell short keys
```sh
!foo                                     # Will run the last command that started with foo
ctl+a                                    # brings your cursor to the beginning of the command line
ctl+e                                    # brings your cursor to the end of the command line
ctl+r <search_string> ctl+r		 # search through your bash history for commands that match a search string. Step through results by repeating ctl+ r	 
ctrl+K 					 # removes all text from the cursor to the end of the line.
Ctrl+R 					 # starts a reverse search, through the bash history, simply type characters that should be unique to the command you want to find in the history.
Ctrl+S 					 # launches a forward search, through the bash history.
Ctrl+G 					 # quits reverse or forward search, through the bash history.
Ctrl+X and then Backspace		 # removes all the text from the cursor to the beginning of the line.
Ctl-l               			 # soft clear of the screen
Ctl-u               			 # wipe cirrent command line 
Ctl-c               			 # interrupt the current process (break)
Ctl-d               			 # exit
```

# Process Inspection (/proc dir)
```
cd /proc/<PROCESS_NUMBER>
cat /proc/<PROCESS_NUMBER/status			# status file shows the running process , its status, the user & group ID for the person running bash, a full list of the groups the user is a member of & the process ID & parent process ID.
cat /proc/<PROCESS_NUMBER/cmdline			# The cmdline file shows the command line used to start the process.
cat /proc/<PROCESS_NUMBER/environ			# The environ file shows the environment variables that are in effect.
cat /proc/<PROCESS_NUMBER/limits 			# The limits file contains information about the limits imposed on the process.

```
## Manageing process
```sh
ps -ef | less  						# this will give us similar information includeing parent process info with the PPID. 
ps -fax | less 						# will give the forrest display of processes. Shows the relations between processes.
ps aux --sort pmem | less 				# sort the view by the pmemory amount. 
```
## Directing data
```
# sign is used for redirecting the output of a program to something other than stdout (standard output, which is the terminal by default).
> 

>>	#  appends to a file or creates the file if it doesn't exist.
> 	#  overwrites the file if it exists or creates it if it doesn't exist.
```

# Useful misc Commands  
```sh
bash -x <SCRIPT_NAME>                                                       # runs a script in debug mode
set -x                                                                      # puts the shell in debug mode
set +x                                                                      # takes the shell it off debug mode
<COMAND> 2>/dev/null                                                        # 2 relates to the stderr output and will redirect it to the null device 
!<CMD_HISTORY_NUMBER>                                                       # this will run a specific command from your history eg: !234

uname -a                                                                    # will list all the key info about the system you are on
dd if=/dev/zero of=<FILE_TO_CREATE> bs=<BLOCK_SIZE> count=<MEGABYTE_SIZE>   # This will create a file of zeros. Useful for testing data transfers and compressions
 
dd if=/dev/urandom of=/root/<RNADOM_DUMMY_KEY_NAME> bs=4096 count=1         # This will create a random key of stuff with this
dd if=/dev/zero of=/dev/null						    # copy nothing to nowhere, to juts get a process running
su                                                                          # The switch user command , without any arguments will ask for the root and then switch you to the root user. 
su -                                                                        # Same as above but wil open a new shell with the root environment variables
w                                                                           # Not a typo, type w to see who is logged in on the system AND what they are going 
chmod u+s <file>                                                            #  set the Set User ID (SUID)
chmod +t <file>                                                             # set the Stickybit on the file
find / -perm /4000                                                          # locate files that have SUID
find / -perm /2000                                                          # locate files that have SGID
find / -perm /1000                                                          # locate files that have Sticky bit

stat <FILENAME>                                                             # returns stats on a file eg: size, device, access and mod times

man hier								    # info on the layout of filesystems

sudo purge                                                                  # Purge inactive memory ( mac only??)
sudo !! 								    # redo last command but as root
<SPACE> <SOME_COMMAND>							    # Command will NOT appear in the history
fc 									    # this will open the last command in an editor for when your command sqrewed up and you dont want to trail through it on the terminal
ssh -L<LOCAL_PORT>:<MACHINE_IP>:<PORT> USER@<MACHINE_IP> -N		    # port forward from a cloud service to access it without exposeing it publicly
watch -c -n 1 kubectl top nodes						    # run a command and watch it every 1 second (-n) and get a colourful UI (-c). eg Can also take float time values

sudo -l									    # after prompting got the current user password, you can see all of the sudo commandsyou may run as another user
ps -aux | grep <USER> | cut -d " " -f 6 | tr '\n' ' '			    # Get a line of all the proccess numbers , so you can send them to kill .

sslscan --verbose --show-sigs <FQDN>				sslscan preferred

ffmpeg -i inputfile.mov -q:v 0 outputFile.mp4				    # Useful cli util for converting video
```
# Useful misc functions

```sh
# makes a dir and then cds into it
mcd () {
    mkdir -p "$1"
    cd "$1"
}
```

```sh
#!/bin/bash

# reads a file and if it has a = , if will copy the line to a new file for use in xsser

input="clean_urls.csv"
SUB='='
while IFS= read -r line
do
  if [[ "$line" =~ .*"$SUB".* ]]; then
  echo "$line" >> varUrls.txt
  else
  echo no
  fi  
done < "$input"
```

```sh
lsmod                                   # list all drivers that are currently loaded
modinfo <NAME_OF_KERNEL_DRIVER>         # Get more info on a driver
strace <BASH_COMMAND>                   # will run a system call trace on and command. This can come in handy when you want to see exactly what happened and exactly what might have gone wrong with a linux command. 
strace -c <BASH_COMMAND>                # This shows the counter view of the strace so you can enumerate the time, calls, errors, syscalls. Great for compareing commands.
man (7) signal                          # will show you the man page for all the different Linux signals
netstat -tulpen                         # list open ports
netstat -vanp tcp                       # check what ports are running what
netstat -anv | grep -i listen		# on macwill show listening ports ( see the PID column below) 		
												PID
tcp4       0      0  127.0.0.1.631          *.*                    LISTEN      131072 131072  93781      0 0x0080 0x00000006
tcp6       0      0  ::1.631                *.*                    LISTEN      131072 131072  93781      0 0x0080 0x00000006
tcp6       0      0  ::1.54151              *.*                    LISTEN      131072 131072    475      0 0x0180 0x00000002


sudo lsof -i tcp -nP                    # for mac list all open tcp ports

```

## Vscode short keys

- `⌘+K+0` - collapse all fucntions to lowest level
- `⌘+K+J` - Expand all fucntions to lowest level

For VSCode on a Mac, to collapse or expand just one function:
- To collapse the current function: Place your cursor within the function you wish to collapse, then press `Command+Option+[`.
- To expand the collapsed function: With your cursor in the function (or on its collapsed header), press `Command+Option+]`.


## 1password cli
```
brew install --cask 1password-cli
op --version
op signin
op item create --title='NAME_OF_ITEM' --category=password --generate-password=20,letters,digits,symbols 		# 1password cli cmd to make a password and add it to your vault 
op item edit NAME_OF_ITEM md5hash=SOME_TEXT_YOU_APPLY									# append a value to an item
```
Create apassword but dont add it to your vault, grep it , cut it and clean the white spaces:
- `op item create --title='IS_THIS_ALIVE' --category=password --generate-password=20,letters,digits,symbols --dry-run | grep password | cut -d":" -f2 | awk '{ gsub(/ /,""); print }'`

## Digital OCena cli tool
```
 doctl compute droplet create --image ubuntu-22-04-x64 --size s-1vcpu-1gb --region nyc1 --ssh-keys 38069069 <NAME_OF_THE_DROPLET>
```
### without netstat 
```sh

cat /proc/net/tcp | grep -v "rem_address" /proc/net/tcp  | awk  '{x=strtonum("0x"substr($3,index($3,":")-2,2)); for (i=5; i>0; i-=2) x = x"."strtonum("0x"substr($3,i,2))}{print x":"strtonum("0x"substr($3,index($3,":")+1,4))}'

```
# automation commands 
```sh
while true; do echo -n "This is a test of while loop";date ; sleep 5; done	# as long as true do something and then sleep for 5 seconds
while read line; do echo "$line" | grep <TERM> ; done < <INPUT_FILE>		# while there is data to read from the INPUT_FILE, echo it and grep for the term
```
# curl 
```sh
curl -I https://test.com					   # just displays the headers, not the source code of the webpage
curl --path-as-is						   # prevent canonicalisation (normalisation) of the url.
curl 'http://WEBSITE.COM' --request-target '/some/odd/exstension/' # alternative to prevent canonicalisation (normalisation) of the url.
curl google.com --trace-ascii -					   # will trace the request in a readble way.
```
#  systemctl - Control the systemd system and service manager

```sh
systemctl <tab> <tab>                   # lists all the commands for systemctl
systemctl list-dependencies             # list the dependencies tree
systemctl daemon-reload                 # will update all the service files 
systemctl start <service_name>          # starts a service
systemctl show <service_name>           # will list the details of a service such as Restart
```

# Groups and Users
```sh
groupadd sales                          # adds the group called sales
useradd -G sales Lisa                   # adds a user called Lisa to the group called sales
chgrp sales /data/account               # sets the ownership of the /data/sales dir to the sales group
setfacl -m  d:g:sales:rx /data/sales    # set file acl -m (modify)  d:g:sales:rx is default setting on all files on the group called sales 
setfacl -m  g:sales:rx /data/sales      # without the d: will take care of the directory itself
getfacl <FILE_NAME>                     # return the access controls for a file
chown linda account                     # changes the ownership of the account folder to linda
chmod g+s <FILE_NAME>                   # applies the sticky bit to the file meaning only the owner can delete the file
chattr +i <FILE_NAME>                   # will make the file immutable and so unchangeable and undeletable
chattr -i <FILE_NAME>                   # will undo the immutable setting of a file.
  
ctl+l will clear the screen
su -                            # su stands for switch user and will switch your user. If you don't supply an a user name and just the dash, it will switch you to the root account and open a login shell.
man -k <SEARCH_TERM>            # will return search results for the term from all man pages 
man -k <SEARCH_TERM> | grep 8   # this will look for root user commands (because of the 8)
apropos <SEARCH_TERM>           # search for the term in all the man pages
```
# ls (listing files)
```sh
ls                      # simple listing 
ls -d                   # just show the directory names , not their contents
ls -l                   # long list 
ls -a                   # shows all files including hidden files
ls -lrt                 # sorts on last modification date
ls -ld /home            # lists the properties of the home directory
ls -li <FILE_NAME>      # we will list the inode numbers in the listing 
```
# Wildcards ( Globbing)
```sh
*               # everything
?               # one signal char
[a-c]           # range from a to c
ls [a-c]*       # list all files that start with an a, b or c
ls ?[z-s]*      # list files where the second char is anything from z up to s. 
ls *?[a-z]      # any files which end in a lower case letter  
ls a?s*         # return files that start with a; have any letter; then an s; and then any amount of any letter.
ls a[lm]        # return files that have an l or m on the second position
```
# cp (Copy)
```sh
cp <FILE> <DESTINATION>
cp /etc/hosts .
cp -R /
/my 
``` 
# Directory cmds
```sh
cd -                        # goes back to the previous directory
mkdir -p files/morefiles    # -p for parents. This will make the files directory with the morefiles directory within if they don't exist already
cp <FILE_NAME>  ..          # .. means one level up , so this will copy the file to the above directory 
cp ../../<FILE_NAME>        # will copy it two directories up
cp ../<FILE_NAME> .         # this will go up one level, look for the file and copy it to the current directory
tmp_dir=$(mktemp -d -t ci-XXXXXXXXXX)  # make a temp directory. running mcd ( alias) before this will mv into the dir.
```
# find -- find things ( Really good Man page)
```sh
find / -name "hosts"                                                    # find <SEARCH_DIR> -name <SEARCH_NAME >
mkdir /root/amy; find / -user amy -exec cp {} /root/amy \;              # make a dir and copy all these files into it
find / -size +100M                                                      # look for files greater than 100 megabytes

find / -type f -size 100M                                               # find files only that are greater than 100 megabytes
find /etc -exec grep -l Bob {} \; -exec cp {} root/Bob/ \; 2>/dev/null  # find files from the etc dir that contain Bob and return the file names and then copy them to a dir /root/Bob. Any errors are sent to the null device
find /etc -name '*' -type f | xargs grep "foo"                          # look for files only, with any name and within those search for the string "foo". 
find <LOCATION> -type f \( -iname "*.json" \) -exec grep -il <TERM> {} \; > filesOfInterest.txt 2>&1 # find in location files that have .json in them and execute grep on them to search for the term; and then send there name to a file , and errors elsewhere
find / -type d -name "foo"                                              # find a directory with the name foo
find / -type f -print | xargs grep "foo" 2>/dev/null			# find files and print the lines where foo occurs, send errors to dev/null
find /Location/of/Files -mtime +100 -type f -delete			# Delete files over 100 days old
```
# tar (tape archiver) 

```tar``` was created a long time ago to stream files to a back-up tape. The basic use is to put files together in one archive; with the option to compress the data. Compression can be added with either ```-z``` (gzip) to ```-j``` (bzip2) as the compression utility.
Basic usage to archive ..

```sh
tar -cvf <NAME_OF_CONTENTS> <CONTENTS_TO_BACKUP>    # (create , verbose , file to create , contents TO THE CURRENT DIRECTORY)
tar -cvf <NAME_OF_CONTENTS> -C <NAME_TO_BACKUP_TO>  # (create , verbose , file to create , Location to store) and then to extract
tar -xvf <NAME_OF_CONTENTS>                         # (extract , verbose , file to extract TO THE CURRENT DIRECTORY)
tar -tvf <NAME_OF_CONTENTS> <NAME_TO_BACKUP_TO>     # (inspect contents only, verbose , file)
tar -tzvf <NAME_OF_CONTENTS> <NAME_TO_BACKUP_TO>    # This will compress the archive down with gzip. FYI - There is marginal saving between the two compression types.
```
## zip
```sh
zip -er FILENAME.zip FILE_TO_BE_ZIPPED
```

## Shell escapeing 
```
sudo -u victim find /etc -name passwd -exec bash \;		# use find to look for an obvious result and then execute bash

sudo -u victim vim 						# 1st - Open vim as the the privledged user
:!/bin/bash							# 2nd - In the vim terminal type the command to get a shell open as the user

sudo -u victim less /etc/passwd					# 1st - open an arbitry file with less
At the less search icontype:  !/bin/bash			# 2nd - This will open a shell !!
```
## Running Languages
```
/usr/bin/ruby -e 'require "irb" ; IRB.start(__FILE__)'		# ruby - run commands by putting them in backticks eg; `uname -a`

perl -e 'print `cat /home/victim/key.txt`'			# notice to use single (hard) quotes around the back ticks for yuor cmd so they aget run at the right times.

```
### Running python from the url/address bar

`http://ptl-665534be-b624e42e.libcurl.st/hello/hacker%22%2bstr(%20__import__('os').popen('uname%20-a').read())%2b%22`
Notice the `__import__('os').popen('uname%20-a').read()` . We have added either sied an URL encoded '+' sigh as `%2b`.


# Text editing on Linux

## VI(m) - 

There a few working modes in VI. VIM is VI(improved)
- Command mode - Esc will always bring you back to command mode
- Insert mode - esc , i
- Visual mode - esc, v
When you start, you will get command mode.
To set line numbers in vi, type

### Simple VI commands(all you need) 
- :q! - get out without saving 
- u - undo
- dd - delete a line 
- o - open a new line
- visual mode
- esc, v - go into visual mode. Then use the arrow to select the blocks of text you want
- d - cut the text in the block
- p - paste the text in the block
- y - (yank) is to copy the text in your block 

- 0	move to beginning of the current line
- $	move to end of line
- H	move to the top of the current window (high)
- M	move to the middle of the current window (middle)
- L	move to the bottom line of the current window (low)
- 1G	move to the first line of the file
- 20G	move to the 20th line of the file
- G	move to the last line of the file

### search and replace
- / - will bring up the searcher in the bottom left
- gg - bring you to the top
- :%s/foo/bar/ - substitute the first foo and replace it with bar
- :%s/foo/bar/g - globally substitute all foo and replace them with bar

```vimtutor``` in the terminal will open the vimtutor, a very fast and useful resource to learn how to use vi. 

# extra VI commands
```
Escape Mode:
^ 			# to move the cursor to the start of the current line. 
$ 			# to move the cursor to the end of the current line.
%s />\r/g		# Globally (g) substitute (%s) all greater than signs (>) with carrige returns (r) 
```

### More or Less
```more``` was the original file pager so ```less``` was developed (a play on less is more).More was a developed a bit more but you can still do more with ```less```.

Less is based on VI so many keys work in there, such as search. 
- g - go to the top of the file
- G - go to the bottom of the file
- q - quit and go back to the terminal
- / - search the file
    - n - go to the next search result

### head (look from the top) and tail (look from the bottom)
```sh
head /etc/passwd                        # see the first 10 (default) lines 
head -n 5 /etc/passwd                   # see the first 5 lines 
head -n 5 /etc/passwd | tail -n 1       # get the first 5 lines and then show the last line of that
tail -f /var/log/messages               # tail with the fraction option which will keep the file open and show updates, eg failed logins
```

### cat (concatenate) and tac (reads from bottom to top )
```sh
cat -A      # shows all non-printable chars ( eg $ equals 'Enter pressed')
cat -b      # numbers lines 
cat -n      # numbers lines, but not empty lines
cat -s      # suppressed repeated empty lines
```
### Common text processing utils
```sh
cut -d : -f 1 /etc/passwd                           # cut -d <DELIMITER> -f <FIELD> <FILE_TO_INSPECT> -- will return the filtered output
cut -d : -f 1 /etc/passwd | sort                    # as above with the sort alphabetically 
cut -d : -f 1 /etc/passwd | tr [:lower:] [:upper:]  # as before but will translate to UPPER CASE !
sed -n 5p /etc/passwd                               # prints line 5 of /etc/passwd
sed -i s/foo/bar/g <FILE>                           # Immediately(-i) globally(g) substitute(s) bar for foo in the file 
sed -i -e '2d' <FILE>                               # Immediately(-i) edit(-e) the file by deleting the 2nd line ('2d') 
gsed -i '/foo/ a bar' <FILE>                        # where you read foo, append bar to a new line underneath
awk -F : '{print \$4 }' /etc/passwd                 # print the 4th column from a /etc/passwd
awk -F : '{print \$4 }' /etc/passwd | sort -n       # as above including a numerical sort
awk -F : ' /foo/ {print \$4 }' <FILE>               # print the value at 4th column from a the line that contains foo 
```

## grep (get regular expression)
```sh
grep -i <TERM> <FILE>                       # search for term on a file and be insensitive to case
cat <FILE> | grep <TERM> | grep -v foo      # search for term and exclude any reference to foo
grep -R <TERM> <LOCATION>                   # do a recursive search for the tem in the directory
grep -R <TERM> <LOCATION> -l                # do a recursive search for the tem in the directory
grep -R foo / -l 2>/dev/null                # recursive list from root of all the files that contain foo  
grep -A3 <TERM> <LOCATION>                  # search for the term and also return 3 lines AFTER the result
grep -B5 <TERM> <LOCATION>                  # search for the term and also return 5 lines BEFORE the result 
grep '^...$'  * 2>/dev/null                 # get all lines from all files that contain exactly 3 chars
grep '\<foo\>' <FILE>                       # return entire lines that contain a particular string eg; foo  
grep '^abc' <FILE>                          # lines that START with 'abc' 
grep 'abc$' <FILE>                          # lines that END with 'abc' 
grep 'a.c' <FILE>                           # lines that contain "a" ANYTHING "C"  
man -k user | egrep '1|8'                   # to use the logical OR in the expression we need to use extended grep
egrep 'ab{2}c' <FILE>                       # look for expression that have an a , 2 bs and then a c at the end. 
egrep '*[bB]*' <FILE>                       # look for expressions that have any kind of b in the middle 
egrep '(123){2}' <FILE>                     # look for occurrences of 123 that happen twice in a row ( repetition operator {})
egrep 'ab+c' <FILE>                         # look for expressions that have b ONE or more times
egrep 'ab*c' <FILE>                         # look for expressions that have b ZERO or more times

```

## Piping
A pipe ```|``` is used to send the output of one command to be used as unput for the next command.
- ps aux | grep http

The tee command combines redirection and piping; It allows you to write output to somewhere, and at the same time, use it as input for another command.
- ps aux | tee \<FILE_NAME\> | grep ssh 


## ssh (secure shell) 
```sh
ssh-keygen                                      # running this will start the process of creating a pair of RSA keys. You can set a passphrase on these keys which is more secure and recommended
ssh-copy-id <SERVER_IP_ADDRESS>                 # This is a simple way to copy ver your public key. You will be asked to authenticate to the Server just once.
```

### scp (OpenSSH secure file copy)
```
scp <FILE> <SERVER_IP_ADDRESS>:/<FOLDERNAME>    # copy a LOCAL file to the address and file name on the REMOTE server
scp <SERVER_IP_ADDRESS>:/<FOLDERNAME> <FILE>    # copy a REMOTE file to the address and file name on the LOCAL server
```
### ssh tunnel on Mac 
[see this](https://www.hostdime.com/kb/hd/security/browsing-the-internet-through-an-ssh-tunnel-on-macos)

Until you configure your mac and browser , your connection will not be secure.
```
ssh -f -N -M -S /tmp/sshtunnel -D 1080 USER@server.domain.com -p22 -vvv

where:
-f 	# Run in the background
-N 	# This tells the SSH process to not execute any commands on the remote server (we are only forwarding traffic through the remote server).
-M: 	# Put the SSH client into master mode, so we can easily enter a command later to gracefully end the SSH tunnel without having to kill the connection.
-S:	# Used in conjunction with the -M command. This sets up a special kind of file (called a socket) that will allow us to enter a command later to gracefully end the SSH tunnel without having to kill the connection. /tmp/sshtunnel is the full path to the socket file this command is creating.
-D: 	# This sets up a dynamic application level forwarding service and 1080 is the port it will listen on. This command creates the SOCKS proxy we'll use later.
-p: 	# Specify the port on which the remote server is listening for SSH connections.
-vvv:   # Maximum Verbosity of debug statements


TO CLOSE THE connection Gracefully

ssh -S /tmp/sshtunnel -O exit server.domain.com -p22
```

## history ( Command history util) 
```sh
history         # prints a list of all the commands from your history to the terminal
history -w      # appends the latest commands to the .bash_history file
history -c      # clears your history but not the .bash_history file. That will need deleting separately
!164            # repeats command 164 from your history
!!              # repeats the last command that was executed during our terminal session
```

### Run Docker images
```
docker run -it --name test registry.access.redhat.com/ubi8/ubi:8.1 bash		# RHEL 8
```

### Packages Mangers
```sh
rpm -qa					# list all packages with Red Hat Package manager

```

### Session management 
`Loginctl`allows for current session management.
```sh
loginctl <tab> <tab>                        # get all the options.
loginctl list-sessions
loginctl show-session <session-id>          # will show whats been going on with a user such as files open etc. 
loginctl show-user <username>
loginctl terminate-session <session-id>
```
## tcpdump 
Maintained here https://www.tcpdump.org/
Great `man` page.

```sh
ip link show                                               # this will show all your network cards so you know which hones to scan
tcpdump -D                                                 # Lists the available interfaces for packet capture
tcpdump -i eth0 -w $(date +%d-%m-%Y).pcap                  # This will write the output of the tcpdump to a pcap file with the date in the title of the file.
tcpdump -n -i eth0                                         # will not show the host names but instead ip addresses
tcpdump -tttt -i eth0                                      # 4 x t will give you the time stamp in your captures 
tcpdump -n -i eth0 port 22                                 # this will filter to just see things leaveing on port 22
tcpdump -w ssh.pcap -i eth0 dst 192.168.4.10 and port 22   # filter on particular ips and ports , and write t oa certain file

tcpdump tcp                                                # only show tcp traffic
tcpdump -v						   # verbose output
tcpdump -vv						   # very verbose output
tcpdump host 192.168.2.5                                   # filter the packet capture to only gather packets going to or coming from the host 192.168.2.5.
tcpdump src host 192.168.2.5                               # filter the packet capture to only gather packets coming from 192.168.2.5.
tcpdump dst host 192.168.2.5                               # filter the packet capture to only gather packets going to 192.168.2.5.

tcpdump portrange 21-23                                    # filter across a port range
tcpdump port 443                                           # filter the packet capture to only gather packets with a source or destination of port 443.
tcpdump src port 1055                                      # capture traffic being sourced from port 1055.
tcpdump dst port 443                                       # capture traffic destined for port 443.

```

## Change your MAC address
```
ifconfig <interface_name> down                          # disable an interface
ifconfig <interface_name> hw ether <new_MAC_address>    # must be 12 chars split by colon
ifconfig <interface_name> down                          # re-enable an interface
```

## nmap (network mapping tool) 
```sh
nmap -sn <Network_IP+SubnetMask>        # scans the entire network
nmap -v -A <Network_IP+SubnetMask>      # agressive verbose network scan
nmap -PN <Ip_Address>                   # pierces through the fire wall apparently ???
nmap -O <Ip_Address>                    # scans for the operating system
nmap -PA                                # tcp AK scan ( 2nd half handshake )
nmap -n -T4 -vvv -p-                    # fast(-T) scan on all tcp ports(-p-) with very, very verbose (vvv) output

```
## File transfer with `netcat` (nc) - CAUTION: this will open a port until you close it
reciever: 
```
nc -l -p 1234 > File.txt
```

Sender: 
```
nc -w 3 <ip_address> 1234 < File.txt
```
## Webservers
### Ruby
```sh
ruby -run -e httpd . -p 80
```
### Python
```
# openssl req -nodes -x509 -keyout server.key -out server.cert 			# make the certs first.

from http.server import HTTPServer, BaseHTTPRequestHandler, SimpleHTTPRequestHandler
import ssl
httpd = HTTPServer(('0.0.0.0', 4443), SimpleHTTPRequestHandler)
httpd.socket = ssl.wrap_socket (httpd.socket, keyfile="/home/bg/https/server.key",
certfile='/home/bg/https/server.cert', server_side=True)
httpd.serve_forever()
```

## mysql 
```
mysql -u alice -p 							# login as the user Alice and prompt me for a password
mysql> show databases;
mysql> show tables;
mysql> use <DATABASE_NAME>;
mysql> select * from <TABLE_NAME>;
mysql> select load_file('/var/lib/mysql-files/foo.txt');		# Read a file from mysql. Nice if you have privledge, yes ??
```


## postgresql

```
CREATE TABLE demo(t text);						# create atable out of some text
COPY demo from '[FILENAME]';						# copy the text for the table from a file 
SELECT * FROM demo;							# get all from the new table
```


## SQLmap
`https://github.com/sqlmapproject/sqlmap`
```
git clone --depth 1 https://github.com/sqlmapproject/sqlmap.git sqlmap-dev		# clone sqlmap latest dev

python3 sqlmap.py -r <REQUEST_FILE> --level=2 --time-sec=8 --dbms "postgresql" -p category –"proxy=http://localhost:8081" --batch

-r 				# a file of a fresh http request
--level				# the level of intensity 1-5. Default is 1
--time-sec			# time to wait for the response
-- dbms				# the type of dbms you are targeting (if you know)
-p 				# target parameter

python3 sqlmap.py -u "<TARGET_URL>" --cookie="<COOKIE/SESSION_ID_1>; <COOKIE/SESSION_ID_N" --tables --batch

--batch 			# !!! this will choose the default options when running a scan . Best not to use as it may start trying to crack password
--schema 			# Enumerate the DB schema
--tables 			# Enumerate the DB tables
--password			# Enumerate DBMS users password hashes

python3 sqlmap.py -u "<TARGET_URL>" --cookie="<COOKIE/SESSION_ID_1>; <COOKIE/SESSION_ID_N" --data="<REQUEST_DATA>" -p <PARAM> --dbs

---dbs 				# Enumerate the DBMS data bases

python3 sqlmap.py -u "<TARGET_URL>" --cookie="<COOKIE/SESSION_ID_1>; <COOKIE/SESSION_ID_N" --data="<REQUEST_DATA>" -p <PARAM> --dbs -D <SPECIFIC_KNOWN_DB> --tables --batch --threads <NUMBER_OF_THREADS>

--threads			# concurrent threads to run to increase speed

python3 sqlmap.py -u "<TARGET_URL>" --cookie="<COOKIE/SESSION_ID_1>; <COOKIE/SESSION_ID_N" --data="<REQUEST_DATA>" -p <PARAM> -T <TARGET_VALUE> --tables --batch --threads 5 --dump

-T				# DBMS database table(s) to enumerate
--dump 				# Dump DBMS database table entries

python3 sqlmap.py -r BASIC.txt -p id –"proxy=http://localhost:8081"

Runs SQL map with a request copied into a text file, a selected parameter and via my proxy (zap)
```

### Dealing with hashes
```
hash-identifier # Liniux tool to identify hashes
hashcat '<SUSPECT_HASH>' <FILE_PATH_OF_DICTIONARY> 
```

## Semgrep ( Semantic Grep)
Getting started
DL rules locally
```
semgrep -l <LANG> --config=<LOCATION_OF_RULES_DIR-or-FILE> -q -o <REPORT_FILE_NAME> <SOURCE_CODE_DIR>
- q 				# quiet mode
--config=<RULES>		# the set of rules. Can be set to "auto" too.
```
Try...
```sh
semgrep -l java --config /Users/geoffreyowden/mystuff/SemGrepTool/semgrep-rules/java/lang/security/audit -q -o FullSecAudit.log CODE/
```
## Mend work
```
cat MendFIndingsRAW.txt | jq '.[] | {resource:.resource, message:.message}' > CleanedMendJSONoutput.json # Get the file names adn the messages into a file 
cat CleanedMendJSONoutput-working.json | grep 'CVE' | cut -d" " -f 5 | uniq | wc -l 	# how many uniq CVE are there

cat CleanedMendJSONoutput-working.json | grep 'Component:' | cut -d" " -f 11 | awk '!a[$0]++' # Get all the uniq package values
```
## node

```sh
npm list -g						# list pakages installed globally
npm view <package-name> version				# list the version for a specific package

```
## Kubernetes
```sh
kubectl exec --stdin --tty <POD_NAME> -- /bin/bash   				 # get a shell on a machine
kubectl config set-context --current --namespace=<insert-namespace-name-here>    # Set your default namespacce to something else
kubectl -n <NAMESPACE> get pvc | grep -v NAME | awk '{print $1}' | xargs -I arg kubectl delete pvc -n <NAMESPACE> --ignore-not-found=true arg # Delete pvc from a namspace
kubectl config get-contexts							 # get all the contexts from your kube Config file
kubectl config delete-context							 # Delte a context from your kube config and the kube config file.
kubectl get --v=5 -o wide -w pod <POD_NAME>					 # get the pod with debug level 5 (0-9) Trace level verbosity 
kubectl get --v=9 -o wide -w pod <POD_NAME>					 # get the pod with debug level 0 (0-9) Network Trace level verbosity 
kubectl -n <NAMESPACE> get events --sort-by='{.lastTimestamp}'			 # good way to look for erros in your Kubernetes stack
```

## Docker 
```sh
docker exec -it <CONTAINER_NAME> /bin/bash           # get a shell on a machine
docker container logs -f <CONTAINER_NAME>	     # follow the logs on a running container

GET AN IMAGE ON AN OVA
docker login -u "<WORK_EMAIL>" -p <ARTIFAC_API_KEY> apic-dev-docker-local.artifactory.swg-devops.com
docker pull <IMAGE_LOCATION_AND_NAME> 

STOP
docker stop $(docker ps -a -q)

Remove
docker rm $(docker ps -a -f status=exited -q)	     # remove all excited containers
docker rmi $(docker images -a -q)		     # remove all images

Restart
containers=$(sudo docker ps | awk '{if(NR>1) print $NF}') ; for container in $containers; do docker restart $container; done		# restarts all the containers

COPY FILES BACK AND FORTH
docker cp <CONTAINER>:<FILE_AND_LOCATION> <HOST_DESTINATION>		# from Container to Host
docker cp <HOST_DESTINATION> <CONTAINER>:<FILE_AND_LOCATION>		# from Host to Container

```


### Juice shop on docker
```
docker pull bkimminich/juice-shop			# Pull the Juice Shop
docker run --rm -p 3000:3000 bkimminich/juice-shop	# Start the Juice shop
```
### DVWA on docker

```sh
docker run --rm -it -p 8808:8808 vulnerables/web-dvwa  # U: admin PW: password
```

### Kali on docker

```sh
docker run -t -i kalilinux/kali-rolling
then on the box...

apt update && apt -y install kali-linux-headless

apt-get install python3-pip

```
### xsser tool

```sh
python3 xsser --all='<URL_address>' --cookie='Some_Session_cookie=<Auth_cookie_data>' 	# will scan all urls in the domain, taking in the auth token (whatever that is set as)

python3 xsser --auto -u '<URL_address>=XSS' --cookie='Some_Session_cookie=<Auth_cookie_data>' # will run a predefined list of xss on the var. 1291 request accross 5 threads
```

## File system cmds
```sh
df -aTh   #  display free (df) disk space on all(-a) mount points (-T) and make it human readable (-h)
```
## Bash special environment variables
```sh
echo $$             # The process ID of the current script or shell
echo $USER          # The username of the user running the script
echo $HOSTNAME      # The hostname of the machine
echo $RANDOM        # A random number
echo $LINENO        # The current line number in the script
```
## Bash special scripting variables ( that can also be echoed )
```sh
echo $0             # The name of the Bash script
echo $1 - $9        # The first 9 arguments to the Bash script
echo $#             # Number of arguments passed to the Bash script
echo $@             # All arguments passed to the Bash script
echo $?             # The exit status of the most recently run process
```

# Bash Test Operators
## Integer Comparison
```sh
if [ "$a" -eq "$b" ]    # -eq             -> is equal to

if [ "$a" -ne "$b" ]    # -ne             -> is not equal to

if [ "$a" -gt "$b" ]    # -gt             -> is greater than 

if [ "$a" -ge "$b" ]    # -ge             -> is greater than or equal to

if [ "$a" -lt "$b" ]    # -lt             -> is less than

if [ "$a" -le "$b" ]    # -le             -> is less than or equal to

if (("$a" < "$b"))      # <               -> is less than (within double parentheses)

if (("$a" <= "$b"))     # <=              -> is less than or equal to (within double parentheses)

if (("$a" > "$b"))      # >               -> is greater than (within double parentheses)

if (("$a" >= "$b"))     # >=              ->  is greater than or equal to (within double parentheses)
```

## String Comparison
```sh
if [ "foo" = "foo"] # with single brackets use single '='. Returns Boolean 

if [[ $a == z* ]]   # True if $a starts with an "z" (pattern matching).

if [[ $a == "z*" ]] # True if $a is equal to z* (literal matching).

if [ $a == z* ]     # File globbing and word splitting take place.

if [ "$a" == "z*" ] # True if $a is equal to z* (literal matching).

if [ "$a" != "$b" ] #  != -> is not equal to. This operator uses pattern matching within a [[ ... ]] construct.

if [[ "$a" < "$b" ]]        # <  ->  is less than, in ASCII alphabetical order
if [ "$a" \< "$b" ]        # < -> Note that the < needs to be escaped within a [ ] construct.

if [[ "$a" > "$b" ]]    # > -> is greater than, in ASCII alphabetical order. 
if [ "$a" \> "$b" ]     # > Note that the > needs to be escaped within a [ ] construct.
	
if [ -z "$s" ] # -z -> string is null that is, has zero length

if [ -n "$s" ] # -n -> string is not null.
```

## File Test Operators 
```sh
-e      # file exists

-a      # is deprecated and its use is discouraged.
	
-f      # file is a regular file (not a directory or device file)
	
-d      # file is a directory
	
-h      # file is a symbolic link

-L      # file is a symbolic link
	
-b      # file is a block device
	
-c      # file is a character device
	
-p      # file is a pipe
	
-S      # file is a socket
	
-s      # file is not zero size
	
-t      # file (descriptor) is associated with a terminal device
        # This test option may be used to check whether the stdin [ -t 0 ] 
        # or stdout [ -t 1 ] in a given script is a terminal.

-r      # file has read permission (for the user running the test)
	
-w      # file has write permission (for the user running the test)
	
-x      # file has execute permission (for the user running the test)

-g      # set-group-id (sgid) flag set on file or directory

-u      # set-user-id (suid) flag set on file

-k      # sticky bit set

-O      # you are owner of file

-G      # group-id of file same as yours

-N      # file modified since it was last read

-nt     # file f1 is newer than f2
        if [ "$f1" -nt "$f2" ]

-ot     # file f1 is older than f2
        if [ "$f1" -ot "$f2" ]

-ef     # files f1 and f2 are hard links to the same file
        if [ "$f1" -ef "$f2" ]

!       # "not" -- reverses the sense of the tests above (returns true if condition absent).
```

# Git on the terminal

### Clone Directory

```sh
git clone <url>
```


### Create Project
```sh
cd project/
git init                    # initializes the repository
git add .                   # add those 'unknown' files
git commit                  # commit all changes, edit changelog entry
git rm --cached <file>...   # ridiculously complicated command to undo, in case you forgot .gitignore
```


### Branching and Merging
```sh
git branch                          # show list of all branches (* is active)
git checkout -b linux-work          # create a new branch named "linux-work"
<make changes>
git commit -a
git checkout master                 # go back to master branch
git merge linux-work                # merge changesets from linux-work (Git >= 1.5)
git pull . linux-work               # merge changesets from linux-work (all Git versions)
git branch -m <oldname> <newname>   # rename branch
git branch -m <newname>             # rename current branch
```


### Delete Project
```sh
git branch -d <branchname>   	# deletes local branch
git push origin :<branchname>	# deletes remote branch
git remote prune <branchname>	# update local/remote sync
```


### Merging Upstream
```sh
git remote -v 									# Get list of remote branches
git remote add upstream <upstream github url>	# Add original as upstream
git remote -v 									# Check upstream

git fetch upstream 								# Get original repo
git checkout development						# Switch to main branch in local fork
git merge upstream/development					# Merge original with fork

git diff --name-only | uniq | xargs subl		# Fix conflicts in Sublime Text
```


### Importing Patches
```sh
git apply < ../p/foo.patch
git commit -a
```


### Exporting Patches

```sh
git commit -a -m "commit message"
git format-patch HEAD^  # creates 0001-commit-message.txt
                        # (HEAD^ means every patch since one revision before the
                        # tip of the branch, also known as HEAD)
```



### Inspecting Revisions

# Inspect history visually
```
gitk    # this opens a Tk window, and shows you how the revisions are connected
```
# Inspect history
```sh
git log     # this pipes a log of the current branch into your PAGER
git log -p  # ditto, but append a patch after each commit message
```
# Inspect a specific commit
```sh
git show HEAD   # show commit info, diffstat and patch
                # of the tip of the current branch
```


### Referring to Revisions
# by name
```sh
git log v1.0.0  # show history leading up to tag "v1.0.0"
git log master  # show history of branch "master"
```
# relative to a name
```sh
git show master^    # show parent to last revision of master
git show master~2   # show grand parent to tip of master
git show master~3   # show great grand parent to tip of master (you get the idea)
```
# by output of "git describe"
```sh
git show v1.4.4-g730996f    # you get this string by calling "git describe"
```
# by hash (internally, all objects are identified by a hash)
```sh
git show f665776185ad074b236c00751d666da7d1977dbe
git show f665776    # a unique prefix is sufficient
```
# tag a revision
```sh
git tag v1.0.0                      # make current HEAD known as "v1.0.0"
git tag interesting v1.4.4-g730996f # tag a specific revision (not HEAD)
```


### Comparing Revisions
# diff between two branches
```sh
git diff origin..master             # pipes a diff into PAGER
git diff origin..master > my.patch  # pipes a diff into my.patch

# get diffstat of uncommitted work
```sh
git diff --stat HEAD
```

## git add -p is your friend

#### git add -p is basically "git add partial (or patch)"

Patch mode allows you to stage parts of a changed file, instead of the entire file. This allows you to make concise, well-crafted commits that make for an easier to read history. This feature can improve the quality of the commits. It also makes it easy to remove parts of the changes in a file that were only there for debugging purposes - prior to the commit without having to go back to the editor.

It allows you to see the changes (delta) to the code that you are trying to add, and lets you add them (or not) separately from each other using an interactive prompt. Here's how to use it: 

from the command line, either use
- git add -p
- or you can use git add -i and choose type 5 or p (for patch). 
 
Git will ask you which files you would like to partially stage; then, for each section of the selected files, it will display hunks of the file diff and ask if you would like to stage them, one by one:

![here's a visual](http://i.imgur.com/UbSnkwX.png)

At each point, you will be asked whether you want to "stage this hunk". Here are the commands you can use:
####commonly used commands
- y - stage this hunk
- n - do not stage this hunk
- a - stage this and all the remaining hunks in the file
- d - do not stage this hunk nor any of the remaining hunks in the file

#### more advanced commands
- g - select a hunk to go to
- / - search for a hunk matching the given regex
- j - leave this hunk undecided, see next undecided hunk
- J - leave this hunk undecided, see next hunk
- k - leave this hunk undecided, see previous undecided hunk
- K - leave this hunk undecided, see previous hunk
- s - split the current hunk into smaller hunks
- e - manually edit the current hunk
- ? - print help


#### Some cool tips from the internet: 

- If git presents you with a chunk larger than what you would like to add, you can use the "e" interactive command to specify the exact lines that you want added or removed. This is probably the most powerful option. As promised, it will open the hunk in a text editor and you can edit it to your hearts content
- Split the hunk into smaller hunks. This only works if there’s unchanged lines between the changes in the displayed hunk, so this wouldn’t have any effect in the example above
- git reset -p works in a similar way
- git commit -p it combines git add -p and git commit in one command.



## homebrew

```sh
brew doctor                     # checks you system for potential problems
brew cleanup --prune-prefix     # Only prune the symlinks and directories from the prefix and remove no other
brew cleanup --force -s &>/dev/null
brew cask cleanup &>/dev/null
rm -rfv /Library/Caches/Homebrew/* &>/dev/null
brew tap --repair &>/dev/null
```
## node
```sh
npm outdated 				# find the packages with updates

```

## tcpdump (on mac needs to be run as root)
```sh

see https://danielmiessler.com/study/tcpdump/

```
### Cli tools

[grex - Regex checker](https://github.com/pemistahl/grex)  - simplify creating regular expressionssimplify the often complicated and tedious task of creating regular expressions

## Firefox Short keys

```sh
Ctl + t				# Create new tab
Ctl + w				# delete current tab
Ctl + k				# take cursor to the search bar
Ctl + l				# copy the URL in searchbar 
Ctl + u				# Look at the HTML or XML source for the page you're viewing
Cmd + shift + b			# Toggle the bookmarks toolbar on and off
```
