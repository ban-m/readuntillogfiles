# Log file of Read Until experiment
- Author: Bansho Masutani<banmasutani@gmail.com>

## Remark:

The Dyss packeges was moved to a [GitHub repository](https://github.com/ban-m/dyss), as BitBucket no longer support Mercurial repositories. (2020/09/08)


## Short Summary
  This repository contains log files obtained during sequencing with "Read Until" API bundled with MinION sequencer.
  One may find it useful when validating/questioning about results in our paper. For example, if you want to know how quickly our algorithm can process each query in replicate no.2,  you can just type the following unix command:
  ```
  cat ./logfile-replicate-2/*.log | grep "processing "
  ```

  If you want to see the result itself(i.e. fast5 files), see [repository in sequence read archive](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA445929).

## Description
  Generally speaking, file with .log extention contains the standard err from "ReadUntil"API and our algorihtms and .out extention contains the summary of the experiment.

Each folder corresponds to the experiment described in the paper as follows:

+ ./logfile-replicate-1 <-> table2. repr1.
    - The experiment was carried out for about 18.5 hours and the order of log files is
        - 2018-02-24-dyss-sc-record-test.log : 1 minute
        - 2018-02-24-dyss-sc-record.log : 2.5 hours
        - 2018-02-24-dyss-sc-record-1300.log : 5 hours
        - 2018-02-24-dyss-sc-record-1805.log : 5 hours
        - 2018-02-24-dyss-sc-record-2307.log : 6 hours
    - The information contained in Dyss section may not be so useful, because Dyss assumed every "batch" of the queries was 30 length long.
+ ./logfile-replicate-2 <-> table2. repr2.
    - The experiment was carried our for about 18.5 hours and the order of log file is
        - 2018-02-28-dyss-sc-1315.log : 1 minute
        - 2018-02-28-dyss-sc-record-1315.log : 3.5 hours
        - 2018-02-28-dyss-sc-record-1555.log : 3 hours
        - 2018-02-28-dyss-sc-record-1825.log : 6 hours
        - 2018-02-28-dyss-sc-record-0130.log : 6 hours
    - The information contained in Dyss section may not be so useful, because Dyss assumed every "batch" of the queries was 30 length long.
+ ./logfile-hotswap <-> Fig4.
    - The experiment was carried our for 5.5 hours for chr01,an internally error of MinKNOW occured, then 9 hours for chr02.
        - 2018-03-14-dyss-sc-1500.log : for chr01, 5.5 hours.
        - 2018-03-14-dyss-sc2-2105.log : for chr02, 2 hours.
        - 2018-03-14-dyss-sc2-2300.log : for chr02, 7 hours.
+ ./logfile-ecoli <-> Table 3. repl1 and 2.
    - The experiment was carried our for 18.5 hours and 4.5 hours, for two biological replicate, respectively.
        - 2018-06-27-ecoli.log: for 4.5 hours run.
        - 2018-06-28-ecoli.log: for 18.5 hours run.

## Comment

  There is a plenty of room to improve the performance of our algorithm implimentation.
  
  For example, we can `grep Chunked` for .log file to see that the chunking was carried for 6000 long queries.
  This suggests that the classification applied for the raw signal as long as 6000, which is too long for current DTW scoring system, which use first 250 events(~ 2000 signals).
  
  In addition, we can `grep "Interval" | grep -v "[^d]0 query in queue` to see that the classifier was not so good at catching up the throuput of a sequencer during first a few hours.
  Even though this phenomenon disappear in a few hours and this consisits a small fraction of entire procedure(48 hours), we may fix this problem by using a hash function for DTW.


## Parameter tuning and others

+ For those interested in parameter tuning of hill function, see [this repository](https://github.com/ban-m/hill_function_fitting)
+ For those interested in score in Table 1., see [this repository](https://github.com/ban-m/score_calculate)
+ For those interested in speed checking in Table 1., see [this repository](https://github.com/ban-m/long_reference_speedcheck)
