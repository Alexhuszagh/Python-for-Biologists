# Design a Primer

Now we know the basics, let's apply this to a biological problem.

1. Make 500 primers with 20 nucleotides for a target gene sequence below in the appended file, of a format similar to:
cccggaagcgaacgtcgc...

## Break Problem into Parts

1. Represent sequence as data type
2. Grab subset of sequence of primer length
3. Use loops to repeatedly grab sequence subset at a different starting point
4. Translate sequence to complement

## Step 1

**Which data type is best suited to represent the gene sequence?**
- Int
- Float
- String
- Dictionary


```python
>>> sequence = "cccggaagcgaacgtcgccgcggcgccgggggtggaagatgccgctgccggttcaggtgtttaacttgcaggtagggcttggtggctgcgctcgccgcgt"
```

## Step 2

We can then access the elements using a slice on the string, as was shown for the list.

```python
>>> primer_length = 20
>>> sequence[0: primer_length]
'cccggaagcgaacgtcgccg'
>>>
>>> sequence[1: primer_length + 1]
'ccggaagcgaacgtcgccgc'
>>>
>>> start = 1
>>> sequence[start: primer_length + start]
'ccggaagcgaacgtcgccgc'
```

## Step 3

**Which type of loop should we use to changing the starting point?**
- While Loop
- For Loop

```python
>>> sequence_length = len(sequence)
>>>
>>> for start in range(sequence_length):
...    target = sequence[start: primer_length + start]
```

## Step 4

**What collection type should we use to translate a target sequence to a primer?**
- List
- Dictionary

```python
>>> sequence_length = len(sequence)
>>>
>>> for start in range(sequence_length):
...     target = sequence[start: primer_length + start]
```
