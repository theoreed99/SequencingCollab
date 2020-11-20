#Project Submission for Reed, Collars, Gordon
#
#To use: bash Bioinformatics_Project2020.sh "path_to_ref_sequences/" "path_to_muscle" "path_to_HMMbuild" "path_to_proteomes/" "path_to_HMMsearch"
#
#(1) Creating a file with the mcrA genes
cat "$1"/mcrAgene_*.fasta > "$1"/allmcrA.fasta
#
#(2) Creating a file with the hsp70 genes
cat "$1"/hsp70gene_*.fasta > "$1"/allhsp70.fasta
#
#(3) Running both the mcrA and hsp70 genes through muscle in order to allign sequences
"$2" -in "$1"/allmcrA.fasta -out "$1"/allmcrAalligned.fasta
"$2" -in "$1"/allhsp70.fasta -out "$1"/allhsp70alligned.fasta
#
#(4) Making HMM files for mcrA and hsp70 for the aligned sequences (HMM build)
"$3" ./mcrAhmm.fasta "$1"/allmcrAalligned.fasta
"$3" ./hsp70hmm.fasta "$1"/allhsp70alligned.fasta
#
#(5) Run a for loop to run the HMM files through each of the proteomes
echo "proteome mcrA_genes hsp70_genes" > final.txt
for file in "$4"/proteome_*.fasta
a=$(echo $file)
b=$("$5" ./mcrAhmm.fasta $file| grep ">>"| wc -l)
c=$("$5" ./hsp70hmm.fasta $file| grep ">>"| wc -l)
echo "$a $b $c" >> final.txt
#
#(6) List the most resistant proteomes first
#All proteomes contain at least one of each gene (mcrA and hsp70)
cat final.txt| grep -E "[1-9] [1-9]"| sort -k 3 -n -r| cut -d ' ' -f 1 > candidates.txt
