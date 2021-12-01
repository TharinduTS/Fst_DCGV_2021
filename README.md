# Fst_DCGV_2021

Got geno files for input as explained in

https://github.com/TharinduTS/ABBA_BABA_2021

copy scripts from following and save using vi

```
https://github.com/simonhmartin/genomics_general/blob/master/genomics.py
https://github.com/simonhmartin/genomics_general/blob/master/popgenWindows.py
```
then created a txt file with sample name and population name like

pop_list.txt
```txt
JM_no_label1_Draken_CCACGT_cuttrim_sorted_final_l_only.bam      popC
JM_no_label2_Draken_TTCAGA_cuttrim_sorted_final_l_only.bam      popD
```

Loaded pythin
```bash
module load python/3.8.2
virtualenv --no-download ~/ENV
source ~/ENV/bin/activate
pip install --no-index --upgrade pip
pip install numpy --no-index
```

Then calculated Fst values by

```bash
python popgenWindows.py -w 50000 -m 50 -g l_only_all_chrs.geno -o l_only_output.csv.gz -f phased --popsFile pops.txt

python popgenWindows.py -w 50000 -m 50 -g s_only_all_chrs.geno -o s_only_output.csv.gz -f phased --popsFile pops.txt

python popgenWindows.py -w 50000 -m 50 -g l_and_S_all_chrs.geno -o l_and_S_all_output.csv.gz -f phased --popsFile pops.txt

```
