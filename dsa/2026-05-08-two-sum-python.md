# Two Sum — Python

Date: 2026-05-08
Language: Python
Topic: Hash map lookup pattern

## What was practiced

Worked through the classic Two Sum problem:

> Given a list of numbers and a target, return the indices of two numbers that add up to the target.

Example:

```python
nums = [2, 7, 11, 15]
target = 9
# answer: [0, 1]
```

## Starting mental model

Initial brute-force idea:

```text
For each number:
    check it against every other number
    if num + other == target:
        return both indices
```

This works conceptually, but it has issues:

- It can accidentally check a number against itself.
- It can re-check pairs that were already checked.
- If loop bounds are wrong, it can go out of bounds.
- It is `O(n^2)` because it compares many pairs.

Correct brute-force Python shape:

```python
def two_sum(nums, target):
    for i in range(len(nums)):
        for j in range(i + 1, len(nums)):
            if nums[i] + nums[j] == target:
                return [i, j]
```

Why `j = i + 1` matters:

- avoids checking the same item twice
- avoids old pairs
- avoids checking `nums[i] + nums[i]`

## Better solution: hash map

Use a dictionary called `seen` to remember numbers already passed.

```python
def two_sum(nums, target):
    seen = {}

    for i, num in enumerate(nums):
        complement = target - num

        if complement in seen:
            return [seen[complement], i]

        seen[num] = i

    return []
```

## What `enumerate` means

`enumerate(nums)` loops through the list while giving both:

- the index
- the value

Example:

```python
nums = [2, 7, 11, 15]

for i, num in enumerate(nums):
    print(i, num)
```

Output:

```text
0 2
1 7
2 11
3 15
```

Mental translation:

```text
for each item in nums:
    i = the item's index
    num = the item's value
```

## What `complement` means

The complement is the number needed to reach the target if the current number is used.

```python
complement = target - num
```

Example:

```python
target = 9
num = 7
complement = 9 - 7  # 2
```

Meaning:

```text
If I use 7, I need 2 to make 9.
```

## What the dictionary stores

```python
seen[num] = i
```

Means:

```text
key   = number seen
value = index where it was seen
```

Example after seeing `2` at index `0`:

```python
seen = {2: 0}
```

Meaning:

```text
I have seen number 2 at index 0.
```

## Step-by-step example

```python
nums = [2, 7, 11, 15]
target = 9
seen = {}
```

First loop:

```python
i = 0
num = 2
complement = 9 - 2  # 7
```

`7` is not in `seen`, so store current number:

```python
seen[2] = 0
# seen is now {2: 0}
```

Second loop:

```python
i = 1
num = 7
complement = 9 - 7  # 2
```

`2` is in `seen`, so return:

```python
return [seen[2], 1]
# return [0, 1]
```

## Complexity

Brute force:

- Time: `O(n^2)`
- Space: `O(1)`

Hash map:

- Time: `O(n)`
- Space: `O(n)`

Why hash map is `O(n)`:

There is only one loop. Dictionary lookup like this:

```python
if complement in seen:
```

is approximately `O(1)`, not another full scan of the list.

So for each number:

- calculate complement: `O(1)`
- check dictionary: `O(1)`
- insert into dictionary: `O(1)`

Repeated for `n` numbers gives `O(n)`.

## Final English explanation

For each number in the list, get its index and value. Calculate the complement, meaning the number needed to reach the target. Check whether that complement has already been seen in the dictionary. If it has, return the saved index of the complement plus the current index. If not, store the current number in the dictionary with the number as the key and its index as the value. Continue until found.

Important correction:

- Not “check if complement is in the list.”
- Correct: “check if complement is in the dictionary of numbers already seen.”

## Pattern note

This is the **lookup-before-store** pattern.

Why lookup before store matters:

- It prevents using the same index twice.
- It checks only numbers that came before the current one.
- It turns pair-search from brute force into one-pass lookup.

Use this pattern when a problem asks:

```text
Find two things that combine to a target/value/condition.
```

Common signals:

- pair sum
- complements
- seen-before lookup
- return indices or matching pair
