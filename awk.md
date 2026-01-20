# **🚀 Complete `awk` Mastery Guide**

## **📚 PART 1: BASIC TUTORIAL**

### **What is `awk`?**
**AWK** = Aho, Weinberger, Kernighan (creators)  
**Purpose**: Pattern scanning and processing language for text files

### **Basic Structure:**
```bash
awk 'pattern { action }' file.txt
```
or
```bash
awk -F delimiter 'pattern { action }' file.txt
```

### **How it Works:**
```
awk reads line → splits into fields ($1, $2, ...) → applies pattern → executes action
```

### **Built-in Variables:**
- `$0` = Entire line
- `$1, $2, ...` = Individual fields
- `NF` = Number of fields in current line
- `NR` = Current line number
- `FS` = Input field separator (default: space)
- `OFS` = Output field separator (default: space)

---

## **🔄 PART 2: ALL VARIATIONS WITH EXAMPLES + PRACTICE Q&A**

### **1. Print Specific Columns**
```bash
echo "John 25 Engineer" | awk '{print $1, $3}'
# Output: John Engineer
```

**Practice Q1:** Extract first and last name from "Jethalal Champaklal Gada"
```bash
echo "Jethalal Champaklal Gada" | awk '{print $1, $3}'
# Output: Jethalal Gada
```

**Practice Q2:** Get only the age from "Name: John Age: 25 City: NY"
```bash
echo "Name: John Age: 25 City: NY" | awk '{print $4}'
# Output: 25
```

---

### **2. Change Field Separator**
```bash
echo "apple,banana,cherry" | awk -F, '{print $2}'
# Output: banana
```

**Practice Q1:** Extract username from /etc/passwd format "root:x:0:0"
```bash
echo "root:x:0:0:root:/root:/bin/bash" | awk -F: '{print $1}'
# Output: root
```

**Practice Q2:** Get domain from email "user@example.com"
```bash
echo "user@example.com" | awk -F@ '{print $2}'
# Output: example.com
```

---

### **3. Print Line Numbers**
```bash
echo -e "apple\nbanana\ncherry" | awk '{print NR, $0}'
# Output:
# 1 apple
# 2 banana
# 3 cherry
```

**Practice Q1:** Add "Line X:" prefix to each line
```bash
echo -e "cat\ndog\nfish" | awk '{print "Line " NR ":", $0}'
# Output:
# Line 1: cat
# Line 2: dog
# Line 3: fish
```

**Practice Q2:** Show only odd-numbered lines
```bash
echo -e "a\nb\nc\nd\ne" | awk 'NR%2==1 {print NR, $0}'
# Output:
# 1 a
# 3 c
# 5 e
```

---

### **4. Print Last Field**
```bash
echo "apple banana cherry mango" | awk '{print $NF}'
# Output: mango
```

**Practice Q1:** Get file extensions "file.txt backup.tar.gz script.sh"
```bash
echo "file.txt backup.tar.gz script.sh" | awk '{print $NF}' | awk -F. '{print $NF}'
# Output: txt gz sh
```

**Practice Q2:** Extract last word from each line
```bash
echo -e "hello world\nawk is powerful\ngood morning" | awk '{print $NF}'
# Output:
# world
# powerful
# morning
```

---

### **5. Conditional Printing**
```bash
echo -e "John 25\nJane 30\nBob 20" | awk '$2 > 25 {print $1}'
# Output: Jane
```

**Practice Q1:** Show names of people older than 21
```bash
echo -e "Jetha 45\nTapu 18\nBhide 50" | awk '$2 > 21 {print $1}'
# Output:
# Jetha
# Bhide
```

**Practice Q2:** Print lines where first field is "error"
```bash
echo -e "error disk full\ninfo backup done\nerror memory low" | awk '$1 == "error"'
# Output:
# error disk full
# error memory low
```

---

### **6. BEGIN and END Blocks**
```bash
echo -e "10\n20\n30" | awk 'BEGIN{sum=0} {sum+=$1} END{print "Sum:", sum}'
# Output: Sum: 60
```

**Practice Q1:** Count total lines in input
```bash
echo -e "apple\nbanana\ncherry" | awk 'END{print "Total lines:", NR}'
# Output: Total lines: 3
```

**Practice Q2:** Add header and footer to output
```bash
echo -e "data1\ndata2" | awk 'BEGIN{print "=== START ==="} {print $0} END{print "=== END ==="}'
# Output:
# === START ===
# data1
# data2
# === END ===
```

---

### **7. String Concatenation**
```bash
echo "Jetha 45" | awk '{print "Name: " $1 ", Age: " $2}'
# Output: Name: Jetha, Age: 45
```

**Practice Q1:** Create sentence from fields
```bash
echo "apple red sweet" | awk '{print "The " $1 " is " $2 " and " $3 "."}'
# Output: The apple is red and sweet.
```

**Practice Q2:** Format as key-value pairs
```bash
echo "name=Jetha age=45 city=Mumbai" | awk '{for(i=1;i<=NF;i++) print $i}'
# Output:
# name=Jetha
# age=45
# city=Mumbai
```

---

### **8. Built-in Functions - length()**
```bash
echo "hello" | awk '{print length($0)}'
# Output: 5
```

**Practice Q1:** Show length of each word
```bash
echo "cat elephant dog" | awk '{for(i=1;i<=NF;i++) print $i, length($i)}'
# Output:
# cat 3
# elephant 8
# dog 3
```

**Practice Q2:** Print only long words (>4 chars)
```bash
echo "I love programming in bash" | awk '{for(i=1;i<=NF;i++) if(length($i)>4) print $i}'
# Output:
# programming
```

---

### **9. Built-in Functions - substr()**
```bash
echo "hello world" | awk '{print substr($0, 1, 5)}'
# Output: hello
```

**Practice Q1:** Extract first 3 characters of each word
```bash
echo "elephant banana cherry" | awk '{for(i=1;i<=NF;i++) print substr($i,1,3)}'
# Output:
# ele
# ban
# che
```

**Practice Q2:** Get last 3 characters
```bash
echo "filename.txt backup.sh" | awk '{print substr($1, length($1)-2)}'
# Output:
# txt
# .sh
```

---

### **10. Built-in Functions - toupper()/tolower()**
```bash
echo "Hello World" | awk '{print toupper($0)}'
# Output: HELLO WORLD
```

**Practice Q1:** Capitalize first letter of each word
```bash
echo "hello world from bash" | awk '{for(i=1;i<=NF;i++) $i=toupper(substr($i,1,1)) substr($i,2)}1'
# Output: Hello World From Bash
```

**Practice Q2:** Convert entire line to lowercase
```bash
echo "HELLO World FROM AWK" | awk '{print tolower($0)}'
# Output: hello world from awk
```

---

### **11. Pattern Matching with ~**
```bash
echo -e "apple pie\nbanana split\napple juice" | awk '/apple/ {print}'
# Output:
# apple pie
# apple juice
```

**Practice Q1:** Find lines containing numbers
```bash
echo -e "error 404\nsuccess\nwarning 500" | awk '/[0-9]/'
# Output:
# error 404
# warning 500
```

**Practice Q2:** Match lines starting with "A" or "a"
```bash
echo -e "apple\nBanana\ncherry\nAvocado" | awk '/^[Aa]/'
# Output:
# apple
# Avocado
```

---

### **12. Field Comparison**
```bash
echo -e "apple 100\nbanana 50\napple 200" | awk '$1 == "apple" {print $2}'
# Output:
# 100
# 200
```

**Practice Q1:** Show products with price > 75
```bash
echo -e "apple 100\nbanana 50\ncherry 80" | awk '$2 > 75 {print $1, $2}'
# Output:
# apple 100
# cherry 80
```

**Practice Q2:** Find duplicate first fields
```bash
echo -e "apple red\nbanana yellow\napple green" | awk 'seen[$1]++ {print "Duplicate:", $1}'
# Output:
# Duplicate: apple
```

---

### **13. Summing Columns**
```bash
echo -e "10\n20\n30" | awk '{sum+=$1} END{print sum}'
# Output: 60
```

**Practice Q1:** Calculate total sales
```bash
echo -e "apple 100\nbanana 50\ncherry 80" | awk '{total+=$2} END{print "Total:", total}'
# Output: Total: 230
```

**Practice Q2:** Average of numbers
```bash
echo -e "10\n20\n30\n40" | awk '{sum+=$1; count++} END{print "Average:", sum/count}'
# Output: Average: 25
```

---

### **14. If-Else Conditions**
```bash
echo -e "John 25\nJane 17\nBob 30" | awk '{if($2 >= 18) print $1, "Adult"; else print $1, "Minor"}'
# Output:
# John Adult
# Jane Minor
# Bob Adult
```

**Practice Q1:** Grade students based on marks
```bash
echo -e "John 85\nJane 45\nBob 70" | awk '{if($2 >= 80) grade="A"; else if($2 >= 60) grade="B"; else grade="C"; print $1, grade}'
# Output:
# John A
# Jane C
# Bob B
```

**Practice Q2:** Check file type by extension
```bash
echo -e "file.txt\nscript.sh\ndata.csv\nimage.jpg" | awk '{if($0 ~ /\.txt$/) print $0, "Text"; else if($0 ~ /\.sh$/) print $0, "Script"; else print $0, "Other"}'
# Output:
# file.txt Text
# script.sh Script
# data.csv Other
# image.jpg Other
```

---

### **15. Arrays in awk**
```bash
echo -e "apple\nbanana\napple\ncherry\nbanana" | awk '{count[$0]++} END{for(item in count) print item, count[item]}'
# Output:
# apple 2
# banana 2
# cherry 1
```

**Practice Q1:** Count word frequency
```bash
echo "apple banana apple cherry banana apple" | awk '{for(i=1;i<=NF;i++) freq[$i]++} END{for(w in freq) print w, freq[w]}'
# Output:
# apple 3
# banana 2
# cherry 1
```

**Practice Q2:** Group by first field
```bash
echo -e "fruit apple\nfruit banana\nveg carrot\nfruit cherry" | awk '{group[$1]=group[$1] $2 " "} END{for(g in group) print g ":", group[g]}'
# Output:
# fruit: apple banana cherry
# veg: carrot
```

---

### **16. While Loop in awk**
```bash
echo "5" | awk '{i=1; while(i<=$1) {print i; i++}}'
# Output:
# 1
# 2
# 3
# 4
# 5
```

**Practice Q1:** Print multiplication table
```bash
echo "3" | awk '{i=1; while(i<=10) {print $1 " x " i " = " $1*i; i++}}'
# Output:
# 3 x 1 = 3
# 3 x 2 = 6
# 3 x 3 = 9
# ...
```

**Practice Q2:** Reverse a string
```bash
echo "hello" | awk '{len=length($0); result=""; while(len>0) {result=result substr($0,len,1); len--} print result}'
# Output: olleh
```

---

### **17. For Loop in awk**
```bash
echo "hello world" | awk '{for(i=1;i<=NF;i++) print "Field", i, ":", $i}'
# Output:
# Field 1 : hello
# Field 2 : world
```

**Practice Q1:** Print characters of a word
```bash
echo "awk" | awk '{for(i=1;i<=length($0);i++) print substr($0,i,1)}'
# Output:
# a
# w
# k
```

**Practice Q2:** Calculate factorial
```bash
echo "5" | awk '{fact=1; for(i=1;i<=$1;i++) fact*=i; print "Factorial:", fact}'
# Output: Factorial: 120
```

---

### **18. Next Command**
```bash
echo -e "apple\n#comment\nbanana\n#ignore\ncherry" | awk '/^#/{next} {print}'
# Output:
# apple
# banana
# cherry
```

**Practice Q1:** Skip empty lines
```bash
echo -e "line1\n\nline2\n  \nline3" | awk '/^[[:space:]]*$/{next} {print NR, $0}'
# Output:
# 1 line1
# 3 line2
# 5 line3
```

**Practice Q2:** Process only valid data
```bash
echo -e "error: x\nok: data1\ninvalid\nok: data2" | awk '!/^ok:/{next} {print $2}'
# Output:
# data1
# data2
```

---

### **19. Multiple Field Separators**
```bash
echo "apple,banana;cherry" | awk -F'[,;]' '{print $1, $2, $3}'
# Output: apple banana cherry
```

**Practice Q1:** Parse log with multiple delimiters
```bash
echo "2024-01-18 10:30:45,ERROR,disk full" | awk -F'[, ]' '{print "Date:", $1, "Level:", $3, "Msg:", $4, $5}'
# Output: Date: 2024-01-18 Level: ERROR Msg: disk full
```

**Practice Q2:** Split by space or colon
```bash
echo "name: John age: 25 city: NY" | awk -F'[: ]' '{print $2, $4, $6}'
# Output: John 25 NY
```

---

### **20. Output Formatting with printf**
```bash
echo -e "apple 100\nbanana 50\ncherry 80" | awk '{printf "%-10s $%5.2f\n", $1, $2}'
# Output:
# apple      $100.00
# banana     $ 50.00
# cherry     $ 80.00
```

**Practice Q1:** Create formatted table
```bash
echo -e "John 25 50000\nJane 30 75000" | awk '{printf "| %-10s | %3d | %8d |\n", $1, $2, $3}'
# Output:
# | John       |  25 |    50000 |
# | Jane       |  30 |    75000 |
```

**Practice Q2:** Align decimal numbers
```bash
echo -e "10.5\n3.14159\n100.0" | awk '{printf "%8.3f\n", $1}'
# Output:
#   10.500
#    3.142
#  100.000
```

---

## **🧪 PART 3: 15 SITUATIONAL Q&A WITH OUTPUT**

### **Q1. Extract IP Addresses from Log**
```bash
echo -e "192.168.1.1 - GET /index\n10.0.0.5 - POST /api" | awk '{print $1}'
# Output:
# 192.168.1.1
# 10.0.0.5
```

### **Q2. Calculate Disk Usage Percentage**
```bash
df -h | awk '/\/$/ {print $5}' | tr -d '%'
# Output: 45 (or whatever your root usage is)
```

### **Q3. Find Largest File in Directory**
```bash
ls -la | awk 'NR>1 && $5 > max {max=$5; file=$9} END{print "Largest:", file, max " bytes"}'
# Output: Largest: video.mp4 104857600 bytes
```

### **Q4. Parse CSV and Sum Column**
```bash
echo -e "apple,100\nbanana,50\ncherry,80" | awk -F, '{sum+=$2} END{print "Total:", sum}'
# Output: Total: 230
```

### **Q5. Convert Date Format**
```bash
echo "18-01-2024" | awk -F- '{print $3"-"$2"-"$1}'
# Output: 2024-01-18
```

### **Q6. Remove Duplicate Lines**
```bash
echo -e "apple\nbanana\napple\ncherry\nbanana" | awk '!seen[$0]++'
# Output:
# apple
# banana
# cherry
```

### **Q7. Count HTTP Status Codes**
```bash
echo -e "200 OK\n404 Not Found\n200 OK\n500 Error" | awk '{count[$1]++} END{for(code in count) print code, count[code]}'
# Output:
# 200 2
# 404 1
# 500 1
```

### **Q8. Extract Email Domains**
```bash
echo -e "user1@example.com\nuser2@test.com\nadmin@example.com" | awk -F@ '{print $2}' | sort | uniq -c
# Output:
# 2 example.com
# 1 test.com
```

### **Q9. Calculate Average Response Time**
```bash
echo -e "request1 150ms\nrequest2 200ms\nrequest3 100ms" | awk '{sum+=gensub(/ms/,"","g",$2)} END{print "Avg:", sum/NR "ms"}'
# Output: Avg: 150ms
```

### **Q10. Format JSON Output**
```bash
echo -e "name age\nJetha 45\nBabita 40" | awk 'NR==1 {split($0,headers)} NR>1 {printf "{"; for(i=1;i<=NF;i++) printf "\"%s\":\"%s\"%s", headers[i], $i, (i<NF?", ":"") ; print "}"}'
# Output:
# {"name":"Jetha","age":"45"}
# {"name":"Babita","age":"40"}
```

### **Q11. Monitor CPU Usage**
```bash
top -bn1 | awk '/^%Cpu/ {print "User:", $2 "%, System:", $4 "%, Idle:", $8 "%"}'
# Output: User: 15.5%, System: 2.3%, Idle: 82.2%
```

### **Q12. Parse Apache Log for 404 Errors**
```bash
# Simulated log
echo -e '192.168.1.1 - [18/Jan/2024] "GET /index.html" 200\n10.0.0.5 - [18/Jan/2024] "GET /missing" 404' | awk '$9 == 404 {print $1, $7, $9}'
# Output: 10.0.0.5 /missing 404
```

### **Q13. Convert Markdown to HTML**
```bash
echo -e "# Title\n## Subtitle\nSome text" | awk '/^# / {gsub(/^# /,""); print "<h1>" $0 "</h1>"} /^## / {gsub(/^## /,""); print "<h2>" $0 "</h2>"} !/^#/ {print "<p>" $0 "</p>"}'
# Output:
# <h1>Title</h1>
# <h2>Subtitle</h2>
# <p>Some text</p>
```

### **Q14. Find Most Frequent Word**
```bash
echo "apple banana apple cherry banana apple mango" | awk '{for(i=1;i<=NF;i++) words[$i]++} END{max=0; for(w in words) if(words[w] > max) {max=words[w]; word=w} print "Most frequent:", word, "(" max " times)"}'
# Output: Most frequent: apple (3 times)
```

### **Q15. Generate SQL INSERT Statements**
```bash
echo -e "Jetha 45 Mumbai\nBabita 40 Mumbai" | awk '{printf "INSERT INTO users (name, age, city) VALUES (\x27%s\x27, %s, \x27%s\x27);\n", $1, $2, $3}'
# Output:
# INSERT INTO users (name, age, city) VALUES ('Jetha', 45, 'Mumbai');
# INSERT INTO users (name, age, city) VALUES ('Babita', 40, 'Mumbai');
```

---

## **🔥 BONUS: 5 ADVANCED CHALLENGES**

### **Challenge 1: Process /etc/passwd**
```bash
awk -F: 'BEGIN{printf "%-15s %-10s %s\n","Username","UID","Shell"} {printf "%-15s %-10s %s\n", $1, $3, $7}' /etc/passwd | head -5
```

### **Challenge 2: Network Interface Stats**
```bash
ifconfig | awk '/^[a-z]/ {interface=$1} /RX packets/ {print interface ": RX " $5 " bytes, TX " $2 " packets"}'
```

### **Challenge 3: Disk Usage by Directory**
```bash
du -sk * | sort -rn | awk 'BEGIN{print "Size\tDirectory"}{if($1>1024) printf "%.1fM\t%s\n", $1/1024, $2; else print $1 "K\t" $2}' | head -10
```

### **Challenge 4: Parse ps output**
```bash
ps aux | awk 'NR>1 {cpu+=$3; mem+=$4; count++} END{printf "Processes: %d\nCPU: %.1f%%\nMemory: %.1f%%\n", count, cpu, mem}'
```

### **Challenge 5: Create HTML Table from CSV**
```bash
echo -e "Name,Age,City\nJetha,45,Mumbai\nBabita,40,Mumbai" | awk -F, 'BEGIN{print "<table border=1>"} NR==1{print "<tr><th>" $1 "</th><th>" $2 "</th><th>" $3 "</th></tr>"} NR>1{print "<tr><td>" $1 "</td><td>" $2 "</td><td>" $3 "</td></tr>"} END{print "</table>"}'
```

---

## **🎯 QUICK REFERENCE CARD**

| Task | Command | Example |
|------|---------|---------|
| **Print columns** | `awk '{print $1,$3}'` | `echo "a b c" | awk '{print $1,$3}'` |
| **Change FS** | `awk -F: '{print $1}'` | `echo "a:b:c" | awk -F: '{print $2}'` |
| **Line numbers** | `awk '{print NR, $0}'` | `echo -e "a\nb" | awk '{print NR, $0}'` |
| **Last field** | `awk '{print $NF}'` | `echo "a b c" | awk '{print $NF}'` |
| **Condition** | `awk '$2 > 10'` | `echo "a 15" | awk '$2 > 10'` |
| **BEGIN/END** | `awk 'BEGIN{} END{}'` | `awk 'END{print NR}' file` |
| **Sum column** | `awk '{sum+=$1} END{print sum}'` | `echo -e "1\n2\n3" | awk '{sum+=$1} END{print sum}'` |
| **String length** | `awk '{print length($0)}'` | `echo "hello" | awk '{print length($0)}'` |
| **Substring** | `awk '{print substr($0,1,3)}'` | `echo "hello" | awk '{print substr($0,1,3)}'` |
| **Case change** | `awk '{print toupper($0)}'` | `echo "hi" | awk '{print toupper($0)}'` |
| **Pattern match** | `awk '/error/'` | `echo "error: x" | awk '/error/'` |
| **If-else** | `awk '{if($1=="a") print "yes"}'` | `echo "a b" | awk '{if($1=="a") print "yes"}'` |
| **Arrays** | `awk '{count[$1]++}'` | `echo -e "a\na\nb" | awk '{count[$0]++} END{for(i in count) print i, count[i]}'` |
| **Loop** | `awk '{for(i=1;i<=NF;i++) print $i}'` | `echo "a b c" | awk '{for(i=1;i<=NF;i++) print $i}'` |
| **printf** | `awk '{printf "%10s\n", $1}'` | `echo "hello" | awk '{printf "%10s\n", $1}'` |

---

## **💡 PRO TIPS**

1. **Use `-F` for non-space delimiters** (comma, colon, tab, etc.)
2. **`$0`** is entire line, **`$1,$2...`** are fields
3. **`NF`** = number of fields, **`NR`** = current line number
4. **Pattern before `{}`** acts as filter: `/error/ {print}`
5. **Use `BEGIN`** for initialization, **`END`** for summary
6. **Arrays are associative** - great for counting/grouping
7. **`next`** skips to next line without executing rest
8. **Combine with other tools** (`sort`, `uniq`, `grep`) for power

---

## **📝 PRACTICE PROJECTS**

1. **Log Analyzer**: Parse web server logs, count status codes, find top IPs
2. **System Monitor**: Process `ps`, `top`, `df` output for dashboard
3. **Data Cleaner**: Fix CSV/TSV files, remove duplicates, validate formats
4. **Report Generator**: Create formatted reports from raw data
5. **Text Transformer**: Convert between formats (JSON↔CSV, Markdown↔HTML)

---

**awk is not just a command, it's a full programming language! Master it and you can process any text data with ease.** 🚀
