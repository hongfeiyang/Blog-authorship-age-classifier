This file describes the data for COMP30027 2018S1, Project 2. It is a heavily-altered form of the "Blog Authorship Corpus", available from http://u.cs.biu.ac.il/~koppel/BlogCorpus.htm and described in:
   Schler, Jonathan, Moshe Koppel, Shlomo Argamon, and James Pennebaker (2006) Effects of Age and Gender on Blogging. In the Proceedings of 2006 AAAI Spring Symposium on Computational Approaches for Analyzing Weblogs. Stanford, USA.

The tarball contains 5 files:

- train_raw.csv: This is a file of 276415 training instances, one per line. Each one contains the raw text of a blog entry, and some metadata. The format of the file is as follows:
    User_ID,Gender,Age,Occupation,Star_Sign,Date,Text
  A detailed description of the fields:
    User ID: a number between 5114 and 4336651. All posts by a single user appear in the same data set.
    Gender: this is self-identified, taking either the value "female" or the value "male"
    Age: this is self-identified, taking a value between 13 and 48
    Occupation: this is self-identified, taking one of 39 different values; a number of values were not recorded, which was indicated with the value "indUnk"
    Star_Sign: this is self-identified, taking one of 12 different values
    Date: this is enclosed in quotation marks, as it is comma-delimited
    Text: this is the raw text of a blog entry; it is enclosed in quotation marks, and usually is padded with a number of spaces. HTML formatting has been (mostly) stripped, and hypertext references have (mostly) been replaced by the string "urllink"

- train_top10.csv: This is a file of 276415 training instances, one per line. Each one is a CSV representation of some token frequencies within the blog text. The format of the file is as follows:
    Instance_ID,List_of_30_token_frequencies,Class
  A detailed description of the fields:
    Instance_ID: a number from 1 to 276415, prefixed by the character "1" - so "11" to "1276415"
    List_of_30_token_frequencies: The frequency within the blog text (case-folded, and stripped of non-alphabetic characters) of the following tokens has been recorded:
      anyways
      cuz
      digest
      diva
      evermean
      fox
      gonna
      greg
      haha
      jayel
      kinda
      levengals
      literacy
      lol
      melissa
      nan
      nat
      postcount
      ppl
      rick
      school
      shep
      sherry
      spanners
      teri
      u
      ur
      urllink
      wanna
      work
    Class: this is based on the self-identified Age in the "raw" file. It has been mapped on to four classes, whose names define an inclusive range as follows:
      14-16
      24-26
      34-36
      44-46

- dev_raw.csv: This is a file of 45332 development instances, one per line. Its format is identical to the format of train_raw.csv

- dev_top10.csv: This is a file of 45332 development instances, one per line. Its format is identical to the format of train_top10.csv, except as follows:
    Instance_ID: a number from 1 to 45332, prefixed by the character "2" - so "21" to "245332"
    Class: this is based on the self-identified Age in the "raw" file. Some instances are not within the ranges above, and their class has been recorded as "?"

- README.txt: This is the file you are currently reading.

The following files will be released shortly before the submission deadline:

- test_raw.csv: This is a file of 43014 test instances, one per line. Its format is identical to the format of train_raw.csv, except that the content of the following fields has been replaced by "?":
    Gender
    Age
    Occupation
    Star_Sign
    Date
  If your classifier depends on knowing these values, you will need to build (another) classifier to predict them.

- test_top10.csv: This is a file of 43014 test instances, one per line. Its format is identical to the format of train_top10.csv, except as follows:
    Instance_ID: a number from 1 to 43014, prefixed by the character "3" - so "31" to "343014"
    Class: all instances have been recorded as "?", whether or not the Age falls within one of the categories defined above

The features in the {train,dev,test}_top10 CSV files were determined as follows:
   - the blog posts in train.raw were case-folded, and non-alphabetic characters were removed (tr/[A-Z]/[a-z]/;s/[^a-z ]//g)
   - 627632 different alphabetical "word" types were identified
   - for each class, predictive features were automatically identified based on the presence of the "word" (n.b. not the frequency):
     - the top 10 types, according to Mutual Information
     - the top 10 types, according to Chi-Square
   - these 80 "word" types were sorted, and duplicates were removed, leaving 30 to be used as features
