# Log file of Read Until experiment

- Author: Bansho Masutani<banmasutani@gmail.com>

## Short Summary
  This repository contains some log files obtained during sequencing runs with "Read Until" API bundled with MinION sequencer.
  One may find it informative when validating/questioning about results in our paper which is published soon.
  For example, if you want to know how quickly our algorithm can process each query in replicate 2,
  you can just type the following unix command:
  ```
  cat ./logfile-replicate-2/*.log | grep "processing "
  ```


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
    + The information contained in Dyss section may not be so useful, because Dyss assumed every "batch" of the queries was 30 length long.
  
    + ./logfile-replicate-2 <-> table2. repr2.
        - The experiment was carried our for about 18.5 hours and the order of log file is
            - 2018-02-28-dyss-sc-1315.log : 1 minute
            - 2018-02-28-dyss-sc-record-1315.log : 3.5 hours
            - 2018-02-28-dyss-sc-record-1555.log : 3 hours
            - 2018-02-28-dyss-sc-record-1825.log : 6 hours
            - 2018-02-28-dyss-sc-record-0130.log : 6 hours
    + ./logfile-hotswap <-> Fig4.
        - The experiment was carried our for 5.5 hours for chr01,an internally error of MinKNOW occured, then 9 hours for chr02.
            - 2018-03-14-dyss-sc-1500.log : for chr01, 5.5 hours.
            - 2018-03-14-dyss-sc2-2105.log : for chr02, 2 hours.
            - 2018-03-14-dyss-sc2-2300.log : for chr02, 7 hours.
  

## Comment

  There is a plenty of room to improve the performance of our algorithm implimentation.
  
  For example, we can ``` grep Chunked ``` for .log file to see that the chunking was carried for 6000 long queries.
  This suggests that the classification applied for the raw signal as long as 6000, which is a kind of 'over-kill' for current DTW scoring system using first 250 events(~ 2000 signals).
  
  In addition, we can ``` grep "Interval" | grep -v "[^d]0 query in queue" to see that the classifier was not so good at catching up the throuput of a sequencer.
  Even though this phenomenon disappear in a few hours and this consisits a small fraction of entire procedure(48 hours), we may fix this problem by using a hash function for DTW.

