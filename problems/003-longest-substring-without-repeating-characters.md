# 003. Longest Substring Without Repeating Characters

### Category: String / Sliding Window / Two Pointers

🎥 Source: *L3. Longest Substring Without Repeating Characters* (Take U Forward) :contentReference[oaicite:2]{index=2}

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
