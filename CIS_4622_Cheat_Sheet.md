**Note: The tables aren't my work, they're from HackTheBox**

# Linux Fundamentals

| **Command** | **Description** |
| --------------|-------------------|
| `man <tool>` | Opens man pages for the specified tool. | 
| `<tool> -h` | Prints the help page of the tool. | 
| `apropos <keyword>` | Searches through man pages' descriptions for instances of a given keyword. | 
| `cat` | Concatenate and print files. |
| `whoami` | Displays current username. | 
| `id` | Returns users identity. | 
| `hostname` | Sets or prints the name of the current host system. | 
| `uname` | Prints operating system name. | 
| `pwd` | Returns working directory name. | 
| `ifconfig` | The `ifconfig` utility is used to assign or view an address to a network interface and/or configure network interface parameters. | 
| `ip` | Ip is a utility to show or manipulate routing, network devices, interfaces, and tunnels. | 
| `netstat` | Shows network status. | 
| `ss` | Another utility to investigate sockets. | 
| `ps` | Shows process status. | 
| `who` | Displays who is logged in. | 
| `env` | Prints environment or sets and executes a command. | 
| `lsblk` | Lists block devices. | 
| `lsusb` | Lists USB devices. | 
| `lsof` | Lists opened files. | 
| `lspci` | Lists PCI devices. | 
| `sudo` | Execute command as a different user. | 
| `su` | The `su` utility requests appropriate user credentials via PAM and switches to that user ID (the default user is the superuser).  A shell is then executed. | 
| `useradd` | Creates a new user or update default new user information. | 
| `userdel` | Deletes a user account and related files. |
| `usermod` | Modifies a user account. | 
| `addgroup` | Adds a group to the system. | 
| `delgroup` | Removes a group from the system. | 
| `passwd` | Changes user password. |
| `dpkg` | Install, remove and configure Debian-based packages. | 
| `apt` | High-level package management command-line utility. | 
| `aptitude` | Alternative to `apt`. | 
| `snap` | Install, remove and configure snap packages. |
| `gem` | Standard package manager for Ruby. | 
| `pip` | Standard package manager for Python. | 
| `git` | Revision control system command-line utility. | 
| `systemctl` | Command-line based service and systemd control manager. |
| `ps` | Prints a snapshot of the current processes. | 
| `journalctl` | Query the systemd journal. | 
| `kill` | Sends a signal to a process. | 
| `bg` | Puts a process into background. |
| `jobs` | Lists all processes that are running in the background. | 
| `fg` | Puts a process into the foreground. | 
| `curl` | Command-line utility to transfer data from or to a server. | 
| `wget` | An alternative to `curl` that downloads files from FTP or HTTP(s) server. |
| `python3 -m http.server` | Starts a Python3 web server on TCP port 8000. | 
| `ls` | Lists directory contents. | 
| `cd` | Changes the directory. |
| `clear` | Clears the terminal. | 
| `touch` | Creates an empty file. |
| `mkdir` | Creates a directory. | 
| `tree` | Lists the contents of a directory recursively. |
| `mv` | Move or rename files or directories. | 
| `cp` | Copy files or directories. |
| `nano` | Terminal based text editor. | 
| `which` | Returns the path to a file or link. |
| `find` | Searches for files in a directory hierarchy. | 
| `updatedb` | Updates the locale database for existing contents on the system. |
| `locate` | Uses the locale database to find contents on the system. | 
| `more` | Pager that is used to read STDOUT or files. |
| `less` | An alternative to `more` with more features. | 
| `head` | Prints the first ten lines of STDOUT or a file. |
| `tail` | Prints the last ten lines of STDOUT or a file. | 
| `sort` | Sorts the contents of STDOUT or a file. |
| `grep` | Searches for specific results that contain given patterns. | 
| `cut` | Removes sections from each line of files. |
| `tr` | Replaces certain characters. | 
| `column` | Command-line based utility that formats its input into multiple columns. |
| `awk` | Pattern scanning and processing language. |
| `sed` | A stream editor for filtering and transforming text. | 
| `wc` | Prints newline, word, and byte counts for a given input. |
| `chmod` | Changes permission of a file or directory. |
| `chown` | Changes the owner and group of a file or directory. |

### Notes for Linux Fundamentals
- Random paths (ex: to a mail directory) may be stored in the environment variables, utilize **env** for this one
- MTU is the maximum transmission unit, or the largest packet size. It can be found utilizing **ifconfig**
- Remember to read manual pages
- **ls -al** works as usual, apparently files have indexes (otherwise known as inodes) stored in a system table. You can view them utilizing the **-i** flag. You can also utilize the **-t** flag to sort by last time modified
- **cd** apparently has a **-** option to cd into the previous directory
- There are some keyboard shortcuts. **CTRL + L** quickly clears the screen, while **CTRL + R** allows for searching the command history for a specific command
- **mkdir** has a **-p** flag that allows for making multiple directories at a time (ex: **mkdir -p CIS_3213/Week_1_Work**
- There is a **tree** command that allows for displaying a file tree
- For **mv** and **cp**, you can specify multiple files. If you specify a directory as the last parameter, you move or copy the files into that directory
- For **find**, there are many options for filetype, filename, owner, filesize, last edit date, etc. Here it is below:

- `find / -type f -name *.conf -user root -size +20k -newermt 2020-03-03 -exec ls -al {} \; 2>/dev/null`

| **Option** | **Description** |
| - | - |
| `-type f` | Hereby, we define the type of the searched object. In this case, 'f' stands for 'file'. |
| `-name *.conf` | With '-name', we indicate the name of the file we are looking for. The asterisk (*) stands for 'all' files with the '.conf' extension. |
| `-user root` | This option filters all files whose owner is the root user. | 
| `-size +20k` | We can then filter all the located files and specify that we only want to see the files that are larger than 20 KiB. |
| `-newermt 2020-03-03` | With this option, we set the date. Only files newer than the specified date will be presented. |
| `-exec ls -al {} \;` | This option executes the specified command, using the curly brackets as placeholders for each result. The backslash escapes the next character from being interpreted by the shell because otherwise, the semicolon would terminate the command and not reach the redirection. |
| `2>/dev/null` | This is a STDERR redirection to the 'null device', which we will come back to in the next section. This redirection ensures that no errors are displayed in the terminal. This redirection must not be an option of the 'find' command. |

- Note to self: Be sure to put any redirection commands a space from anything previous
- There are file descriptors, which are indicators of connections for input/output operations. STDIN is 0, STDOUT is 1, STDERR is 2. You can redirect any of these streams to a file (or /dev/null to get rid of it). For example, if we wanted to direct command output to a file log.txt and errors to another file, we would do `<command> 2>error.txt 1>log.txt`. You can also use just `>` to redirect all remaining output (which may include normal output and errors)
- To redirect to standard input, utilize `<`. For example, `cat < stdout.txt` redirects contents of stdout.txt as STDIN.
- We know about using `>` to overwrite and `>>` to append. Apparently `<<` makes a stream from a file to add to standard input - this ends through an `EOF` (End-Of-File) function.
- **Piping** allows direction of standard output as input to another program. `grep` allows for text filtering, while `wc` allows to count the number of words (or lines, or anything really)
- You can read files via `more` (which leaves text on the terminal) and `less` (which doesn't, but has more options). There's also the typical `head` and `tail`. `sort` sorts the output alphabetically (likely by ASCII value)
- You can utilize `grep` to filter results, the `-v` flag allows for an inverted search
- `cut` splits text by delimeter. Utilize the `-d"<delimiter>"` flag to specify the delimiter and `-f<index_list>` to define which 1-indexed element to access
- `tr` replaces all instances (within the input) of the first string argument with the second string argument
- `column -t` will make tabular columns of output

From this point on I realized it would be better to utilize a tabular format of examples and explanations

| Example | Explanation |
| - | - |
| `cat /etc/passwd \| grep -v "false\\|nologin" \| tr ":" " " \| column -t  \| awk '{print $1, $NF}' \| sed 's/bin/HTB/g' \| wc -l` | Display text of /etc/passwd. Exclude lines with "false" or "nologin", then replace colons with spaces, then display columns in tabular form. Then, only show the first and last columns. Then, substitute 's' bin for HTB (g replaces all matches). Then, display the number of lines (number of matches) |
| `cat /etc/passwd \| grep cry0l1t3` | Display the cry0l1t3 line in /etc/passwd |
| `cat /etc/passwd \| cut -d":" -f1` | Cut /etc/passwd by delimiter :, display first field only (usernames) |
| `cat /etc/passwd \| grep cry0l1t3 \| cut -d":" -f1,3` | Print /etc/passwd, printing only the line with cry0l1t3. Cut by colons and display fields 1 and 3 (the username and uid) |
| `cat /etc/passwd \| grep cry0l1t3 \| cut -d":" -f1,3 \| sed 's/:/,/g'` | Same as above, but all colons replaced with commas |
| `cat /etc/passwd \| tr ":" " " \| column -t \| awk '{print $1, $3, $NF}' \| tr " " ","` | Print /etc/passwd. Replace all colons with spaces. Arrange output tabularly. Then, include only the first, third, and last columns (username, uid, and shell). Replace spaces with commas for csv output. |
| `cat /etc/passwd \| tr ":" " " \| column -t \| awk '{print $1, $3, $NF}' \| tr " " "," \| grep -v "nologin\\|false" ` | Same as above, but excluding lines with nologin or false |
| `cat /etc/passwd \| tr ":" " " \| column -t \| awk '{print $1, $3, $NF}' \| tr " " "," \| grep -v "nologin" \| wc -l` | Similar to above, but only excluding nologin lines this time. Also the output is the number of lines (number of matching users) |


### [Regex Operators](https://www.geeksforgeeks.org/write-regular-expressions/)

To apply these, utilize the -E option in grep
| **Operators** | **Description** |
| - | - |
| `(a)` | The round brackets are used to group parts of a regex. Within the brackets, you can define further patterns which should be processed together. |
| `\[a-z\]` | The square brackets are used to define character classes. Inside the brackets, you can specify a list of characters to search for. |
| `{1,10}` | The curly brackets are used to define quantifiers. Inside the brackets, you can specify a number or a range that indicates how often a previous pattern should be repeated. |
| `\|` | Also called the OR operator and shows results when one of the two expressions matches |
| `.*` | Operates similarly to an AND operator by displaying results only when both expressions are present and match in the specified order |
| `.` | Wildcard character, can be any character |
| `*` | Repeat previous character 0 or more times |
| `^` and `$` | The beginning and end of a string respectively |
| `grep -E "(my\|false)" /etc/passwd` | Grep for all lines containing my OR false in /etc/passwd |
| `grep -E "(my.*false)" /etc/passwd` | Grep for all lines containing my AND false in /etc/passwd |

- Regarding directory permissions, execute permissions are required to traverse; write permissions are required to make, delete, rename files/subdirectories

| Example | Explanation |
| - | - |
| `chmod a+r shell && ls -l shell` | Adds read permissions for all three groups and displays permissions |
| `chmod 754 shell && ls -l shell` | Gives owner all perms, group read and execute, and others read perms. Display perms |
| `chown root:root shell && ls -l shell` | Makes the root user and root group the owner of a file. Display this change |

- Set User ID and Set Group ID bits allow people to run files as other users/groups, and is dangerous as a route for privilege escalation
- The sticky bit ensures that only the owner user or root can delete or rename files. In `ls -l`, a lowercase t means execute permissions are enabled for other users and uppercase T means execute permissions are disabled for other users.
- Regarding packages the Advanced Package Manager (APT) handles dependencies and the sources can often be found in `/etc/apt/sources.list/` or `/etc/apt/sources.list.d`. APT also provides caching of package information


| Example | Explanation |
| - | - |
| `apt-cache search <keyword>` | Searches APT cache - if you put the name of a package, it gives information about that package. |
| `apt list --installed` | Lists installed packages |
| `sudo apt install impacket-scripts -y` | installs package |
| `mkdir ~/nishang/ && git clone https://github.com/samratashok/nishang.git ~/nishang ` | Makes a directory and clones into it |
| `wget http://archive.ubuntu.com/ubuntu/pool/main/s/strace/strace_4.21-1ubuntu1_amd64.deb` | Downloads a package strace from URL |
| `sudo dpkg -i strace_4.21-1ubuntu1_amd64.deb` | Installs from .deb file via dpkg |
| `systemctl start ssh` | Starts the OpenSSH Service |
| `systemctl status ssh` | View information about OpenSSH |
| `systemctl enable ssh` | Add OpenSSH to a SysV service script, which runs SSH on startup |
| `ps -aux \| grep ssh` | View the process running OpenSSH |
| `systemctl list-units --type=service` | List all services |
| `journalctl -u ssh.service --no-pager` | View OpenSSH service error logs |

# Week 1 Class 2 Notes
- Linux starts with the root directory **/**. There is the **/home** for users except root (which has **/root**. The root is the highest privilege - targeted by attackers!
- Usual user accounts should have limited privileges, though they often aren't limited enough (due to bad practice). This is why we have a privilege escalation module!
- **/etc** is where configuration files are (ex: for Apache, databases)
- **/var** includes logs (very important for incident investigation or troubleshooting) and emails, web files, cron jobs
- **/tmp** for temporary files, **/bin** for binaries
- YOU WANT TO COPY THE PATH TABLES TO THIS FILE

- There are multiple Linux distributions for multiple purposes. Some try to resemble Windows
- ParrotOS is our OS, BlackArch is difficult learning curve for cybersecurity, Kali Linux is popular, Ubuntu and CentOS are general

- You utilize the shell. MobaXterm is a terminal emulator with multiple protocols and payment levels (free, premium). Terminals allow multitasking!
- We utilize BASH (Bourne-Again Shell). There are other shells which may have different commands!

- There is a customizable prompt. For **$** it's a regular user, for **#** it's a root/superuser.
- We utilize **sudo** to get elevated privileges

- **man** will get the manual of an application/binary
- **curl** allows use of different protocols to get a webpage. Developers sometimes leave sensitive information in HTML comments!

- These are the common commands. When we first root a system, we need to know the user rights. We utilize **whoami** to learn who we are. We can recon the website to know the user's role (ex: developer role, who have rights to run, patch, execute, write, etc.). We can use the **id** to tell us the user and group membership
- **hostname** gives the hostname of the system. **uname (-a)** gives OS info (ex: release version, date released, hardware platform, etc. Knowing the OS version allows us to go on exploit-db.com and search for an exploit, then copy-paste it into an executable like a script kiddie.
- **pwd** shows the current directory
- **ifconfig** and **ip** shows local network interface configuration. Newer OS utilizes **ip** more
- **netstat** (network statistics) and **ss** (socket statistics). To communicate between devices, end devices make the sockets. Netstat utilizes _Active Internet connections_ for connection to another computer and then _Active UNIX domain sockets_ for inter-process communication
- You can see **who** to see who is logged in, and **env** to see environmental variables (so that we don't have to type the path manually.
- In the environmental variables, the OS sees the **Path** from environmental variables to open executables. In Windows CMD, you use the **set** command instead
- There is user information in **/etc/passwd**, includes usernames, home directories, and shells. **/usr/sbin/nologin** are not users for logging in, but for applications to use. **/bin/bash** is a shell used for normal users.

- We can use **ls** to list files, **ls -l** to have more details, and **ls -la** to include hidden files (starting with .). **.bash_history** shows command history and possibly credentials. **.bashrc** allows for prompt customization, while **cd** allows to change directory via relative or absolute paths
- Files have inode references, which are OS references to allow for location of files in the system
- Old disks have layers of plates with a spinning head, which are split into sectors and tracks. The inode number will show where the file is in the disk. But solid-state drives have many chips of memory where there are grids of data.
- **.bash_logout** executed upon logout

- **touch** utilized to make files. **nano** and **vim** can make and edit files! **vim** requires memorizing different commands
- Pipes **|** allows to redirect output of a command to another command's input

- You can utilize **which** to find the binary of a command
- For **find**, specify the directory to start the search. You can filter by filetype, filename, user owner, filesize, last modified. You can execute a command on the results. You can also send errors (2) to **/dev/null** to remove them. There is also standard input (0) and standard output (1)
- You can utilize **wc** to count lines, words, etc.

- FILTERING CONTENTS (where we're stuck)
- **less** for the whole file, **head** and **tail**, **sort**, **grep**. In **grep**, we can use double quotes to make the characters interpreted literally
- We can utilize **netstat** to see listening services for connections.

- Regular Expressions are for filtering patterns in long strings

# Linux Fundamentals Cont

The filter contents questions are especially hard. Let's start with the third one:
- Private link [here](https://usfedu-my.sharepoint.com/:w:/r/personal/leonardwright_usf_edu/Documents/Spring%202025/CIS%204622/Linux%20Fundamentals/Filter%20Contents.docx?d=w4ecf6db08b554f3f8a032abdc2ac1353&csf=1&web=1&e=Ln2szQ)


- You can kill processes with `kill`, `pkill`, `pgrep`, and `killall`. There are some signals out there:

| **Signal** | **Description** |
| - | - |
| 1 | SIGHUP - This is sent to a process when the terminal that controls it is closed. |
| 2 | SIGINT - Sent when a user presses [Ctrl] + C in the controlling terminal to interrupt a process. |
| 3 | SIGQUIT - Sent when a user presses [Ctrl] + D to quit. |
| 9 | SIGKILL - Immediately kill a process with no clean-up operations. |
| 15 | SIGTERM - Program termination. |
| 19 | SIGSTOP - Stop the program. It cannot be handled anymore. |
| 20 | SIGTSTP - Sent when a user presses [Ctrl] + Z to request for a service to suspend. The user can handle it afterward. |

| **Command** | **Description** |
| - | - |
| `kill 9 <PID>` | Forcefully kill process with PID |
| `CTRL + Z` | Puts a process in the background, suspending it |
| `jobs` | View background jobs and their IDs|
| `bg` | Make a process run in the background. Any output prints in the foreground, and CTRL + C does not work until the process is brought to foreground |
| `fg <id>` | Make a process run in the foreground |
| `<command> &` | Runs <command> in the background. |
| `;` | Semicolons can be used to run commands in sequence. If a command fails, subsequent commands are still executed |
| `&&` | Double ampersands can be used to run commands in sequence. If a command fails, subsequent commands are not executed |
| `\|` | Pipes can execute commands in sequence. Output of the first command becomes input of the second command, etc. |

### Task Scheduling

- Apparently services have Type fields. You can see them in the .service files.

The timers are not my work, but from HackTheBox
- You can make a custom service that runs jobs every now and then. Here's how you do that:

```
sudo mkdir /etc/systemd/system/mytimer.timer.d
sudo nano /etc/systemd/system/mytimer.timer
sudo nano /etc/systemd/system/mytimer.service
```

/etc/systemd/system/mytimer.timer
```
[Unit]
Description=My Timer

[Timer]
# Run only once after system boot
OnBootSec=3min
# Run regularly
OnUnitActiveSec=1hour

[Install]
WantedBy=timers.target
```

/etc/systemd/system/mytimer.service
```
[Unit]
Description=My Service

[Service]
ExecStart=/full/path/to/my/script.sh

[Install]
WantedBy=multi-user.target
```

Then run
```
sudo systemctl daemon-reload
sudo systemctl start mytimer.timer
sudo systemctl enable mytimer.timer
```

- Regarding cron, you must make a `crontab` file. There's a special format:

| **Time Frame** | **Description** |
|-|-|
| Minutes (0-59) | This specifies in which minute the task should be executed. |
| Hours (0-23) | This specifies in which hour the task should be executed. |
| Days of month (0-31) | This specifies on which day of the month the task should be executed. |
| Months (1-12) | This specifies in which month the task should be executed. |
| Days of the week (0-7) | This specifies on which day of the week the task should be executed. |

Example crontab:
```
# System Update every 6 hours
0 */6 * * * /path/to/update_software.sh
```

### Network Services - this will need office hours

SSH is what you'd expect. Of course the config files are /etc/ssh/sshd_config

NFS is basically secure FTP. There are some perms:

| **Permissions** | **Description** |
|-|-|
| rw | Gives users and systems read and write permissions to the shared directory. |
| ro | Gives users and systems read-only access to the shared directory. |
| no_root_squash | Prevents the root user on the client from being restricted to the rights of a normal user. |
| root_squash | Restricts the rights of the root user on the client to the rights of a normal user. |
| sync | Synchronizes the transfer of data to ensure that changes are only transferred after they have been saved on the file system. |
| async | Transfers data asynchronously, which makes the transfer faster, but may cause inconsistencies in the file system if changes have not been fully committed. |

NFS commands:
```
# SERVER
mkdir nfs_sharing
echo '/home/desertstargazer/nfs_sharing <**ip_network**>/<**subnet_mask**>(rw,sync,no_root_squash)' >> /etc/exports # may need to chmod /etc/exports for write first
# CLIENT
mkdir ~/target_nfs
mount 10.129.12.17:/home/john/dev_scripts ~/target_nfs
tree ~/target_nfs
```

Apache: install apache2. Config is /etc/apache2/apache2.conf. You may need to get root permissions. Add the following:

```
<Directory /var/www/html>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
</directory>
```

For this to work, you need to host the files in the server and then start the service. You then need to connect to the server's IP via client to access the files. This may require running two VMs on a network!

`sudo python3 -m http.server 443 -b 192.168.159.129`: This allows you to run an HTTP server bound to a specific IP address (of an interface). This may allow VMs to establish a client-server relationship again.

OpenVPN: the package openvpn. The configuration file is **/etc/openvpn/server.conf** or **/etc/openvpn/<username>.conf**
- Utilize `sudo openvpn --config <config file>` to get a file to connect to the server

### Working with Web Services
- Once again apache didn't boot. I tried making /var/logs/apache2, which made it stop crashing the first time, but there still weren't any files. I then purged and reinstalled and couldn't get it to work again
- You can utilize `wget` to download html files, `curl` to just print them
- I eventually got it to work out with two Ubuntu 20 VMs

`python3 -m http.server` starts a server

These other commands start an HTTP server in port 8080:
- `npm install http-server; http-server -p 8080`
- `php -S 127.0.0.1:8080`

### Backup and Restore
- rsync allows for large data backups (because it only transfers changed data each time)
- Duplicity and Deja Dup allows for backups with GUI (rsync as backend)


| **Command** | **Description** |
| `rsync -av /path/to/mydirectory user@backup_server:/path/to/backup/directory` | Backs up a directory to a directory on a (potentially remote) backup directory. -a flag preserves attributes (ex: perms) while -v allows for verbose output |
| `rsync -avz --backup --backup-dir=/path/to/backup/folder --delete /path/to/mydirectory user@backup_server:/path/to/backup/directory` | Backup with -z for compressed backups (faster transfers). --backup makes incremental backups, while --delete will remove files no longer in the source |
| `rsync -av user@remote_host:/path/to/backup/directory /path/to/mydirectory` | Restores backup |
| `rsync -avz -e ssh /path/to/mydirectory user@backup_server:/path/to/backup/directory` | Backs up over SSH |
- You may potentially use cron to automate backups

### File System Management
- There are many file systems (ex: ext2, ext3, ext4, etc.)
- Linux is based on UNIX - an inode table contains metadata for files and directories (incuding perms, ownership, filesize)
- `fdisk` is used to manage physical storage devices (hard disk, SSD). Drives can be partitioned into separate logical units, which can have different file system formats (ext4, NTFS, FAT32)
- `fdisk`, `gpart`, and `GParted` can be used to manage partitions
- Each partition mounted to a specific directory at boot time as defined by **/etc/fstab**

| **Command** | **Description** |
| `ls -il` | Show files with their inode numbers |
| `sudo fdisk -l` | Show disk partitions - they are the device name followed by a number |
| `cat /etc/fstab` | Show file systems mounted at boot |
| `mount` | View currently mounted file systems`
| `sudo mount /dev/sdb1 /mnt/usb` | Mount a USB drive in /dev/sdb1 to /mnt/usb |
| `sudo umount /mnt/usb` | Unmount the USB drive from above. The USB drive must not be used by any processes - using processes must be shut down first |
| `lsof \| grep cry0l1t3` | Search for files opened by user cry0l1t3 |
| `mkswap` | Setup up a swap area on a device. Make sure the swap space is on a separate partition and that it is encrypted to prevent sensitive data disclosure. Swapping is used to write inactive memory to the partition to free up memory. Swaps can also be used for hibernation to store the system state before power off (allowing it to be restored on power on) |
| `swapon` | Use a swap

In **/etc/fstab**, if you want to unmount the USB at shutdown add the line `/dev/sdb1 /mnt/usb ext4 rw,noauto,user 0 0`

### Containerization

We'll start with _Docker_. They are lightweight and not as vulnerable as virtual machines, though breakout is still possible

Installation script:
```
#!/bin/bash

# Preparation
sudo apt update -y
sudo apt install ca-certificates curl gnupg lsb-release -y
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker Engine
sudo apt update -y
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y

# Add user htb-student to the Docker group
sudo usermod -aG docker htb-student
echo '[!] You need to log out and log back in for the group changes to take effect.'

# Test Docker installation
docker run hello-world
```

- You can make Docker images from Dockerfiles. The Dockerfile will contain a bunch of bash commands and must be named **Dockerfile**, here's an example

```
# Use the latest Ubuntu 22.04 LTS as the base image
FROM ubuntu:22.04

# Update the package repository and install the required packages
RUN apt-get update && \
    apt-get install -y \
        apache2 \
        openssh-server \
        && \
    rm -rf /var/lib/apt/lists/*

# Create a new user called "docker-user"
RUN useradd -m docker-user && \
    echo "docker-user:password" | chpasswd

# Give the docker-user user full access to the Apache and SSH services
RUN chown -R docker-user:docker-user /var/www/html && \
    #chown -R docker-user:docker-user /var/run/apache2 && \
    chown -R docker-user:docker-user /var/log/apache2 && \
    #chown -R docker-user:docker-user /var/lock/apache2 && \
    usermod -aG sudo docker-user && \
    echo "docker-user ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# Expose the required ports
EXPOSE 22 80

# Start the SSH and Apache services
CMD service ssh start && /usr/sbin/apache2ctl -D FOREGROUND
```

| **Command** | **Description** |
| `docker build -t fs_docker .` | Build a docker image from a Dockerfile. Apply a tag, which must be in all lowercase. If the Dockerfile has an error somewhere, the docker image doesn't load |
| `docker run -p 8022:22 -p 8080:80 -d FS_docker` | Run a docker image. For the ports, the first is the host port, the second is the port on the docker image. This also utilizes the Docker tag. At this point the image will be visible via `docker ps` |
| `docker ps` | List all running containers |
| `docker stop` | Stop a running container |
| `docker start` | Start a stopped container |
| `docker restart` | Restart a running container |
| `docker rm` | Remove a container |
| `docker rmi` | Remove a Docker image |
| `docker logs` | View the logs of a container |

- Docker containers are immutable, any change made to them while they are running is lost. To make a changed container, you need to modify the Dockerfile and build a new Docker container.

Next, do _Linux Containers (LXC)_. They allow multiple linux systems on the same host! This is lightweight virtualization. Fortunately we can just install `lxc` and `lxc-utils`, but Docker is more user friendly apparently

| **Command** | **Description** |
| - | - |
| `sudo lxc-create -n linuxcontainer -t ubuntu` | Make a new container **linuxcontainer** with a template **ubuntu** |
| `lxc-ls` | List all existing containers |
| `lxc-stop -n <container>` | Stop a running container |
| `lxc-start -n <container>` | Start a stopped container |
| `lxc-restart -n <container>` | Restart a running container |
| `lxc-config -n <container name> -s storage` | Manage container storage |
| `lxc-config -n <container name> -s network` | Manage container network settings |
| `lxc-config -n <container name> -s security` | Manage container security settings |
| `lxc-attach -n <container>` | Connect to a container |
| `lxc-attach -n <container> -f /path/to/share` | Connect to a container and share a specific directory or file |

- Containers allow to quickly penetration test a certain environment or play with malware. You need to secure it though (ex: remove packages on the container or using cgroups to limit CPU resource usage)
- Configuration file is in **/usr/share/lxc/config** and will have the name of the container
- `lxc.cgroup.cpu.shares = 512`: 100% system utilization is 1024, so this puts a cap of 50%
- `lxc.cgroup.memory.limit_in_bytes = 512M`: Self-explanatory. Max 0.5G in RAM
- `sudo systemctl restart lxc.service`: Apply changes

- I still need help with the lxc containers

### Network Configuration

| **Command** | **Description** |
| - | - |
| `ifconfig` | Shows information on each network interface, including IP address, subnet mask, broadcast
| `ip addr` | Same as above in a slightly different format |
| `sudo ifconfig eth0 up` OR `sudo ip link set eth0 up` | Activates the eth0 interface |
| `sudo ifconfig eth0 192.168.1.2` | Assigns IP 192.168.1.2 to interface eth0 |
| `sudo ifconfig eth0 netmask 255.255.255.0` | Assigns subnet mask 255.255.255.0 to interface eth0 |
| `sudo route add default gw 192.168.1.1 eth0` | Assigns 192.168.1.1 as default gateway for eth0 |
| `sudo systemctl restart networking` | Restarts networking to save changes |

Important files

- **/etc/resolv.conf**: configures DNS servers
```
nameserver 8.8.8.8
nameserver 8.8.4.4
```
- **/etc/network/interfaces**: Makes persistent network changes across reboots
```
auto eth0
iface eth0 inet static
  address 192.168.1.2
  netmask 255.255.255.0
  gateway 192.168.1.1
  dns-nameservers 8.8.8.8 8.8.4.4
```

- Discretionary Access Control (DAC): File owners control the read/write/execute/delete permissions to their fiels
- Mandatory Access ControL (MAC): Resources are assigned security levels, and only users cleared for that level or higher can access those resources (govt, healthcare, financial)
- Role-Based Access Control (RBAC): There are roles with permissions. It's basically like groups and permissions in Windows/Linux.
- It's important to monitor and capture network traffic to identify and patch security issues

| **Command** | **Description** |
| - | - |
| `ping <remote host>` | Verify connectivity with remote host. Also shows connection latency |
| `traceroute <remote host>` | Shows route of packets to remote host, including IP addresses and connection latencies for any intermediary routers. Asterisks show the packets may have dropped or ICMP was blocked. |
| `netstat -a` | Display network connections and associated ports. Can identify network activity

- More notes for AppArmor, SELinux, and tcpwrap coming shortly

### Remote Desktop Protocols in Linux
- X11 utilizes protocols to give a Ubuntu GUI. For a Linux computer, there's an X server which utilizes the ports 6000 and 6001-6009, which can help render the local GUI and share files. X11 is in plaintext
- In **/etc/ssh/sshd_config**, setting **X11Forwarding** to **yes** allows for SSH tunneling of X11. You can then execute ssh with the -X option to get GUI. But this is a bad idea because X11 is insecure - attackers can log keystrokes, move the mouse, take screenshots, etc.
- X Display manager Control Protocol (XDMCP) utilizes UDP port 177 to provide remote desktop sessions, but it is insecure and vulnerable to MITM.
- Virtual Network Computing (VNC) is remote desktop and more secure since communication is encrypted and access requires authentication. Some give the remote user the local screen, others utilize virtual sessions (like RDP). VNC usually uses port 5900 and incremented ports

TigerVNC Setup

Server:
| **Command** | **Description** |
| - | - |
| `sudo apt install xfce4 xfce4-goodies tigervnc-standalone-server -y` | Install required packages. TigerVNC needs the XFCE4 desktop manager (not GNOME) |
| `vncpasswd` | Configures a password for the VNC connection |
| `chmod +x ~/.vnc/xstartup` | Makes the file executable |
| `vncserver` | Starts TigerVNC server. Only do this when the two configuration files below are made |
| `vncserver -list` | Lists VNC sessions. You want to note the RFB Port number. |

**~/.vnc/startup**
```
#!/bin/bash
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
/usr/bin/startxfce4
[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
x-window-manager &
```

**~/.vnc/config**
```
geometry=1920x1080
dpi=96
```

Client:
| **Command** | **Description** |
| - | - |
| `ssh -L 5901:127.0.0.1:5901 -N -f -l htb-student <server_ip>` | Any connections to the client's 5901 port will be forwarded (redirected) to the server at port 5901. This is called port forwarding. Enter the password |
| `sudo apt install xtightvncviewer` | Get GUI for VNC viewing |
| `xtightvncviewer localhost:5901` | Connects to local port 5901, which is forwarded to the VNC server by the SSH command. Enter the password and then the GUi for the server will pop up |
