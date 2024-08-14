# 3D SARS-CoV-19 Protein Visualization With Biopython

## Overview
This project demonstrates how to visualize the 3D structure of the SARS-CoV-19 protein using Biopython. Biopython is a set of tools for biological computation written in Python. It is a distributed collaborative effort to develop Python libraries and applications that address the needs of current and future work in bioinformatics.

## Table of Contents
1. [Attributes of Biopython](#attributes-of-biopython)
2. [Understanding FASTA File Format](#understanding-fasta-file-format)
3. [Sequence Manipulation Using Biopython](#sequence-manipulation-using-biopython)
4. [Transcription & Translation Studies](#transcription--translation-studies)
5. [Basic Local Alignment Using NCBI-BLAST](#basic-local-alignment-using-ncbi-blast)
6. [Reading PDB File](#reading-pdb-file)
7. [Visualizing SARS-CoV-19 Protein Structure](#visualizing-sars-cov-19-protein-structure)
8. [Observations](#observations)
9. [Further Reading](#further-reading)

## Attributes of Biopython
Biopython provides a wide range of functionalities, including:
- Sequence Analysis (DNA/RNA/Protein)
- Transcription & Translation studies
- Accessing Bioinformatics Databases (e.g., NCBI, PDB)
- 3D Structure Analysis

To explore the attributes of Biopython, you can use the following code:
```python
import Bio
dir(Bio)
```
## Understanding FASTA File Format
FASTA is a text-based format for representing nucleotide sequences or peptide sequences. Each sequence in the FASTA format begins with a single-line description, followed by lines of sequence data.

The `Sequence_Data` folder contains the fasta files.

```python
from Bio import SeqIO

# Loading FASTA file
seq_file_read = SeqIO.read("/Users/montaha.chowdhury/Documents/Comp Bio Learning/3D SARS-Cov-2 Protein Visualization/3D-SARS-CoV-19-Protein-Visualization/Sequence_Data/sequence.fasta", "fasta")
seq_file_read
```

## Sequence Manipulation Using Biopython
Biopython allows various sequence manipulations such as indexing, slicing, concatenation, codon search, GC content calculation, and finding complements.

Example: Indexing and Slicing

```python
seqfromfile = seq_file_read.seq
print(seqfromfile[0:4])  # Output: 'ATTA'
```
## Example: GC Content

```python
from Bio.SeqUtils import gc_fraction
gc_content = gc_fraction(seqfromfile)
print(gc_content)  # Output: 0.3797277865097147
```

Transcription & Translation Studies
Biopython provides tools for transcription (DNA to RNA) and translation (RNA to protein).

Example: Transcription

```python
mRNA = seqfromfile.transcribe()
print(mRNA[:10])  # Output: 'AUUAAAGGUU'
```
## Example: Translation

```python
protein_seq = seqfromfile.translate()
print(protein_seq[:10])  # Output: 'IKGLYLPR*Q'
```
## Basic Local Alignment Using NCBI-BLAST
You can perform a BLAST search to find regions of similarity between biological sequences.

Example: Performing a BLAST Search

```python
from Bio.Blast import NCBIWWW, NCBIXML

result_handle = NCBIWWW.qblast("blastp", "pdb", read.seq)
blast_qresult = SearchIO.read(result_handle, "blast-xml")
print(blast_qresult[0:5])
```
## Reading PDB File
Retrieve and parse PDB files to analyze the 3D structure of proteins.

Example: Reading a PDB File

```python
from Bio.PDB import PDBParser

parser = PDBParser()
structure = parser.get_structure("7D4F", "Sequence_data/7D4F.pdb")
print(structure)
```

## Visualizing SARS-CoV-19 Protein Structure
It was recommended to use nglview to visualize the 3D structure of the protein. But I used PyMOL for viewing the structure. 

<img src="images/Screenshot%202024-08-14%20at%2021.57.37.png" alt="Screenshot" width="500"/>


## Observations
Length of the sequence: 29903 base pairs
- GC content: 37.97%
- The largest protein has a length of 29903 amino acids
- The largest protein BLAST results correspond to Structure of COVID-19 RNA-dependent RNA polymerase bound to suramin.
- Protein 7D4F has 3 unique protein chains and a DNA binding domain

## Further Reading
- [Biopython Tutorial and Cookbook](https://biopython.org/DIST/docs/tutorial/Tutorial.html)
- [Transcription & Translation](https://en.wikipedia.org/wiki/Transcription_(biology))

