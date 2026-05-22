<h2>Solve Cryptarithmetic Problem,a CSP(Constraint Satisfaction Problem) using Python</h2> 
<h3>NAME : PRADHOSH K M      </h3>
<h3>REGISTER NUMBER : 212224060192     </h3>
<h2>AIM</h2>
<p>
    To solve Cryptarithmetic Problem,a CSP(Constraint Satisfaction Problem) using Python
</p>

### PROCEDURE
```
INPUT:
The algorithm takes three words as input.

   BASE
 + BALL
 --------
  GAMES

OUTPUT:
The algorithm assigns digits (0–9) to each letter such that the equation is satisfied.

Example Output:
   B A S E        2 4 6 1
   B A L L        2 4 5 5
  --------       --------
  G A M E S      0 4 9 1 6
```

### ALGORITHM
```
Define a node structure containing:
- letter
- corresponding digit value

Function isValid(nodeList, count, word1, word2, word3)

Input:
- nodeList → list of letter-digit mappings
- count → number of elements
- word1, word2, word3 → input strings

Output:
- Returns TRUE if word1 + word2 = word3
- Otherwise returns FALSE


BEGIN

1. Compute value of word1:
   m ← 1
   val1 ← 0
   For each letter from right to left in word1:
       Find corresponding value from nodeList
       val1 ← val1 + (m × value)
       m ← m × 10

2. Compute value of word2:
   m ← 1
   val2 ← 0
   For each letter from right to left in word2:
       Find corresponding value from nodeList
       val2 ← val2 + (m × value)
       m ← m × 10

3. Compute value of word3:
   m ← 1
   val3 ← 0
   For each letter from right to left in word3:
       Find corresponding value from nodeList
       val3 ← val3 + (m × value)
       m ← m × 10

4. Check condition:
   If val3 = val1 + val2:
       Return TRUE
   Else:
       Return FALSE

END
```
### PROGRAM
```python
import itertools

def solve_cryptarithmetic(addends, result, find_all=False, verbose=False):
    words = addends + [result]

    # Extract all unique letters
    letters = []
    for w in words:
        for ch in w:
            if ch not in letters:
                letters.append(ch)

    if len(letters) > 10:
        raise ValueError("Too many letters. Max 10 allowed.")

    # Leading letters cannot be zero
    leading = {w[0] for w in words}

    def word_value(word, mapping):
        val = 0
        for c in word:
            val = val * 10 + mapping[c]
        return val

    solutions = []

    for perm in itertools.permutations(range(10), len(letters)):
        mapping = dict(zip(letters, perm))

        # Leading zero check
        if any(mapping[ch] == 0 for ch in leading):
            continue

        # Compute values
        add_sum = sum(word_value(w, mapping) for w in addends)
        result_val = word_value(result, mapping)

        if add_sum == result_val:
            solutions.append(mapping.copy())
            if not find_all:
                return mapping

    return solutions if find_all else (solutions[0] if solutions else None)

if __name__ == "__main__":
    addends = ["BASE", "BALL"]
    result = "GAMES"

    solution = solve_cryptarithmetic(addends, result)

    if solution:
        print("\nSolution Found:")
        for k in sorted(solution):
            print(f"{k} -> {solution[k]}")

        def num(word):
            return int("".join(str(solution[ch]) for ch in word))

        print("\nCheck:")
        print(f"{addends[0]} ({num(addends[0])})")
        print(f"+ {addends[1]} ({num(addends[1])})")
        print(f"= {result} ({num(result)})")

    else:
        print("No solution found.")
```
### OUTPUT
<img width="321" height="221" alt="image" src="https://github.com/user-attachments/assets/0bfd0121-3d6d-4b65-a56c-0cc46015d457" />

### RESULT
Thus a Cryptarithmetic Problem was solved using Python successfully
