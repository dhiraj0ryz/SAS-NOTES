# SAS TUTORIAL FOR BEGINNERS TO ADVANCED - PRACTICAL GUIDE 

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













































