## Code around the code
A tutorial by Lalitha Sivakumar (https://la2pixel.github.io)  

---
### Who This Is For

People who can code, write scripts, build models, analyze data but feel that the surrounding infrastructure often feels like a black box. Whether you're a grad student, early-career data scientist, or research engineer, this guide will help you confidently run, manage, and collaborate on code in real-world setups :)

---

### Structure

| Part | Topic | What's inside? |
|------|-------|---------|
| [Part I](./part1_shell_terminal.md) | Shell and Terminal | Navigate files, redirect output, and automate workflows through pipes and filters. |
| [Part II](./part2_envs.md) | Environments and Packages | Understand virtualenv, `conda`, and system packages. Create reproducible setups. |
| [Part III](./part3_git.md) | Git and GitHub | Track changes, collaborate, and resolve conflicts. Solo and team workflows. |
| [Part IV](./part4_ssh.md) | Remote Machines and SSH | SSH into clusters, transfer files securely, and run remote jobs. |
| [Part V](./part5_shell_variants.md) | Shell Variants & Cross-Platform | `Bash` vs `Zsh`, Windows vs Unix, quoting rules, portability tips. |
| [Part VI](./part6_docker.md) | Containers (Docker) | Build reproducible environments that run anywhere. |
| [Part VII](./part7_workflows.md) | Clean Code and Automation | Use Makefiles, shell scripts, linters, and pre-commit hooks. |
| [Part VIII](./part8_config.md) | Hidden State and Configuration | Understand `.bashrc`, `PATH`, and environment variables. |
| [Part IX](./part9_debugging.md) | Debugging and Diagnostics | Read logs, track processes, and fix environment or permission issues. |
| [Part X](./part10_project_org.md) | Project Organization | Structure notebooks, libraries, and packages for reuse and clarity. |

---

### Add-on Topics

| Topic | What's inside? |
|-------|---------|
| [Networking Essentials](./part11_networking.md) | Basics of IP, ports, firewalls, and SSH tunnels — critical for remote workflows and Docker. |
| [Permissions and Ownership](./part12_permissions.md) | Understand `chmod`, `chown`, and secure file access — especially on shared systems. |
| [Python/R Internals](./part13_internals.md) | How `import` works, how to write packages, and how interpreters find code. |
| [Monitoring and Job Scheduling](./part14_monitoring.md) | Tools like `htop`, `nvidia-smi`, and SLURM to manage resources and jobs. |

---

### Why I Wrote This

When I started my Master’s in [Quantitative Data Science Methods](https://uni-tuebingen.de/fakultaeten/wirtschafts-und-sozialwissenschaftliche-fakultaet/faecher/fachbereich-sozialwissenschaften/methodenzentrum/studium/msc-qds/) (after a Bachelor's in Economics), I could write code but I couldn’t run it anywhere except my laptop. I didn’t know what a shell was, or why code broke across machines. This guide is my attempt to document what I learned and what I wish had been available when I started: not just how to code, but how to operate confidently within the software ecosystem that surrounds the code.

---

## How to Use This

- Browse topics in order, or jump to whatever’s blocking you.
- Each file is standalone, with examples and takeaways.
- Built for people who learn best by doing.
---
