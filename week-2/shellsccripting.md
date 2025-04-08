# 🐚 Day-8: Shell Scripting & Commands

---

## 1️⃣ Working with Arrays in Bash

```bash
a[0]="zara"
a[1]="askdhkasdh"
a[2]="adakjhsdj"

echo "${a[0]}"  # Output: zara
echo "${a[1]}"  # Output: askdhkasdh
```

> Bash arrays are zero-indexed. `${a[0]}` refers to the first element.

---

## 2️⃣ Conditional Statements in Bash

### Variables for Testing
```bash
balance=500
withdrawl=1200
daily_limit=1000
account_type="savings"
description=""
```

### Comparison Operators
```bash
if [ $balance -eq 5000 ]; then
  echo "Balance is exactly 5000"
fi

if [ $withdrawl -ne 1000 ]; then
  echo "Withdrawn amount is not 1000"
fi

if [ $balance -gt $withdrawl ]; then
  echo "You have a valid balance to withdraw money"
fi
```

### Logical AND / OR
```bash
if [ $withdrawl -le $balance -a $withdrawl -le $daily_limit ]; then
  echo "Transaction approved"
else
  echo "Transaction not approved"
fi

if [ $withdrawl -le $balance -o $balance -ge 500 ]; then
  echo "Customer is valuable to the bank"
fi
```

### Logical NOT and Extended Conditions
```bash
if [[ ! $withdrawl -le $balance || $balance -ge 500 ]]; then
  echo "Customer is valuable to the bank"
fi
```

### String Comparisons
```bash
if [ "$account_type" = "savings" ]; then
  echo "This is a savings account"
fi

if [ -z "$description" ]; then
  echo "Description is not provided"
fi
```

---

## 3️⃣ User Input in Bash

### Timed Input
```bash
read -t 5 -p "Quick 5 sec: " pin
```

### Standard Input
```bash
echo "Enter your name"
read name
echo "$name"
```

### Multiple Inputs
```bash
read -p "Enter account number and password: " acn password
echo $acn
echo $password
```

### Silent Input (Hidden Password)
```bash
read -s -p "Enter password: " p
```

---

## 4️⃣ Case Statements in Bash

```bash
read -p "Enter selection [1-3]: " selection

case $selection in
  1) accounttype="checking"; echo "You have selected checking";;
  2) accounttype="saving"; echo "You have selected saving";;
  3) accounttype="current"; echo "You have selected current";;
  *) accounttype="random"; echo "Random selection";;
esac
```

> `case` is cleaner than multiple `if` blocks. `*` handles the default case.

---

## 5️⃣ Using `grep` for Searching Text

### Basic Search
```bash
grep "selection$" case.sh         # Match 'selection' at end of line
grep -Ril "selection" case.sh     # Recursive, ignore case, list filenames
```

### Character Classes & Wildcards
```bash
grep "[0-9]" case.sh              # Any digit
grep "[a-zA-Z]" case.sh           # Any letter
grep "[aeiou]" case.sh            # Any vowel

grep "s*n" case.sh                # Matches 'sn', 'ssn', 'ssssn'
grep "se*n" case.sh               # Matches 'sn', 'sen', 'seen'
grep "selecti*n" case.sh          # Matches 'selection', 'selectiion', etc.

grep "sel.n" case.sh              # Matches 'selan', 'selbn', etc.
grep "selicti.n" case.sh          # Matches 'selection', 'selictiyn', etc.
```

---

## 🧾 Summary of Options & Flags

| Command | Option | Purpose                                |
|---------|--------|----------------------------------------|
| `read`  | `-p`   | Prompt message before input            |
| `read`  | `-t`   | Set timeout for input                  |
| `read`  | `-s`   | Silent input (passwords)               |
| `grep`  | `-R`   | Recursive directory search             |
| `grep`  | `-i`   | Case-insensitive match                 |
| `grep`  | `-l`   | Show only filenames with matches       |
| `if`    | `-eq`  | Equal to (numeric)                     |
| `if`    | `-ne`  | Not equal to (numeric)                 |
| `if`    | `-gt`  | Greater than                           |
| `if`    | `-le`  | Less than or equal to                  |
| `if`    | `-a`   | Logical AND                            |
| `if`    | `-o`   | Logical OR                             |
| `if`    | `-z`   | Check if string is empty               |

---

## ✅ Key Takeaways

- Practiced **arrays**, **if conditions**, **case statements**, and **input handling** in Bash  
- Used `grep` for pattern matching with **wildcards**, **classes**, and **regex**  
- Learned to write **interactive and conditional scripts**  
