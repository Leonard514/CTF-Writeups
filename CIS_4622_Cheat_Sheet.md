Note: The tables aren't my work, they're from HackTheBox

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
