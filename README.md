# Code to gather Ngrams from google books

### Data source
The data is take from [googles ngrams](http://storage.googleapis.com/books/ngrams/books/datasetsv3.html)

The ngrams are stored as large compressed files that are sorted and split by size.

The format is: ngram TAB year TAB match_count TAB volume_count (Repeat) TAB year TAB match_count TAB volume_count, ... 

Each files size is around 400MB - 500MB and around 1400MB if you extract it for the 2grams. As n changes, the file size and amount may change. n = 1 has 24, n = 2 has 489,  n = 3 has 6881, n = 4 has 6668, n = 5 has 19423 files.

### Extraction method 

I used python to get the data. I processed the data one file at a time with a buffer without saving the file. I processed each file selecting words without parts of speech tags and summing the total occurrence from 1990 to February 2020. I then used a priority queue and took the top 1000 items. I then saved the file. There is an example of an intermediate random file for the bigram showing the occurrence then the ngram:

A Pr intermediate file for bigram:  
    (14561073, 'Proceedings of'),  
    (10833244, 'Prime Minister'),  
    (10588830, 'Proc .'),  
    (7036010, 'Prior to'),  
    (6596211, 'Professor of'),  
    (5769636, 'Program ,'),  
    (5600473, 'Princeton University'),  
    (4533204, 'Program .'),  

I will mention that I skipped over _ symbol because there are part of speech tags within the data that I am uninterested in. This also means I skipped _ symbol though, which won't be in a common ngram for my use case.

### Merging method

I then created another priority queue with a size of 10,000 and went through each file. I used 2 priority queues to take ngrams with and without symbols or special characters. The files were saved.

A 2gram without symbols or special characters file:  
    (5300515095, 'of the')  
    (2950334073, 'in the')  
    (1939208961, 'to the')  
    (1250796674, 'and the')  
    (1191540665, 'on the')  
    (949312195, 'for the')  
    (890209782, 'to be')  
    (786258968, 'of a')  
 
### The data

The data files are too large, so I only included the 1 gram and 2 gram with no symbols data. If you want access to the raw data create an issue and i'll find another way to get it.
 
### Future work

Right now, I have only collected ngrams for n = 1 and 2. It takes a lot of time to download and unzip the files. In the future I would like to use a cloud provider and create several instances at once to speed the job up/ make it feasible.

