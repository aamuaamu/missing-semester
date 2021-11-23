1. If you don’t have any past experience with Git, either try reading the first couple chapters of Pro Git or go through a tutorial like Learn Git Branching. As you’re working through it, relate Git commands to the data model.

2. Clone the repository for the class website.
  - Explore the version history by visualizing it as a graph.
  - Who was the last person to modify `README.md`? (Hint: use `git log` with an argument).
  - What was the commit message associated with the last modification to the `collections:` line of `_config.yml`? (Hint: use `git blame` and `git show`).

    **Solution**
    ```bash
    git clone https://github.com/missing-semester/missing-semester
    ```
    ```bash
    cd missing-semester
    git log --all --graph --decorate --oneline > ~/history.txt
    ```
    ```bash
    git log -p README.md
    ```
    ```bash
    git blame _config.yml | grep "collections:" | sed -E 's/([^ ]*) .*$/\1/' | git show 
    ```
   - The visualization of the version history is in ~/history.txt.
   - (As of November 23, 2021) Anish Athalye is the last person to modify README.md on July 27, 2020.
   - The last commit message associated with the last midificaiton to the 'collections:` line of `_config.yml` is: Merge branch 'ds2606/master'

3. One common mistake when learning Git is to commit large files that should not be managed by Git or adding sensitive information. Try adding a file to a repository, making some comits and then deleting that file from history (you may want to look at this).

    ```bash
    git filter-branch --force --index-filter \
    "git rm --cached --ignore-unmatch PATH-TO-YOUR-FILE-WITH-SENSITIVE-DATA" \
    --prune-empty --tag-name-filter cat -- --all
    ```

4. Clone some repository from GitHub, and modify one of its existing files. What happens when you do git stash? What do you see when running git log --all --oneline? Run git stash pop to undo what you did with git stash. In what scenario might this be useful?

5. Like many command line tools, Git provides a configuration file (or dotfile) called ~/.gitconfig. Create an alias in ~/.gitconfig so that when you run git graph, you get the output of git log --all --graph --decorate --oneline. Information about git aliases can be found here.

6. You can define global ignore patterns in ~/.gitignore_global after running git config --global core.excludesfile ~/.gitignore_global. Do this, and set up your global gitignore file to ignore OS-specific or editor-specific temporary files, like .DS_Store.
7. Fork the repository for the class website, find a typo or some other improvement you can make, and submit a pull request on GitHub (you may want to look at this).
