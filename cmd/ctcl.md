
## Conquering the Command Line - Notes
### Chapter 1
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

### Chapter 2: Ack/Ag (Fast file searching)
* `ag` faster than `ack`, really powerful searching (`ag PATTERN [PATH]`)
* regex by default, use `-Q` for exact pattern
* list of files: `-l`
* scoping to files: `-G` (e.g. `ag PATTERN -lG file_pattern`)
* ignoring certain directories: `--ignore-dir=DIRNAME`
* use .ackrc/.agignore w/ same purpose as .gitignore
* expects stardard input, so compatable w piping e.g. `ps -e | ag forego`
* use `time` to benchmark commands

### Chapter 3: cURL
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

### Chapter 4: Find (Search for files)
* Use to search for files whose path, or name, contains a query term
* `find PATH_TO_SEARCH OPTIONS PATTERN`
* `-name` for filename e.g. `find . -name \*model.rb, -path` for path search
* append `-type d` (dir) or `f (file)`
* `-not` in front of `-path` flag for `!`, (e.g. `find . -not -path \*t\* -type f`)
* find files modified in the last 5 days: `find . -mtime -5`
* find by size: `find . -size +200k`
* `-add` `-delete` `-print` tags for verbose file removal

### Chapter 5: grep (Search in files)
* `grep PATTERN FILE`
* `-c` count occurrences
* multiple files: `grep PATTERN FILE1 FILE2`
* `-R` search recursively
* invert searches w/ `-v`, search for all lines that don't contain

### Chapter 6: Ps
* by default, displays processes that belong to current user, that are associated with the same terminal in which ps is run
* `ps -e` view all processes
* `ps -L` view all column options, and `ps -O [Col options,..]`
* use `-m` to sort by memory usage, `-r` for cpu

### Chapteer 7: Sed
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


### Chapter 8: Tar
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

