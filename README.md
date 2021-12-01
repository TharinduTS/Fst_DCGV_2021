# Fst_DCGV_2021

Got geno files for input as explained in

https://github.com/TharinduTS/ABBA_BABA_2021

copy scripts from following and save using vi

```
https://github.com/simonhmartin/genomics_general/blob/master/genomics.py
https://github.com/simonhmartin/genomics_general/blob/master/popgenWindows.py
```
then created a txt file with sample name and population name like- In local computer

pop_list.txt
```txt
JM_no_label1_Draken_CCACGT_cuttrim_sorted_final_l_only.bam      popC
JM_no_label2_Draken_TTCAGA_cuttrim_sorted_final_l_only.bam      popD
```

You can easily assign populations in the next command using this R script

DO NOT USE THE FILE WITH SAMPLE NAMES AND POP NAMES DIRECTLY AS MENTIONED IN MANUAL OF THE SCRIPT. IT DOES NOT CAL Fst etc FOR SOME REASON

```R
#set current path as wd
library("rstudioapi") 
setwd(dirname(getActiveDocumentContext()$path))

pop_list<-read.table("./pop_list.txt")


final_list_to_paste<-"paste following in the terminal:  "

for (pop in unique(pop_list$V2)) {
  
  pop_1<-pop_list$V1[pop_list$V2==pop]
  
  sample_list<-noquote(toString(pop_1))
  
  full_cmd<-paste(" -p ",pop," ",sample_list,sep = "")
  
  final_list_for_this_pop<-gsub(", ",",",full_cmd)
  
  final_list_to_paste<-paste(final_list_to_paste,final_list_for_this_pop,sep = "")
}

print(final_list_to_paste)

```

Loaded pythin
```bash
module load python/3.8.2
virtualenv --no-download ~/ENV
source ~/ENV/bin/activate
pip install --no-index --upgrade pip
pip install numpy --no-index
```
Then Fst etc can be calculated using output from above R script likr following ( R script gives -p XXXXX part organized)

This may take few hours
```
for i in *.geno ; do python popgenWindows.py -w 50000 -m 50 -g ${i} -o ${i}_output.csv.gz -f phased -p Inhaca 2014_Inhaca_10_Inhaca_ATATGT_cuttrim_sorted.bam,2014_Inhaca_150_Inhaca_ATCGTA_cuttrim_sorted.bam,2014_Inhaca_152_Inhaca_CATCGT_cuttrim_sorted.bam,2014_Inhaca_24_Inhaca_CGCGGT_cuttrim_sorted.bam,2014_Inhaca_38_Inhaca_CTATTA_cuttrim_sorted.bam,2014_Inhaca_52_Inhaca_GCCAGT_cuttrim_sorted.bam,2014_Inhaca_65_Inhaca_GGAAGA_cuttrim_sorted.bam -p Draken 946_Draken_TCGTT_cuttrim_sorted.bam,993_Draken_GGTTGT_cuttrim_sorted.bam,JM_no_label1_Draken_CCACGT_cuttrim_sorted.bam,JM_no_label2_Draken_TTCAGA_cuttrim_sorted.bam -p Other BJE2897_Lendu_TTCCTGGA_cuttrim_sorted.bam,BJE3252_Cameroon_TATCGGGA_cuttrim_sorted.bam,RT5_Botsw_GGATTGGT_cuttrim_sorted.bam,amnh17260_Nigeria_GTGAGGGT_cuttrim_sorted.bam -p DCGV BJE3508_DeDorn_ATTGA_cuttrim_sorted.bam,BJE3509_DeDorn_CATCT_cuttrim_sorted.bam,BJE3510_DeDorn_CCTAG_cuttrim_sorted.bam,BJE3511_DeDorn_GAGGA_cuttrim_sorted.bam,BJE3512_DeDorn_GGAAG_cuttrim_sorted.bam,BJE3513_DeDorn_GTCAA_cuttrim_sorted.bam,BJE3514_DeDorn_TAATA_cuttrim_sorted.bam,BJE3515_DeDorn_TACAT_cuttrim_sorted.bam,BJE3547_GRNP_TAGGAA_cuttrim_sorted.bam,BJE3548_GRNP_GCTCTA_cuttrim_sorted.bam,BJE3549_GRNP_CCACAA_cuttrim_sorted.bam,BJE3550_GRNP_CTTCCA_cuttrim_sorted.bam,BJE3551_GRNP_GAGATA_cuttrim_sorted.bam,BJE3552_GRNP_ATGCCT_cuttrim_sorted.bam,BJE3553_GRNP_AGTGGA_cuttrim_sorted.bam,BJE3554_GRNP_ACCTAA_cuttrim_sorted.bam,BJE3573_VicW_CGCGGAGA_cuttrim_sorted.bam,BJE3574_VicW_CGTGTGGT_cuttrim_sorted.bam,BJE3667_Citrus_CGCTT_cuttrim_sorted.bam,BJE3668_Citrus_TCACG_cuttrim_sorted.bam,BJE3669_Citrus_CTAGG_cuttrim_sorted.bam,BJE3670_Citrus_ACAAA_cuttrim_sorted.bam,BJE3671_Citrus_TTCTG_cuttrim_sorted.bam,BJE3672_Citrus_AGCCG_cuttrim_sorted.bam,BJE3673_Citrus_GTATT_cuttrim_sorted.bam,BJE3674_Citrus_CTGTA_cuttrim_sorted.bam,BJE3675_Citrus_ACCGT_cuttrim_sorted.bam,BJE3676_Citrus_GCTTA_cuttrim_sorted.bam,BJE3677_Citrus_GGTGT_cuttrim_sorted.bam,BJE3678_Citrus_AGGAT_cuttrim_sorted.bam -p Laigns BJE3525_Laigns_GAATTCA_cuttrim_sorted.bam,BJE3526_Laigns_GAACTTG_cuttrim_sorted.bam,BJE3527_Laigns_GGACCTA_cuttrim_sorted.bam,BJE3528_Laigns_GTCGATT_cuttrim_sorted.bam,BJE3529_Laigns_AACGCCT_cuttrim_sorted.bam,BJE3530_Laigns_AATATGG_cuttrim_sorted.bam,BJE3531_Laigns_ACGTGTT_cuttrim_sorted.bam,BJE3532_Laigns_ATTAATT_cuttrim_sorted.bam,BJE3533_Laigns_ATTGGAT_cuttrim_sorted.bam -p BW BJE3534_BW_CTCG_cuttrim_sorted.bam,BJE3535_BW_TGCA_cuttrim_sorted.bam,BJE3536_BW_ACTA_cuttrim_sorted.bam,BJE3537_BW_CAGA_cuttrim_sorted.bam,BJE3538_BW_AACT_cuttrim_sorted.bam,BJE3539_BW_GCGT_cuttrim_sorted.bam,BJE3541_BW_CGAT_cuttrim_sorted.bam,BJE3542_BW_GTAA_cuttrim_sorted.bam,BJE3543_BW_AGCG_cuttrim_sorted.bam,BJE3544_BW_GATG_cuttrim_sorted.bam,BJE3545_BW_TCAG_cuttrim_sorted.bam,BJE3546_BW_TGCGA_cuttrim_sorted.bam -p Kimber BJE3575_Kimber_GTACTT_cuttrim_sorted.bam,BJE3576_Kimber_GTTGAA_cuttrim_sorted.bam,BJE3577_Kimber_TAACGA_cuttrim_sorted.bam,BJE3578_Kimber_TGGCTA_cuttrim_sorted.bam,BJE3579_Kimber_TATTTTT_cuttrim_sorted.bam,BJE3580_Kimber_CTTGCTT_cuttrim_sorted.bam,BJE3581_Kimber_ATGAAAG_cuttrim_sorted.bam,BJE3582_Kimber_AAAAGTT_cuttrim_sorted.bam -p Niewou BJE3633_Niewou_CGCTGAT_cuttrim_sorted.bam,BJE3640_Niewou_CGGTAGA_cuttrim_sorted.bam,BJE3641_Niewou_CTACGGA_cuttrim_sorted.bam,BJE3642_Niewou_GCGGAAT_cuttrim_sorted.bam,BJE3644_Niewou_TAGCGGA_cuttrim_sorted.bam,BJE3645_Niewou_TCGAAGA_cuttrim_sorted.bam,BJE3647_Niewou_TCTGTGA_cuttrim_sorted.bam -p ThreeS BJE3654_ThreeSis_TGCTGGA_cuttrim_sorted.bam,BJE3655_ThreeSis_ACGACTAG_cuttrim_sorted.bam,BJE3656_ThreeSis_TAGCATGG_cuttrim_sorted.bam,BJE3657_ThreeSis_TAGGCCAT_cuttrim_sorted.bam,BJE3658_ThreeSis_TGCAAGGA_cuttrim_sorted.bam,BJE3659_ThreeSis_TGGTACGT_cuttrim_sorted.bam,BJE3660_ThreeSis_TCTCAGTG_cuttrim_sorted.bam,BJE3661_ThreeSis_CGCGATAT_cuttrim_sorted.bam,BJE3662_ThreeSis_CGCCTTAT_cuttrim_sorted.bam,BJE3663_ThreeSis_AACCGAGA_cuttrim_sorted.bam,BJE3664_ThreeSis_ACAGGGA_cuttrim_sorted.bam,BJE3665_ThreeSis_ACGTGGTA_cuttrim_sorted.bam,BJE3666_ThreeSis_CCATGGGT_cuttrim_sorted.bam -p Vred Vred_8_Vred_GCTGTGGA_cuttrim_sorted.bam ;done

```
You can find the column number from comma seperated column name using this command(will be useful for next step)
Change file name and column name
```
head l_only_output.csv | sed -e 's:,: :g' | tr -s ' ' '\n' | nl -nln |  grep "Fst_Inhaca_Draken" | cut -f1
```


****** This method does not calculate Fst etc for some reason. Therefore had to use the method above. DO NOT TRY THIS METHOD **********************

Then calculated Fst values by

```bash
python popgenWindows.py -w 50000 -m 50 -g l_only_all_chrs.geno -o l_only_output.csv.gz -f phased --popsFile pops.txt

python popgenWindows.py -w 50000 -m 50 -g s_only_all_chrs.geno -o s_only_output.csv.gz -f phased --popsFile pops.txt

python popgenWindows.py -w 50000 -m 50 -g l_and_S_all_chrs.geno -o l_and_S_all_output.csv.gz -f phased --popsFile pops.txt

```
