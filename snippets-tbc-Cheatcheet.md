
### Linux Version


`awk '!/^$/' FILENAME > NEWFILE.out.  # remove wmpty lines` 
```
# The following commands can all find os name and version in Linux:
cat /etc/os-release
lsb_release -a
hostnamectl

# Find Linux kernel version
uname -r 
```
`usermod -aG sudo <USERNAME>  # add <USERNAME> to the sudoers group` 


Create a webserver with node
`npx http-server -p 9999`


Disable the CSS by pasting the following into the dev tools console
`var el = document.querySelectorAll('style,link'); for (var i=0; i<el.length; i++) {el[i].parentNode.removeChild(el[i]);};`


`brew install mitmproxy`
`pip3 install mitmproxy2swagger # Plugin to scrape an api of all its endpoints`


CMD: `zip -r <FILETOEXTRACT> $(find /opt/ibm/isim/ -name "*.jar")`


`grep MemTotal /proc/meminfo` - Get the total ram/Memory of the system


`for i in $(compgen -a); do alias $i ; done` # List all the aliases and the see what commmands they actually do



`find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2> /dev/null` # List of all SUID and SGID Executables - from : https://atom.hackstreetboys.ph/linux-privilege-escalation-suid-sgid-executables/



`watch -n 60 "date && free -h"` # Run two commands in watch at the same time every 60 seconds


### Regexes for vs code

`password(.*)"(.*)"`# find the term "password" followed by anything and then a pair of quotations marks with text within them
`auth(.*)"(.*)"`# find the term "auth" followed by anything and then a pair of quotations marks with text within them


`detect-secrets -C . scan > .secrets.basline` # Run detect secrts and make a basline file for the repo
`detect-secrets audit .secrets.baseline`

`trufflehog --regex <FULLPATHTOCODE>`



### Cheatsheet

`alias chee='callCheatSh(){ curl cheat.sh/"$@" ;}; callCheatSh'`
