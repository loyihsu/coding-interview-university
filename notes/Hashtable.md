# Dictionary: Abstract Data Tyepe (ADT)

* Video: [MIT OpenCourse: ITA Dictionary](https://www.youtube.com/watch?v=0M_kIqhwbFo&list=PLUl4u3cNGP61Oq3tWYp6V_F-5jb5L2iHb&index=8)

Maintain set of items, each with a *key*.

- insert(item): overwrite any existing key)
- delete(item)
- search(key): return nil or item with the key; O(lgN) via AVL -> down to O(1)

## Python: `dict`

D[key] ~search
D[key]=val ~insert
del D[key] ~delete

## Motivation

- docdict
- database
- compilers & interpreters
- network router/server
- substring search
- string commonalitites
- file/dir sync
- cryptography

## Simple approach: Direct-access table

- store items in array indexed by key

### Problem
1. Keys may not be nonneg. integers
2. Gigantic memory hog

### Solutions

1. Prehash: maps keys to nonneg integers. In theory, keys are finite & discrete (string of bits) ex. Python: hash(x)
2. Hashing: Reduce universe `U` of all keys (integers) down to reasonable size m for table `U -> 1, 2, ..., m-1`

## Chaining

linked list of colliding elements in each slot of hash table

### Simple Uniform Hashing

Each key is equally likely to be hashed to any slot of the table, independent of where other keys hashing.

#### Analysis

- Expected length of chain fo n keys, m slots = n/m
- running time=O(1 + |chain|)

## Hash functions

1. division method: `h(k) = k mod m`
2. multiplication method: `[(a*k) mod 2^w] >> (w-r)`
3. Universal hashing: `h(k)=[(ak+b)mod p] mod m`

# Table Doubling

* Video: [MIT OpenCourse: Table Doubling](https://www.youtube.com/watch?v=BRO7mVIFt08&index=9&list=PLUl4u3cNGP61Oq3tWYp6V_F-5jb5L2iHb)

## How to choose `m`?

Idea: Start small; grow/shrink when needed

* If m > n: grow table
* If m == n/4: shrink table to m/2

### Grow Table

* make a table of the new size
* rehash

Double the size: O(1+2+4+8+...+N) = O(N)
Add one space: O(1+2+3+4+5...+N) = O(N^2)

#### Amortization

- Operation takes "T(N) amortized" if k operations take <= k*t(N) time

* k inserts take O(k) time
* O(1) amortized/insert

## String matching

* Simple way: search through all and find one: O(|s|\*(|t|-|s|) = O(|s|\*|t|)

### Rolling hash ADT

* r.append(c): Add char c to end of X
* r.skip(c): Delete first char of X
* r reamins a string x

#### Karp-Rabin algorithm

```
for c in s: rs.append(c)
for c in t[:len(s)]: rt.append(c)
if rs() == rt():
	for i in range(len(s)):
		rt.skip(t[i-len(s)]
		rt.append(t[i])
		if rs() == rt():
			check whether s == t[i-len(s)+1:i+1]
			if equal: found match
			else : happens with probability <= 1/|s|
```