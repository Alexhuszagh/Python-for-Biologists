# Design a Primer

Now we know the basics, let's apply this to a biological problem.

1. Make 500 primers with 20 nucleotides for a target gene sequence below in the appended file, of a format similar to:
cccggaagcgaacgtcgc...

## Break Problem into Parts

1. Represent sequence as data type
2. Grab subset of sequence of primer length
3. Use loops to repeatedly grab sequence subset at a different starting point
4. Translate sequence to complement
5. Libraries: Free Work
6. Extra Features (G/C Content, Repetitive Bases)
7. Organize code for functions

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
>>> sequence = "cccggaagcgaacgtcgccgcggcgccgggggtggaagatgccgctgccggttcaggtgtttaacttgcaggtagggcttggtggctgcgctcgccgcgt"
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
>>> primer_length = 20
>>> sequence_length = len(sequence)
>>>
>>> dna_to_rna = {'a': 'u', 't': 'a', 'c': 'g', 'g': 'c'}
>>>
>>> for start in range(sequence_length):
...     target = sequence[start: primer_length + start]
...     primer = ''
...     for dna_letter in target:
...         rna_letter = dna_to_rna[dna_letter]
...         primer += rna_letter
...     primer = primer[::-1]
```

## Step 5

* Libraries are packaged code which provide you with tools to simplify your own work.
* Good langauges have good libraries to simplify your life

**Using a library to calculate melting temperature**

```python
>>> from Bio.SeqUtils import MeltingTemp as mt
>>>
>>> sequence = "cccggaagcgaacgtcgccgcggcgccgggggtggaagatgccgctgccggttcaggtgtttaacttgcaggtagggcttggtggctgcgctcgccgcgt"
>>> primer_length = 20
>>> sequence_length = len(sequence)
>>>
>>> dna_to_rna = {'a': 't', 't': 'a', 'c': 'g', 'g': 'c'}
>>> min_temp = 52
>>> max_temp = 65
>>>
>>> for start in range(sequence_length - primer_length + 1):
...     target = sequence[start: primer_length + start]
...     primer = ''
...     for dna_letter in target:
...         rna_letter = dna_to_rna[dna_letter]
...         primer += rna_letter
...     primer = primer[::-1]
...
...     temperature = mt.Tm_staluc(primer)
...     if min_temp < temperature < max_temp:
...         print(primer)
cggcgacgttcgcttccggg
gcggcgacgttcgcttccgg
cgcggcgacgttcgcttccg
ccgcggcgacgttcgcttcc
gccgcggcgacgttcgcttc
atcttccacccccggcgccg
...
cggcgagcgcagccaccaag
```

## Step 6

* Using built-in Python tools, such as "Counter" and string searching quickly smartens the primer design
    * Counter creates a dictionary counter with each element in a sequence as key and the count as a value
        * 'aacgt' -> {'a': 2, 'c': 1, 'g': 1, 't': 1}
    * re allows advanced string matching

### Using Counter to provide G/C content bounds

```python
>>> from collections import Counter
>>> counts = Counter(sequence)
>>> counts
Counter({'g': 41, 'c': 28, 't': 19, 'a': 12})
```

* Counter is a part of the standard library, comes with every Python installation
* 40-60% G/C content
* No more than 3 G or C nucleotides in last 5 nucleotides

**Write short code to count G/C content in primer**

```python
>>> from collections import Counter
>>> min_gc = 0.4
>>> max_gc = 0.6
...
>>> primer_nt_counts = Counter(primer)
>>> gc_count = (primer_nt_counts['g'] + primer_nt_counts['c'])
>>> gc_content = gc_count / float(sum(primer_nt_counts.values()))
>>>
>>> end_counts = Counter(primer[-5:])
>>> end_gc = (end_counts['g'] + end_counts['c'])
>>> max_end_gc = 3
>>>
>>> if min_gc < gc_content < max_gc and end_gc <= max_end_gc:
>>>     print(primer)
```

### Using string searching to avoid repetitive sequences

```python
>>> repetitive_bases = ['a'*5, 't'*5, 'c'*5, 'g'*5]
>>> if not any([repetitive in primer for repetitive in repetitive_bases]):
...     print(primer)
```

## Step 7

```python
from collections import Counter
from Bio.SeqUtils import MeltingTemp as mt

sequence = "cccggaagcgaacgtcgccgcggcgccgggggtggaagatgccgctgccggttcaggtgtttaacttgcaggtagggcttggtggctgcgctcgccgcgt"
primer_length = 20
sequence_length = len(sequence)

min_temp = 52
max_temp = 65


def check_temperature(primer):
    temperature = mt.Tm_staluc(primer)
    return min_temp < temperature < max_temp

min_gc = 0.4
max_gc = 0.6
max_end_gc = 3


def good_gc_content(primer):
    '''
    Asserts G/C content is within 40-60% and not more than 3 G/C in
    5 3' nts.
    '''

    primer_nt_counts = Counter(primer)
    gc_count = (primer_nt_counts['g'] + primer_nt_counts['c'])
    gc_content = gc_count / float(sum(primer_nt_counts.values()))

    end_counts = Counter(primer[-5:])
    end_gc = (end_counts['g'] + end_counts['c'])

    return min_gc < gc_content < max_gc and end_gc <= max_end_gc

repetitive_bases = ['a'*5, 't'*5, 'c'*5, 'g'*5]


def check_repetitive(primer):
    '''Determines if any repetitive nts > 4 bp in primer sequence'''

    return not any([repetitive in primer for repetitive in repetitive_bases])


def check_primer(primer):
    '''
    Returns true if the primer has no repetitive sequences, is in Tm range,
    and has approproate G/C content
    '''

    temperature = check_temperature(primer)
    gc = good_gc_content(primer)
    repetitive = check_repetitive(primer)

    return all([temperature, gc, repetitive])

dna_to_rna = {'a': 't', 't': 'a', 'c': 'g', 'g': 'c'}


def get_primers(sequence):
    '''Predicts a series of primers for a given target sequence'''

    for start in range(sequence_length - primer_length + 1):
        target = sequence[start: primer_length + start]
        primer = ''
        for dna_letter in target:
            rna_letter = dna_to_rna[dna_letter]
            primer += rna_letter
        primer = primer[::-1]

        if check_primer(primer):
            print(primer)

get_primers(sequence)
```
