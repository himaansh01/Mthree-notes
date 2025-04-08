# 📘 Python String Manipulation Functions

## 1️⃣ remove_outermost_parenthesis(s)

**🎯 Purpose:**  
Removes the outermost parentheses from a valid string.

**💡 Strategy:**  
Use a counter to track nesting instead of a stack.

**⏱ Complexity:**  
Time: O(n), Space: O(n)

```python
def remove_outermost_parenthesis(s):
    result = []
    open_count = 0
    for char in s:
        if char == '(' and open_count > 0:
            result.append(char)
        elif char == ')' and open_count > 1:
            result.append(char)
        if char == '(':
            open_count += 1
        elif char == ')':
            open_count -= 1
    return ''.join(result)

# Example
print(remove_outermost_parenthesis("(()())"))  # Output: "()()"
```

---

## 2️⃣ reverse_words(s)

**🎯 Purpose:**  
Reverses the order of words in a sentence.

**💡 Strategy:**  
Use split() and slicing to reverse efficiently.

**⏱ Complexity:**  
Time: O(n), Space: O(n)

```python
def reverse_words(s):
    words = [word for word in s.split() if word]
    return ' '.join(words[::-1])

# Example
print(reverse_words("my name is PK"))  # Output: "PK is name my"
```

---

## 3️⃣ largest_odd_number(s)

**🎯 Purpose:**  
Find the largest odd number by trimming from the right.

**💡 Strategy:**  
Scan from end to start and return early.

**⏱ Complexity:**  
Time: O(n), Space: O(1)

```python
def largest_odd_number(s):
    for i in range(len(s) - 1, -1, -1):
        if int(s[i]) % 2 == 1:
            return s[:i + 1]
    return ""

# Example
print(largest_odd_number("354270"))  # Output: "35427"
print(largest_odd_number("24680"))   # Output: ""
```

---

## 4️⃣ longest_common_substring(words)

**🎯 Purpose:**  
Finds the longest substring shared by all strings.

**💡 Strategy:**  
Start from the shortest word and check all its substrings.

**⏱ Complexity:**  
Time: O(n * m²), Space: O(1)

```python
def longest_common_substring(words):
    if not words:
        return ""
    shortest = min(words, key=len)
    longest_substr = ""
    for i in range(len(shortest)):
        for j in range(i + 1, len(shortest) + 1):
            substr = shortest[i:j]
            if all(substr in word for word in words):
                if len(substr) > len(longest_substr):
                    longest_substr = substr
            else:
                break
    return longest_substr

# Example
words = ["flight", "lightning", "slight"]
print(longest_common_substring(words))  # Output: "light"
```

---

## 5️⃣ are_rotations(s1, s2)

**🎯 Purpose:**  
Checks if two strings are rotations of each other.

**💡 Strategy:**  
Check if s2 is a substring of s1+s1.

**⏱ Complexity:**  
Time: O(n), Space: O(n)

```python
def are_rotations(s1, s2):
    if len(s1) != len(s2):
        return False
    return s2 in (s1 + s1)

# Example
print(are_rotations("abcd", "cdab"))  # Output: True
print(are_rotations("abcd", "cdba"))  # Output: False
```

---

## 6️⃣ is_anagram(s1, s2)

**🎯 Purpose:**  
Checks if two strings are anagrams.

**💡 Strategy:**  
Count character frequency with dictionaries.

**⏱ Complexity:**  
Time: O(n), Space: O(1)

```python
def is_anagram(s1, s2):
    if len(s1) != len(s2):
        return False
    char_count_s1 = {}
    char_count_s2 = {}
    for char in s1:
        char_count_s1[char] = char_count_s1.get(char, 0) + 1
    for char in s2:
        char_count_s2[char] = char_count_s2.get(char, 0) + 1
    return char_count_s1 == char_count_s2

# Example
print(is_anagram("listen", "silent"))  # Output: True
print(is_anagram("hello", "world"))    # Output: False
```

---

## ✅ Summary Table

| Function                      | Technique Used      | Time Complexity | Space Complexity |
|------------------------------|---------------------|-----------------|------------------|
| remove_outermost_parenthesis | Counter tracking    | O(n)            | O(n)             |
| reverse_words                | Split & reverse     | O(n)            | O(n)             |
| largest_odd_number           | Right-to-left scan  | O(n)            | O(1)             |
| longest_common_substring     | Brute force         | O(n * m²)       | O(1)             |
| are_rotations                | s1 + s1 trick       | O(n)            | O(n)             |
| is_anagram                   | Frequency map       | O(n)            | O(1)             |
