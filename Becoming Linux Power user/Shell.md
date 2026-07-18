# What is a Shell in Linux, and how does it differ from the Kernel?
The Shell is a command-line interpreter (or command processor) that provides a user interface to the Linux operating system. It reads user commands, interprets them, and executes them either directly or by invoking other programs. The shell acts as an intermediary between the user and the kernel by translating human-readable commands into system calls that the kernel can understand.
In contrast, the Kernel is the core component of the Linux operating system. It is a low-level program that manages hardware resources (CPU, memory, I/O devices, etc.), handles process scheduling, memory management, file system operations, and provides essential services through system calls. While the shell is a user-space program that can be replaced or customized (e.g., bash, zsh, fish), the kernel runs in privileged kernel-space mode and is the same for all shells on a given Linux system

# What are the main types of shells available in Linux? Briefly explain the most commonly used ones and their key differences.
The primary types available include Bourne Shell (sh), Bourne Again Shell (bash), Z Shell (zsh), Friendly Interactive Shell (fish), C Shell (csh), and TENEX C Shell (tcsh)
In Linux, shells are broadly categorized into two families:

Bourne family (POSIX-compliant):
sh (Bourne Shell): The original Unix shell, minimalistic and highly portable.
bash (Bourne Again Shell): The most widely used shell on Linux distributions. It is a superset of sh with added features like command-line editing, history, tab completion, arrays, and better scripting capabilities. It is usually the default login shell (/bin/bash).

C-shell family:
csh / tcsh: Syntax similar to C language, popular for interactive features like aliases and job control, but less preferred for scripting due to incompatibilities with Bourne-style scripts.


Other notable modern shells include zsh (Z Shell), which extends bash with powerful autocompletion, plugins, and themes (popular with Oh My Zsh framework), and fish (Friendly Interactive Shell), which focuses on user-friendliness with syntax highlighting and simplified scripting.
Most production Linux systems use bash as the default because of its balance between compatibility and advanced features.

# Explain the difference between Environment Variables and Shell (Local) Variables in Linux. How are they created, viewed, and when should you use each?
The difference between Environment Variables and Shell (Local) Variables lies in their scope—specifically, whether they are passed down to child processes (like scripts or programs launched from that terminal).Key Differences at a GlanceFeatureShell (Local) VariableEnvironment VariableScopeCurrent shell session only.
Current shell AND all its child processes. InheritanceInvisible to scripts/programs you run. Inherited by scripts/programs you run. Naming ConventionUsually lowercase (by convention). 
Usually UPPERCASE (by convention).Primary UseTemporary loops, logic, script-only data.System configurations, paths, API keys.How to Create and Modify Them1. Shell (Local) VariablesThese are restricted to the exact terminal window where you type them.Creation: Type the name directly, with no spaces around the equals sign.
```bash
my_var="Hello World"
```

Use code with caution.Verification: If you open a sub-shell by typing bash, this variable will disappear. Typing exit to return to the parent shell makes it visible again.

2. Environment VariablesThese are promoted so that any program started by this terminal can read them.Creation (Method A): Export an existing local variable.
```bash
my_var="Hello World"
export my_var
```
Use code with caution.Creation (Method B): Create and export it in a single step.
```bash
export MY_ENV_VAR="Universal Data"
```

Use code with caution.Temporary Export: Pass a variable to a single specific command without changing your current shell environment.
```bash
USER_ID=42 ./run_script.sh
```
Use code with caution.How to View ThemView a single variable: Use the echo command with a $ prefix. Works for both types.bashecho $my_var
Use code with caution.List all active Environment Variables: Use printenv or env.
```bash
printenv
```
# Or filter for a specific one:
```bash
printenv MY_ENV_VAR
```
Use code with caution.List all variables (Local + Environment): Use the set command. Because it outputs thousands of lines, it is best to filter it.bashset | grep my_var
Use code with caution.Delete a variable: Use unset to wipe it from memory.
```bash
unset my_var
```

Use code with caution.When to Use EachUse Shell (Local) Variables When:Writing a for loop inside a script where the iterator index doesn't matter outside the loop. 
Storing a temporary file path inside a backup script.Holding intermediate mathematical calculations.Use Environment Variables When:Modifying system behavior, like adding a new folder to your binary executable search path (export PATH=$PATH:/new/folder).Passing configuration secrets to applications (e.g., export DATABASE_URL="mongodb://...").Changing terminal behavior globally, like setting your default text editor (export EDITOR="nano").
