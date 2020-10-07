# phylogeny_phylip
Bootstrapping in PHYLIP (by NJ)
adopted from http://www.sfu.ca/~carmean/phylip1.html

## 1. Seqboot - input: seq.aln file (e.g. from ClustalW)
create 100 datasets (seed to e.g. 4333)

## 2. DNAdist (try Max-L) input: outfile from Seqboot
change to sequential and multiple datasets

## 3. Neighbour - input: outfile from DNAdist
change to multiple datasets

## 4. Consensus tree - input: treefile from Neighbour
don't forget to remove commas from names of taxa

## 5. Bootstrap tree found in outfile
