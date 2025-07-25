# 003. Longest Substring Without Repeating Characters

### Category: String / Sliding Window / Two Pointers

🎥 Source: *L3. Longest Substring Without Repeating Characters* (Take U Forward) https://youtu.be/-zSxTJkcdAo?si=lB4sGRKj8ADsPgd5

---

## ❓ Problem Summary
Given a string `s`, find the length of the longest substring without repeating characters. Return the maximum length.

---

## 🧠 Approaches

### 1. Brute-Force (All Substrings — Too Slow)
- Check every possible substring using nested loops and verify uniqueness using a set.
- **Time**: O(n³)  
- **Space**: O(n)  

---

### 2. Sliding Window + Two Pointers (Optimal)
- **Idea**: Maintain a dynamic window `[left, right)` with no duplicates.
- **State**:  
  - `left`, `right` pointers  
  - `freq` map or array counting characters  
  - `current_len = right - left`
- **Algorithm**:
  - Expand `right` one by one.
  - If `s[right]` is already in window (freq > 0), increment `left` and decrement freq until no duplicate.
  - Update `max_len = max(max_len, right - left + 1)`
- **Time Complexity**: O(n) — each character is visited at most twice  
- **Space Complexity**: O(1) or O(256) for ASCII char map

```python
def lengthOfLongestSubstring(s):
    freq = {}
    left = max_len = 0
    for right, ch in enumerate(s):
        freq[ch] = freq.get(ch, 0) + 1
        while freq[ch] > 1:
            freq[s[left]] -= 1
            left += 1
        max_len = max(max_len, right - left + 1)
    return max_len
```
---

### 3. Why it works
1. Shrinking the window on-the-fly avoids re-scanning substrings.
2. Adjusting only when duplicates appear keeps it efficient.

### 4. Why You Might Get Stuck
1. Forget to decrement frequency when moving left.
2. Off-by-one bugs in window length calculation.
3. Not resetting state correctly between different runs.

### 5. Edge Cases
1. Empty string → 0
2. Single-character string → 1
3. All characters identical → 1
4. Entire string unique → len(s)

### 6. Key Takeaways
1. This is the classic sliding-window pattern for substring problems.
2. Ideal when asked about “longest/shortest substring with condition”.
3. Only one pointer moves: right goes forward; left shrinks on demand.
