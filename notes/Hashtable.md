# Dictionary: Abstract Data Tyepe (ADT)

* Video: [MIT OPenCourse: ITA Dictionary](https://www.youtube.com/watch?v=0M_kIqhwbFo&list=PLUl4u3cNGP61Oq3tWYp6V_F-5jb5L2iHb&index=8)

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

