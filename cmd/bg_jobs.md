# Unix Background Jobs - Notes
_Source: [http://www.thegeekstuff.com/2010/05/unix-background-job/](http://www.thegeekstuff.com/2010/05/unix-background-job/)_

* Exexcuting a background job
    * Appending `&` to a command runs it in the background
    * e.g. `$ find / -ctime -1 > /tmp/changed-file-list.txt &`

* Sending current foreground job to background
    * `CTRL+Z` will suspend current foreground job
    * `bg` will make that job run in the background

* View all background jobs with `jobs`

* Move background job to foreground with `fg`
    * If multiple background jobs - use `jobs` to list them and `fg %1` (to bring job #1 to foreground)

* Kill specific job with `kill %`
    * e.g. `$kill %2`

