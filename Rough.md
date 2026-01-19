# **🚀 Complete `sed` Mastery Guide**

## **📚 PART 1: BASIC TUTORIAL**

### **What is `sed`?**
**Stream Editor** - processes text line-by-line (Read → Modify → Output)

### **Basic Syntax:**
```bash
sed 's/pattern/replacement/flags' file.txt
```
- `s` = substitute command
- `pattern` = text to find
- `replacement` = text to replace with
- `flags` = options (g, i, p, etc.)

### **How it works:**
```
Input → [sed reads line] → [apply command] → [output line] → Repeat
```

---

## **🔄 PART 2: ALL VARIATIONS WITH EXAMPLES + PRACTICE Q&A**

### **1. Basic Substitution**
```bash
echo "hello world" | sed 's/world/universe/'
# Output: hello universe
```

**Practice Q1:** Replace "cat" with "dog" in "I love my cat"
```bash
echo "I love my cat" | sed 's/cat/dog/'
# Output: I love my dog
```

**Practice Q2:** Replace "foo" with "bar" in "foo foo foo"
```bash
echo "foo foo foo" | sed 's/foo/bar/'
# Output: bar foo foo
```

---

### **2. Global Replacement (all occurrences)**
```bash
echo "apple apple apple" | sed 's/apple/orange/g'
# Output: orange orange orange
```

**Practice Q1:** Replace ALL "day" with "night" in "day after day"
```bash
echo "day after day" | sed 's/day/night/g'
# Output: night after night
```

**Practice Q2:** Replace all "a" with "@" in "banana"
```bash
echo "banana" | sed 's/a/@/g'
# Output: b@n@n@
```

---

### **3. Case-Insensitive Replacement**
```bash
echo "Apple apple APPLE" | sed 's/apple/orange/gi'
# Output: orange orange orange
```

**Practice Q1:** Replace all "hello" (any case) with "hi" in "Hello HELLO hello"
```bash
echo "Hello HELLO hello" | sed 's/hello/hi/gi'
# Output: hi hi hi
```

**Practice Q2:** Replace "error" (case-insensitive) with "issue" in "Error: file not found"
```bash
echo "Error: file not found" | sed 's/error/issue/i'
# Output: issue: file not found
```

---

### **4. Replace Nth Occurrence Only**
```bash
echo "apple apple apple apple" | sed 's/apple/orange/2'
# Output: apple orange apple apple
```

**Practice Q1:** Replace only 3rd "the" with "a" in "the the the the"
```bash
echo "the the the the" | sed 's/the/a/3'
# Output: the the a the
```

**Practice Q2:** Replace 2nd "x" with "y" in "xox xox xox"
```bash
echo "xox xox xox" | sed 's/x/y/2'
# Output: xox yox xox
```

---

### **5. Print Only Changed Lines**
```bash
echo -e "apple\nbanana\napple" | sed -n 's/apple/orange/p'
# Output:
# orange
# orange
```

**Practice Q1:** Print only lines where "error" is replaced with "issue"
```bash
echo -e "error: disk full\ninfo: backup done\nerror: memory low" | sed -n 's/error/issue/p'
# Output:
# issue: disk full
# issue: memory low
```

**Practice Q2:** Print lines where numbers are found and replaced
```bash
echo -e "age: 25\nname: john\nscore: 100" | sed -n 's/[0-9]\+/NUM/p'
# Output:
# age: NUM
# score: NUM
```

---

### **6. Delete Lines**
```bash
echo -e "line1\nline2\nline3" | sed '/line2/d'
# Output: line1 \n line3
```

**Practice Q1:** Delete lines containing "debug" from log
```bash
echo -e "error: crash\ninfo: started\ndebug: x=10\nerror: timeout" | sed '/debug/d'
# Output:
# error: crash
# info: started
# error: timeout
```

**Practice Q2:** Delete empty lines
```bash
echo -e "first\n\nsecond\n\nthird" | sed '/^$/d'
# Output:
# first
# second
# third
```

---

### **7. Delete Specific Line Numbers**
```bash
echo -e "A\nB\nC\nD" | sed '2,3d'
# Output: A \n D
```

**Practice Q1:** Delete lines 1-3 from a 5-line file
```bash
echo -e "1\n2\n3\n4\n5" | sed '1,3d'
# Output:
# 4
# 5
```

**Practice Q2:** Delete only line 2
```bash
echo -e "apple\nbanana\ncherry" | sed '2d'
# Output:
# apple
# cherry
```

---

### **8. Add Line Numbers**
```bash
echo -e "apple\nbanana\ncherry" | sed = | sed 'N;s/\n/ /'
# Output:
# 1 apple
# 2 banana  
# 3 cherry
```

**Practice Q1:** Add line numbers in format "Line X:"
```bash
echo -e "cat\ndog\nfish" | sed = | sed 'N;s/\n/: /'
# Output:
# 1: cat
# 2: dog
# 3: fish
```

**Practice Q2:** Add numbers in parentheses
```bash
echo -e "red\ngreen\nblue" | sed = | sed 'N;s/\n/) /'
# Output:
# 1) red
# 2) green
# 3) blue
```

---

### **9. Insert Text Before Line**
```bash
echo -e "line1\nline2" | sed '2 i INSERTED'
# Output:
# line1
# INSERTED
# line2
```

**Practice Q1:** Insert "START" before first line
```bash
echo -e "data1\ndata2" | sed '1 i START'
# Output:
# START
# data1
# data2
```

**Practice Q2:** Insert divider before line 3
```bash
echo -e "a\nb\nc\nd" | sed '3 i -----'
# Output:
# a
# b
# -----
# c
# d
```

---

### **10. Append Text After Line**
```bash
echo -e "line1\nline2" | sed '1 a APPENDED'
# Output:
# line1
# APPENDED
# line2
```

**Practice Q1:** Add "END" after last line
```bash
echo -e "item1\nitem2" | sed '$ a END'
# Output:
# item1
# item2
# END
```

**Practice Q2:** Add blank line after each line
```bash
echo -e "hello\nworld" | sed 'a\ '
# Output:
# hello
# 
# world
# 
```

---

### **11. Change Entire Line**
```bash
echo -e "old line\nanother line" | sed '/old/c NEW LINE'
# Output:
# NEW LINE
# another line
```

**Practice Q1:** Change "error" lines to "FIXED"
```bash
echo -e "info: ok\nerror: disk\nwarning: cpu" | sed '/error/c FIXED'
# Output:
# info: ok
# FIXED
# warning: cpu
```

**Practice Q2:** Change line 2 to "MODIFIED"
```bash
echo -e "first\nsecond\nthird" | sed '2 c MODIFIED'
# Output:
# first
# MODIFIED
# third
```

---

### **12. Multiple Commands**
```bash
echo "hello world" | sed -e 's/hello/Hi/' -e 's/world/Universe/'
# Output: Hi Universe
```

**Practice Q1:** Replace "foo" with "bar" AND "baz" with "qux"
```bash
echo "foo and baz" | sed -e 's/foo/bar/' -e 's/baz/qux/'
# Output: bar and qux
```

**Practice Q2:** Remove spaces AND add parentheses
```bash
echo "hello world" | sed -e 's/ //g' -e 's/.*/(&)/'
# Output: (helloworld)
```

---

### **13. Using Different Delimiters**
```bash
echo "/path/to/file" | sed 's|/path/to|/new/location|'
# Output: /new/location/file
```

**Practice Q1:** Replace dates with | delimiter
```bash
echo "2024/01/18" | sed 's|2024/01/18|2024-01-18|'
# Output: 2024-01-18
```

**Practice Q2:** Replace "C:\Windows" with "/mnt/c"
```bash
echo "C:\\Windows\\System" | sed 's|C:\\Windows|/mnt/c|'
# Output: /mnt/c\System
```

---

### **14. Save Changes to File**
```bash
echo "foo" > test.txt
sed -i 's/foo/bar/' test.txt
cat test.txt
# Output: bar
```

**Practice Q1:** Create backup while editing
```bash
echo "old" > file.txt
sed -i.bak 's/old/new/' file.txt
ls file*
# Output: file.txt file.txt.bak
```

**Practice Q2:** Edit multiple files in place
```bash
echo "hello" > f1.txt; echo "hello" > f2.txt
sed -i 's/hello/world/' f1.txt f2.txt
cat f1.txt f2.txt
# Output: world \n world
```

---

### **15. Extract Range of Lines**
```bash
seq 10 | sed -n '3,7p'
# Output: 3 4 5 6 7
```

**Practice Q1:** Extract lines 5-8 from a file
```bash
echo -e "a\nb\nc\nd\ne\nf\ng\nh\ni\nj" | sed -n '5,8p'
# Output:
# e
# f
# g
# h
```

**Practice Q2:** Print everything except lines 2-4
```bash
seq 6 | sed '2,4d'
# Output:
# 1
# 5
# 6
```

---

### **16. Print Lines Matching Pattern**
```bash
echo -e "error: failed\ninfo: success\nerror: crash" | sed -n '/error/p'
# Output:
# error: failed
# error: crash
```

**Practice Q1:** Show only lines starting with "#"
```bash
echo -e "# comment\ncode\n# another" | sed -n '/^#/p'
# Output:
# # comment
# # another
```

**Practice Q2:** Show lines containing numbers
```bash
echo -e "apple\nbanana2\ncherry\n45" | sed -n '/[0-9]/p'
# Output:
# banana2
# 45
```

---

### **17. Replace with Backreference**
```bash
echo "hello world" | sed 's/\(hello\) world/\1 universe/'
# Output: hello universe
```

**Practice Q1:** Swap two words
```bash
echo "Jetha Babita" | sed 's/\(.*\) \(.*\)/\2 \1/'
# Output: Babita Jetha
```

**Practice Q2:** Duplicate first word
```bash
echo "hello world" | sed 's/\([^ ]*\).*/\1 \1/'
# Output: hello hello
```

---

### **18. Using & (Matched Pattern)**
```bash
echo "price: 100" | sed 's/[0-9]\+/& USD/'
# Output: price: 100 USD
```

**Practice Q1:** Add quotes around all words
```bash
echo "apple banana cherry" | sed 's/[a-z]\+/"&"/g'
# Output: "apple" "banana" "cherry"
```

**Practice Q2:** Wrap numbers in brackets
```bash
echo "age 25 score 100" | sed 's/[0-9]\+/[&]/g'
# Output: age [25] score [100]
```

---

### **19. Transform Case**
```bash
echo "Hello World" | sed 's/.*/\U&/'      # UPPERCASE
# Output: HELLO WORLD

echo "Hello World" | sed 's/.*/\L&/'      # lowercase
# Output: hello world
```

**Practice Q1:** Convert first letter uppercase
```bash
echo "hello world" | sed 's/\b\(.\)/\u\1/g'
# Output: Hello World
```

**Practice Q2:** Make entire sentence lowercase
```bash
echo "HELLO WORLD FROM BASH" | sed 's/.*/\L&/'
# Output: hello world from bash
```

---

### **20. Remove Empty Lines**
```bash
echo -e "line1\n\nline2\n  \nline3" | sed '/^$/d'
# Output: line1 \n line2 \n line3
```

**Practice Q1:** Remove lines with only spaces
```bash
echo -e "hello\n   \nworld\n\t\n" | sed '/^[[:space:]]*$/d'
# Output:
# hello
# world
```

**Practice Q2:** Remove empty lines AND trim spaces
```bash
echo -e "  hello  \n\n  world  " | sed '/^$/d;s/^ *//;s/ *$//'
# Output:
# hello
# world
```

---

## **🧪 PART 3: 15 SITUATIONAL Q&A WITH OUTPUT**

### **Q1. Remove All HTML Tags**
**Task:** Clean HTML to get only text
```bash
echo "<p>Hello <b>World</b></p>" | sed 's/<[^>]*>//g'
# Output: Hello World
```

**Q2. Convert CSV to TSV**
**Task:** Change commas to tabs
```bash
echo "apple,100,red" | sed 's/,/\t/g'
# Output: apple    100    red
```

**Q3. Add Prefix to Each Line**
**Task:** Add line numbers as "Line X: "
```bash
echo -e "apple\nbanana\ncherry" | sed '=;s/^/Line /;N;s/\n/: /'
# Output:
# Line 1: apple
# Line 2: banana
# Line 3: cherry
```

**Q4. Reverse Order of Words**
**Task:** "first second" → "second first"
```bash
echo "Jetha Babita" | sed 's/\(.*\) \(.*\)/\2 \1/'
# Output: Babita Jetha
```

**Q5. Extract Usernames from /etc/passwd**
**Task:** Get only first field (usernames)
```bash
echo -e "root:x:0:0:root:/root:/bin/bash\njetha:x:1000:1000:Jethalal:/home/jetha:/bin/bash" | sed 's/:.*//'
# Output:
# root
# jetha
```

**Q6. Remove Comments from Config File**
**Task:** Delete lines starting with # and empty lines
```bash
echo -e "# Config file\nPORT=8080\n# Debug mode\nDEBUG=true" | sed '/^#/d;/^$/d'
# Output:
# PORT=8080
# DEBUG=true
```

**Q7. Convert Multi-line to Single Line**
**Task:** Join lines with semicolon
```bash
echo -e "apple\nbanana\ncherry" | sed ':a;N;$!ba;s/\n/;/g'
# Output: apple;banana;cherry
```

**Q8. Double Space File**
**Task:** Add blank line after each line
```bash
echo -e "line1\nline2\nline3" | sed G
# Output:
# line1
#
# line2
#
# line3
```

**Q9. Remove Leading/Trailing Spaces**
**Task:** Clean whitespace
```bash
echo "   hello world   " | sed 's/^ *//;s/ *$//'
# Output: hello world
```

**Q10. Increment All Numbers by 1**
**Task:** Add 1 to every number in text
```bash
echo "Score: 10, Level: 5, Lives: 3" | sed 's/[0-9]\+/echo $((&+1))/ge'
# Output: Score: 11, Level: 6, Lives: 4
```

**Q11. Swap Two Words**
**Task:** "cat and dog" → "dog and cat"
```bash
echo "cat and dog" | sed 's/\(cat\) and \(dog\)/\2 and \1/'
# Output: dog and cat
```

**Q12. Format Phone Numbers**
**Task:** 1234567890 → (123) 456-7890
```bash
echo "1234567890" | sed 's/\(...\)\(...\)\(....\)/(\1) \2-\3/'
# Output: (123) 456-7890
```

**Q13. Remove Duplicate Lines**
**Task:** Keep only first occurrence of each line
```bash
echo -e "apple\nbanana\napple\ncherry\nbanana" | sed '$!N; /^\(.*\)\n\1$/!P; D'
# Output:
# apple
# banana
# cherry
```

**Q14. Capitalize First Letter of Each Word**
**Task:** "hello world" → "Hello World"
```bash
echo "hello world from bash" | sed 's/\b\(.\)/\u\1/g'
# Output: Hello World From Bash
```

**Q15. Extract Text Between Markers**
**Task:** Get content between START and END
```bash
echo -e "ignore\nSTART\nimportant data\nEND\nignore" | sed -n '/START/,/END/{/START\|END/d;p}'
# Output: important data
```

---

## **🔥 BONUS: 5 ADVANCED CHALLENGES**

### **Challenge 1: Convert JSON to CSV**
```bash
echo '{"name":"Jetha","age":45,"city":"Mumbai"}' | sed 's/{//;s/}//;s/"//g;s/:/,/g'
# Output: name,Jetha,age,45,city,Mumbai
```

### **Challenge 2: Create Markdown Table**
```bash
echo -e "Name|Age|City\nJetha|45|Mumbai\nBabita|40|Mumbai" | sed 's/|/ | /g;1 s/.*/| & |/;1! s/.*/| & |/;2 a |---|---|---|'
# Output:
# | Name | Age | City |
# |---|---|---|
# | Jetha | 45 | Mumbai |
# | Babita | 40 | Mumbai |
```

### **Challenge 3: Sort Lines by Length**
```bash
echo -e "apple\nbanana\nkiwi\ngrapes" | sed 's/.*/&\t&/' | sed 's/.*/\L&\t&/' | sort -k2 | sed 's/\t.*//'
# Output depends on locale, but sorts by length
```

### **Challenge 4: Generate SQL INSERT Statements**
```bash
echo -e "Jetha,45,Mumbai\nBabita,40,Mumbai" | sed "s/\(.*\),\(.*\),\(.*\)/INSERT INTO users VALUES('\1',\2,'\3');/"
# Output:
# INSERT INTO users VALUES('Jetha',45,'Mumbai');
# INSERT INTO users VALUES('Babita',40,'Mumbai');
```

### **Challenge 5: Create HTML List**
```bash
echo -e "apple\nbanana\ncherry" | sed 's/.*/<li>&<\/li>/;1 i <ul>;$ a </ul>'
# Output:
# <ul>
# <li>apple</li>
# <li>banana</li>
# <li>cherry</li>
# </ul>
```

---

## **🎯 QUICK REFERENCE CARD**

| Task | Command | Example |
|------|---------|---------|
| **Replace first** | `sed 's/old/new/'` | `echo "foo" | sed 's/foo/bar/'` |
| **Replace all** | `sed 's/old/new/g'` | `echo "f f f" | sed 's/f/b/g'` |
| **Case-insensitive** | `sed 's/old/new/i'` | `echo "Foo" | sed 's/foo/bar/i'` |
| **Delete lines** | `sed '/pattern/d'` | `echo -e "a\nb" | sed '/a/d'` |
| **Print matching** | `sed -n '/pattern/p'` | `echo -e "a\nb" | sed -n '/a/p'` |
| **Insert before** | `sed '3 i text'` | `echo "a" | sed '1 i START'` |
| **Append after** | `sed '3 a text'` | `echo "a" | sed '$ a END'` |
| **Change line** | `sed '3 c text'` | `echo "old" | sed 'c new'` |
| **Line numbers** | `sed =` | `echo -e "a\nb" | sed =` |
| **In-place edit** | `sed -i 's/old/new/'` | `sed -i 's/a/b/' file` |
| **Backup edit** | `sed -i.bak` | `sed -i.bak 's/a/b/' file` |

---

## **💡 PRO TIPS**

1. **Test without `-i` first!** Always check output before saving
2. **Use `-n` + `p`** for filtering (like grep)
3. **Backreferences** `\1, \2` are powerful for rearranging
4. **Different delimiters** `s|old|new|` when `/` is in pattern
5. **Combine with other tools** `grep`, `awk`, `cut` for complex tasks
6. **Address ranges** `1,5s/old/new/` for specific lines
7. **`&`** in replacement means "whatever was matched"

---

**Practice makes perfect! Try these exercises daily to master `sed`.** 🚀
