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
******* seems like there is a little bug in the script and it leaves one pop combination in resulte. Therefore running only those two, seperately this time *****
P.S. could be due to different numbering in perl??
(try giving column number for the first fst value -1 next time for jackknife??)
``` bash
for i in *.geno ; do python popgenWindows.py -w 50000 -m 50 -g ${i} -o ${i}_output_Inhaca_Draken.csv.gz -f phased -p Inhaca 2014_Inhaca_10_Inhaca_ATATGT_cuttrim_sorted.bam,2014_Inhaca_150_Inhaca_ATCGTA_cuttrim_sorted.bam,2014_Inhaca_152_Inhaca_CATCGT_cuttrim_sorted.bam,2014_Inhaca_24_Inhaca_CGCGGT_cuttrim_sorted.bam,2014_Inhaca_38_Inhaca_CTATTA_cuttrim_sorted.bam,2014_Inhaca_52_Inhaca_GCCAGT_cuttrim_sorted.bam,2014_Inhaca_65_Inhaca_GGAAGA_cuttrim_sorted.bam -p Draken 946_Draken_TCGTT_cuttrim_sorted.bam,993_Draken_GGTTGT_cuttrim_sorted.bam,JM_no_label1_Draken_CCACGT_cuttrim_sorted.bam,JM_no_label2_Draken_TTCAGA_cuttrim_sorted.bam ;done
```
unzip all csv outputs
```bash
gunzip *.gz
```

Then 

1.save this jackknife script in the same directory as CSVs above

2.You can find the column number from comma seperated column name using this command
Change file name and column name
```
head l_only_output.csv | sed -e 's:,: :g' | tr -s ' ' '\n' | nl -nln |  grep "Fst_Inhaca_Draken" | cut -f1
```
3. change "selected columns" in the line,
```
my @selected_chrs = (97..174);
```
to the column numbers with values you want to use jackknife for

in this case it is first column with Fst values (97/starting Fst.. in output CSV) and the last (174)


test_block_jackknife_withFst.pl
```
#!/usr/bin/env perl
use strict;
use warnings;


# This program reads in the output csv created above
# and calculates the standard error of the weighted mean value 

my $inputfile = $ARGV[0];

# print headers first

print "pop1","\t","pop2","\t","Fst","\t","CI_1","\t","CI2","\n";

#loop for selected columns
my @selected_chrs = (97..174);

for my $j (@selected_chrs){

#take column no

my $chr = $j;

unless (open DATAINPUT, $inputfile) {
        print "Can not find the input file.\n";
        exit;
}

my @windowsites;
my @Fst_values;
my $sumsites=0;
my $counter=0;
my @temp;
my $y;
my $x;

while ( my $line = <DATAINPUT>) {
        @temp=split(',',$line);
        if($temp[0] ne 'scaffold'){
                # if fDM is not numeric, it shouldn't contribute to the weighted average
                if($temp[$chr] !~ /nan/){
                        # load the number of sites for each window
                        $windowsites[$counter]=$temp[4];
                        # also load the Fst for each window
                        $Fst_values[$counter]=$temp[$chr];
                        # sum all the sites
                        $sumsites+= $temp[4];
                        # keep track of how many windows are loaded
                        $counter+=1;
                }
        }
}

my $weighted_Fst_average=0;

# calculate the weighted average of Fst
for ($y = 0 ; $y <= $#Fst_values; $y++ ) {
        $weighted_Fst_average+=($windowsites[$y]*$Fst_values[$y]/$sumsites);
}

# Print it
# print "The weighted Fst average is ",sprintf("%.6f",$weighted_Fst_average),"\n";


# now calculate the standard error.
my @jack_sumsites;
my $jack_averagesites;
my @jack_fst_values;
my $jack_weighted_average=0;
my @jack_weighted_fdm_values;
my @jackarray;
my $counter2=0;

for ($y = 0 ; $y < $counter; $y++ ) {
        for ($x = 0 ; $x < $counter; $x++ ) {
                # leave out one row for each jackknfe replicates
                if($y != $x){
                        # load the number of sites for each window
                        $jack_sumsites[$counter2]=$windowsites[$x];
                        # add them up to eventually get the average
                        $jack_averagesites+=$windowsites[$x];
                        # also load the Fst stat for each window
                        $jack_fst_values[$counter2]=$Fst_values[$x];
                        # keep track of the number of windows
                        $counter2+=1;
                }
        }
        # make the $jack_averagesites an average
        $jack_averagesites=$jack_averagesites/($counter2);
        # calculate the weighted average
        for ($x = 0 ; $x < $counter2; $x++ ) {
                $jack_weighted_average+=($jack_sumsites[$x]*$jack_fst_values[$x]/$jack_averagesites);
        }
        push(@jackarray,($jack_weighted_average/$counter2));
        # reset variables
        $jack_weighted_average=0;
        $jack_averagesites=0;
        @jack_fst_values=();
        $counter2=0;
}

# now calculate the variance of the jackknife replicates

# first we need the mean
my $jack_mean=0;
for ($x = 0 ; $x < $counter; $x++ ) {
        $jack_mean+=$jackarray[$x];
}
$jack_mean=$jack_mean/($counter);

my $jack_var=0;
for ($x = 0 ; $x < $counter; $x++ ) {
        $jack_var+=($jack_mean-$jackarray[$x])**2;
}
# for the sample variance, divide by (n-1)
#print "jack_fst_var ",sprintf("%.9f",$jack_var/($counter-1)),"\n";
my $sterr = sqrt($counter*($jack_var/($counter-1)));
#print "The standard error of the weighted fst is ",sprintf("%.5f",$sterr),"\n";
#print "The 95\%CI of the weighted fst is ",
#sprintf("%.6f",($weighted_Fst_average-1.96*$sterr))," - ",sprintf("%.6f",($weighted_Fst_average+1.96*$sterr)),"\n";


#get col names
my $header = `head -n 1 $inputfile`;
chomp ($header);
my @colnames = split (/,/,$header);

my $pops = @colnames[$chr];

chomp ($pops);
my @popnames = split (/_/,$pops);


# print "\n","\n","\n","summary","\n","\n","\n";
# trying tab seperated fst outputs

#print "pop1","\t","pop2","\t","Fst","\t","CI_1","\t","CI2","\n";

print $popnames[1],"\t",$popnames[2],"\t",sprintf("%.6f",$weighted_Fst_average),"\t",sprintf("%.6f",($weighted_Fst_average-1.96*$sterr)),"\t",sprintf("%.6f",($weighted_Fst_average+1.96*$sterr)),"\n";
}

close DATAINPUT;

```

4. Then run it with something like

```bash
#!/bin/sh
#SBATCH --job-name=bwa_505
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --time=36:00:00
#SBATCH --mem=32G
#SBATCH --output=bwa505.%J.out
#SBATCH --error=bwa505.%J.err
#SBATCH --account=def-ben

#SBATCH --mail-user=premacht@mcmaster.ca
#SBATCH --mail-type=BEGIN
#SBATCH --mail-type=END
#SBATCH --mail-type=FAIL
#SBATCH --mail-type=REQUEUE
#SBATCH --mail-type=ALL

for i in *all_pops_output.csv; do perl test_block_jackknife_withFst.pl ${i} > ${i}_fst_summary.tsv ; done
```
