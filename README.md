# Code Around the Code

## Some background about me
When I started my Master’s in Data Science (after doing a Bachelor’s in Economics), I realized that even though I could write code, I had no idea how any of it actually *worked* internally. I had inner echoes with a lot of disconnected questions (What’s a shell? Why do things break when I move code to another machine? What are `conda` `git` etc. really?)
Most programming tutorials teach you how to write code. This one focuses on everything around the code — installing software, managing environments, using the terminal, versioning with Git, and running things on remote machines.  It's what I wish I had when I started, and I aim to close the gap.

## Who This Is For

You already know how to write code, run scripts or jupyter notebook for data analysis/modelling.
But you still struggle with things like:

- Setting up environments   
- Understanding what Git and GitHub actually do  
- Using the terminal or shell with any confidence  
- Running code on a remote server, or even understanding how to log in
- Understaning 'clean' and 'production level' code.
---

## How This Guide Works

- Each section starts with a situation.  
  Example: “You join a research lab and are told to SSH into a server. You’ve never done that before.”

- You’ll see real commands, not toy examples — with enough explanation to understand how and why they work.

- At the end of every page, you’ll know what you can now do that you couldn’t before.

No fluff, no jargon. Just a clear path through the ecosystem.


---

## Structure

Part I: Shell and Terminal
- What is a shell, and what happens when you type a command?
- Navigating files and folders (`pwd`, `cd`, `ls`)
- Redirection, piping, and working with output
- Text filtering with `grep`, `awk`, `sed`, etc.

Part II: Packages, Modules, and Environments
- What is a “package” and what is a “module”?
- Package managers: `apt`, `pip`, `conda`, etc.
- Virtual environments and reproducibility

Part III: Git and GitHub
- What Git actually tracks: snapshots, not diffs
- Branching and merging: modeling parallel work
- Pull requests, remotes, and collaboration

Part IV: Working with Remote Machines
- SSH and the public-key model
- Secure file transfer (`scp`, `rsync`)
- Remote dev via VSCode, `tmux`, or `screen`

Part V: Shell Variants and Cross-Platform Work
- Bash, Zsh, Fish, Powershell — what's the difference?
- Common gotchas between Unix and Windows
- Environment variables and quoting rules

Part VI: Containers and Environments
- Why software breaks across machines
- What Docker is and what problems it solves
- Basic Dockerfiles and running containers
- When to use Docker vs. virtual environments

Part VII: Developer Workflows and Tooling
- Project structure and good coding hygiene
- Makefiles and shell scripts for automation
- Pre-commit hooks, linters, and formatters
- Intro to CI/CD (GitHub Actions or GitLab pipelines)

Part VIII: Configuration and Hidden State
- Dotfiles: `.bashrc`, `.zshrc`, `.gitconfig`
- Environment variables and startup behavior
- Aliases and shell customization
- `PATH`, `PYTHONPATH`, and interpreter resolution

Part IX: Debugging and Diagnostics
- Understanding logs and tracebacks
- Checking running processes and memory usage
- File permissions and common permission errors
- Networking diagnostics and tunnel issues

Part X: Code and Project Organization
- Module layout and import resolution
- `requirements.txt`, `pyproject.toml`, `setup.py`
- Separating scripts, notebooks, and libraries
- Naming conventions, documentation, and readmes

---

## Example: Cloning a Repo via SSH

```bash
# Check if you already have SSH keys:
ls ~/.ssh/id_*.pub

# Generate one if you don't:
ssh-keygen -t ed25519 -C "your.email@domain.com"

# Add the public key (~/.ssh/id_ed25519.pub) to your GitHub account

# Test the SSH connection:
ssh -T git@github.com

# Clone your project:
git clone git@github.com:org/repo.git
