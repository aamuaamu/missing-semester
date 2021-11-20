**Job control**
1. From what we have seen, we can use some `ps aux | grep` commands to get our jobs’ pids and then kill them, but there are better ways to do it. Start a `sleep 10000` job in a terminal, background it with `Ctrl-Z` and continue its execution with `bg`. Now use `pgrep` to find its pid and `pkill` to kill it without ever typing the pid itself. (Hint: use the `-af` flags).

    **Solution**
    ```bash
    pgrep -a sleep
    pkill -f sleep
    ```
    
2. Say you don’t want to start a process until another completes. How would you go about it? In this exercise, our limiting process will always be `sleep 60` &. One way to achieve this is to use the `wait` command. Try launching the `sleep` command and having an `ls wait` until the background process finishes.

      **Solution**
      ```bash
      sleep 60 &
      wait %1
      ls
      ```

**Alias**
1. Create an alias `dc` that resolves to `cd` for when you type it wrongly.

      **Solution**
      ```bash
      alias dc=cd
      ```
2. Run `history | awk '{$1="";print substr($0,2)}' | sort | uniq -c | sort -n | tail -n10` to get your top 10 most used commands and consider writing shorter aliases for them. Note: this works for Bash; if you're using ZSH, use `history 1` instead of just `history`.

