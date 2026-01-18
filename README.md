# Shell-bash-scripting

---

### **Linux OS – Simplified Structure**

**1. Hardware**  
- The physical components of the computer (CPU, RAM, storage, etc.).

**2. Kernel**  
- Written in **C programming language**.  
- Acts as the **core bridge** between hardware and software.  
- Manages resources, memory, processes, and device drivers.

**3. Shell**  
- A **command-line interface (CLI)** for users to interact with the OS.  
- Takes user commands and passes them to the kernel for execution.  
- Examples: Bash, Zsh.

**4. Applications**  
- **User-level programs** (web browsers, text editors, office tools, etc.).  
- Run on top of the OS, using services provided by the kernel via the shell or GUI.

---

### **Key Takeaway**  
The Linux OS follows a **layered architecture**:  
**User** → **Applications** → **Shell** → **Kernel** → **Hardware**  
Each layer communicates with the layer below it, with the Kernel at the center of all operations.

<img width="309" height="437" alt="image" src="https://github.com/user-attachments/assets/1d02628d-47ce-4f08-96c2-41ef8fee3878" />


First Hello World Shell Script**

## **✅ What Just Happened: Step-by-Step Breakdown**

### **1. **Checking Shell Environment**
```bash
echo "hello world"   # Simple command execution in terminal
```
- **Purpose**: Test basic command execution
- **Output**: Shows terminal is working correctly

### **2. **Creating a Text File**
```bash
vim hello.txt        # Open Vim editor to create/modify file
```
**File Content:**
```
This is a new file.
```
- **Tool used**: Vim (text editor)
- **Action**: Created a simple text file

### **3. **Creating Shell Script File**
```bash
vim hello.sh         # Create shell script file
```
**File Content (inferred from execution):**
```bash
#!/bin/bash
echo "Hello world"
```
- **Shebang line** (`#!/bin/bash`): Tells system to use Bash interpreter
- **Script body**: Simple `echo` command

### **4. **Checking File List**
```bash
ls                  # List all files in current directory
ls -lrth            # Detailed listing with human-readable sizes
```
**Key flags used:**
- `-l`: Long format listing
- `-r`: Reverse order (oldest first)
- `-t`: Sort by modification time
- `-h`: Human-readable file sizes

**Directory contents observed:**
```
hello.sh        # Our shell script (32 bytes)
hello.txt       # Our text file (20 bytes)
devops/         # Directory
cloud/          # Directory
story.txt       # Text file (39 bytes)
... etc
```

### **5. **Verifying Bash Path**
```bash
which bash        # Locate bash executable
```
**Output:** `/bin/bash`
- Confirms Bash is installed at standard location
- Used in shebang line for script

### **6. **Making Script Executable**
```bash
chmod +x hello.sh  # Add execute permission
```
**Permission change:**
- Before: `-rw-r--r--` (read/write for owner, read for others)
- After: `-rwxr-xr-x` (execute permission added for all)

**Numeric equivalent:**
- `644` → `755` (owner: rwx, group: r-x, others: r-x)

### **7. **Executing the Script**
```bash
./hello.sh        # Run script from current directory
```
**Output:**
```
Hello world
```
- `./` means "in current directory"
- Without `./`, shell would search in `$PATH` directories

---

## **🎯 KEY CONCEPTS LEARNED**

**File Permissions (Unix/Linux)**
**Symbolic notation:**
```
-rwxr-xr-x
│└─┬──┴─┬──┴─┬──┴── Owner permissions (u)
│  │    │    └─── Group permissions (g)
│  │    └────── Others permissions (o)
│  └────────── File type (- = regular file, d = directory)
```
**Permission types:**
- `r` = read (4)
- `w` = write (2)
- `x` = execute (1)

### **Enhance the Script:**
```bash
#!/bin/bash
# Author: Your Name
# Date: 2024-01-18
# Description: Enhanced hello world script

echo "Hello, $(whoami)!"                    # Show username
echo "Current directory: $(pwd)"            # Show current path
echo "Today is: $(date)"                    # Show current date/time
echo "System: $(uname -s) $(uname -r)"      # Show OS info
```

## **📊 SCRIPT EXECUTION FLOW**
```
User types: ./hello.sh
     ↓
Shell reads first line: #!/bin/bash
     ↓
Shell executes: /bin/bash hello.sh
     ↓
Bash reads script line by line
     ↓
Executes: echo "Hello world"
     ↓
Output displayed in terminal
```


