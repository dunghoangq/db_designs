# About Minhashing

## Problem

2 massive documents, need to know if they are familiar without comparing every single word against every other word ($O(M \times N)$).

## Jaccard Similarity

Given sets $A, B$:

$$
J(A, B) = \frac{|A \cap B|}{|A \cup B|}
$$

But direct calculation requires:

1. Find intersection
2. Find unique of both (union)
3. Calculate the ratio

This is not efficient! -> **Random permutation**.

## Characteristic Matrix

| Element | Set A | Set B |
|---------|-------:|-------:|
|  e1    |   1   |   0 |
|  e2    |   0   |   1 |
|  e3    |   1   |   1 |
|  e4    |   0   |   0 |

- x := both columns = 1
- y := one of columns = 1

$$
J(A, B) = \frac{x}{x + y}
$$

## Permutation (MinHash trick)

Minhash function:

> $h(S)$: index of the first row under permutation where Set $S$ has a 1.

What is the probability of $h(A) = h(B)$?

$$
P(h(A) = h(B)) = \frac{x}{x + y} = J(A, B)
$$

## Algorithm

- M(i, c): smallest h_i(r) for which column c has 1 in row r.

```text
for each row r
    for each hash function h_i
        compute h_i(r)

    for each column c
        if c has 1 in row r
            for each hash function h_i
                if h_i(r) < M(i, C)
                    M(i, c) = h_i(r)
```