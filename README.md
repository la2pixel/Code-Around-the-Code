# Code Around the Code

### Background
When I started my Master’s in Data Science (after doing a Bachelor’s in Economics), I realized that even though I could write code, I had no idea how any of it actually *worked* internally. Most programming tutorials teach you how to write code. It turned out I wasn’t alone in this. Many data science environment setup tutorials—like the one on DataCamp—focus on installation steps (Python, R, Git, Shell) but don’t explain *why* each tool is essential :contentReference[oaicite:1]{index=1}. Similarly, guides on Git for data scientists cover commands, but often skip the system-level understanding and mental models behind them :contentReference[oaicite:2]{index=2}. This one focuses on everything around the code — installing software, managing environments, using the terminal, versioning with Git, and running things on remote machines.  It's what I wish I had when I started, and I aim to close the gap.

### Who This Is For

You already know how to write code, run scripts or jupyter notebook for data analysis/modelling.
But you still struggle with things like:

- Setting up environments   
- Understanding what Git and GitHub actually do  
- Using the terminal or shell with any confidence  
- Running code on a remote server, or even understanding how to log in
- Understaning 'clean' and 'production level' code.
---

### Part I: Shell and Terminal  
You’re told to “run this command” — but what *is* a shell, and what happens when you hit enter?  
We cover:
- What a shell is and how it interprets commands
- Moving around your file system (`pwd`, `cd`, `ls`)
- Redirecting output, chaining commands, and using pipes
- Filtering large logs or data with `grep`, `awk`, `sed`

---

### Part II: Packages, Modules, and Environments  
You installed a package. Why can’t Python find it? Why do things break when you change machines?  
We unpack:
- The difference between system packages, language modules, and environments
- Tools like `apt`, `pip`, `conda`, and when to use which
- Creating isolated environments for reproducibility

---

### Part III: Git and GitHub  
You cloned a repo, but now you’re told to make a branch, commit, and open a pull request.  
Here we explain:
- How Git tracks changes (not line-by-line diffs, but snapshots)
- What branching actually means, and why it’s powerful
- Collaborating through remotes, forks, and PRs

---

### Part IV: Working with Remote Machines  
You join a team and are asked to SSH into a compute server. You're lost.  
This part covers:
- How SSH works and why key-pairs are needed
- Copying files securely (`scp`, `rsync`)
- Developing remotely with VSCode, `tmux`, or `screen`

---

### Part V: Shell Variants and Cross-Platform Work  
Your script works on your machine but breaks on someone else’s.  
We look at:
- Key differences between Bash, Zsh, Fish, and PowerShell
- Quoting rules, path differences, and environment variables
- How to write portable, cross-platform scripts

---

### Part VI: Containers and Environments  
Your code runs on your laptop but fails in production.  
Here we dig into:
- What containers like Docker do — and why they're useful
- Writing `Dockerfile`s and running isolated containers
- When to use Docker vs. virtual environments

---

### Part VII: Developer Workflows and Tooling  
Your project is growing. How do you stay organized and automate the boring stuff?  
We explore:
- Project layouts and version control hygiene
- Writing Makefiles and shell scripts to automate tasks
- Using linters, formatters, and CI tools like GitHub Actions

---

### Part VIII: Configuration and Hidden State  
Why does your terminal behave differently than your teammate’s?  
We demystify:
- What dotfiles do (`.bashrc`, `.zshrc`, `.gitconfig`)
- How shell startup works and where your aliases live
- How `PATH` and `PYTHONPATH` affect what code runs

---

### Part IX: Debugging and Diagnostics  
Something broke. You have an error message — now what?  
You’ll learn:
- How to interpret logs, tracebacks, and exit codes
- Checking CPU/memory usage and inspecting processes
- Diagnosing file permission or network issues

---

### Part X: Code and Project Organization  
Your code works. How do you structure it for others (and future-you)?  
We cover:
- How Python finds your modules (and what `import` really does)
- Dependency files: `requirements.txt`, `setup.py`, `pyproject.toml`
- Best practices for scripts, notebooks, and libraries
