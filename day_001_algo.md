---

````markdown
# Day 1 - Python Warmup Review (Two Sum, Move Zeroes, Reverse String)

## ✅ 1. Two Sum

### Your implementation:
```python
resIndex = dict()
for i in range(len(nums)):
    if (target - nums[i]) in resIndex:
        return [i, resIndex[target - nums[i]]]
    resIndex[nums[i]] = i
````

### ✅ Review:

* ✅ Time complexity: O(n), using a hash map for fast lookup.
* ✅ Logical flow is correct and variable names are understandable.
* ⚠️ Minor suggestion: interviewers usually prefer returning the smaller index first: `return [resIndex[...], i]`.

### ✅ Optimized version (more pythonic):

```python
def twoSum(self, nums: List[int], target: int) -> List[int]:
    seen = {}
    for i, num in enumerate(nums):
        if target - num in seen:
            return [seen[target - num], i]
        seen[num] = i
```

---

## ✅ 2. Reverse String

### Your implementation:

```python
left, right = 0, len(s) - 1
while left < right:
    s[left], s[right] = s[right], s[left]
    left += 1
    right -= 1
```

### ✅ Review:

* ✅ Classic two-pointer approach.
* ✅ In-place swapping with O(n) time and O(1) space.
* ✅ No redundancy, clean and readable.

**✅ No improvement needed.**

---

## ✅ 3. Move Zeroes

### Your implementation:

```python
z_idx, no_z_idx = 0, 0
while (z_idx < nlen) and (no_z_idx < nlen):
    if nums[z_idx] != 0:
        z_idx += 1
        continue
    if nums[no_z_idx] == 0:
        no_z_idx += 1
        continue
    if z_idx < no_z_idx:
        nums[z_idx], nums[no_z_idx] = nums[no_z_idx], nums[z_idx]
        continue
    no_z_idx += 1
```

### ❌ Issues:

* The logic contains redundant branches and makes boundary conditions harder to manage.
* It's possible to fail some edge cases due to index misalignment.

### ✅ Recommended clean approach (using insert pointer):

```python
def moveZeroes(self, nums: List[int]) -> None:
    insert_pos = 0
    for i in range(len(nums)):
        if nums[i] != 0:
            nums[insert_pos] = nums[i]
            insert_pos += 1
    for i in range(insert_pos, len(nums)):
        nums[i] = 0
```

### Explanation:

* First pass: copy all non-zero values to the front.
* Second pass: fill the rest with zeroes.
* ✅ Time O(n), space O(1), logic is clean and robust.

### ✅ Alternative using two pointers (your style, simplified):

```python
def moveZeroes(self, nums: List[int]) -> None:
    z, n = 0, 0
    while n < len(nums):
        if nums[n] != 0:
            nums[z], nums[n] = nums[n], nums[z]
            z += 1
        n += 1
```

---

## ✅ Summary

| Problem        | Your Solution  | Improvement Needed | Recommendation                       |
| -------------- | -------------- | ------------------ | ------------------------------------ |
| Two Sum        | ✅ Correct      | ✅ Minor tweak      | Use `enumerate`, clean return        |
| Reverse String | ✅ Perfect      | ❌ No improvement   | —                                    |
| Move Zeroes    | ❌ Over-complex | ✅ Needs cleanup    | Use `insert pointer` or cleaner swap |

```

---

