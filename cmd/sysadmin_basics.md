# Linux Sysadmin Basics - Notes
_Notes on the awesome [Linux Sysadmin Basics](https://www.youtube.com/playlist?list=PLtK75qxsQaMLZSo7KL-PmiRarU7hrpnwK) tutorials_

### Misc
* `cut` split input on delimiter
  * e.g. `cat file.txt | cut -d: -f2`
* `sort` sort by first letter on line

### File Permissions
_e.g. drwxr-xr-x 4 alarm alarm 4.0K Dec 29 04:23 builds_

* (0:file type)(1,3:owner)(4,6:group)(7,9:other)
* `chmod` to change permissions: read (4), write (2), execute (1)
  * e.g. `chmod 777` sets rwxrwxrwx
  * uses octal binary representation, ___, 111 => 7 => rwx
  * `chown` to change owner
  * `chown group`:owner file/dir

### User Account Management
* /etc/passwd stores all users, login, nonlogin
* e.g. `alarm:x:1000:1000::/home/alarm:/bin/bash`
  * `username:password:uid:groupid:user_folder:default_shell`
* `!` before or in place of password disables login
* /etc/skel is skeleton dir that is copied into each new users home dir

### Processes
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

### cron tasks
* `crontab -l` view table of tasks
* `crontab -e` edit table of tasks
  * tasks are in (min) (hour) (dom) (moy) (wd) (cmd) format
  * stored in /var/spool/cron/crontabs and package specific jobs in /etc/cron.d/
  * system-wide in /etc/crontab, has extra user col
  * dom (date of month) and dow (date of week) are greedy, runs if either is true

### Using SSH as proxy
  * `ssh -N -D 8090 USER@IP_ADR` no-login ssh on port 8090. Use `localhost` on port 8090 in browser to connect.

### $PATH and environment variables
* `printenv` to view all env variables
* `$PATH` varaible lists all directories bash should search though whenever you give it a command
* `export VARNAME=[var contents]` to export env var
* `unset VARNAME` clear var
