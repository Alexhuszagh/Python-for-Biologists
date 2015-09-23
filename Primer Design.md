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
...         primer += dna_to_rna
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
>>> dna_to_rna = {'a': 'u', 't': 'a', 'c': 'g', 'g': 'c'}
>>> min_temp = 52
>>> max_temp = 65
>>>
>>> for start in range(sequence_length - primer_length):
...     target = sequence[start: primer_length + start]
...     primer = ''
...     for dna_letter in target:
...         rna_letter = dna_to_rna[dna_letter]
...         primer += rna_letter
...
...     temperature = mt.Tm_staluc(primer)
...     if min_temp < temperature < max_temp:
...         print(primer)
gggccuucgcuugcagcggc
ggccuucgcuugcagcggcg
gccuucgcuugcagcggcgc
ccuucgcuugcagcggcgcc
cuucgcuugcagcggcgccg
uucgcuugcagcggcgccgc
gcgccgcggcccccaccuuc
cgccgcggcccccaccuucu
gccgcggcccccaccuucua
ccgcggcccccaccuucuac
cgcggcccccaccuucuacg
gcggcccccaccuucuacgg
cggcccccaccuucuacggc
ggcccccaccuucuacggcg
gcccccaccuucuacggcga
accuucuacggcgacggcca
uucuacggcgacggccaagu
cuacggcgacggccaagucc
uacggcgacggccaagucca
acggcgacggccaaguccac
cggcgacggccaaguccaca
ggcgacggccaaguccacaa
gcgacggccaaguccacaaa
uccaucccgaaccaccgacg
ccaucccgaaccaccgacgc
caucccgaaccaccgacgcg
aucccgaaccaccgacgcga
ucccgaaccaccgacgcgag
cccgaaccaccgacgcgagc
ccgaaccaccgacgcgagcg
cgaaccaccgacgcgagcgg
gaaccaccgacgcgagcggc
aaccaccgacgcgagcggcg
```
