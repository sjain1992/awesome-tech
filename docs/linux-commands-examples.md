<!-- MarkdownTOC -->

- [Linux Commands Examples](#linux-commands-examples)

<!-- /MarkdownTOC -->

[![commandlinefu](images/commandlinefu.com)](http://commandlinefu.com/)

[![climagic youtube](images/climagic-icon.png)](https://www.youtube.com/user/climagic)

[![linux skill](images/linuxskill.png)](https://www.youtube.com/channel/UCmzTzKZT3yWaIiFvEyIHrOg)

<center>

|[![climagic twiiter](images/climagic.png)](https://twitter.com/climagic)|[![unixtooltip twitter](images/unixtooltip_twitter.png)](https://twitter.com/UnixToolTip)|
|:---:|:---:|

|[![commandlinefu 0 star](images/commandlinefu0star.png)](https://twitter.com/commandlinefu)|[![commandlinefu 3 star](images/commandlinefu3star.png)](https://twitter.com/commandlinefu3)|[![commandlinefu 10 star](images/commandlinefu10star.png)](https://twitter.com/commandlinefu10)|
|:---:|:---:|:---:|

</center>

# Linux Commands Examples
- [Linux Commands Tweets](linux-commands-tweets.md)
- [nixCraft: My 10 UNIX Command Line Mistakes](http://www.cyberciti.biz/tips/my-10-unix-command-line-mistakes.html)

- Make your prompt safer with # so that if you accidentally copy & paste it, it doesn't run. 🌟🌟🌟🌟🌟

		PS1="# $PS1"

- In bash, cd - takes you back to your previous directory.

- Tired of repeatedly pressing 'y' through some shell process? Try the 'yes' command: 🌟

		yes | rm *.txt 
		yes | fsck /dev/FOO

- Edit a file on a remote server using vim from your local *nix desktop

		vim scp://user@server1//etc/httpd/httpd.conf 

- In vim this will search all lines (%s) for wlan0 and replace all the instances per line (g) with eth3 and confirm (c)

		:%s/wlan0/eth3/gc 
		
- Using +F option or pressing F in less is similar to `tail -f filename.log` but can use less's features. 🌟🌟

		less +F filename.log 

- Show the first and last 5 lines of the file 'log'.

		(head -5; tail -5) < log
		
- Make less more like more, but still more than more. Percent of file in prompt, etc. 

		export LESS='-sCmqPm--Less--(?eEND:%pb\%.)'

- This environment variable will invoke 'less' with these options when it is used. Like when viewing a man page.

		export LESS="-S -j10 -i" 

- Find out which of your directories(below the current directory) occupy at least 1GB of space. 🌟🌟

		du -h . | grep "^[0-9\.]\+G"

- Total bytes used by 5+ year old directories in CWD:

		find . -mtime +$((365*5)) -maxdepth 1 -exec du -sb {} \; |awk '{s+=$1}END{print s}'

- List of empty subdirectories of current directory.

		find . -empty -type d

- Find and long list mp3 files in Music dir older than a year and larger than 10MB.

		find music -name '*.mp3' -mtime +365 -a -size +10M -ls 

- Like ping, but it uses an ARP request to check, which gets around host firewalls blocking ICMP. Only works on same subnet

		arping 10.0.8.5

- Show directory size and sort by human readable amount (MB, GB, etc.). Requires GNU sort for -h option. 🌟🌟

		du -sh */ | sort -h 

- Show the total space used on all your local disk partitions. 🌟

		df -lP |awk '{sum += $3} END {printf "%d GiB\n", sum/2**20}' 

- Print disk space used on all ext3 or 4 FS in GiB.

		df -Pl -t ext3 -t ext4 | tail -n+2 | awk '{ sum+=$3 } END { print sum/2**20 }'

- Quickly remove duplicate lines from a log/text file on Unix/Linux system: 

		awk '!seen[$0]++' app.logfile

- Life is too short to run the same command twice.

		export HISTSIZE=0 

- Want to increments all numbers in input.txt? 

		perl -pe 's/(\d+)/ 1 + $1 /ge' input.txt

- cp - u will only copy files that don't exist, or are newer than their existing counterparts, in the destination directory.
- Print server serial/product/manufacturer:
		
		for i in serial-number manufacturer product-name; do 
		echo "$i $(dmidecode -s system-${i})"; 
		done

- Copy a file using "ionice -c 3" to give it idle priority to reduce load on the system.

		ionice -c 3 cp vm1.img vm1-clone.img

- Remove the prefix 'unwanted' from the beginning of each filename with .jpg suffix in CWD.

		rename 's/^unwanted//' *.jpg

- Find file duplicates in 'dir' recursively based on size and mdsum and log to dupes.txt

		fdupes -r dir > dupes.txt

- Quickly find the largest 5 files in the CWD tree without crossing filesystem boundaries 🌟🌟🌟

		find . -xdev -ls | sort -n -k 7 | tail -5

- counts files in the current path by modification month

		find . -maxdepth 1 -type f -printf '%TY-%Tm\n' | sort | uniq -c 

- Use the */ trick to get only the directories, then use ${dir%/} to remove the trailing / you get

		for dir in */ ; do echo "${dir%/}" ; done

- Move current year pics to 2015 directory.

		find . -maxdepth 1 -daystart -type f -name '*.jpg' -mtime -$( date +%j ) -exec mv -v {} 2015/ \;

- Lower case all files in a folder.

		for f in *; do b=$(echo "$f" | tr '[A-Z]' '[a-z]'); mv "$f" "$b"; done

- Print the day of the year. Can be useful with things like find.

		date +%j 

- Make month histogram of dates of files in current directory.

		ls -la --full-time |tr -s " " |cut -f6 -d " "|cut -c1-7 | sort | uniq -c

- Use cut to print out columns 1, 5 and 10 through 15 in data.csv and write that to new.csv

		cut -d, -f1,5,10-15 data.csv > new.csv 
		
- Want to store log of your ssh session? Try:
		
		ssh -l user server1 | tee -a ~/myssh.log

- Want to find out which file is the oldest in tar ball archive?

		tar -tvf xkcd-tar-bomb.tar.gz | sort -k 4 -r | head

- Add ssh key to remote host. Wrong: 

		cat key | ssh usr@box 'cat >> .ssh/authorized_keys' 

- Add ssh key to remote host. Correct: 🌟🌟

		ssh-copy-id usr@box

- Create a dynamic SOCKS5 proxy on port 8989 using an SSH connection. Some apps can be configured to use this.

		ssh -D 8989 you@remotehost 

- After all the host keys and auth, you'll be on server3.

		ssh -t user1@server1 'ssh -t user2@server2 "ssh -t user3@server3"'

- The awk variable $1 contains the first field in a record, $2 the second, $3 the third, etc. $0 contains all fields.

- Print all from 3rd field to end of line. Very useful for log parsing.

		awk '{ print substr($0, index($0,$3)) }' mail.log

- List top 20 404's URLs in descending order by reqs.

		awk '$9 == "404" {print $7}' access.log |sort|uniq -c|sort -rn| head -n 20

- List 10 largest open file on Unix:

		lsof /|awk '{ if($7>1048576) print $7/1048576 "MB" " " $9 " " $1 }'|sort -nu|tail 

- *"Attempt"* to recover an accidentally removed file. 🌟🌟

		fgrep --binary-files=text -C 2000 "string in file" /dev/sda > recovereddata.out 

- Replace foo with bar only on lines that contain 'bang'. Use in pipeline or with file args. 🌟

		sed "/bang/ s/foo/bar/" 

- Recursive search and replace old with new string, inside files. recursively traverse the directory structure from . down, look for string "oldstring" in all files, and replace it with "newstring", wherever found 🌟🌟

		$ grep -rl oldstring . |xargs sed -i -e 's/oldstring/newstring/'

		also:
		
		grep -rl oldstring . |xargs perl -pi~ -e 's/oldstring/newstring'

- Watch web server access log for HTTP status code 500 & display entry generated that code: 🌟

		tail -f access.log | awk '$9 == 500 { print $0 }'

- You can actually follow more than one log at once and get new updates on them. Use -q to not print filename header.  🌟

		tail -f *.log 

- list top 50 404's in descending order.

		awk '$9 == "404" {print $7}' access.log |sort|uniq -c|sort -rn| head -n 50

- Request by hour graph.

		awk '{print $4}' apache_log|sort -n|cut -c1-15|uniq -c|awk '{b="";for(i=0;i<$1/10;i++){b=b"#"}; print $0 " " b;}'

- Count syslog hits per minute in your messages log file. Useful for doing quick stats.

		awk -F: {'print $1 ":" $2'} messages |uniq -c

- Get list of top URLs from all logs combined 🌟🌟🌟

		zcat access_log*.gz |cat - access_log |awk '{print $7}' |sed 's/\?.*//' |sort|uniq -c|sort -nr 

- For Mar 22nd, print the req fields for hosts from two letter gTLD

		fgrep 22/Mar/2015 access_log |awk '$1~/\.[a-z][a-z]$/{print $6 " " $7}'

- Want to extract files to another directory using tar command? Try 

		tar xvf file.tar -C /path/to/dir

- Compress files with xz in PWD according to size, starting with smallest.

		ls -Sr1 | while IFS=$'\n' read -r file; do xz "$file"; done
		
- The utility 'file' reports a file's type. With the option -z it will try to look inside zipped files.

- Compare the contents of 2 dirs. Show only 2 columns, each for files unique to the directory:

		comm -3 <(ls -1 dir1) <(ls -1 dir2)

- Want to see your FreeBSD server cpu temperature? Try:

		sysctl -a |grep temper

- Want to delete a single command from history on a Linux, OS X & Unix Bash shell? 🌟

		history -d N

- Want to resume failed download on Linux/Unix/OSX/BSD?

		curl -LOC - url 
		wget -c url

- Quick and easy way to make a mirror of a website

		wget -m http://www.example\.com/

- Is my HTTPD using Gzip?

		curl -sILH 'Accept-Encoding: gzip,deflate' http://cyberciti.biz | grep Content-Encoding

- Want to use the curl command with proxy username/password on Linux/Unix? 

		curl -x usr:pwd@proxy:port url

- You can use the text-based web browser to browse the Internet in console

		w3m cyberciti.biz
		lynx cyberciti.biz 

- Search (grep) for multiple error message on Linux/Unix: 🌟🌟🌟

		egrep -w 'warning|error|critical' /var/log/messages

- Search for names and build a frequency count for each name.

		egrep -wo "(Donnie|Frank|Roberta|Grandma)" story.txt |sort|uniq -c|sort -r 

- Determine if a port is open with bash:

		: </dev/tcp/127.0.0.1/80

		For times when netcat isn't available.

		Will throw a Connection refused message if a port is closed.

		Scriptable:
		(: </dev/tcp/127.0.0.1/80) &>/dev/null && echo "OPEN" || echo "CLOSED" 

- [The following is Juniper screenOS authentication backdoor - master ssh password:](https://t.co/IQOGT33oTC)

		<<< %s(un='%s') = %u

- [Want to list all iptables rules with line numbers? Try](http://www.cyberciti.biz/faq/linux-viewing-all-iptables-rules-with-numbers-command/)

		iptables -L -n -v --line-numbers

- Capture all port 123 traffic to a file on a Linux/Unix like system: 

		tcpdump -s 1514 port 123 -w file 
		
		Read captured traffic: 
		tcpdump -r file

- Show only up to the first 10 packets by each source IP:

		tcpdump -nn ip | awk '{s=$3;sub(/\.[0-9]+$/,"",s);if(a[s]++<10){print}}' 

- Want to see whether there was an error after executing a command but no error message was displayed? $? shows the exit status. Try 

		echo $?

- Want to see disks attached to Linux server? Try 

		lsscsi

- Want to list SCSI devices (or hosts) and their attributes under Linux operating systems? Try 

		lsscsi -g

- Want to delete existing SAN LUNs on Linux? 🌟

		multipath -f map # Flush a multipath devicemap 
		echo 1>/sys/block/sdc/device/delete # Delete sdc

- List both running privileged and unprivileged lxc containers: 

		netstat -ax | egrep '@.*/lxc/.*/command$'	

- Show the TCP and UDP ports being listened on and if you're root, also show the process associated, user, etc. 🌟🌟🌟
	
		netstat -lepunt

- Want to find out the MAC addresses of the KVM powered VM? Try

		virsh dumpxml VM_NAME | grep 'mac address'	

- Want to list block devices on #Linux easily? Try 

		lsblk 
		lsblk -m 
		lsblk -f

- Start a web service on port 8000 that uses the current directory as its document root

		python -m SimpleHTTPServer

- Use perl regex (negative look-behind/look-ahead assertions) to get URLs.

		grep -P -o '(?<=href=")http:\S+(?=")' *.html 

- WP abuse

		grep -h "POST /.*wp-login.php" *-access_log |awk '$1!~/^my.ip.addr$/{print $1}' |sort|uniq -c|sort -nr |head -50> wp-abusers.txt 

- Make slideshow from *.jpg

		for p in *.jpg; do ffmpeg -loop_input -f image2 -i $p -t 3 -r 4 -s 1080x720 -f avi - >> slides.avi; done 
		
- Wrap the lines of draft.txt at 72 characters wide, doing so at spaces, not middle of word (-s)

		fold -w 72 -s draft.txt > newdraft.txt

- tail log & highlight errors (if your grep supports --color)

		tail -f foo.log|egrep --line-buffered --color=auto 'ERROR|WARN|$'

- Random color per log line.

		tail -F syslog |while read -r line;do printf "\033[38;5;%dm%s\033[0m\n" $(($RANDOM%255)) "$line";done

- Instead of typing the user & group, if they are the same you can just type the user followed by a colon

		chown -R www-data: * 

- Show the query and results of 'select' queries going to your mysql server. Won't work on socket conns

		ngrep -d eth0 -i 'select' port 3306

- Show what processes are using port 80 either locally or remotely. Need to be root for unowned processes. 🌟

		lsof -i TCP:80 

- On Linux, print out a list of the process IDs that are in the zombie state.

		ps aux | awk '{if ($8=="Z") { print $2 }}'
		
- What I've done this week

		git log --author=$USER --format="- %B" --since=-7days --reverse |mail -s "What I've done this week" boss@company\.com

- Which days I've worked...

		git log --date=short --format="%ci"|awk '{print $1}'|uniq 

- I find brace expansion useful for renaming files. This cmd expands to "mv Picture.jpg Picture-of-my-cat.jpg"

		mv Picture{,-of-my-cat}.jpg

- Show % reports of CPU statistics for every active task in the server at two second intervals. 🌟

		pidstat 2 5

- Suspend and reattach a process to screen

		longcmd ; [Ctrl-Z] ; bg ; disown ; screen ; reptyr $( pidof longcmd )

- Want to clean metadata from images and other files on Linux? Try 

		mat -d file.jpg # Display it 
		mat file.jpg # Clean it

- Apparently according to testing, this is the fastest way to delete millions of small files.

		rsync -a -delete empty/ foo/

- See top & bottom 5 log entries on unix/linux 

		(echo "--[head]---"; head -5; echo "--[bottom]--"; tail -5) </var/log/httpd/php.log
		
- Test reachability of a cloud DNS server & measure the round-trip time 🌟

		for i in {1..4};do ping -q -c 4 ns-cloud-c${i}.googledomains.com;done

- To find in which file an event has been logged in use following which will display the last modified logs on linux 

		ls -ltr /var/log | tail

- Want to detect execution in a virtualized environment on Linux? 

		systemd-detect-virt 

		OR 

		dmidecode -s system-manufacturer

- TCP vulnerability? Easy to mitigate with ansible:
 
		- sysctl: name=net.ipv4.tcp_challenge_ack_limit value=999999999 sysctl_set=yes

- Live dmesg output in human readable format (colors, timing)

		dmesg -wH 

- List open ports on Linux: 

		netstat -an --inet | grep LISTEN | grep -v 127.0.0.1

		ss -l     (all open ports)

		ss -nlp

		ss -4nlp  (ipv4)

		ss -6nlp  (ipv6)

		ss -s     (summary)

		ss -lp | grep 4949  (who is responsible for opening socket/port #4949)

		ss -t -a    (All TCP sockets)

		ss -x -a    (unix sockets)

		ss -4 state time-wait

		ss -o state fin-wait-1

		ss -4 state time-wait -o

- Display HTTP connections:

		ss -o state established '( dport = :http or sport = :http )'

- Compare local and remote log file with vim. Edit a file and show differences:

		vimdiff /path/local/log scp://192.168.1.25/path/log

- The sed command p prints. For example, print lines 3 through 7 of a file: 

		sed -n '3,7p' somefile

- Quickly find the largest 5 files in the CWD tree without crossing filesystem boundaries:

		find . -xdev -ls | sort -n -k 7 | tail -5

- List the 20 largest files or folders under the current working directory:

		du -ma | sort -nr | head -n 20

- Search the file system, but don't descend into the /sys or /proc directories:

		find / \( -path /proc -o -path /sys \) -prune -o -print

- Scan your internal network for hosts listening on TCP port 22 (SSH protocol):

		nmap --open -p T:22 192.168.1.0/24   (prints closed/filtered ports) 
		nmap 192.168.1.0/24 -p22    

- Display top bandwidth hogs on website:

		awk '{a[$1] += $10} END {for (h in a) print h " " a[h]}' access_log | sort -k 2 -nr | head -10

- Determine what lines two different files have in common. The comm program requires sorted files:

		comm -12 <(sort names1) <(sort names2) 
		
- Add this to .vimrc and all searches in vim will use "very magic" mode which acts like egrep:

		nnoremap / /\v

- Long list (-l) only the directories in the current directory. .*/ and */ are utilizing your shell's glob matching ability:

		ls -ld .*/ */ 

- Show only the processes matching httpd, ignoring the line of the grep process itself (regex trick):

		ps auxww | grep "[h]ttpd"

- Show tabs in a file:

		cat -T

- strace is a sysadmin godsend. This will follow pid 927 and its children, writing to "smtpd.<pid>":

		strace -p 927 -o smtpd -ff -tt

- While in #vim insert mode, insert the filename of the current file into the buffer or vim command prompt:
		
		[Ctrl-R] % 

- In #vim, re-select the previous selection:

		gv

- In vim, this will left shift indentation of selected lines by one tab. > for right:

		v (select text with cursor movement) <

- Comment out selected lines in vim using block select mode. :

		[Ctrl-V] (move cursor down across beginning of lines) [I] [#] [Esc]

- In vim, depending on your term color scheme, these can help you w/ syntax highlighting:

		:set bg=dark or :set bg=light 

- Open all your JS source files in vim tabs. Then use :tabn and :tabp to switch between them. :tabe newfile to open new tab:

		vim -p *.js 

- This vim command will turn off the current search highlighting until the next search. Use :set hlsearch to turn on:

		:noh

- Check net before slow scan:

		for d in {1..254};do ping -c3 10.3.0.5 > /dev/null ||{ echo "VPN is down";break; }; nmap -T1 10.3.0.$d ; done

- You can use the -n option with make to preview what it will do first before actually doing it:

		make -n install

- Who can see your 8.8.8.8 requests?:

		traceroute 8.8.8.8|awk -F[\(\)] '$2~/[0-9]/{print $2}'|while read i;do echo $i;geoiplookup $i;done

- The sed command p prints. For example, print lines 3 through 7 of a file:
		
		sed -n '3,7p' somefile

- Filter out lines containing 'spam': 

		sed '/spam/d' somefile

- Show some full file paths referenced in the process table to try to find out where systems are storing data:

		ps auxww | grep -o "/[^\ ]*"

- Did they really only change what they say they did?:

		diff <(docx2txt < agreement.docx) <(docx2txt < newagreement.docx)

- Handy Bash feature: Process Substitution:

		$ some-command <(another-command)
		$ diff <(curl http://somesite/file1) <(curl http://somesite/file2)
		https://medium.com/@joewalnes/handy-bash-feature-process-substitution-8eb6dce68133#.pfgkrudmb

- Use the -w option in diff to ignore differences in whitespace (tabs instead of spaces, etc.)

		diff -w index.html bookexample/index.html

- mping nic.uz:

		mping(){ ping $@|awk -F[=\ ] '/time=/{t=$(NF-1);f=2000-14*log(t^18);c="play -q -n synth 1 pl "f"&";print $0;system(c)}';}

- Prefix each line with the local time based on epoch time in 1st column:

		|gawk '{printf("%s %s\n",strftime("%Y-%m-%d_%T", $1),$0)}' 

- Optimize all png files for faster loading site:

		find . -type f -iname "*.png" -print0|xargs -I {} -0 optipng "{}"

- Backslashing the * glob instead of quoting the expression:

		find ./music -name \*.mp3 -exec cp {} ./new \;

- Find files under /var/log that are readable by the current user. Takes groups and ACLs into account:

		find /var/log -readable -ls 

- Prefix the epoch time in column 1 with the local time:
	
		tail -f udp.log|gawk '{printf("%s %s\n",strftime("%Y-%m-%d_%T", $1),$0)}'

- Want to display date/time for each bash command history on a Linux/Unix?

		HISTTIMEFORMAT="%d/%m/%y %T "

- Regular Expression: will match one of the first five letters of the alphabet

		[a-eA-E]

- Regular Expression: The -f option in grep lets you specify a file of regular expressions, one per line.

- Regular Expression: The awk variable NR contains the current record number.

- curl supports numeric ranges. This is the full 14 days of unix-mas from 2012:

		curl -Ns http://www.climagic\.org/uxmas/[1-14]

- Skip first 2 fields & print rest of the line on Linux/Unix:

		awk '{ $1=""; $2=""; print}' input

- Automatic Security Updates in RHEL/CentOS 7:

		yum --security update

- The GNU version of date lets you do things like the following:

		date -d "today + 90 days"
		date -d "+90 days"

- Search man pages for a given string:

		man -k string

- Output a file, displaying non-printing characters: 

		cat -v
		cat -A

- Print lines of file without printing ones already seen. $0 means whole line in awk. 'a' is an array:

		awk '!a[$0]++' file

- Use jq to pretty print some json data with ANSI color coded syntax and use -R in less to process the color:

		jq -C '.' data.json | less -R

- Replace all variables $val with $pid in getproc.pl, except on commented lines. *FIXED*:

		sed -i -e '/^\s*#/!s/$val\>/$pid/g' getproc.pl

- Gen 20 random users/passwords:

		for i in {1..20} ; do rig|head -1 |tr A-Z a-z;done |while read f l;do echo ${f:0:1}${l}:$(pwgen 12 1);done

- Quickly create a large file on a linux system:

		fallocate -l 10G 10Gigfile
		truncate -s 10M output.file
		truncate -s 10G output.file
		https://www.cyberciti.biz/faq/howto-create-lage-files-with-dd-command/

- How to reboot a systemd linux box forcefully: 

		systemctl reboot --force --force 

- Shell scripts run in their own subshell, so a cd in a script effects only the subshell. To script a cd, use an alias instead.

- Directly attach screen/tmux over ssh session & save a useless parent bash process:

		ssh -t box screen -r s
		ssh -t box tmux a
		https://github.com/brejoc/ssht 

- alias this to `ssh` and it will (re)open a screen session named like your current user on the remote host:

		#!/usr/bin/env bash

		###
		# call `SSH_SCREEN=1234 ./ssh user@host` to connect to screen 1234
		# for example when there are multiple detached sessions with the same name
		###

		#set -o xtrace #debug

		set -o nounset
		set -o errexit
		set -o pipefail

		/usr/bin/ssh -t $@ "screen -R ${SSH_SCREEN:-${USER}}"

- How the Network Time Protocol will handle the leap second: 

		2016-12-31 23.59.59 
		2016-12-31 23.59.60 <-- leap second 
		2017-01-01 00.00.00

- Analyze your whole lastlog to see the different remote hosts for each user:

		last -da | awk '{print $1 " " $NF}' | sort | uniq -c

- Show top count for col3, 2016-07 - 2017-01:

		sed -n '/^2017-01/,/^2016-06/p' logs.csv |sed '$d' |awk -F, '{print $3}' |sort|uniq -c|sort -rn

- grep gziped log files from .gz files in dirs starting with 2017-01-1 & 1 wild character:
	
		zgrep SSH::Password_Guessing 2017-01-1?/notice.*gz

[![largest open files](images/largest_open_files.png)](https://twitter.com/nixcraft)

<div class="container">
<iframe width="560" height="315" src="https://www.youtube.com/embed/GaAfhO1kpUk?rel=0" frameborder="0" allowfullscreen class="video"></iframe>
</div>
<br/>

<div class="container">
<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/UvZY7bYt2Lo?rel=0" frameborder="0" allowfullscreen class="video"></iframe>
</div>
<br>

<div class="container">
<iframe src="//www.slideshare.net/slideshow/embed_code/key/zyZZiqphwk4WEs" width="668" height="714" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen class="video"> </iframe> <div style="margin-bottom:5px"> <strong> <a href="//www.slideshare.net/prakashrockz/red-hat-lvm-cheatsheet" title="Red hat lvm cheatsheet" target="_blank">Red hat lvm cheatsheet</a> </strong> from <strong><a href="//www.slideshare.net/prakashrockz" target="_blank">Prakash Ghosh</a></strong> </div>
</div>
<br/>

<center>
<blockquote class="imgur-embed-pub" lang="en" data-id="a/Ia5mz"><a href="//imgur.com/a/Ia5mz">Got inspired and made this wallpaper today. Hope you enjoy.</a></blockquote><script async src="//s.imgur.com/min/embed.js" charset="utf-8"></script>
</center>

