/* ALL CODE FOR INTRODUCTION TO SAS 9.3 SEMINAR */

*********************************************************
*                   Entering Data                       *
*********************************************************; 

*2.1 Import wizard and  proc import;
proc import datafile="c:\sas_data\hs0.xlsx" dbms = excel replace out=hs0;
 range = "hs0$";
 getnames = yes;
run;

*2.2 Data Steps;
* Infile a comma-separated-values (.csv) file;
data temp;
 infile 'c:\sas_data\hs0.csv' delimiter=',' dsd;
 length prgtype $10;
 input gender id race ses schtyp prgtype $ read write math science socst ;
run;

proc print data = temp (obs=10);
run;

* Enter data directly into SAS using input;
data hsb10;
 input id female race ses schtype $ prog
 read write math science socst;
datalines;
 147 1 1 3 pub 1 47 62 53 53 61
 108 0 1 2 pub 2 34 33 41 36 36
 18 0 3 2 pub 3 50 33 49 44 36
 153 0 1 2 pub 3 39 31 40 39 51
 50 0 2 2 pub 2 50 59 42 53 61
 51 1 2 1 pub 2 42 36 42 31 39
 102 0 1 1 pub 1 52 41 51 53 56
 57 1 1 2 pub 1 71 65 72 66 56
 160 1 1 2 pub 1 55 65 55 50 61
 136 0 1 2 pub 1 65 59 70 63 51
;
run;

proc print data=hsb10;
run;

*2.3 Saving SAS data files;

* Save temporary dataset "temp" as a permanent file;

data 'c:\sas_data\hs0';
 set temp;
run;

proc print data='c:\sas_data\hs0';
run;

libname IN 'c:\sas_data';
data in.hs0; 
  set temp; 
run;

*********************************************************
*                   Exploring Data                      *
*********************************************************; 

* Set output to be left justified rather than centered;
options nocenter;

* Examine data using proc contents and proc print;
proc contents position data=in.hs0;
run;
proc print data=in.hs0 (obs=20);
run;

* If we only want to print some variables, we can use the var statement;
proc print data=in.hs0 (obs=20);
  var gender id race ses schtyp prgtype read;
run;

* Create a temporary dataset called hs0 ;
data hs0;
  set in.hs0;
run;

* Descriptive statistics with proc means and proc univariate;
proc means data=hs0;
run;

proc univariate data=hs0;
   var read write;
run;

* means for a subset of variables using var;
proc means data=hs0 n mean median std var;
  var read math science write;
run;

* means for a subset of variables using var;
proc means data=hs0 n mean median std var;
  where read>=60;
  var read math science write;
run;

* means broken down by group (ses) using class;
proc means data=hs0 n mean median std var;
  class ses; 
  var read math science write;
run;

*  histogram with normal curve overlay from proc univariate;
proc univariate data=hs0 noprint;
  var write;
  histogram / normal;
run;

* Frequency distribution table;
proc freq data=hs0;
  table ses;
run;

* Frequency distribution table;
proc freq data=hs0;
  table gender schtyp prgtype;
run;

* a crosstab using proc freq plus cumulative frequency graph;
proc freq data=hs0;
  table prgtype*ses / plots=freqplot;
run;

* correlations using proc corr with pairwise 
deletion of missing observations (default) ;
proc corr data=hs0; 
  var write read science;
run;

* correlations using proc corr with listwise 
deletion of missing observations (nomiss option) ;
proc corr data=hs0 nomiss; 
  var write read science;
run;

* Scatter plot matrix;
proc corr data=hs0 nomiss plots=matrix;
  var write read science;
run;

* a scatter plot ;
proc sgplot data = hs0;
  scatter x = read  y = write;
run;

* scatter plot with id number a marker;
proc sgplot data=hs0;
  scatter x=write y=read / markerchar=id;
run;

* scatter plot with gender of observation indicated;
proc sgplot data=hs0;
  scatter x=write y=read / group=gender;
run;

* vertical bar chart representing mean of varaible write by ses with error bars;
proc sgplot data=hs0;
  vbar ses /response = write stat=mean limits=both;
run;

* histogram of variable read with normal curve and density plot overlayed;
proc sgplot data=hs0;
  histogram read;
  density read / type=normal;
  density read /type = kernel;
run;

*********************************************************
*                   Modifying Data                      *
*********************************************************; 

*2.1 Proc Format, labels and renaming variables ;

* Examine the dataset;
proc contents data = in.hs0;
run;

* print observations in dataset hs0;
proc print data = in.hs0;
run;

* Create value labels for the variable schtyp;
proc format;
  value scl 1 = "public"
            2 = "private";
run;

* Frequency table using the labels with a format statement;
proc freq data = hs0;
  tables schtyp;
  format schtyp scl.;
run;

proc contents data=hs0;
run;

*  permanently apply a value label to a variable in a data step;
data hs0b;
  set in.hs0;
  format schtyp scl.;
run;
proc contents data=hs0b;
run;
* label the dataset and schtyp;
data hs0b(label="High School and Beyond");
  set hs0b;
  label schtyp = "type of school";
run;

* Rename schtype to public and gender to female in a temporary dataset hs0b;
data hs0b; 
   set hs0b (rename=(schtyp=public gender=female));
   label schtyp = "type of school";
run;

proc contents data=hs0b;
run;

*2.2 Putting things together in a long data step;

*  Proc format followed by a dataset that performs a variety of tasks;
proc format;
  * create value labels for schtyp ;
  value scl 1 = "public"
            2 = "private";

  * create value labels for grade ;
  value abcdf 0 = "F" 
              1 = "D" 
              2 = "C" 
              3 = "B" 
              4 = "A";

  * create value labels for female ;
  value fm 1 = "female"
           0 = "male";

run; 

* create data file hs1, label it  and rename the variable gender to female ;
data hs1(label="High School and Beyond") ;

  set in.hs0 (rename=(gender=female));  

  * label the variable schtyp ;
  label schtyp = "type of school";
  
  * apply value labels to schtyp;
  format schtyp scl.;

  * apply value labels to female;
  format female fm.;

  * the if-then statements create a new variable, called prog,
    which is numeric variable ;
  if prgtype = "academic"   then prog = 1;
  if prgtype = "general"    then prog = 2;
  if prgtype = "vocational" then prog = 3;
    
  * the if statement recodes values of 5 in the variable race to be missing (.) ;
  if race = 5 then race = .;

  * create a variable called total that is the sum of read, write, math, and science ;
  total = read + write + math + science;

  * the if-then statements recode the variable total into the variable grade ; 
  if (total < 80) 			then grade = 0;  
  if (80  <= total  <  110) then grade = 1; 
  if (110 <= total  <  140) then grade = 2; 
  if (140 <= total  <  170) then grade = 3; 
  if (total  >= 170) 		then grade = 4;
  if (total = .) 			then grade = .;

 * apply value labels to variable grade;
  format grade abcdf.;
run;

proc contents data = hs1;
run;
proc print data = hs1 (obs = 20);
run;
proc freq data = hs1;
  tables schtyp*female;
run;

* Save temporary dataset as a permanent dataset;
data in.hs1;
  set hs1;
run;

*2.3 Recoding a continuous variable using formats

*Recoding a continuous variable using formats;
proc format;         
   * create format for test score; 
   value score 25 - 60 = "low score"
	       61 -80 = "high score"; 
run;
	
data hs1_read;
   set hs1;
 * apply value labels to variable read;
 format read score.;
 run;

 * variable read can be used in its original format;
proc means data=hs1_read;
var read;
run; 

 * variable read can be also be used in class statement as categorical;
proc means data=hs1_read;
class read;
  var total;
run;	

*2.4 Creating new variables using procedures; 

* standardize read and write using proc standard;
proc standard data = hs1 mean=0 std=1 out=hs1b;
   var read write ;
run;

* look at the data;
proc print data=hs1b (obs=10);
run;

*2.5 Using SAS functions;

* create variables using SAS function;
data hs1b;
  set hs1;
  total2 = sum(of read write math science);
  * similarly, mean, max, min and more;
  x3 = ordinal(3, read, write, math, science);
  mean= mean(of read write math science);
run;
title "";

proc print data=hs1b (obs=20);
  var read write math science total total2 x3 mean;
run;

*********************************************************
*                   Managing Data                       *
*********************************************************;

*2.1 Creating a library;
libname in "c:\sas_data\";

proc print data=in.hs1 (obs=10);
  var write read science;
run;

proc print data="c:\sas_data\hs1" (obs=10);
  var write read science;
run;

*2.2 Selecting cases using if or where statements;
data highread lowread;
  set in.hs1;
  if read >=60 then output highread;
  if read < 60 then output lowread;
run;

title "high reading scores";
proc means data=highread n mean;
  var read;
run;

title "low reading scores";
proc means data=lowread n mean;
  var read;
run;

title; /* this statement clears the title we set earlier */

* using where statement;
data highread;
  set in.hs1;
  where read >=60;
run;

proc print data = highread;
run;

*2.3 Keeping variables;
* keeping a subset of variables;
data hskept;
  set highread;
  keep id female read write;
run;

*2.4 Dropping variables;
* dropping a subset of variables;
data hsdropped;
  set highread;
  drop ses prog;
run;

*2.5 Appending datasets;

* Look at frequency of variable "female" in each file ;
proc freq data=in.hsmale;
  tables female;
run;

proc freq data=in.hsfemale;
  tables female;
run;

* Use DATA step to combine the two files and save them as hsmasters ;
data in.hsmaster;
  set in.hsmale in.hsfemale;
run;

* Now you should have a file with both males and females;
proc ttest data=in.hsmaster;
  by female;
  var write;
run;

*2.6 Merging datasets;

* examine the two datasets;
proc print data=in.hsdem ;
run;

proc print data=in.hstest ;
run;

* sort both files by the variable that identifies the cases in each file (id);
proc sort data=in.hsdem out=dem;
  by id;
run;

proc sort data=in.hstest out=test;
  by id;
run;

* merge the datasets;
data all;
  merge dem test;
  by id;
run;

proc print data=all;
run;
*********************************************************
*                   Analyzing Data                      *
*********************************************************; 

*2.1 Chi-squared test;
proc freq data=in.hs1;
  table prgtype*ses / chisq expected;
run;

*2.2 T-tests;
* one sample t-test;
proc ttest data=in.hs1 H0=50;
  var write;
run;

* paired t-test;
proc ttest data=in.hs1;
  paired write*read;
run;

* two sample independent t-test;
proc ttest data=in.hs1;
  class female;
  var write;
run;

*2.3 ANOVA;
* Oneway ANOVA with type III sums of squares only;
proc glm data=in.hs1;
  class prog;
  model write=prog / ss3;
run;
quit;

*ancova;
proc glm data=in.hs1;
  class prog;
  model write = read prog / ss3;
run;
quit;

* 2.4 Regression ;
proc reg data=in.hs1;
  model write = female read;
run;
quit;

* OLS with diagnostic plots, this code also outputs a temporary dataset (temp) that contains the 
predicted values of math and the residuals ;
proc reg data =in.hs1 plots=diagnostics;
  model math = write socst;
  output out=temp p=predict r=resid;
run;
quit;

* look at the temporary dataset (temp);
proc print data=temp (obs=20);
  var math predict resid;
run;

*2.5 Logistic regression;
* create a dichotomous variable honcomp;
data hs2;
  set in.hs1;
  honcomp = (write >= 60);
run;

* Logistic regression with descending option (so model predicts 1s rather than 0s);
proc logistic data=hs2 descending;
  model honcomp = female read;
run;

*2.6 Nonparametric tests;
* signtest (nonparametric analog of the single sample t-test);
proc univariate data=in.hs1 mu0=50;
  var write;
run; 

* signrank test (nonparametric analog of the paired t-test);
* create the difference variable (diff);
data hs1c;
  set in.hs1;
  diff = read - write;
run;

* test that diff=0;
proc univariate data=hs1c;
  var diff;
run;

* ranksum (nonparametric analog of the independent two-sample t-test);
proc npar1way data=in.hs1;
  class female;
  var write;
run;

* kruskal wallis  (nonparametric analog of the one-way ANOVA);
proc npar1way data=in.hs1;
  class ses;
  var write;
run;
