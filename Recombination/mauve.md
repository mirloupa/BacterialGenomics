# WGS alignment with ProgressiveMauve and ClonalFrame analysis.
(created 04/2019)  
Investigation of regions of recombination in Xf.

## 1. Copy .gbf files of filtered, clean genomes (from Prokka) to a new directory.
```bash
mkdir /data2/scratch2/mirabl/Xf_proj/NCBI_Xf55/Genome_seq/ProgMauve
for file in /data2/scratch2/mirabl/Xf_proj/NCBI_Xf55/Genome_seq/Xf/DNA_fasta/*.fasta.gz; do
  file_short=$(basename $file | sed s/".fasta.gz"//g)
  echo $file_short
  cp /data2/scratch2/mirabl/Xf_proj/NCBI_Xf55/Genome_seq/Xf/Annotation/"$file_short"/*.gbf /data2/scratch2/mirabl/Xf_proj/NCBI_Xf55/Genome_seq/ProgMauve"$file_short".gbk
done
```
## 2. Align genomes using progressiveMauve
```bash
qsub ~/SUB_PBS/Xf_proj/prog-mauve.pbs *.gbk ncbi-xf55_progmauve.xmfa
```
which contains the following script:
```bash
progressiveMauve --output=OUTPUT.xmfa --output-guide-tree=progmauve.tre --backbone-output=progmauve.backbone INPUTS.gbk
```
Take all strains belonging to each clade including cherry strains and others.  
order genomes with contigs with mauve against pacbio/complete genome  
align with progressive-mauve  
extract core with stripSubsetLCBs - extract only the LCBs (homologous blocks) that are present in all strains  
Convert to fasta and concatenate the alignment (all LCB alignments concantenated together)  
Convert to phylip format  
Build tree with RaxMLL (with GTR model, 100 bootstraps)  
Use this tree and xmfa alignment output for ClonalFrameML  

#CORE AND ACCESSORY GENOMES for each STRAIN
#Concatenate contigs in fasta file into 1 contig
#Extract coordinates of core genome LCBs for strain from core.xmfa and store in txt file
#Use coordinates to pull out core genome regions from fasta to either get core genome or remove to get accessory genome
