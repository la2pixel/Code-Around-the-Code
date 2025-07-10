### Part I: Shell and Terminal

> **Who this is for**:  
You’ve written code in Jupyter or Python scripts, but when someone says "just SSH into the cluster" or "run it from the terminal," you're unsure what to do. This part of the guide helps you understand what the terminal is, how to use it effectively, and how to feel at home in any computing environment — local, remote, or cloud.

---

#### What Is a Shell, really?

A *shell* is a text-based interface to your computer — it lets you run programs, navigate files, and chain together commands. There are many types of shells:

- `bash`: the standard shell on most Unix/Linux systems
- `zsh`: default on newer macOS versions
- `fish`: user-friendly, auto-suggesting shell
- `sh`: a minimal, portable shell
- `PowerShell`: Windows-native shell with its own syntax

Most of this guide assumes you're using `bash` or a bash-compatible shell (`zsh`, `sh`).

---

#### Starting Simple: Opening the Terminal

- On **Linux/macOS**, use `Terminal.app` or `Ctrl+Alt+T`
- On **Windows**, install [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/) or use Git Bash / PowerShell

You'll see a prompt like:

```bash
username@hostname:~$
```

This means: you're logged into your machine, and your current directory is your home folder (`~`).

---

#### Navigation: Moving Around Files and Folders

The first thing to learn is how to **navigate**. Try this:

```bash
pwd            # Shows your current directory
ls             # Lists files in your current folder
cd Documents/  # Changes directory
cd ..          # Moves up one folder
cd ~           # Goes to your home directory
```

*An example where this might come in handy*:  
You're trying to run a file someone shared on Slack — find it with `ls`, navigate to it with `cd`, and check what’s inside using `cat` or `less`.

---

#### Viewing and Reading Files

```bash
cat file.txt         # Print whole file to screen
less file.txt        # View large file one screen at a time
head file.txt        # View first 10 lines
tail -n 50 file.txt  # View last 50 lines
```

Use this to quickly check `.log`, `.csv`, or `.txt` outputs.

---

#### Writing Files and Output Redirection

You can **save output** or redirect it:

```bash
python train.py > out.log           # Save stdout to a file (overwrite)
python train.py >> out.log          # Append to log file
python train.py 2> errors.log       # Save errors (stderr)
python train.py &> combined.log     # Save both stdout and stderr
```

*An example where this might come in handy*:  
- Submitting batch jobs on a cluster  
- Logging progress during a long training run  
- Debugging script errors

---

#### Pipes: Combining Commands Like Lego

Use `|` to **pipe output** of one command into another:

```bash
cat access.log | grep "404"
ps aux | grep python
du -sh * | sort -hr | head
```

- `cat access.log` → reads the file  
- `grep "404"` → filters lines that contain 404 errors  
- `sort -hr` → sorts by size  
- `head` → shows top 10 entries

These let you write expressive and powerful one-liners.

---

#### Understanding Processes and System State

```bash
ps aux               # Show all running processes
top / htop           # Interactive system monitor
kill 12345           # Kill a process by PID
```

Use these when:
- Your code is stuck or using too much memory
- You’re checking if a script is still running

---

#### Variables, Paths, and Environment

Shells let you define temporary variables:

```bash
export DATA_DIR=~/datasets/gpt
cd $DATA_DIR
```

Check your current environment:

```bash
echo $PATH              # List of locations to look for programs
env                     # Full environment variable list
which python            # Shows path to current Python executable
```

---

#### Scripting: Automate Repetitive Work

You can write a `.sh` file:

```bash
#!/bin/bash
echo "Training started"
python train.py --config cfg.yaml
echo "Done"
```

Make it executable:

```bash
chmod +x run.sh
./run.sh
```

Use when:
- Running a workflow with multiple steps
- Repeating the same job many times (e.g. 10 different seeds)

---

#### Search and Filter Like a Pro

##### `grep` — find lines in text

```bash
grep "loss" train.log
grep -i "error" logs/*.log
grep -rn "TODO" src/
```

- `-r`: recursive
- `-n`: show line numbers
- `-i`: ignore case

##### `awk` — filter columns

```bash
awk '{print $2}' scores.txt
awk -F',' '{print $1}' data.csv
```

- `-F','`: use comma as field separator

##### `sed` — find and replace

```bash
sed 's/dog/cat/g' input.txt > output.txt
```

---

#### Real-Life Scenarios

| Situation | What You’ll Do |
|----------|----------------|
| Need to find the highest accuracy in multiple logs | `grep "accuracy" logs/*.log | awk '{print $NF}' | sort -nr | head -1` |
| Copy files from local to remote server | `scp model.pkl user@server.edu:~/models/` |
| Check which Python version is being used | `which python` |
| Count how many `.py` files are in a folder | `find . -name "*.py" | wc -l` |

---

#### Summary

```
+------------------------+
| Terminal / Shell       |
+------------------------+
| cd, ls, pwd            | → Navigate
| >, >>, |, &, 2>        | → Output control
| grep, awk, sed         | → Text processing
| ps, htop, kill         | → Process control
| export, echo $VAR      | → Environment mgmt
| ./script.sh            | → Automation
+------------------------+
```

---

#### What You Can Now Do

✅ Navigate and explore any Unix-like system  
✅ Redirect and save outputs of programs  
✅ Search and filter logs, datasets, and results  
✅ Monitor jobs and understand running processes  
✅ Automate workflows with `.sh` scripts  
✅ Confidently use the terminal in local or remote setups

---

#### Coming Up

Now that you can interact with your system using the shell, we’ll explore how to install, manage, and isolate Python packages — so you can stop worrying about “it works on my machine” errors.

→ [Part II: Packages and Environments](./part-2-packages.md)
