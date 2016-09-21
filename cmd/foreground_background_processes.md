# Bash Foreground/Background Processes

### Managing Foreground Processes

`ctrl-c` sends SIGINT signal to process

`ctrl-z` sends SIGTSTP (suspend)

### Managing Background Processes

`command ping -i 5 google.com &`  starts a background process (begin execution and immediately return to user prompt)

`jobs` to list all background/stopped processes

use `kill %1` to kill process w/ num 1

### Changing Process State

`ctrl-z` + `bg` to start command again in the background (operates on the most recently stopped process)

use `fg` to bring background process to foreground

### Dealing with SIGHUPS

When terminal instance closes - it typically sends SIGHUP signal to all processes tied to the terminal. This tells all processes to terminate because their controlling terminal will soon be unavailable. 

`nohup` command makes the started process immune to the SIGHUP signal. It will then continue running when the terminal closes - now as the child of the init system

    - Each terminal runs its own independent job queue, so the program's job will be killed but not the process. To kill the process, look up its PID with `pgrep -a`

In order to do something similar but not having to declare at time of exection, use `disown -h %1`
    - removes process from job queue. `-h` flag allows for ignoring of SIGHUP but not others. 
