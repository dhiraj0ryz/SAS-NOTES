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

'''data temp;
input name $ ID;
cards;
Sam 12
Sandy 13
Reno 11
Farhan 10
;
proc print;
run;'''



*IMPORTING DATA INTO SAS*
I. Entering Data Directly in SAS Program
The keywords are as follows:
1. DATA -  The DATA step always begins with a DATA statement. The purpose of the DATA statement is to tell SAS that you are creating a new data set i.e. outdata.
2. INPUT -  To define the variables used in data set.
3. Dollar sign ($) - To identify variable as character.
4. DATALINES - To indicate that lines following DATALINES statement a real data.(We can use Cards instead of Datalines)
5. PROC PRINT - To print out the contents of data set in output window.
6. RUN - The DATA step ends with a RUN statement.
Reading Delimited Data
- The default delimiter is blank. If you have a data file with other delimiters such as comma or tab you need to define the delimiter before defining the variables using INFILE and DLM = options.
- For tab delimiter, the syntax would be infile 'file-description' dlm='09'x
- For colon delimiter, the syntax would be infile 'file-description' dlm=':'

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


