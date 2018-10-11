ob Control in ZSH and Bash
All processes in ZSH/Bash under job control are in 3 states: foregrounded, backgrounded and suspended.

* run command in the foreground  
$ command  

* run commend in the background  
$ command &  

  
### show the list of jobs ([job-id] priority status command)  
#### jobs   

* show all running jobs  
$ jobs -r  

* show all stopped jobs  
$ jobs -s  
  
* show all jobs  
$ jobs  
  
* show all jobs with process ids  
$ jobs -l

* show all jobs with process group ids  
$ jobs -p  

* only in ZSH, show all jobs with the directory the started in  
$ jobs -d  

* show status about 1 job  
$ jobs %6  

Once we are running the command, we can suspend by sending the SIGTSTP signal using the keyboard:
$ Ctrl + Z

It will return us to the shell. At this point can do a few things (note that kill is the shell built in kill not the unix kill, which can be accessed via command kill ):

* foreground the job 1 (return it to the foreground)  
$ fg %1  
* background the job 2 (make it continue in the background)  
$ bg %2  

* kill the job 3 (sends SIGTERM, not like Ctrl + C which sends SIGINT)  
$ kill %3  
  
* suspend the job 4 (equal to Ctrl + Z)  
$ kill -TSTP %4  

* continue the job 5 (equal to bg %5)  
$ kill -CONT %5   
  


the above flags can be combined to filter for specific jobs  
Or (using prefix search), which only works with fg or bg, but not kill:  
  
$ fg %command  
$ bg %command  

There are some shortcuts like:  
##### foreground the most recent backgrounded job
%  

##### same thing as above  
%+  

##### foreground the second most recent backgrounded job  
%-  
  
But for best portability across commands, use the job numbers %n where n is the job number.  
  
In ZSH, if you use try to suspend a function operation, it will fork the shell. That function will now be in a totally different process, so any mutation side effects will not be reflected in your shell. This is good of course, because functions should be pure.

To send a signal to all jobs, or kill all of them, use this function:  
  
: '  
killjobs - Run kill on all jobs in a Bash or ZSH shell, allowing one to optionally pass in kill parameters  

Usage: killjobs [zsh-kill-options | bash-kill-options]  
  
With no options, it sends `SIGTERM` to all jobs.  
'
killjobs () {

    local kill_list="$(jobs)"
    if [ -n "$kill_list" ]; then
        # this runs the shell builtin kill, not unix kill, otherwise jobspecs cannot be killed
        # the `$@` list must not be quoted to allow one to pass any number parameters into the kill
        # the kill list must not be quoted to allow the shell builtin kill to recognise them as jobspec parameters
        kill $@ $(sed --regexp-extended --quiet 's/\[([[:digit:]]+)\].*/%\1/gp' <<< "$kill_list" | tr '\n' ' ')
    else
        return 0
    fi

}


link : https://gist.github.com/CMCDragonkai/6084a504b6a7fee270670fc8f5887eb4
