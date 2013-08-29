---
title: Sets Theory
date: August 29 2013 15:36
layout: note
---

# Definition of Sets and Tuples
- Element: *a* &isin; Set
- Set: unordered collection of elements (no duplicates)
	-
- Tuple: ordered list of elements of fixed size (duplicates allowed)
	- k-tuple: ( x-1, x-2, x-3, ..., x-k )
	- Strings are special tuples
	- Not all elements have to be of the same type in a tuple

## Styles of defining sets & tuples
- list: S = { 1, 2, 3, 4, 5 }
- pattern: S = { 1, 4, 9, 25, ... }
- subsets: A &sube; B &forall; x &isin; A &rarr; x &isin; B
- rule: [a, b] = { x: a &le; x &and; x &le; b }

## Some useful set definitions
- &#8469; (Natural Numbers) = { 0, 1, 2, 3, ... }
- &#8484; (Integers) = { ..., -3, -2, -1, 0, 1, 2, 3, ... }
- &empty; (Empty Set) = { }

## Cross-product

Given two sets, A and B:
> A &times; B = { (a, b): &forall; a &isin; A &and; b &isin; B }

# Relations and Predicates

## First-order logic: quantifiers
- Predicate: a function with range B = { T, F }

## Relations and Functions
- relation: a subset, S, of A &times; B
- function: a relation f &sube; A &times; B, f: A &rarr; B with the property &forall; a &isin; A &exist; b &isin; B &and; (a, b) &isin; f
	- &forall; a &isin; A &exist; a unique f(a) &isin; B