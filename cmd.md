# Misc Bash/Unix/Terminal Notes

* Unix: os built by Bell Labs in 1969, many modern day OSes are based on concepts and standards that came in Unix
* Bash: a shell. A shell is a CLI (vs GUI)

### General
_Command structure: [command][flag/option][argument]_

* ctrl+a/e/r/u to navigate/clear the line
	* ctrl+f/b move forward/backward a character
* `ls -rtlh` "list by reversed time of modif"
* `**` list all subfiles
* `mv [oldfilename] [newfilename]` rename files
* Press tab twice to show matches
* `man [command name]`: view manual of specified command
* `diff` compare two files
* `>>` appeand output to filename
* `cp <old> <new>` copy file
* `which [command]` write path of exec to stndout
* `!!` run previous command
* `!` run last command with those characters
* crtl-r to search previous commands
* `head`/`tail` to inspect first/last 10 lines of file
* `pipe` works by taking stdin as input
* `tail -f` view a file that's actively changing (tailing a log file)
* `ping` speradically ping webpage (check if down)
* `grep` search for substring in file
* `wc` word/line/character count
* `ps aux` view all processes running
* `top` (or improved `htop`) view running process stats
* `kill -15 <pid>` for individual process, `pkill` for all w/ that name
* `echo $PATH` to print path
* `cd -` cd to prev directory
* chaining: `&&`, `;`, or `&&` (only runs next if prev succeeded)
* `cp -r folder_name` copy folder and contents
* `grep -ri query folder_name` scan for string in all files in folder
* `pushd`, `popd`, and `dirs` push, pop, and list directory stack
	* head of stack is pwd
* `apropos` search the whatis database for strings (looks through help files)
* output into command `cd $(dirname $(which rails))`
* `w` to view user stats

### Less
* `h` see commands
* ctrl-f/b to navigate up/down in file
* `/` and `n` to search/cylce results
* `G` pageEnd
* `1G` head

### Linux Sysadmin Basics
* `cut` split input on delimiter
  * e.g. `cat file.txt | cut -d: -f2`
* `sort` sort by first letter on line

#### File Permissions
_e.g. drwxr-xr-x 4 alarm alarm 4.0K Dec 29 04:23 builds_

* (0:file type)(1,3:owner)(4,6:group)(7,9:other)
* `chmod` to change permissions: read (4), write (2), execute (1)
	* e.g. `chmod 777` sets rwxrwxrwx
	* uses octal binary representation, ___, 111 => 7 => rwx
	* `chown` to change owner
	* `chown group`:owner file/dir

#### User Account Management
* /etc/passwd stores all users, login, nonlogin
* e.g. `alarm:x:1000:1000::/home/alarm:/bin/bash`
	* `username:password:uid:groupid:user_folder:default_shell`
* `!` before or in place of password disables login
* /etc/skel is skeleton dir that is copied into each new users home dir

#### Processes
* `init` is first process started, pid 1, spawns startup scripts etc
* niceness rates how nice process is being to others, low priority has high niceness
* all processes created by some other process, except `init`, so they have parent IDs
* signals sent between processes and to kernal to communicate things like death, status
* `kill <pid>`
	* `kill -l` to list all signals: 9 is kill, 15 is terminate
* ctrl c interrupts
* `killall <process>` kill parent and children processes
* processes ultimately want cpu time
	* can be in 4 states: runnable, sleeping, zombie (finished, waiting to pass on data), stopped
	* `nice -n (-20,19)` set niceness. Higher number, lower priority ( use -20 to utilize all cpu on task)
	* `renice <niceness> <pid>` set niceness of existing process
* /proc filesystem
	* has dir for each pid
	* in each dir, files that display info as read

#### cron tasks
* `crontab -l` view table of tasks
* `crontab -e` edit table of tasks
	* tasks are in (min) (hour) (dom) (moy) (wd) (cmd) format
	* stored in /var/spool/cron/crontabs and package specific jobs in /etc/cron.d/
	* system-wide in /etc/crontab, has extra user col
	* dom (date of month) and dow (date of week) are greedy, runs if either is true

#### Using SSH as proxy
  * `ssh -N -D 8090 USER@IP_ADR` no-login ssh on port 8090. Use `localhost` on port 8090 in browser to connect.

### $PATH and environment variables
* `printenv` to view all env variables
* `$PATH` varaible lists all directories bash should search though whenever you give it a command
* `export VARNAME=[var contents]` to export env var
* `unset VARNAME` clear var

### OSx directory structure
* `man hier`
* `/bin` essential commandline binaries - all files and programs need to boot the os and
* `/etc` machine local system config - admin, config, and system files
* `/dev` device files - mount points for attached hardware
* `/sbin` essential system binaries
* `/usr` all non-essential command-line binaries, libararies, header files
* `/tmp` temp files
* `/var` log and other variable content files
* Home directory, '/Users/jakedex' can be represented with ~. This is default initial folder.


### Conquering the command line
#### Chapter 1
* hard links: create and updates and identical copy of the file on disk `ln source_file target_file`
	* only work on current file system
	* target lives on without soruce
* symbolic links: works w directories `ln -s source_file target_file`
	* system creates a small, symbolic file that points to source
* copying multiple files: `cp file1 file2 file3 file4 dir`
* copying directories: `cp -vR dir1 dir2`
* pipe (`|`) redirects output as input for another command
* `>` writes output to file
* `<` reads from file

#### Chapter 2: Ack/Ag (Fast file searching)
* `ag` faster than `ack`, really powerful searching (`ag PATTERN [PATH]`)
* regex by default, use `-Q` for exact pattern
* list of files: `-l`
* scoping to files: `-G` (e.g. `ag PATTERN -lG file_pattern`)
* ignoring certain directories: `--ignore-dir=DIRNAME`
* use .ackrc/.agignore w/ same purpose as .gitignore
* expects stardard input, so compatable w piping e.g. `ps -e | ag forego`
* use `time` to benchmark commands

#### Chapter 3: cURL
  * tool for working w URLs from the command line - can query, post data, FTP, etc
  * `curl -i URL` see info about response
  * `-L` to follow redirect from 302 response
  * `-O` to download file
  * `curl -o FILENAME URL` save to specified file name
  * to make POST request: `curl -X POST URL`
  * PUT is request that uploads data
  * `curl -X POST -d "REQUEST_BODY" URL`
  * to POST/PUT file: `curl -X POST -d @FILENAME URL`
  * http auth: `curl -X POST -u "USER:PASS" URL`
  * to save cookies/header to file for login: `curl -X POST --dump-header FILE_TO_SAVE -u "user1:password1" \quiet-waters-1228.herokuapp.com/login`
    * `curl -b HEADER_FILE URL` pass headers back to the server

#### Chapter 4: Find (Search for files)
* Use to search for files whose path, or name, contains a query term
* `find PATH_TO_SEARCH OPTIONS PATTERN`
* `-name` for filename e.g. `find . -name \*model.rb, -path` for path search
* append `-type d` (dir) or `f (file)`
* `-not` in front of `-path` flag for `!`, (e.g. `find . -not -path \*t\* -type f`)
* find files modified in the last 5 days: `find . -mtime -5`
* find by size: `find . -size +200k`
* `-add` `-delete` `-print` tags for verbose file removal

#### Chapter 5: grep (Search in files)
* `grep PATTERN FILE`
* `-c` count occurrences
* multiple files: `grep PATTERN FILE1 FILE2`
* `-R` search recursively
* invert searches w/ `-v`, search for all lines that don't contain

#### Chapter 6: Ps
* by default, displays processes that belong to current user, that are associated with the same terminal in which ps is run
* `ps -e` view all processes
* `ps -L` view all column options, and `ps -O [Col options,..]`
* use `-m` to sort by memory usage, `-r` for cpu

#### Chapteer 7: Sed
_editor that allows use of pattern matching to search and replace w/in file_

* e.g. `sed "s/regexp/replacement/option" FILE_NAME`
* global replacement `s/regexp/repl/g`
* nth replacement e.g. `s/regexp/repl/3`
* `-i` edit the file in place
  * use `-i.extension`, e.g. `-i.tmp` for a backup file
* to match lines, preceed s/ with regexp
* & variable in the replace section represents a match from the search section
  * e.g. `sed "s/[aeiou]/\u&/g" FIlENAME`
  * use special character \u with & var to manipulate matches
* use `p` option to print only changed lines to console
  * `sed -n '1~2p' FILENAME` print every other line of file to console
  * use d option to delete any lines that match pattern
  * use ; to chain sed commands together e.g. `sed 's/<[^>]*>//g;/^$/d' FILENAME`


#### Chapter 8: Tar
_tape archive_

* tar quickly joins together files into one larger file, while preserving meta-data
* doesn't compress files by default, but does have a flag that will compress w/ gzip
* known as tarballs
* `-c` create basic archive
* `-f` read/save to a file
  * e.g. `tar -cf DEST_FILE.tar SOURCE FILES/FOLDERS`
* `-v` see which files are added to archive
* `-T` and pipe coupled with find to generate list of files and use tar to archive them
  * e.g. `find . -name \*.sketch | tar -cvf ARCHIVE_NAME.tar -T -`
* `-t` view files inside of archive
  * e.g. `tar -tf ARCHIVENAME.tar`
* `-r` append files to archive (they can't already be compressed)
* `-u` update files already in archive

