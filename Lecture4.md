1. Take this [short interactive regex tutorial](https://regexone.com/)
2. Find the number of words (in `/usr/share/dict/words`) that contain at least three as and don’t have a 's ending. What are the three most common last two letters of those words? `sed`’s `y` command, or the `tr` program, may help you with case insensitivity. How many of those two-letter combinations are there? And for a challenge: which combinations do not occur?

    **Solution** (I do not have access to the word list, but here is a hypothetical solution assuming one word per line)
    ```bash
    cat /usr/share/dict/words | tr "[A-Z]" "[a-z]" | grep -E ".*a.*a.*a.+" | sed -E "s/.*(..)$/\1" | uniq -c | sort -r | head -n3
    ```
    (`tr "[A-Z]" "[a-z]"` changes all letters to small case, 
     `-E` is for extended regular expression,
     `\1` is the first capture group,
     `uniq -c` displays unique lines, along with the multiplicity of each line)
3. To do in-place substitution it is quite tempting to do something like `sed s/REGEX/SUBSTITUTION/ input.txt > input.txt`. However this is a bad idea, why? Is this particular to `sed`? Use `man sed` to find out how to accomplish this.
    
    **Solution**
     Directly modifying a file without saving a backup of the original file is a bad idea as we risk losing content of the original file.
     
4. Find your average, median, and max system boot time over the last ten boots. Use `journalctl` on Linux and `log show` on macOS, and look for log timestamps near the beginning and end of each boot. 

    **Solution**
    ```bash
    journalctl | grep -E 'Startup finished in .*\+.*' | tail -n10 | sed -E 's/.*= (.*)s.$/\1/' | R --slave -e 'x <- scan(file="stdin", quiet=TRUE); summary(x)'
    ```
