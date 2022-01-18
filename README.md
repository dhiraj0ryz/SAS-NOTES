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


























