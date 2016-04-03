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
* `ctrl-w` delete last word
* `alt-b` and `alt-f` to move by word
* `history` to see previous commands
* 


### Less
* `h` see commands
* ctrl-f/b to navigate up/down in file
* `/` and `n` to search/cylce results
* `G` pageEnd
* `1G` head

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

