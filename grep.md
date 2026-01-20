# 📚 **Complete grep Tutorial with Examples, Practice Questions & Real-World Scenarios**

## **PART 1: BASIC GREP TUTORIAL**

### **What is grep?**
`grep` (Global Regular Expression Print) searches for patterns in files/output.

**Basic Syntax:**
```bash
grep [options] pattern [file...]
```

---

## **PART 2: ALL GREP VARIATIONS WITH EXAMPLES & PRACTICE**

### **1. Basic Pattern Search**
```bash
# Search for word in file
grep "error" logfile.txt
```
**Practice Q1:** Find "success" in status.log
```bash
echo -e "error: failed\nsuccess: done\nerror: retry\nsuccess: complete" > status.log
grep "success" status.log
# Output: success: done \n success: complete
```

**Practice Q2:** Find "192.168" in network.log
```bash
echo -e "10.0.0.1 connected\n192.168.1.1 connected\n172.16.0.1 timeout" > network.log
grep "192.168" network.log
# Output: 192.168.1.1 connected
```

---

### **2. Case-Insensitive Search (`-i`)**
```bash
grep -i "error" file.txt  # Finds ERROR, Error, error, etc.
```
**Practice Q1:** Find all "DEBUG" ignoring case
```bash
echo -e "DEBUG: start\nDebug: process\ndebug: end\nINFO: done" > app.log
grep -i "debug" app.log
# Output: DEBUG: start \n Debug: process \n debug: end
```

**Practice Q2:** Find "admin" in any case
```bash
echo -e "Admin user\nNormal user\nADMIN login\nGuest user" > users.txt
grep -i "admin" users.txt
# Output: Admin user \n ADMIN login
```

---

### **3. Invert Match (`-v`) - Lines NOT containing pattern**
```bash
grep -v "success" log.txt  # Show lines without "success"
```
**Practice Q1:** Show lines without "warning"
```bash
echo -e "error: crash\nwarning: memory\ninfo: started\nwarning: disk" > alerts.txt
grep -v "warning" alerts.txt
# Output: error: crash \n info: started
```

**Practice Q2:** Filter out commented lines (starting with #)
```bash
echo -e "# config file\nPORT=8080\n# debug mode\nHOST=localhost" > config.txt
grep -v "^#" config.txt
# Output: PORT=8080 \n HOST=localhost
```

---

### **4. Count Matches (`-c`)**
```bash
grep -c "pattern" file.txt  # Returns count, not lines
```
**Practice Q1:** Count how many errors
```bash
echo -e "error: disk\ninfo: ok\nerror: memory\nwarning: cpu\nerror: network" > system.log
grep -c "error" system.log
# Output: 3
```

**Practice Q2:** Count lines with numbers
```bash
echo -e "user1\nuser2\nadmin\nuser3\nguest" > accounts.txt
grep -c "[0-9]" accounts.txt
# Output: 3  (user1, user2, user3)
```

---

### **5. Show Line Numbers (`-n`)**
```bash
grep -n "error" file.txt  # Shows line numbers with matches
```
**Practice Q1:** Find "TODO" with line numbers
```bash
echo -e "function start()\n# TODO: fix bug\nreturn true\n# TODO: add test" > code.py
grep -n "TODO" code.py
# Output: 2:# TODO: fix bug \n 4:# TODO: add test
```

**Practice Q2:** Find IP addresses with their line numbers
```bash
echo -e "Server started\nIP: 192.168.1.1\nConnected to 10.0.0.1\nFailed: 8.8.8.8" > connections.txt
grep -n "[0-9]\+\.[0-9]\+\.[0-9]\+\.[0-9]\+" connections.txt
# Output: 2:IP: 192.168.1.1 \n 3:Connected to 10.0.0.1 \n 4:Failed: 8.8.8.8
```

---

### **6. Recursive Search (`-r`)**
```bash
grep -r "function" /path/to/dir/  # Search in all files recursively
```
**Practice Q1:** Find all ".py" files containing "import"
```bash
mkdir test_dir
echo "import os" > test_dir/file1.py
echo "def main()" > test_dir/file2.py
echo "import sys" > test_dir/file3.txt
grep -r "import" test_dir/
# Output: test_dir/file1.py:import os \n test_dir/file3.txt:import sys
```

**Practice Q2:** Find "password" in all config files
```bash
echo "PASSWORD=secret" > test_dir/app.conf
echo "user: admin" > test_dir/db.conf
echo "PASSWORD=1234" > test_dir/service.conf
grep -r "PASSWORD" test_dir/
# Output: test_dir/app.conf:PASSWORD=secret \n test_dir/service.conf:PASSWORD=1234
```

---

### **7. Whole Word Search (`-w`)**
```bash
grep -w "error" file.txt  # Matches "error" but not "errors" or "error404"
```
**Practice Q1:** Find exact word "run" not "running" or "rerun"
```bash
echo -e "run the app\nrunning process\nrerun test\nrun again" > commands.txt
grep -w "run" commands.txt
# Output: run the app \n run again
```

**Practice Q2:** Find "port" as whole word
```bash
echo -e "PORT=8080\nREPORT generated\nexport PATH\nairport code" > settings.txt
grep -w "port" settings.txt
# Output: PORT=8080
```

---

### **8. Show Context Lines (`-A`, `-B`, `-C`)**
```bash
grep -A 2 "error" file.txt    # After context (2 lines after match)
grep -B 2 "error" file.txt    # Before context (2 lines before)
grep -C 2 "error" file.txt    # Both (2 lines before & after)
```
**Practice Q1:** Show 1 line before and after "exception"
```bash
echo -e "line1\nline2\nexception occurred\nline4\nline5" > trace.log
grep -C 1 "exception" trace.log
# Output: line2 \n exception occurred \n line4
```

**Practice Q2:** Show 3 lines after "START" marker
```bash
echo -e "BEGIN\nSTART PROCESS\nStep1\nStep2\nStep3\nEND" > workflow.txt
grep -A 3 "START" workflow.txt
# Output: START PROCESS \n Step1 \n Step2 \n Step3
```

---

### **9. Multiple Patterns (`-e`)**
```bash
grep -e "error" -e "warning" -e "fatal" log.txt
```
**Practice Q1:** Find "error" OR "warning" OR "critical"
```bash
echo -e "info: started\nwarning: disk\nerror: memory\ncritical: crash\nnotice: update" > events.log
grep -e "error" -e "warning" -e "critical" events.log
# Output: warning: disk \n error: memory \n critical: crash
```

**Practice Q2:** Find lines with "192.168" OR "10.0"
```bash
echo -e "8.8.8.8\n192.168.1.1\n10.0.0.1\n172.16.0.1" > ips.txt
grep -e "192.168" -e "10.0" ips.txt
# Output: 192.168.1.1 \n 10.0.0.1
```

---

### **10. Fixed Strings (`-F`) - No regex**
```bash
grep -F "error.*" file.txt  # Searches literal "error.*" not regex
```
**Practice Q1:** Find exact string "a.b"
```bash
echo -e "a.b test\na b c\nab process\na.b file" > data.txt
grep -F "a.b" data.txt
# Output: a.b test \n a.b file
```

**Practice Q2:** Find "10.0.0.1" as literal
```bash
echo -e "IP: 10.0.0.1\nRange: 10.0.0.0/24\nGateway: 10.0.0.1" > network.txt
grep -F "10.0.0.1" network.txt
# Output: IP: 10.0.0.1 \n Gateway: 10.0.0.1
```

---

### **11. Perl-Compatible Regex (`-P`) - Advanced patterns**
```bash
grep -P "\d{3}-\d{3}-\d{4}" file.txt  # Matches phone numbers
```
**Practice Q1:** Find dates in YYYY-MM-DD format
```bash
echo -e "Date: 2024-01-18\nEvent: 2023/12/25\nToday: 2024-01-19\nOld: 18-01-2024" > dates.txt
grep -P "\d{4}-\d{2}-\d{2}" dates.txt
# Output: Date: 2024-01-18 \n Today: 2024-01-19
```

**Practice Q2:** Find hexadecimal numbers (0x...)
```bash
echo -e "addr: 0x7ffd\nvalue: 0xFF\ncode: 123\npointer: 0xABCD" > memory.txt
grep -P "0x[0-9A-F]+" memory.txt
# Output: addr: 0x7ffd \n value: 0xFF \n pointer: 0xABCD
```

---

### **12. Only Matching Part (`-o`)**
```bash
grep -o "pattern" file.txt  # Shows only matched part, not whole line
```
**Practice Q1:** Extract only email addresses
```bash
echo -e "Contact: john@example.com\nEmail: jane@test.org\nPhone: 123456" > contacts.txt
grep -o "[a-zA-Z0-9._%+-]\+@[a-zA-Z0-9.-]\+\.[a-zA-Z]\{2,\}" contacts.txt
# Output: john@example.com \n jane@test.org
```

**Practice Q2:** Extract only version numbers
```bash
echo -e "version: 1.2.3\napp v2.0.1\nrelease 3.14" > versions.txt
grep -o "[0-9]\+\.[0-9]\+\.[0-9]\+" versions.txt
# Output: 1.2.3 \n 2.0.1 \n 3.14
```

---

### **13. File Name Only (`-l`)**
```bash
grep -l "pattern" *.txt  # Lists only filenames containing pattern
```
**Practice Q1:** Find which config files contain "password"
```bash
echo "PASSWORD=secret" > config1.txt
echo "USER=admin" > config2.txt
echo "PASSWORD=1234" > config3.txt
grep -l "PASSWORD" *.txt
# Output: config1.txt \n config3.txt
```

**Practice Q2:** Find Python files containing "import os"
```bash
echo "import os" > script1.py
echo "def main():" > script2.py
echo "import os, sys" > script3.py
grep -l "import os" *.py
# Output: script1.py \n script3.py
```

---

### **14. Silent Mode (`-q`) - For scripting**
```bash
if grep -q "error" log.txt; then echo "Found error"; fi
```
**Practice Q1:** Check if file contains "SUCCESS"
```bash
echo -e "error\nwarning\nSUCCESS\ninfo" > result.txt
if grep -q "SUCCESS" result.txt; then echo "Process succeeded"; else echo "Failed"; fi
# Output: Process succeeded
```

**Practice Q2:** Verify config has valid port
```bash
echo "PORT=8080" > server.conf
if grep -q "PORT=[0-9]\+" server.conf; then echo "Valid port config"; fi
# Output: Valid port config
```

---

### **15. Maximum Count (`-m`)**
```bash
grep -m 5 "error" huge.log  # Stop after 5 matches
```
**Practice Q1:** Find first 2 warnings
```bash
echo -e "warning: disk\ninfo: ok\nwarning: memory\nwarning: cpu\nwarning: network" > alerts.log
grep -m 2 "warning" alerts.log
# Output: warning: disk \n warning: memory
```

**Practice Q2:** Get first IP address found
```bash
echo -e "no ip here\nConnected to 192.168.1.1\nAlso 10.0.0.1" > connections.log
grep -m 1 "[0-9]\+\.[0-9]\+\.[0-9]\+\.[0-9]\+" connections.log
# Output: Connected to 192.168.1.1
```

---

## **PART 3: 15 SITUATIONAL QUESTIONS WITH ANSWERS**

### **1. Find all Java method definitions in source files**
```bash
# Find lines like "public void methodName()" or "private String getName()"
grep -r "^\s*\(public\|private\|protected\).*(\s*)" *.java
```

### **2. Check if anyone is logged into the system**
```bash
who | grep -c "^"  # Count logged in users
# OR to see if specific user is logged in
who | grep -q "username" && echo "User is logged in"
```

### **3. Monitor log file for errors in real-time**
```bash
tail -f application.log | grep --line-buffered "ERROR\|CRITICAL\|FAILED"
# Output: Shows errors as they appear in real-time
```

### **4. Find duplicate lines in a file**
```bash
sort file.txt | uniq -d  # Shows only duplicates
# Using grep:
grep -n "^.*$" file.txt | sort | uniq -c | grep -v "^ *1 "
```

### **5. Validate email format in user database**
```bash
grep -P "^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$" emails.txt
# Output: Lists only valid email formats
```

### **6. Find files containing TODO comments**
```bash
grep -r -n -i "todo\|fixme\|xxx" --include="*.{java,py,js}" .
# Output: filename:line: TODO message
```

### **7. Check if port is in use**
```bash
netstat -tulpn | grep ":8080"
# Output: tcp6  0  0 :::8080  :::*  LISTEN  1234/java
```

### **8. Find large files (over 100MB)**
```bash
find . -type f -size +100M -exec ls -lh {} \; | grep -E "^.*\.(log|txt|dat)$"
# Output: -rw-r--r-- 1 user 101M Jan 18 logfile.log
```

### **9. Monitor failed SSH attempts**
```bash
grep "Failed password" /var/log/auth.log | grep -o "from [0-9\.]\+" | cut -d' ' -f2
# Output: List of IPs with failed SSH attempts
```

### **10. Extract SQL queries from application logs**
```bash
grep -P "SELECT|INSERT|UPDATE|DELETE" app.log | grep -v "COUNT\|SUM\|AVG"
# Output: Only DML queries, not aggregate functions
```

### **11. Find memory leaks in Java heap dumps**
```bash
grep -c "java.lang.Object" heapdump.hprof | head -20
# Output: Count of Object instances by class
```

### **12. Check SSL certificate expiration**
```bash
openssl x509 -in certificate.crt -text | grep -A2 -B2 "Not After"
# Output: 
# Not Before: Jan 1 00:00:00 2024 GMT
# Not After : Dec 31 23:59:59 2024 GMT
```

### **13. Find slow database queries**
```bash
grep "duration.*[5-9][0-9]\{2\}\.|duration.*[0-9]\{4,\}" postgresql.log
# Output: Queries taking >500ms or >1000ms
```

### **14. Detect brute force attacks**
```bash
grep "Invalid user" /var/log/secure | awk '{print $10}' | sort | uniq -c | sort -nr | head -10
# Output: Top 10 usernames with failed login attempts
```

### **15. Monitor Kubernetes pod restarts**
```bash
kubectl get pods --all-namespaces | grep -v "Running\|Completed" | grep -E "[0-9]+/[0-9]+"
# Output: Pods not fully running or with restarts
```

---

## **PART 4: QUICK REFERENCE CHEAT SHEET**

```bash
# Most useful combinations:
grep -rn "pattern" .                    # Recursive with line numbers
grep -i "pattern" file                  # Case-insensitive
grep -v "pattern" file                  # Exclude pattern
grep -A3 -B2 "pattern" file             # Context around match
grep -l "pattern" *.txt                 # Only filenames
grep -c "pattern" file                  # Count matches
grep -o "pattern" file                  # Only matching text
grep -P "regex" file                    # Perl regex (advanced)
grep -q "pattern" file                  # Silent for scripts
grep -m5 "pattern" file                 # First 5 matches
grep -E "pattern1|pattern2" file        # Extended regex (OR)
grep -F "exact.text" file               # Fixed string (no regex)
grep -w "word" file                     # Whole word only
grep --color=always "pattern" file      # Highlight matches
```

**Pro Tip:** Combine with other commands:
```bash
ps aux | grep "[j]ava"           # Find Java processes (won't match grep itself)
history | grep "ssh"             # Find ssh commands in history
df -h | grep -E "^/dev/sd"       # Only physical disks
cat /etc/passwd | grep "/bin/bash"  # Users with bash shell
```

**Bhai, yeh complete grep guide hai. Har example try karna, real-world mein kaam ayega! Interview mein bhi puchenge.** 🚀
