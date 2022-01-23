# SAS TUTORIAL FOR BEGINNERS TO ADVANCED - PRACTICAL GUIDE 


1.01 - Beginner guide

*I. SAS Modules*
- Base SAS - It is the most common SAS module. It is used for data manipulation such as filtering data, selecting, renaming or removing columns, reshaping data etc.
- SAS/STAT - It runs popular statistical techniques such as Hypothesis Testing, Linear and Logistic Regression, Principal Component Analysis etc.
- SAS/ACCESS - It lets you to read data from databases such as Teradata, SQL Server, Oracle DB2 etc.
- SAS/GRAPH - You can create simple and complex graphs using this component.
- SAS/ETS - You can perform time series forecasting such as ARIMA, Exponential Smoothing, Moving Average etc. using this module.

*II. Basic SAS Program*
- I. Rules for SAS statements
- All SAS statements (except those containing data) must end with a  semicolon (;)
- Any number of SAS statements can appear on a single line provided they are separated by a semicolon.
- SAS statements typically begin with a SAS keyword. (DATA, PROC)
- SAS statements are not case sensitive, that is, they can be entered in lowercase, uppercase, or a mixture of the two.
- A delimited comment begins with a forward slash-asterisk (/*) and ends with an asterisk-forward slash (*/). All text within the delimiters is ignored by SAS.
- II. Rules for SAS names
- All names must contain between 1 and 32 characters. 
- The first character appearing in a name must be a letter (A, B, ...Z, a, b, ... z) or an underscore (_). Subsequent characters must be letters, numbers, or underscores. That is, no other characters, such as $, %, or & are permitted. Blanks also cannot appear in SAS names.
- SAS names are not case sensitive, that is, they can be entered in lowercase, uppercase, or a mixture of the two. (SAS is only case sensitive within quotation marks.).

*III. Rules for SAS variables*
- If the variable in the INPUT statement is followed by a dollar sign ($), SAS assumes this is a character variable. Otherwise, the variable is considered as a numeric variable.
Difference between 'PROC' steps and 'DATA' step
- DATA Steps
- Any portion of a SAS program that begins with a DATA statement and ends with a RUN statement is called a DATA Step.
- DATA steps are used to manage data.  In detail, DATA steps are used to read raw or external data into a SAS data set, to modify data values, and to subset or merge data sets
- PROC Steps (Procedures)
- Any portion of a SAS program that begins with a PROC statement and ends with a RUN statement is called a PROC Step or Procedures.
- PROC steps are in-built programs that allow us to analyze the data contained in a SAS data set. PROC steps are used to calculate descriptive statistics, to generate summary reports, and to create summary graphs and charts.

*Example*

/*A Simple SAS Program*/
data temp;
input name $ ID;
cards;
Sam 12
Sandy 13
Reno 11
Farhan 10
;
proc print;
run;

*IMPORTING DATA INTO SAS*
I. Entering Data Directly in SAS Program
The keywords are as follows:
1. DATA -  The DATA step always begins with a DATA statement. The purpose of the DATA statement is to tell SAS that you are creating a new data set i.e. outdata.
2. INPUT -  To define the variables used in data set.
3. Dollar sign ($) - To identify variable as character.
4. DATALINES - To indicate that lines following DATALINES statement a real data.(We can use Cards instead of Datalines)
5. PROC PRINT - To print out the contents of data set in output window.
6. RUN - The DATA step ends with a RUN statement.


*Example*
DATA outdata; 
   INPUT age gender $ dept obs1 obs2 obs3; 
   DATALINES; 
1 F 3 17 6 24
1 M 1 19 25 7
3 M 4 24 10 20
3 F 2 19 23 8
2 F 1 14 23 12
2 M 5 1 23 9
3 M 1 8 21 7
1 F 1 7 7 14
3 F 2 2 1 22
1 M 5 20 5 2
3 M 4 21 8 18
1 M 4 7 9 25
2 F 5 10 17 20
3 F 4 21 25 7
3 F 3 9 9 5
3 M 3 7 21 25
2 F 1 1 22 13
2 F 5 20 22 5
;
proc print;
run;


Reading Delimited Data
- The default delimiter is blank. If you have a data file with other delimiters such as comma or tab you need to define the delimiter before defining the variables using INFILE and DLM = options.
- For tab delimiter, the syntax would be infile 'file-description' dlm='09'x
- For colon delimiter, the syntax would be infile 'file-description' dlm=':'


*Example* - Reading Delimited Data

DATA outdata; 
   INFILE Datalines dlm =",";
   INPUT age gender $ dept obs1 obs2 obs3; 
   Datalines; 
1,F,3,17,6,24
1,M,1,19,25,7
3,M,4,24,10,20
3,F,2,19,23,8
2,F,1,14,23,12
;
proc print;
run;


Importing External Data into SAS
Method I : PROC IMPORT

PROC IMPORT is a SAS procedure to import external files into SAS. It automates importing process. You don't need to specify variable type and variable length to import an external file. It supports various formats such as excel file, csv, txt etc.

1. Importing an Excel File into SAS
The main keywords used in the following program are :
1. OUT - To specify name of a data set that SAS creates. In the program below, outdata is the data set saved in work library (temporary library)
2. DBMS - To specify the type of data to import.
3. REPLACE - To overwrite an existing SAS data set.
4. SHEET - To import a specific sheet from an excel workbook
5. GETNAMES - To include variable names from the first row of data.

*Example* - Importing xls files into sas

PROC IMPORT DATAFILE= "c:\deepanshu\sampledata.xls"
OUT= outdata
DBMS=xls   
REPLACE;
SHEET="Sheet1";
GETNAMES=YES;
RUN;

2. Importing a Tab-Delimited File into SAS
The program below is similar to the code of importing excel file. The only difference is DBMS = DLM and delimter = '09'x.

*Example* - a Tab-Delimited File into SAS

PROC IMPORT DATAFILE= "c:\deepanshu\sampledata.txt"
OUT= outdata
DBMS=dlm
REPLACE;
delimiter='09'x;
GETNAMES=YES;
RUN;

3. Importing a Comma-Delimited File with TXT extension

To get comma separated file with a txt extension into SAS, specify delimeter = ','

*Example - Importing a Comma-Delimited File with TXT extension

PROC IMPORT DATAFILE= "c:\deepanshu\sampledata.txt"
OUT= outdata
DBMS=dlm
REPLACE;
delimiter=',';
GETNAMES=YES;
RUN;

4. Importing a Comma-Delimited File with CSV extension

To get comma separated file into SAS, specify DBMS= CSV

*Example - Importing a Comma-Delimited File with CSV extension ( converting from text to csv )

PROC IMPORT DATAFILE= "c:\deepanshu\sampledata.txt"
OUT= outdata
DBMS=csv
REPLACE;
GETNAMES=YES;
RUN;

5. Importing a Space-Delimited File

To extract a space delimited file, specify delimiter = '20'x

*Example -  Importing a Space-Delimited File
PROC IMPORT DATAFILE= "c:\deepanshu\sampledata.txt"
OUT= outdata
DBMS=dlm
REPLACE;
delimiter='20'x;
GETNAMES=YES;
RUN;

6. Importing a file containing multiple delimiter

If two or more delimiters, such as comma and tabs, quote them following delimiter = option

*Example -  Importing a file containing multiple delimiter

PROC IMPORT DATAFILE= "c:\deepanshu\sampledata.txt"
OUT= outdata
DBMS=dlm
REPLACE;
delimiter=','09'x ';
GETNAMES=YES;
RUN;


Method II : Get External File - INFILE

In SAS, there is one more method called INFILE to import an external file. It's a manual method of importing an external file as you need to specify variables and its types and length.

1. Reading a CSV File

INFILE statement - To specify path where data file is saved.
DSD - To set the default delimiter from a blank to comma.
FIRSTOBS=2 : To tell SAS that first row contains variable names and data values starts from second row.

*Example -Reading a CSV File *

data outdata; 
infile 'c:\users\deepanshu\documents\book1.csv' dsd firstobs=2;
input id age gender $ dept $; 
run;

2. Reading a TAB Delimited File

We can use DLM='09'x to tell SAS that we are going to import a tab delimited file. The TRUNCOVER statement tells SAS to assign the raw data value to the variable even if the value is shorter than expected by the INPUT statement.

*Example -Reading a TAB Delimited File*

data outdata;
  infile 'c:\deepanshu\dummydata.txt' DSD dlm='09'x truncover;
  input employee :$30. DOJ :mmddyy8. state :$20.;
run;

*Example -Using a FILENAME statement to handle an external file.*

FILENAME sample 'c:\deepanshu\sampledata.csv' ;
DATA outdata;
infile sample dsd;
INPUT age gender $ dept obs1 obs2 obs3;
run;


2.01 -  Important SAS Shortcuts for Productivity



The following is a list of productivity boosting SAS keyboard shortcuts. It would bring efficiency in writing SAS programming code.

Run or submit a program	F3 or F8
Comment the selected code (/)	Ctrl + /
Uncomment the selected code (/)	Ctrl + Shift + /
Stop Processing or Cancel Submitted Statement	Ctrl + Break
Convert selected text to upper case	Ctrl + Shift + U
Convert selected text to lower case	Ctrl + Shift + L
Find text	Ctrl + F
Find and replace text	Ctrl + H
Copy Selection	Ctrl + C
Paste	Ctrl + V
Cut Selection	Ctrl + X
Go to a particular line	Ctrl + G
To move curser to the matching DO/END statemen	Alt + [ or Alt + ]
To move cursor to matching brace/parentheses	Ctrl + [ or Ctrl + ]
Move to beginning of line	Home
Move to top	CTRL+Home
Move to end	CTRL+End
To close the active window	CTRL+F4
To exit the SAS system	ALT+F4

Important Shortcuts that work only in SAS Enterprise Guide

Description	Shortcut Key
Ctrl+End	Go to the last record, last column
Ctrl+Home	Go to the first record, first column
Ctrl+G	Go to specific row or column
Ctrl + right arrow	Move to last column
Ctrl + left arrow	Move to first column
F2	Rename dataset
Ctrl + I	Format ugly code (Select the code and press Ctrl I)


Other Useful SAS Keyboard Shortcuts

Description	Shortcut Key
Bring up word tip	Alt + F1 + No Selection
Hide the current word tip	Esc
Collapse all folding blocks	Alt + Ctrl + Number pad -
Expand all folding blocks	Alt + Ctrl + Number pad +
Execute the last recorded macro	Ctrl + F1
Undo edit	Ctrl + Z
Redo edit	Ctrl + Y
Clear window	Ctrl + E
Paste program below	F4
Get Help for a SAS procedure	Place the cursor within a procedure name and press F1
Context Help	F1
Move cursor to next case change	Alt + Right
Move cursor to previous case change	Alt + Left
File window	Ctrl + Q
Explorer window	Ctrl + W
Titles window	Ctrl + T
System options window	Ctrl + I
Open file window	Ctrl + O
Save as window	Ctrl + S
Active libraries window	Ctrl + D
Select all	Ctrl + A
Clean up white space	Ctrl + Shift + W
Comment the selection with line comments	Ctrl + /
Undo the Comment	Ctrl + Shift + /
Convert the selected text to lowercase	Ctrl + Shift + L
Convert the selected text to uppercase	Ctrl + Shift + U
Submit selected code	F8
Log	F6
Output	F7
Editor	F8
Keys	F9
Next Window	Ctrl + Tab
Tile	Shift + F4
Cascade	Shift + F5
Next window	Ctrl + F6

How to create keyboard shortcuts in SAS

Open the Enhanced Editor window within SAS.
From the toolbar, select Tools --> Options --> Keys.
Scroll down to the keystroke you would like to assign to the series of commands, looking for a keystroke that has no assignment.
Add the command code under the definition heading. For example: log; clear; output;clear;
Close the Keys window.


3.01 - Base SAS Tutorials

SAS : READ CHARACTER VARIABLE OF VARYING LENGTH

Method I : Use COLON Modifier
We can use colon modifier : to tell SAS to read variable "Name" until there is a space or other delimiter. The  $30. defines the variable as a character variable having max length 30.

*Example - to define length of variable (Name :$30.)

input ID Name :$30. Score;
cards;
1 DeepanshuBhalla 22
2 AttaPat 21
3 XonxiangnamSamnuelnarayan 33
;
proc print noobs;
run;

*Example - to define length of variable, using $ - does not delimit comma in fee (1,000)*

data ex2;
input ID Name:$30. Score fee:$10.;
cards;
1 DeepanshuBhalla 22 1,000
2 AttaPat 21 2,000
3 XonxiangnamSamnuelnarayan 33 3,000
;
run;


*Example - to define length of variable, using comma - will delimit comma removes it ( fee - 1000)*

comma5. informat removes comma and store it as a numeric variable. 5 refers to width of the input field. To read bigger number like 3,000,000, you can use comma10.

data ex2;
input ID Name:$30. Score fee comma5.;
cards;
1 DeepanshuBhalla 22 1,000
2 AttaPat 21 2,000
3 XonxiangnamSamnuelnarayan 33 3,000
;
run;

Method II : Use LENGTH statement prior to INPUT Statement (Lengthy)

In the following program, we use a length statement prior to input statement to adjust varying length of a variable. In this case, the variable Name would be read first. Use only $ instead of $30. after "Name" in INPUT statement. 

It changes the order of variables as the variable Name would be read first. 


data example2;
length Name $30.;
input ID Name $ Score;
cards;
1 DeepanshuBhalla 22
2 AttaPat 21
3 XonxiangnamSamnuelnarayan 33
;
proc print noobs;
run;

Method III : Use Ampersand (&) and Put Extra Space

We can use ampersand (&) to tell SAS to read the variable until there are two or more spaces as a delimeter. This technique is very useful when the variable contains two or more words. For example, if we have observation like "Deepanshu Bhalla" rather than "DeepanshuBhalla".


*Example - to define length of variable, using & before $ to delimit - space

data example1;
input ID Name & $30. Score;
cards;
1 DeepanshuBhalla  22
2 AttaPat  21
3 XonxiangnamSamnuelnarayan  33
;
proc print noobs;
run;

Example II : When a variable contains more than 1 word

In this case, we have a space between First Name and Last Name and we want to store both the first and last names in a single variable.

In this case, the following methods do not work.

Colon modifier (:) does not work for a variable having multiple words
 LENGTH Statement prior to INPUT Statement does not work here.

data example1;
input ID Name & $30. Score;
cards;
1 Deepanshu Bhalla  22
2 Atta Pat  21
3 Xonxiangnam Samnuelnarayan  33
;
proc print noobs;
run;

*Example - reading data from external file.

data temp;
infile "C:\Users\Deepanshu\Desktop\file1.txt";
input ID Name & $30. Score;
proc print noobs;
run;

4.01 -SAS : CREATING OR MODIFYING A VARIABLE

I. Creating a numeric variable

You create variables using the form:  variable = expression;

Suppose you are asked to create a new variable NewPrice, in the existing SAS data set Example1.
Both variables are numeric. The variable NewPrice is twice of OldPrice.

*Example - creating a new numerical veriable*

DATA Example1;
SET Example1;
NewPrice=2*OldPrice;
RUN;

II. Creating a character variable

In the same dataset Example1, let's create a character variable say Type. The character value for set is set 'Good'.

*Example - creating a new character variable*
DATA Example1;
SET Example1;
Type = 'Good';
RUN;

III. Creating or Modifying a variable

Suppose the value of OldPrice is increased by 5 units and you need to calculate the relative change in price. In this case, we are modifying the existing variable OldPrice so we will add 5 to OldPrice. later we calculate the percentage change between old and new price.


*Example - Creating or Modifying a variable*

DATA Readin;
SET Example1;
OldPrice=5 + OldPrice;
NewPrice=OldPrice*2;
Change= ((NewPrice-OldPrice)/ OldPrice);
Format Change Percent10.0;
RUN;

The FORMAT statement is used to display the change value in percentage format. In this case, we are creating a new dataset as well.


5.01 - DROPPING VARIABLES FROM A DATA SET IN SAS

n SAS, there are two ways to handle dropping variables :
1.  DROP = data set option
2. DROP statement

*Example- Base*

DATA outdata; 
   INPUT age gender $ dept obs1 obs2 obs3; 
   DATALINES; 
1 F 3 17 6 24
1 M 1 19 25 7
3 M 4 24 10 20
3 F 2 19 23 8
2 F 1 14 23 12
2 M 5 1 23 9
3 M 1 8 21 7
1 F 1 7 7 14
3 F 2 2 1 22
1 M 5 20 5 2
3 M 4 21 8 18
1 M 4 7 9 25
2 F 5 10 17 20
3 F 4 21 25 7
3 F 3 9 9 5
3 M 3 7 21 25
2 F 1 1 22 13
2 F 5 20 22 5
;
proc print;
run;

I.  Scenario : Create a new variable based on existing data and then drops the irrelevant variables ( Using Drop Statement).

By using the DROP statement, we can command SAS to drop variables only at completion of the DATA step.

*Example - Using drop statement after completion of data step( to extract relevant data in new colomn before dropping).* 

data readin;
set outdata;
totalsum = sum(obs1,obs2,obs3);
drop obs1 obs2 obs3;
run;

In this case drop = option is not recommendable because the variables obs1,obs2 and obs3 are not available for use after data set outdata has been copied into the new data set readin . Hence totalsum would contain missing values only.

data readin;
set outdata (drop = obs1 obs2 obs3);
totalsum = sum(obs1,obs2,obs3);
run;

II. DROP statement can be used anywhere in DATA steps whereas DROP = option must follow the SET statement.

*Example - Using DROP statement to drop variables* 
/ Commnd to drop age and show variables in which gender= age/

data readin;
set outdata;
if gender = 'F';
drop age;
run;

*Example - Using DROP = Option to drop variables using SET statement* 
/ Commnd to drop age and show variables in which gender= age/
data readin;
set outdata (drop = age);
if  gender = 'F';
run;

6.01 - SAS : IF-THEN-ELSE STATEMENTS
Symbolic	Mnemonic	Meaning	Example
=	EQ	equals	IF gender = ‘M’; or
			
			IF gender EQ ‘M’;
^= or ~=	NE	not equal	IF salary NE . ;
> 	GT	greater than	IF salary GT 4500;
< 	LT	less than	IF salary LT 4500;
>=	GE	greater than or equal	IF salary GE 4500;
<=	LE	less than or equal	IF salary LE 4500;
in	IN	selecting multiple values	IF country IN(‘US’ ’IN’);

1. IF statement
IF (condition is true) => It means subsetting a dataset.
*Example - If statement - true condition* 

LE - less than equal to 
LT - less than 

Data readin;
Input ID Q1-Q3;
cards;
85 1 2 3
90 3 4 6
95 5 5 6
100 6 6 4
105 5 5 6
110 6 6 5
;

Data readin1;
Set readin;
IF ID LE 100;
run; 

2. IF-THEN DELETE
IF (condition is true) THEN (delete the selected observations);
*Example - IF-THEN DELETE*
Data readin;
Input ID Q1-Q3;
cards;
85 1 2 3
90 3 4 6
95 5 5 6
100 6 6 4
105 5 5 6
110 6 6 5
;

Data readin1;
Set readin;
IF ID GT 100 THEN DELETE;
run; 

II. IF-THEN-ELSE Statement

Task 2: Suppose you want to set a tag on all the IDs. The condition is :

If value of ID is less than or equal to 100 set "Old" tag otherwise set "New" tag.

IF (condition is true) THEN (perform this action);
ELSE (perform the action that is set when condition is false);

*Example - If - Else statement*
Data readin;
Input ID Q1-Q3;
cards;
85 1 2 3
90 3 4 6
95 5 5 6
100 6 6 4
105 5 5 6
110 6 6 5
;

Data readin1;
Set readin;
IF ID LE 100 THEN TAG ="Old";
ELSE TAG ="New";
run;

III. IF-THEN-ELSE IF Statement

Task 3: Suppose you are asked to update the TAG column.
The conditions for tagging are as follows :
If value of ID is less than 75 then TAG = "Old"
If value of ID is greater than or equal to 75 and less than 100 then TAG = "New"
If value of ID is greater than or equal to 100 then TAG = "Unchecked"
IF (condition is true) THEN (perform this action);
ELSE IF (perform the action when second condition is true);
ELSE IF (perform the action when third condition is true);

*Example - If - Else IF statement* 
( Length Tag $20 is used to define length of character ( by default the length is 3)
Data readin;
Input ID Q1-Q3;
cards;
70 1 2 3
45 1 2 3
85 1 2 3
25 1 2 3
90 3 4 6
95 5 5 6
100 6 6 4
105 5 5 6
110 6 6 5
;

Data readin1;
Set readin;
length TAG $20;
IF ID < 75 THEN TAG ="Old";
ELSE IF 75 <= ID < 100 THEN TAG = "New"; 
ELSE IF ID >= 100 THEN TAG ="Unchecked";
run; 


Symbolic	Mnemonic	Meaning	Example
&	AND	Both conditions true	IF gender =’M’ and age =1;
|	OR	Either condition true	IF gender =’M’ or age =1;
~ or ^	NOT	Reverse the statement	IF country not IN(‘US’,’IN’);

Task 4: Suppose you want to generate an analysis for Q1 including only responses that are valid (non-missing) and less than 3.

*Example-logical operator*
Data readin;
Input ID Q1-Q3;
cards;
85 1 2 3
90 . 4 6
95 2 5 6
100 6 6 4
105 . 5 6
110 6 6 5
;

Data readin1;
Set readin;
IF (Q1 LT 3) AND (Q1 NE .);
run; 

Selecting Multiple Observations :

Suppose you want to set tag "Incorrect" to the specified IDs 1,5,45,76

For this case, the logical statement would look like any one of the following statements. It can be written in three ways shown below.

*Example - Selecting multiple Observations*

Method 1  - IF Q1  in (1 5 3) then Tag="Uncategorised";
Method 2 -  IF Q1=1 or Q1=5 or Q1=3 then Tag="Uncategorised";
Method 3 - IF Q1  in (1, 5, 3) then Tag="Uncategorised";

Data readin1;
Set readin;
Length Tag $20.;
IF Q1 or Q2 or Q3 in (1 5 3) then Tag="fnk u";
proc print;
run;

(IN Operator

IN operator is used to select multiple values of a variable. It is an awesome alternative to OR operator.)

7.01 - SAS : WHERE STATEMENT AND DATASET OPTIONS

Symbolic	Mnemonic	Meaning	Example
=	EQ	equals	WHERE gender = ‘M’; or
			
			WHERE gender EQ ‘M’;
^= or ~=	NE	not equal	WHERE salary NE . ;
> 	GT	greater than	WHERE salary GT 4500;
< 	LT	less than	WHERE salary LT 4500;
>=	GE	greater than or equal	WHERE salary GE 4500;
<=	LE	less than or equal	WHERE salary LE 4500;
in	IN	selecting multiple values	WHERE country IN(‘US’ ’IN’);

*Example - using Where statement *

data readin;
input name $ Section $ Score;
cards;
Tom  A 84
Raj  A 80
Ram  B 71
Atul A 77
Priya B 45
Sandy A 67
Sam  A 57
David B 39
Wolf B 34
Rahul A 95
Sahul C 84
Lahul C 44
;
run;

data readin1;
set readin;
where Section EQ "A";
run;

Task2 : Suppose you want to select section A and B students. You know the variable Section contains information for students' sections.

*Example - using Where statement (logical operatiors) *

data readin;
input name $ Section $ Score;
cards;
Tom  A 84
Raj  A 80
Ram  B 71
Atul A 77
Priya B 45
Sandy A 67
Sam  A 57
David B 39
Wolf B 34
Rahul A 95
Sahul C 84
Lahul C 44
;
run;

data readin1;
set readin;
where Section IN ("A" "B");
run;

Task 3 : Suppose you want to select only those observations in which students did not fill their section information.

*Example - using Where statement to find missing values*

data readin;
input name $ Section $ Score;
cards;
Tom  A 84
Raj  A 80
Ram  B 71
Atul . 77
Priya . 45
Sandy A 67
Sam  A 57
David B 39
Wolf B 34
Rahul . 95
Sahul C 84
Lahul C 44
;
run;

data readin1;
set readin;
where Section is missing;
run;

Note - Missing value does not give output in print format.


data readin;
input name $ Section $ Score;
cards;
Tom  A 84
Raj  A 80
;
run; ( include this while using  command for output data) 

data readin1;
set readin;
where Section is missing;
run;

Task 4 : Suppose you want to select only those observations in which students filled their section information. 

*Example - using Where statement to find Non-Missing Values values*
 
data readin;
input name $ Section $ Score;
cards;
Tom  A 84
Raj  A 80
Ram  B 71
Atul . 77
Priya . 45
Sandy A 67
Sam  A 57
David B 39
Wolf B 34
Rahul . 95
Sahul C 84
Lahul C 44
;
run;

data readin1;
set readin;
where section is not missing;
run;

The NOT operator can be used within WHERE statement in many ways :

1. where section is missing and score is not missing;

2. where not (score in (34,44,84));

3. where not (Score between 50 and 75);

4. where NOT(Section EQ "A"); 

CONTAINS Operator : Searching specific character
Task 5 : Suppose you want to select only those observations in which students' name contain 'hul'.

*Example - using Where statement to Search specific character*

data readin;
input name $ Section $ Score;
cards;
Tom  A 84
Raj  A 80
Ram  B 71
Atul . 77
Priya . 45
Sandy A 67
Sam  A 57
David B 39
Wolf B 34
Rahul . 95
Sahul C 84
Lahul C 44
;
run;

data readin1;
set readin;
where name contains 'hul';
run;

where name contains 'hul' => This would tell SAS to select observations having the values Rahul, Sahul and Lahul for the variable NAME.

Note : The CONTAINS operator is case sensitive.

LIKE Operator : Pattern Matching

The LIKE operator selects observations by comparing the values of a character variable to a specified pattern. It is case sensitive.

Task6 : To select all students with a name that starts with the letter S.

There are two special characters available for specifying a pattern:

1. percent sign (%) - Wildcard Character

2. underscore ( _ ) - Fill in the blanks


*Example - using (% -  Wildcard Character)  to Search pattern matching character*
Note : to find name starting with S 
Use S% ( vice-versa)

data readin;
input name $ Section $ Score;
cards;
Tom  A 84
Raj  A 80
Ram  B 71
Atul . 77
Priya . 45
Sandy A 67
Sam  A 57
David B 39
Wolf B 34
Rahul . 95
Sahul C 84
Lahul C 44
Pahulk A 81
;
run;

data readin1;
set readin;
where name like 'S%';
run;


*Example - using  ( _ - Underscore )  to Search pattern matching character*
 Note : to find  wolf using _ ( use '__lf' or 'wo__' 2 underscore for 2 missing values)
data readin;
input name $ Section $ Score;
cards;
Tom  A 84
Raj  A 80
Ram  B 71
Atul . 77
Priya . 45
Sandy A 67
Sam  A 57
David B 39
Wolf B 34
Rahul . 95
Sahul C 84
Lahul C 44
Pahulk A 81
;
run;
data readin1;
set readin;
where name like '_lf';
run;


Sounds-like Operator : Selecting sound like characters
Task7 : To select names that sound like 'Ram'.

*Example - to Search Sounds-like Operator*

data readin;
input name $ Section $ Score;
cards;
Tom  A 84
Raj  A 80
Ram  B 71
Atul . 77
Priya . 45
Sandy A 67
Sam  A 57
David B 39
Wolf B 34
Rahul . 95
Sahul C 84
Lahul C 44
Pahulk A 81
Rama A 84
;
run;

data readin1;
set readin;
where name = *'Ram';
run;

WHERE = Data Set Option

1. In the example shown below, the WHERE= data set option is used to select only section A data.

data readin1 (where = (section ='A'));
set readin;
run;

2. The following example shows how to use WHERE= data set option in procedures 

proc print data=readin (where=(section='A'));
run;

In this case, you can also use WHERE statement....

proc print data=readin;
where section='A';
run;


8.01 - SAS : WHERE VS. IF STATEMENTS

WHERE condition wins against IF condition in the following cases :

1. The WHERE statement can be used in procedures to subset data while IF statement cannot be used in procedures.

2. WHERE can be used as a data set option while IF cannot be used as a data set option.

3. The WHERE statement is more efficient than IF statement. It tells SAS not to read all observations from the data set.

4. The WHERE statement can be used to search for all similar character values that sound alike while IF statement cannot be used.

IF condition wins against WHERE condition in the following cases :

1. When reading data using INPUT statement.

IF Statement

1. IF Statement can be used when specifying an INPUT statement.

2. When it is required to execute multiple conditional statements

Suppose, you have data for college students’ mathematics scores. You want to rate them on the basis of their scores.

Conditions :
1. If a score is less than 40, create a new variable named “Rating” and give “Poor” rating to these students.
2. If a score is greater than or equal to 40 but less than 75, give “Average” rating to these students.
3. If a score is greater than or equal to 75 but less than or equal to 100, give “Excellent” rating to these students.

This can be easily done using IF-THEN-ELSE IF statements. However, WHERE statement requires variables to exist in the data set.

3. When it is required to use newly created variables in data set.

IF statement can be applied on a newly created variable whereas WHERE statement cannot be applied on a newly created variable. In the below example, IF statement doesn't require variables to exist in the READIN data set while WHERE statement requires variable to exist in the data set.

4. When to Use _N_, FIRST., LAST. Variables

WHERE statement cannot be applied on automatic variables such as _N_, First., Last. Variables. While IF statement can be applied on automatic variables.

Difference : WHERE and IF when merging data sets
WHERE statement applies the subset condition before merging the data sets, Whereas, IF statement applies the subset condition after merging the data sets.

Create 2 Sample Datasets for Merging
data ex1;
input ID Score;
cards;
1 25
2 28
3 35
4 45
;
run;
data ex2;
input ID Score;
cards;
1 95
2 97
;
run;

Merge with WHERE Condition
data comb;
merge ex1 ex2;
by ID;
where score <= 30;
run;
It returns 2 observations. WHERE condition applied before merging. It applies separately on each of the 2 data sets before merging.

Merge with IF Condition
data comb;
merge ex1 ex2;
by ID;
if score <= 30;
run;
It returns 0 observation as IF condition applied after merging. Since there is no observation in which value of score is less than or equal to 30, it returns zero observation.

9.01 - PROC FREQ EXPLAINED WITH EXAMPLES

Create a sample data set

The program below creates a sample SAS dataset which would be used in further examples to explain PROC FREQ.
data example1;
input x y $ z;
cards;
6 A 60
6 A 70
2 A 100
2 B 10
3 B 67
2 C 81
3 C 63
5 C 55
;
run;

Example 1 : To check the distribution of a categorical variable (Character)

Suppose you want to see the frequency distribution of variable 'y'.

*Example - to check frequency distribution of variable*
proc freq data = example1;
tables y;
run;

The TABLES statements tells SAS to return n-way frequency and crosstabulation tables and computes the statistics for these tables.

It answers a question 'which category holds the maximum number of cases'. In this case, the category 'C' contains maximum number of values.

TIP:
Categorical variables are of two types - Nominal and Ordinal. A nominal variable is a categorical variable in which categories do not have any order. For example, gender, city etc. An ordinal categorical variable has categories that can be ordered in a meaningful way. For example, rank, status (high/medium/low) etc

Example 2 : To remove unwanted statistics in the table

Suppose you do not want cumulative frequency and cumulative percent to be displayed in the table. The option NOCUM tells SAS to not to return cumulative scores.

*Example - to check frequency distribution of variable y (not including commulative freq)*

proc freq data = example1;
tables y /nocum;
run;

 If you want only frequency, not percent distribution and cumulative statistics.

*Example - to check frequency distribution of variable y (not including commulative freq, no percent)*

proc freq data = example1;
tables y /nopercent nocum;
run;

Example 3 : Cross Tabulation ( 2*2 Table)
Suppose you want to see the distribution of variable 'y' by variable 'x'.

*Example - to check frequency distribution of variable y*x(cross tabulation)*

proc freq data = example1;
tables y * x;
run; 

Example 4 : Show Table in List Form

proc freq data = example1;
tables y * x / list;
run;

Example 5 : Hide Unwanted Statistics in Cross Tabulation
 
 *Example - to check frequency distribution of variable y*x(hiding unwanted stats)*

proc freq data = example1;
tables y * x / norow nocol nopercent;
run;
The NOROW option hides row percentage in cross tabulation. Similarly, NOCOL option suppresses column percentage.

Example 6 : Request Multiple Tables
Suppose you want to generate multiple crosstabs. To accomplish it, you can run the command below-

 *Example - to check frequency distribution of variable y*(X Z) (hiding unwanted stats)*

proc freq data = example1;
tables y * (x z) / norow nocol nopercent;
run;
The tables y*(x z) statement is equivalent to tables y*x y*z statement. In this case, it returns two tables - y by x and y by z.

Example 7 : Number of Distinct Values

The NLEVELS option is used to count number of unique values in a variable.

proc freq data = example1 nlevels;
tables y;
run;
In this case, it returns 3 for variable Y.

Example 8 : Use WEIGHT Statement

The WEIGHT statement is used when we already have the counts. It makes PROC FREQ use count data to produce frequency and crosstabulation tables.

Data example2;
input pre $ post $ count;
cards;
Yes Yes 30
Yes No 10
No Yes 40
No No 20
;
run;
proc freq data=example2;
tables pre*post;
weight count;run;

Example 9 : Store result in a SAS dataset

Suppose you wish to save the result in a SAS dataset instead of printing it in result window.

proc freq data = example1 noprint;
tables y *x / out = temp;
run;

The OUT option is used to store result in a data file. NOPRINT option prevents SAS to print it in results window.


Example 10 : Run Chi-Square Analysis

The CHISQ option provides chi-square tests of homogeneity or independence and measures of association between two categorical variables.  Also it helps to identify the statistically significant categorical variables that we should include in our predictive model. All the categorical variables with a chi-square value less than or equal to 0.05 are kept.

 *Example - to check frequency distribution of variable y*x with chi-square analysis

proc freq data = example1 noprint;
tables y * x/chisq;
output All out=temp_chi chisq;
run; 

Example 11 : Generate Bar Chart and Dot Plot

The bar chart can be generated with PROC FREQ. To produce a bar chart for variable 'y', the plots=freqplot (type=bar) option is added. By default, it shows frequency in graph. In order to show percent, you need to add scale=percent. The ODS graphics ON statement tells SAS to produce graphs. Later we turn it off.

 *Example - to Generate Bar Chart*

Ods graphics on;Proc freq data=example1 order=freq;
Tables y/ plots=freqplot (type=bar scale=percent);
Run;
Ods graphics off;

Similarly, we can produce dot plot by adding type=dot. See the implementation below-

 *Example - to Generate Dot Plot*

Ods graphics on;
Proc freq data=example1 order=freq;
Tables y/ plots=freqplot (type=dot);
Run;
Ods graphics off;


Example 12 : Include Missing Values in Calculation

By default, PROC FREQ does not consider missing values while calculating percent and cumulative percent. The number of missing values are shown separately (below the table). Refer the image below.

Proc freq data=sashelp.heart;
Tables deathcause;
Run; 

By adding MISSING option, it includes missing value as a separate category and all the respective statistics are generated based on it.

 *Example - to include missing values in proc freq*


Proc freq data=sashelp.heart;
Tables deathcause / missing;
Run;

Example 13 : Ordering / Sorting

In PROC FREQ, the categories of a character variable are ordered alphabetically by default. For numeric variables, the categories are ordered from smallest to largest value.

To sort categories on descending order by frequency (from largest to smallest count), add ORDER=FREQ option

 *Example - ordering/sorting in proc freq*

Proc freq data=sashelp.heart order = FREQ;
Tables deathcause / missing;
Run;

It is generally advisable to show distribution of a nominal variable after sorting categories by frequency. For ordinal variable, it should be shown based on level of categories.

To order categories based on a particular FORMAT, you can use order = FORMATTED option.

10.01 - SAS TIP : SPECIFY A LIST OF VARIABLES

Create a dataset with a list of variables
data dummy;
input q1 q3 q4 q2 q6$ bu$ q5;
cards;
1 2 3 5 sa an 3
2 4 3 6 sm sa 4
6 5 3 8 cb na 3
;
run;

How to specify a list of variables

A single dash (-) is used to specify consecutively numbered variables. For example : q1-q4;

A double dash (--) is used to specify variables based on the order of the variables as they appear in the file, regardless of the name of the variables.

Explanation - example variables are in series q1,q2,q6,q4,q5 so if we command to find out single dash ( q1-q5) hence the output will not include q6 but in case of double dash q6 will be included because it comes in order of variables regardless of the name of the variables.

data dummy1 (drop= q1--q5);
set dummy;
sum = sum(of q1-q4);
sum1 = sum(of q1--q4);
run;

n the above program, q1-q4 includes q1,q2,q3 and q4, whereas q1--q4 includes q1,q3 and q4 only as they appear the same way in file.

How to specify all NUMERIC variables

data dummy1 (drop= q1--q5);
set dummy;
sum = sum(of _numeric_);
run;

How to use double dash in array

The following program subtracts one from values in variables q1,q3 and q4.

data dummy1;
set dummy;
array vars q1--q4;
do over vars;
vars = vars - 1;
end;
run;

How to use numeric variables in array

The following program subtracts one from values in numeric variables.

data dummy1;
set dummy;
array vars _numeric_;
do over vars;
vars = vars - 1;
end;
run;

More Dash Symbol Usage

1. Print all NUMERIC variables from q1 through q6.
proc print;
var q1-numeric-q6;
run;

2.  Print all CHARACTER variables from q1 through q6.
proc print;
var q1-character-q6;
run;

3.  Print all CHARACTER variables.
proc print;
var _character_;
run;

11.01 - SAS : WILDCARD CHARACTER

Example 1 : Keep all the variables start with 'X'

DATA READIN;
INPUT ID X1 X_T $;
CARDS;
2 3 01
3 4 010
4 5 022
5 6 021
6 7 032
;
RUN;

DATA READIN2;
SET READIN (KEEP = X:);
RUN;

Example 2 : Subset data using wildcard character
DATA READIN2;
SET READIN;
IF X_T =: '01';
RUN;

In this case, the COLON (:) tells SAS to select all the cases starting with the character '01'.

Example 3 : Use of WildCard in IN Operator
DATA READIN2;
SET READIN;
IF X_T IN: ('01', '02');
RUN;


In this case, the COLON (:) tells SAS to select all the cases starting with the character '01' and '02'.

Example 4 : Use of WildCard in GT LT (> <) Operators
DATA READIN2;
SET READIN;
IF X_T >: '01';
RUN;


In this case, the COLON (:) tells SAS to select all the cases from character '01' up alphabetically.

Example 5 : WildCard in Function
data example3;
set temp2;
total =sum(of height:);
run;

Example 6 : WildCard in Array
proc sort data = sashelp.class out=class;
by name sex;
run;

proc transpose data = sashelp.class out=temp;
by name sex;
var height weight;
run;


proc transpose data = temp delimeter=_ out=temp2(drop=_name_);
by name;
var col1;
id _name_ sex;
run;

proc sql noprint;
select CATS('new_',name) into: newnames separated by " "
from dictionary.columns
where libname = "WORK" and memname = "TEMP2" and name like "Height_%";
quit;


data temp2;
set temp2;
array h(*) height:;
array newh(*) &newnames.;
do i = 1 to dim(h);
newh{i} = h{i}*2;
end;
drop i;
run;

12.01 - SAS : CHARACTER FUNCTIONS

1. COMPBL Function

It compresses multiple blanks to a single blank.

In the example below, the Name variable contains a record "Sandy   David". It has multiple spaces between the first and last name.

Create a dummy data

*example - COMPBL function to compress multiple blanks to a single blank*

Data char;
Input Name $ 1-50 ;
Cards;
Sandy    David
Annie Watson
Hello ladies and gentlemen
Hi, I am good
;
Run;

Use COMPBL Function

Data char1;
Set char;
char1 = compbl(Name);
run;

2. STRIP Function

It removes leading and trailing spaces.

*Example - STRIP function toremoves leading and trailing spaces*

Data char1;
Set char;
char1 = strip(Name);
run;


3. COMPRESS Function

SYNTAX 
COMPRESS(String, characters to be removed, Modifier)


Default - It removes leading, between and trailing spaces

*Example - STRIP function remmoves leading, between, trailing spaces*

Data char1;
Set char;
char1 = compress(Name);
run;


*Example - STRIP function to remove specific characters*
chart1 - compress all spaces & chart2 = removes those certain character mentioned ( example - compress(char1,',')

Data char1;
Set char;
char1 = compress(Name);
char2 = compress(char1,',');put string;
run;

In SAS 9.1.3, the additional parameter called MODIFIER was added to the function.

The following keywords can be used as modifiers-
a – Remove all upper and lower case characters from String.
ak - Keep only alphabets from String.
kd - Keeps only numeric values
d – Remove numerical values from String.
i – Remove specified characters both upper and lower case from String.
k – keeps the specified characters in the string instead of removing them.
l – Remove lowercase characters from String.
p – Remove Punctuation characters from String.


Example 1 : Keep only alphabets from alphanumeric values
data _null_;
x='ABCDEF-!1234';
string=compress(x,'','ak');put string=;
run;

4. LEFT Function

It moves leading blanks to the end of the value. The length of the string does not change.
Data char1;
Set char;
char1 = left(Name);
run;

5. TRIM Function

It removes trailing spaces.
Data char1;
Set char;
char1 = trim(Name);
run;

6. TRIM(LEFT(string))

It is equivalent to STRIP function. It first removes leading spaces and then trailing spaces.

7. CAT Function


It concatenates character strings. It is equivalent to || sign.

*Example - concatenate function - strings character*

data _null_;
a = 'abc';
b = 'xyz';
c= a || b;
d= cat(a,b);
put c= d =;
run;

Both c and d returns "abcxyz".

Concatenate String and Numeric Value

*Example - concatenate function - strings character*

data _null_;
x = "Temp";
y = 22;
z = x||y;
z1 = cats(x,y);
z2 = catx("",x,y);
put z = z1= z2 =;
run;
z = Temp  22 
z1=Temp22 
z2=Temp 22

Note -

The || keyword inserts multiple spaces when numeric and text values are concatenated.
CATS strips both leading and trailing blanks, and does not insert separators.
CATX strips both leading and trailing blanks, and inserts separators. The first argument to CATX specifies the separator.


8. SCAN Function

It extracts words within a value that is marked by delimiters.
SCAN( text, nth word, <delimiters>)
For example : 

We wish to extract first word in a sentence 'Hi, How are you doing?'. In this case, delimiter is a blank.
data _null_;
string='Hi, How are you doing?';
first_word=scan(string, 1, ' ' );
put first_word =;
run;

last_word returns 'doing?' since it is the last word in the above sentence.

Let's make it a little complicated.

Suppose, delimiter is a character instead of blank or special sign.
string='Hello SAS community people';
beginning= scan( string, 1, 'S' ); ** returns "Hello ";
middle = scan( string, 2, 'S' ); ** returns "A";
end= scan( string, 3, 'S' ); **returns " community people";
	
	
9. SUBSTR

It extracts strings based on character position and length. It is equivalent to MS Excel's MID Function.
= substr(old_var, starting_position, number of characters to keep);
Examples :
t="AFHood Analytics Group";
new_var=substr(t,8,9);
Result : Analytics

10. SUBSTR(Left of =) Function

It replaces a portion of string with new string
substr("old_variable",1,8) = new_data;
Result : New_dataable
	
11. LOWCASE, UPCASE and PROPCASE

LOWCASE converts the character string to lowercase.

UPCASE converts the character string to uppercase.

PROPCASE returns the word having uppercase in the first letter and lowercase in the rest of the letter (sentence format).

12. INDEX Function

It finds characters or words in a character variable

*Example - Index function to find the character or words in a character variable*

data _null_;
string='Hi,How are you doing?';
x = index(string, "How");
put x=;
run;
	
x returns 4 as "How" starts from 4th character.

To select all the records having 'ian' in their character.
if index(name,'ian') > 0;
To select all the records having first letter 'H'
if name =: 'H';
	
13. FIND Function

To locate a substring within a string

FIND (character-value, find-string <,'modifiers'> <,start>)

STRING1 = "Hello hello goodbye"

Examples :

1.  FIND(STRING1, "hello") returns 7

2.  FIND("abcxyzabc","abc",4) 7


14. TRANWRD Function

It replaces all occurrences of a word in a character string. It doesn't replace full phrase (entire value content).
TRANWRD (variable name, find what , replace with)

*Example - TRANWRD function to find and replace word/numbers in character*

Example :  name : Mrs. Joan Smith
name=tranwrd(name, "Mrs.", "Ms.");
Result : Ms. Joan Smith


15. TRANSLATE Function

It replaces specific characters in a character expression
TRANSLATE(source, replace with, find what)
Examples:

x = translate('XYZW','AB','VW');

Result :  "XYZB"

Difference between TRANWRD and TRANSLATE Functions

The TRANSLATE function converts every occurrence of a user-supplied character to another character. TRANSLATE can scan for more than one character in a single call. In doing this, however, TRANSLATE searches for every occurrence of any of the individual characters within a string. That is, if any letter (or character) in the target string is found in the source string, it is replaced with the corresponding letter (or character) in the replacement string. 
The TRANWRD function differs from TRANSLATE in that it scans for words (or patterns of characters) and replaces those words with a second word (or pattern of characters).

16. PRXMATCH

It can be used for the following cases :
When you want to identify if there is alphanumeric (has any letter from A to Z) in a variable.
If you need to search a character variable for multiple different substrings.
PRXMATCH (perl-regular-expression, source);
Perl Regular Expression
^ - start with 
$ - end with 
\D - any non digits 
\d - digits 
? - may or may not have? 
| - or 
* - repeating 
( i:) - turns ON the case insensitive search
(-i:) - turn OFF the case insensitive search

1. Check alphanumeric value

DATA test;
INPUT string $ 1-8;
prxmatch=prxmatch("/[a-zA-Z]/",string);
CARDS;
ACBED
11
12
zx
11 2c
abc123
;
run; 

Note : prxmatch("/[a-zA-Z]/",string) checks first character.


2. Replace multiple words with a new word
if prxmatch('/Luthir|Luthr|Luther/',name) then name='Luthra' ;

17. INPUT and PUT Function

INPUT Function is used to convert character variable to numeric.

*Example - Input function to convert character variable to numberic, x = '12345' (string) which is converted into no( under new_x)*
	
new_num=input(character-variable, 4.);
Example - 
data temp;
x = '12345';
new_x = input(x,5.);
run;
In the above example, the variable x is a character variable as it is defined in quotes '12345'. The newly created variable new_x is in numeric format.

PUT Function is used to convert numeric variable to character.

*Example - Put function to convert numberic character  to  variable, x = 12345 (numberic) which is converted into string ( under new_x)*
	
new_char=put(numeric,4.0);
data temp;
x = 12345;
new_x = put(x,5.);
run;
In this example, the variable x is originally in numeric format and later converted to character in the new variable new_x.

*Example - To find length of the string*

18. LENGTH
It return length of a string.

*Example - To find length of the string*

data _null_;
x='ABCDEF-!1.234';
n= length(x);
put n=;
run;
It returns 13.

If you need to calculate the number of digits in a numeric variable -

First, we need to convert our numeric variable to character to count the number of digits as LENGTH function works only for character variable.

*Example - To find length of the numeric value first convert the numeric value into string  using PUT function and then find the length*

data _null_;
x = 12345;
cnt = length(strip(put(x,12.)));
put cnt=;
run;
In the above nested function, we first converted the variable x to character and then remove spaces by using STRIP function and then count number of digits by using LENGTH() function.

Another Method -
data _null_;
x = 12345;
cnt = int(log10(x)) + 1;
put cnt=;
run;
We can also use LOG10 function to solve it. LOG10 has a property which says :
Number of Digits = Integer value of [LOG10(x)] + 1. For example, LOG10(100) = 2 so Number of digits in 100 = 2 +1. See LOG10(1100) = 3.04 => INT(3.04) = 3 => 3+1 = Number of digits in 1100.


19. IF THEN

It replaces entire phrase.

20. COUNT Function


It counts the number of times that a specified substring appears within a character string.

*Example - To count the number of times a specified substring appears within a character string.*
		
data _null_;
name = "DeepAnshu Bhalla";
x = count(name,"a");
x1 = count(name,"a","i");
put x= x1=;
run;
Result :  x=2 as there are 2 lower case 'a's in the variable name. x1=3 as there are 3 'a's in the variable name (The 'i' modifier ignores case sensitivity)

21. COUNTW Function

	
It counts the number of words in a character string.

*Example - It counts the number of words in a character string.*
data readin;
input name$15.;
cards;
Trait Jhonson
3+3=6
;
run;

data out;
set readin;
x = countw(name);
x1 = countw(name,' ');
proc print;
run;

Output : COUNTW Function
 If you don't specify delimiter in the second parameter of COUNTW function, it would automatically special characters as a delimiter.


13.01 - SAS DATE FORMATS AND INFORMATS

Informats is used to tell SAS how to read a variable whereas Formats is used to tell SAS how to display or write values of a variable.

Informats is basically used when you read or import data from either an external file (Text/Excel/CSV) or read in sample data which was created using CARDS/DATALINES statement. It is also used when you create a new variable in a dataset.

Formats can be used in both Data Steps and PROC Steps whereas Informat can be used only in Data Steps. Let's understand by examples -

Example 1 - Read Dates in SAS

In the program below, we have used INFORMATS ddmmyy8. and ddymmyy10. to read dates in SAS. It creates a dataset called sampledata which is stored in WORK library.

DATA sampledata;
     INPUT @6 date1 ddmmyy8. @15 date2 ddmmyy10.;
    CARDS;
     30-12-16 30-12-2016
  ;
RUN;

The INFORMATS ddmmyy8. is used to read 30-12-16 date and ddmmyy10. to read 30-12-2016 date. 
In this case, 8 and 10 refers to width of the date.


It returns 20818 as it is in SAS date value form. It is not meaningful if you look at the value. You cannot tell which date it is. To display in real date form, use FORMAT statement.
	
*Example - conversion of informat variables into format*

DATA sampledata;
INPUT @6 date1 ddmmyy8. @15 date2 ddmmyy10.;
FORMAT date1 ddmmyy8. date2 ddmmyy10.;
cards;
30-12-16 30-12-2016
;
RUN;
	
How to read DD-MMM-YY format

You can use date11. format for both DD-MMM-YY and DD-MMM-YYYY format.

DATA temp;
INPUT @6 dt date11.;
FORMAT dt date11.;
CARDS;
10-oct-14
;
PROC PRINT NOOBS;
RUN;

	
Example 2 - Display Today's Date

The today() function can be used to generate current date.

*Example - to find today's date*

data _null_;
dt=today();
format dt yymmdd10.;
put dt ;
run;

Result : It returns 2016-12-30 as 30DEC2016 is the today's date. It's in YYYY-MM-DD format because we've used yymmdd10. format. The 10 refers to the width of the date as 2016-12-30 contains 10 elements. The PUT statement is used to show value in log window.

To display date in WORD format
1. Short Word Date Format

The format date9. returns 30DEC2016.
format dt date9.;

2. Complete Word Date Format

The format WORDDATE. returns DECEMBER 30, 2016. No need to specify width in this format. It automatically adjusts the width depending on the month.

*Example - to format  word date returns date format( full name)  without including days*

format dt WORDDATE.;

3. Including WEEK

The format WEEKDATE. gives Friday, December 30, 2016

*Example - to format  word date returns date, days format( full name) *
	
format dt WEEKDATE.;	
	
Display DAY / MONTH / YEAR

In this section, we will see how we can write only day, month, year and weekday.
data _null_;
dt=today();
put "Day :"  dt  DAY.;
put "Month :" dt MONTH.;
put "YEAR:" dt YEAR.;
put "WEEKDAY:" dt DOWNAME.;
run;

We can also use FORMAT in the PUT statement without specifying FORMAT statement explicitly. The DAY. format returned 30, MONTH. format returned 12 and YEAR. format returned 2016. In addition, we have used DOWNAME. format to extract weekday (Friday).	
	
	
Other Popular Formats

Some of the commonly used date formats are listed below -
Formats	Result
DDMMYYP10.	30.12.2016
DDMMYYS10.	30/12/2016
MMDDYYP10.	12.30.2016
MMDDYYS10.	12/30/2016
WORDDATX19.	30 DECEMBER 2016
	
14.01 - SAS : INTCK FUNCTION WITH EXAMPLES

The syntax of INTCK is defined below -

INTCK(date-or-time-interval, start-date-or-time, end-date-or-time, [method])
1. date-or-time-interval : Date or time period needs to be defined in the first parameter. For eg. MONTH, YEAR, QTR, WEEK, HOUR, MINUTE etc. Specify period in single quotes

2. start-date-or-time : Starting date or time to calculate the number of periods.

3. end-date-or-time : End date or time to calculate the number of periods.

4. method : Optional Parameter. Method to calculate the difference. Methods are 'CONTINUOUS' or 'DISCRETE'. By default, it is DISCRETE.
	
The 'YEAR' keyword tells SAS to calculate the number of intervals between dates in terms of year. Since 01JAN2015 is a starting date, it is specified in the INTCK function before 01JAN2017. The FORMAT statement is used to display datevalues in date format when we print our results.	
	
Other alias of year - 'YEARS' and 'YR'-
no_of_years  = intck ('YEARS', date1, date2)
no_of_years  = intck ('YR', date1, date2)	
	
SAS INTCK Examples

Like calculation of years, we can use other intervals such as semiyear, quarter, month, week, day. The examples of these intervals are displayed below -
data temp;
date1 = '01JAN2015'd;
date2 = '01JAN2017'd;
no_of_years  = intck ('YEAR', date1, date2);
no_of_semiyears  = intck ('SEMIYEAR', date1, date2);
no_of_quarters  = intck ('QUARTER', date1, date2);
no_of_months  = intck ('MONTH', date1, date2);
no_of_weeks  = intck ('WEEK', date1, date2);
no_of_days  = intck ('DAY', date1, date2);
format date1 date2 date9.;
proc print data = temp noobs;
run;
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	


