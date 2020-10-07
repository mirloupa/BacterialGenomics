# Phylogenetic tree inference using RAxML

## 1. To run RAxML, use the following script:
PBS script located in ~/SUB_PBS/Xf_proj/raxml.pbs
```
raxmlHPC-SSE3 -m GTRGAMMA -f a -# 1000 -p 12345 -x 12345 -s PHYLIP_FORMAT.aln -n OUTPUT.nwk
```
