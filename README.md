# Description:

Implementation of the BLAST algorithm in the [Seq](https://seq-lang.org/) programming language. Gapped and ungapped nucleotide and protein 2-sequence BLASTing is supported.

The algorithm works basically as follows. First, k-mers (11-mers for nucleotide sequences and 3-mers for protein sequences) for the query sequence are found, and then exact matches to these in the target sequence. Each match is extended in both directions as far as possible (requiring exact matching for nucleotide sequences, and less-than-exact to a certain extent, though ungapped, matching for protein sequences). For ungapped BLAST, these alignments are reported if determined significant. 

For gapped BLAST, alignments within a certain neighborhood are then selected for further gapped extension, where the sequence sections between neighbor alignments are aligned using Smith-Waterman. These improved alignments are reported if determined significant.

Substitution matrices:

 > BLASTn ungapped: +5/-4 match/mismatch
 
 > BLASTn gapped  : +1/-3 match/mismatch, -5/-2 gap open/extend
 
 > BLASTp ungapped: BLOSUM62 match/mismatch for BLASTp ungapped
 
 > BLASTp gapped  : BLOSUM62 match/mismatch, -11, -1 gap open/extend

# Usage:

`BLAST.seq` is executed with input query and target FASTA files and options passed as command-line arguments. 

Options include: 

- nucleotide or protein BLAST (`-B`)
- gapped or ungapped BLAST (`-g`)
- expectation value threshold (`-E`)
- ungapped extension score-drop from max score threshold (`-T`)
- neighborhood distance threshold to perform gapped align (`-n`)

Outputs are written to text files and contain significant alignments with expectation values < E.