1. For this course, you need to be using a Unix shell like Bash or ZSH. If you are on Linux or macOS, you don’t have to do anything special. If you are on Windows, you need to make sure you are not running cmd.exe or PowerShell; you can use Windows Subsystem for Linux or a Linux virtual machine to use Unix-style command-line tools. To make sure you’re running an appropriate shell, you can try the command `echo $SHELL`. If it says something like `/bin/bash` or `/usr/bin/zsh`, that means you’re running the right program.

2. Create a new directory called missing under `/tmp`.

    **Solution:** 
    ```bash
    mkdir /tmp/missing
    ```

3. Look up the touch program. The man program is your friend.

    **Solution:** 
    ```bash
    man touch
    ```

4. Use touch to create a new file called semester in missing.

   **Solution:** 
   ```bash
   touch /tmp/misssing/semester
   ```
   
5. Write the following into that file, one line at a time:
   ```bash
   #!/bin/sh
   curl --head --silent https://missing.csail.mit.edu
   ```
The first line might be tricky to get working. It’s helpful to know that `#` starts a comment in Bash, and `!` has a special meaning even within double-quoted (") strings. Bash treats single-quoted strings (') differently: they will do the trick in this case. See the Bash quoting manual page for more information.

   **Solution:** 
   ```bash
   cd /tmp/missing
   echo '#!/bin/sh' > semester
   echo 'curl --head --silent https://missing.csail.mit.edu' >> semester
   ```
   
6. Try to execute the file, i.e. type the path to the script (`./semester`) into your shell and press enter. Understand why it doesn’t work by consulting the output of `ls` (hint: look at the permission bits of the file).

   **Solution:** 
   On inspection of the following line in the output of `ls -l`:
   ```dash
   -rw-r--r-- l angela angela 0 Nov 15 19:55: semester
   ```
   one can see that the current user (angela) does not have permission to execute the file `semester`. 
   
7. Run the command by explicitly starting the `sh` interpreter, and giving it the file semester as the first argument, i.e. `sh semester`. Why does this work, while `./semester` didn’t?

   **Solution:** 
   The line 
   ```bash
   sh semester
   ```
   passes the argument `semester` to the command `sh`. Since the user has execution premission for `sh`, the above line works. 
   
8. Look up the `chmod` program (e.g. use `man chmod`).

   **Solution:** 
   ```bash
   man chmod
   ```
   (See [4] for a better explanation of permission and `chmod`.)
   
9. Use `chmod` to make it possible to run the `command ./semester` rather than having to type sh semester. How does your shell know that the file is supposed to be interpreted using `sh`? See this page on the shebang line for more information.

   **Solution:** 
   ```bash
   chmod u+x semester
   ```
   
10. Use `|` and `>` to write the “last modified” date output by semester into a file called `last-modified.txt` in your home directory.

   **Solution:** 
   ```bash
   date -r semester > last-modified.txt
   ```
   (See [5] for reference.)
   
11. Write a command that reads out your laptop battery’s power level or your desktop machine’s CPU temperature from `/sys`. Note: if you’re a macOS user, your OS doesn’t have `sysfs`, so you can skip this exercise.

   **Solution:** 
   ```bash
   cat /sys/class/power_supply/BAT1/capacity
   ```
   (See [6] for reference.)
   
 Reference:
 1. On `touch`: https://www.geeksforgeeks.org/touch-command-in-linux-with-examples/
 2. On `cat`: https://www.geeksforgeeks.org/cat-command-in-linux-with-examples/
 3. Difference between `>` and `>>`: https://www.shells.com/l/en-US/tutorial/Difference-between-%E2%80%9C%3E%E2%80%9D-and-%E2%80%9C%3E%3E%E2%80%9D-in-Linux
 4. On `chmod`: https://linuxize.com/post/chmod-command-in-linux/
 5. Get the last-modified date of file: https://superuser.com/questions/737247/get-last-modified-date-of-file-in-linux
 6. How to check the power status: https://www.linuxjournal.com/content/how-check-battery-status-using-linux-command-line
 7. On '|': https://www.redhat.com/sysadmin/pipes-command-line-linux
 8. On 'tail': https://man7.org/linux/man-pages/man1/tail.1.html
