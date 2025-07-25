### Understanding Files, Folders, and Memory  
*A foundational mental model for navigating Unix-like systems*

Before you type a single command, you need to understand how files, folders, memory, and programs actually work under the hood. If you can code but feel lost when things run outside your IDE, this is the gap. This section gives an understanding of what the shell sees and what’s happening when you interact with your machine from the terminal.
After gaining the basic intuition here, if you want the exhaustive list of possible commands, here's [command line reference A-Z](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands) or simply ask Chatgpt for your use case:)

---

#### 1. Storage vs Memory (Disk vs RAM)

Your machine has two kinds of working space:

- **Storage** (long-term): files and folders saved on disk (HDD, SSD), where most shell commands operate.
- **Memory (RAM)** (short-term): when you run a program, it is loaded from disk into the memory.. you don't touch it directly, but you tell programs to read/write files.
---

#### 2. The File System Is a Tree

Every Unix-like system has a *hierarchical file structure*. Think of it like a tree:

```
/                               # root of your system, which is the top level directory
├── home/                       # /home/yourname is your personal workspace, which we can also represent with ~
│   └── yourname/
│       ├── project/            # folders, containing a few files or more folders
│       │   └── model.py        
│       ├── data/
│       └── .bashrc            # hidden configuration files (we will see this later)
├── bin/
├── etc/
└── tmp/

```

---

#### 3. Files Are Just Bytes — Programs Give Them Meaning

A ``.csv`` file is not really a “spreadsheet”, it’s just structured text. a ``.py`` file isn’t code in any functional sense, it’s simply text with Python’s syntax. These files only do something when they’re opened by a program that knows how to interpret them, like Excel or Python respectively. That’s why you can write Python in something as basic as Notepad. The file system doesn’t care- it just stores:
- file name
- file contents (as raw bytes)
- some metadata (size, timestamps, permissions etc)

It’s the program that gives the file its behavior and meaning, like the interpreter, text editor, or spreadsheet software. This is also where tools like IDEs (Integrated Development Environments) and GUIs (Graphical User Interfaces) come in. They don’t change what the file is, but they make it much easier to work with, offering features like syntax highlighting, visualization, and live execution.

> Understanding this is key when working in the terminal: files are just bytes, and meaning only emerges when those bytes are passed to the right program.
---

#### 4. What Happens When You “Run a Program”

When you type something like ```python3 script.py``` on the command line, this is what happens internally:


1. The shell looks for a program called python (using your $PATH -> see right below)
2. It passes ``script.py`` as input
3. It starts a *process* in memory (RAM), which are running programs with a PID (process ID), live in RAM and disappear when done
4. That process runs the Python interpreter
5. It reads your file and does what it says
 
> **Files** are *static*, **processes** are *dynamic*.
---

#### 5. Paths: How You Locate Files

To tell the shell where a file is, you give it a path. There are two types:
##### Absolute Paths (always starts at the root folder /)
For example,

```
/home/yourname/projects/train.py
```

This means: start at the root /, then into home/, then yourname/, then projects/, and open ``train.py``.

##### Relative Paths (start from your current working directory)

To know your current working directory (i.e., the folder you're in right now, just type)

```bash
pwd
```
This should print something like /home/yourname/projects/

Some examples to understand path navigation:

``` bash
./train.py           # 'train.py' in the current folder
../data/file.csv     # go up one folder, then into 'data/', then open 'file.csv'
scripts/run.sh       # go into 'scripts/' subfolder and run 'run.sh'
```

If you were in a different folder — say /home/yourname/tmp/ — the same command would look for a completely different file or break entirely. So it's very important to check your working directory before you start commands. Also, if your script can't find a file, it's probably because your path is wrong, **relative to where you're standing.**

##### Takeaways

> Absolute paths always point to the same file, no matter where you are. Use them for system configs, symlinks, or cross-directory scripting.
> Use relative paths inside projects for portability.
---

####  **6. Navigating the File System**

Now that you know how the file system is structured and how paths work, let’s talk about how to move around in it using the shell. 
The three commands you’ll use constantly are:

- ```pwd```: shows where you are
- ```cd```: moves you somewhere else (It’s the shell equivalent of opening a folder in Finder or Explorer)
- ```ls```: shows what’s in the current folder
    - This shows:
        - ```-l```: long format (permissions, sizes, dates)
        - ```-a```: all files, including hidden ones
        - ```-h```: human-readable sizes (e.g., KB/MB)

##### Move Around with cd

``` bash
cd foldername     # go into a subfolder
cd ..             # 2 dots -> go up one level
cd                # go back home 
cd ~              # same as above
cd -              # jump back to where you were last
```

Here are some examples commands:
```
cd ~/Downloads          # go to Downloads
cd ../data              # go up one level, then into 'data'
cd /etc/nginx           # absolute path to a system folder
cd -                    # toggle back to previous folder
```


##### Tab Completion

Start typing a folder or file name, then hit Tab to auto-complete it. If there are multiple matches, press Tab twice to see them. This saves tons of time and prevents typos, especially in deep folder structures.

##### Rule of thumb

- Think of yourself *standing inside* a folder
- pwd tells you where
- ls shows you what’s there
- cd lets you walk to another folder
- All relative paths are resolved from *where you’re currently standing*

---

#### **7. Viewing and Reading Files ** 

You found a file. Great. Now what?

Before opening VSCode or downloading it from the server — try using shell tools. They’re fast, minimal, and often enough for what you need.

We’ll cover the full range of commands to:
- Dump the file
- Scroll through it
- Look at just the start or end
- Follow it in real time
- Search inside it
- Handle large or binary files

---

##### cat - prints the whole file

bash
cat file.txt


- Works best for short files.
- Dumps everything to the screen.

Caution:
- If the file is huge, your terminal will scroll past it instantly.
- You can pipe it to less or head to control it.

bash
cat long.log | less


---

##### head — View the start of a file

bash
head file.txt


By default, shows the first 10 lines. You can custom specify how many lines to show:

bash
head -n 20 file.txt


You can also combine with cat and pipes:

bash
cat big.csv | head -n 3


---

##### tail — View the end of a file

bash
tail file.txt


Like head, but shows the last 10 lines. You can customize:

bash
tail -n 50 file.txt


Useful when:
- You’re checking the most recent output
- You want to see if a job finished writing results

---

##### tail -f — Follow a file live

bash
tail -f file.log


Use this while a file is being written-- for example, a training script writing logs. It prints new lines as they appear.

Custom: Starts with the last 50 lines, then continues following.
bash
tail -n 50 -f file.log

To stop watching, press Ctrl+C.

---

##### less — View Long Files (Properly)

bash
less file.txt


Why it’s better than cat:
- Scrollable + Searchable (/pattern) + Doesn’t load the whole file into memory

Basic controls:
- q: quit
- space: next page
- b: previous page
- /pattern: search forward
- n: next match
- less is read-only. You’re just viewing.

Tip: pipe any long output into less

bash
ps aux | less


---

##### more — Like less, but worse

bash
more file.txt


You might see this in legacy scripts. It works, but it’s more limited (can’t scroll up easily). Stick to less.

---

#####strings — Read Human-Readable Text from Binary Files

bash
strings binaryfile

This extracts text from files that aren’t plain text — helpful for debugging saved models, weights, or corrupted logs.

---

#### Summary: Which Tool and When?

| Task | Command |
|------|---------|
| Quick check of config file | cat config.yaml |
| Look at first few lines of CSV | head -n 5 data.csv |
| Check last part of a log file | tail train.log |
| Watch logs live while training | tail -f train.log |
| Read through a huge file with search | less long.log |
| Extract readable strings from binary | strings model.bin |

---

### **8. Output Redirection- capture and control output**

By default, anything a command prints shows up in your terminal. But most of the time- especially when running experiments or jobs, you want to save that output to a file. This is called *redirection*. Let’s walk through everything you can do.

##### Basic Redirection: >, >>

bash
python train.py > output.log


This **saves stdout** (regular output) to a file. It overwrites the file if it exists.

To **append** instead of overwrite:

bash
python train.py >> output.log


This is useful for:
- Logging multiple runs
- Appending timestamps or errors

##### Redirecting Errors: 2>

Standard error (stderr) is separate from standard output.

This saves only the errors:

bash
python train.py 2> errors.log


To save both stdout and stderr:

bash
python train.py > out.log 2> err.log


Or combine both into a single file:

bash
python train.py &> full.log     # Bash only


Alternative (more portable):

bash
python train.py > full.log 2>&1


This means: redirect stderr (2>) to wherever stdout (1>) is currently going.

---

##### Redirect Input: < (rare but good to know)

Sometimes you pass input to a program from a file:

bash
some_program < input.txt


Used in:
- Programming contests / scripts that read from stdin
- Some scientific tools and simulations

---

##### Combine with Pipes and Filters

You can redirect and pipe at the same time:

bash
cat logs/*.log | grep "val_loss" > filtered.txt


This:
1. Reads all log files
2. Filters for lines with val_loss
3. Saves the result

---

##### Some edge cases

- If you forget >, your output will scroll by — and might disappear if it’s huge
- If you use > instead of >>, you’ll overwrite logs and lose data
- Always tail your logs to check if things wrote correctly
- Some programs write **only to stderr** — even if it looks like normal output

---

#####  Real Examples You’ll Use

bash
# Save model training logs
python train.py > logs/run1.log

# Save both output and errors
python train.py &> logs/full_run.log

# Append multiple runs to same file
python train.py >> logs/all_runs.log

# Log errors separately
python train.py 2> logs/errors_only.log

# Follow logs live while redirecting from background process
python train.py > logs/out.log 2>&1 &
tail -f logs/out.log

---


#### **9. Pipes and Filters- build your own tools from lego bricks**

If you've ever wished your command-line tools could "just show me the top 10 biggest files" or "find all the failed runs from logs" — this is how you do it. The idea is simple but powerful:

- Use | (pipe) to **pass the output of one command as input to another**
- Combine small, single-purpose tools into flexible, custom workflows

---

##### How to Think About Pipes

Each command reads *from standard input* and writes *to standard output*.  A pipe | takes the output of one and **streams it directly into the next**.
So this:

bash
cat data.txt | grep "error"


Means:
1. cat prints the file
2. grep filters the lines that contain "error"

Same as:

bash
grep "error" data.txt


But piping becomes powerful when you **chain multiple tools**.

---

#### Common Filters You’ll Use with Pipes

Let’s look at the Unix building blocks to filter, sort, summarize, or transform text.

---

##### grep — Filter lines by pattern

bash
grep "val_loss" logs.txt
grep -i "error" *.log          # case-insensitive
grep -r "TODO" src/            # recursive search
grep -rnw . -e "pattern"       # exact word, line numbers


Use it to find:
- Matching log entries
- Keywords in scripts
- Warnings in config files

---

##### sort — Sort lines

bash
sort results.txt
sort -n numbers.txt            # numeric sort
sort -nr scores.txt            # numeric reverse (descending)


Use sort with head to get top-N results.

---

##### uniq — Deduplicate lines

bash
sort items.txt | uniq
uniq -c sorted.txt             # show counts


 uniq only works on consectuive duplicates, so always sort first if needed.

---

###3#  head and tail — Top/bottom N

bash
head -n 5 sorted.txt
tail -n 10 error.log


Use these after sort or grep to focus on recent / best / worst entries.

---

##### wc — Count things

bash
wc -l file.txt                 # line count
wc -w file.txt                 # word count
cat *.py | wc -l               # total lines in all Python files


---

##### cut — Extract columns

bash
cut -d',' -f1,3 data.csv       # first and third columns


-d sets the delimiter (e.g., , or :), -f chooses fields.

---

##### awk — Field-based processing (mini scripting)

bash
awk '{print $2}' scores.txt              # print 2nd column
awk -F',' '{print $1,$3}' file.csv       # with comma delimiter
awk '$3 > 0.8' scores.txt                # filter by value


---

##### Some handy command pipelines

Example (1): Get top 5 largest folders

bash
du -sh * | sort -hr | head -n 5


- du -sh *: show sizes of folders/files
- sort -hr: sort human-readable sizes in reverse
- head -n 5: show top 5

 Example (2): Count failed runs from logs

bash
grep -i "fail" logs/*.log | wc -l


Example (3): Get top 10 accuracy scores from logs

bash
grep "accuracy" *.log | awk '{print $NF}' | sort -nr | head #if accuracy is the last field on each line

#### 🗂 Example: Count Python files in subfolders

bash
find . -name "*.py" | wc -l


---

##### Example: Download, extract, and filter a dataset (in one line)

bash
curl -sO http://example.com/data.csv | awk -F',' '$3 > 0.9' > filtered.csv


### Design rule: think in stages

Each pipe step should do **one thing well**:

bash
[source] | [filter] | [transform] | [sort] | [output]


If something goes wrong, test each stage individually before piping them all together.

---

#### Debugging Tip

Use tee to **split output** — send it to both screen and file:

bash
cat log.txt | tee copy.log | grep "error"


This way you can save the intermediate result *and* keep piping.

---

### Takeaways

- Pipes let you chain simple tools into powerful workflows
- grep, sort, awk, head, cut, uniq are your friends
- Design command chains like data pipelines: clean inputs → filtered data → summarized output
- Once you understand this model, you can inspect, debug, and extract insight from almost any system or dataset using nothing but shell commands

---

####  **10. Processes and System Monitoring**
> Every time you run a command or script, you’re starting a **process**. That process:
- Lives in memory (RAM)
- Gets a unique **PID** (Process ID)
- May use CPU, memory, disk, or GPU
- Can crash, hang, or run forever if something goes wrong
---

##### Job in terminal workflows is: 

- A script or command you’ve started that runs for a while (seconds to hours)
- It might run in the foreground, in the background, or even on a remote machine
- A job may launch one or more processes (e.g., python train.py spawns Python + possibly subprocesses like dataloaders)

Example jobs:
- Training a model
- Downloading a dataset
- Preprocessing files in a batch script

You'll often want to check:
- Is it still running?
- Did it crash?
- Is it using up all my memory or GPU?
- Did it finish writing logs, results, or models?

The rest of this section shows you how to answer those questions.
---

#### What is a Process?

A **process** is just a running instance of a program.

When you run:

bash
python train.py


The shell:
- Finds the python binary
- Loads it into memory
- Passes it your script
- Starts a new process with a PID (e.g., 12345)

When that process ends (normally or with an error), it exits and frees up memory.

---

##### ps — List Current Processes

bash
ps                # basic view (only your current shell session)
ps aux            # full snapshot of all processes
ps -ef            # alternative format (used on some systems)


ps aux output explained:
- USER: who owns it
- PID: process ID
- %CPU / %MEM: usage
- COMMAND: what it’s running

Example:

bash
ps aux | grep python


This shows all processes with "python" in the command.

---

#####  top — Live Process Monitor

bash
top


Live-updating view of running processes.

Controls:
- q: quit
- P: sort by CPU
- M: sort by memory
- k: kill a process (enter PID)
- 1: show CPU cores

---

#### htop — A Better top (if installed)

bash
htop


Way nicer UI:
- Mouse support
- Color-coded bars
- Tree view of processes

Install with:

bash
sudo apt install htop     # Debian/Ubuntu
brew install htop         # macOS


---

#### kill — Stop a Process by PID

bash
kill PID


Example:

bash
kill 12345


This sends **SIGTERM** (soft kill). If that doesn’t work:

bash
kill -9 12345     # force kill (SIGKILL)


---

#####  pkill — Kill by name (No PID Needed)

bash
pkill python


Kills all processes with python in the name. Use carefully!

You can also do:

bash
pkill -f train.py       # full command line match


---

##### killall — Kill all instances of a program

bash
killall python


Same as pkill, but available only on some systems (macOS, some Linux distros).

---

##### time — Measure runtime of a command
bash
time python train.py


Outputs:
- Real (wall time)
- User (CPU time in user space)
- Sys (CPU time in kernel space)

Great for benchmarking scripts.

---

##### jobs — See background/stopped jobs in your shell

bash
jobs


Shows things you started **in this terminal session**, like backgrounded processes.

---

##### ⏮ &, fg, bg —control foreground and background

bash
python train.py &


- Appends & to run in the **background**
- Immediately returns control to your shell

bash
jobs        # list background jobs
fg %1       # bring job 1 to foreground
bg %1       # resume job 1 in background


---

##### ⛓ pstree — Visualize Parent-Child Relationships

bash
pstree -p        # with PIDs
pstree username  # see just your processes


Helpful when debugging subprocesses (e.g., torchrun, mpirun, forks, etc.)

Install with:

bash
sudo apt install pstree


---

##### GPU Processes (if u use CUDA)

bash
nvidia-smi


Shows:
- GPU memory usage
- Active processes
- Who owns them

Kill a rogue GPU process:

bash
kill -9 PID   # from nvidia-smi output


---

##### Zombie Processes

Sometimes ps aux shows [defunct] — these are zombie processes. They’ve finished running but weren’t cleaned up properly.

If your system is clogged with zombies:
- Log out and back in
- Kill the parent process
- Reboot (if all else fails)

---

##### who, w, uptime — Check Logged-In Users (Shared Servers)

bash
who          # who's logged in
w            # who's doing what
uptime       # load averages + active users


This is helpful when:
- You're trying to be polite on a shared server
- You want to see if the machine is under load

---

#####  What to Do If...

| Situation | Command |
|----------|---------|
| My Python script hangs | ps aux | grep python → kill PID |
| Job is running forever | top or htop → check CPU usage |
| GPU is fully used | nvidia-smi |
| I closed the terminal but job is still running | ps aux | grep username |
| A training job silently failed | check tail -f logs/run.log |
| You want to run a script without blocking terminal | python train.py & |
| You want to pause/resume a job | Ctrl+Z → bg / fg |

---

##### Takeaways

- Every program you run is a **process** — it has a PID, uses memory, and can be inspected
- Use ps, top, or htop to see what’s running
- Use kill, pkill, jobs, or nvidia-smi to stop things cleanly
- Foreground/background control (&, fg, bg) lets you run multiple tasks at once
- Knowing how to find and kill stuck jobs will save you hours (and GPUs)

---
→ [Part II: Environments and Packages](./part-2-packages.md)
