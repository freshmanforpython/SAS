1. Data is case sensitivity. Variables and functions are case insensitivity.
2. var: using in **proc means**. For different columns;
   tables: using in **proc freq**. For different values in a column;
   keep: keeping columns in a table to show.

3. Title: Remember to clear title by **"Title; Ods proctitle;"** in the end.
```
Which statement is false concerning the FREQ procedure?
 a.  The NOPROCTITLE option can be placed in the PROC FREQ statement to remove the procedure title The FREQ Procedure.
 b.  The ORDER=FREQ option can be placed in the PROC FREQ statement to display the column values in descending frequency count order.
 c.  The PLOTS= option can be placed in the TABLES statement after the forward slash to create bar charts based on counts or percentages.
 d.  The OUT= option can be placed in the TABLES statement after the forward slash to create a table containing counts and percentages.

Your answer: c
Correct answer: a

The NOPROCTITLE option goes in a global ODS statement to remove the procedure title.
```
4. Lable: **proc print data = xxx lable**.
```
Which statement is true based on the given program?
data baseball2;
    set sashelp.baseball;
    BatAvg=CrHits/CrAtBat;
    label BatAvg="Batting Average";
run;

proc print data=baseball2;
    var Name Team BatAvg;
run;

proc means data=baseball2;
    var BatAvg;
    class Team;
run;

 a.  The column BatAvg will have a permanent label in the sashelp.baseball data set.
 b.  The label for BatAvg will appear in the PROC PRINT report.
 c.  The label for BatAvg will appear in the PROC MEANS report.
 d.  The label for BatAvg will appear in both reports.

Your answer: d
Correct answer: c

The label will appear in the PROC MEANS report. The label will not appear in the PROC PRINT report because the LABEL option is missing in the PROC PRINT statement. The output table work.baseball2 (not the input table sashelp.baseball) contains a permanent label for BatAvg.

```

5. where: determined when the DATA step is compiled (SET or MERGE)
   IF: evaluated at run time; can run new variables that are defined within the step;
   
6. Assume that Sasuser.One does not exist and that the following SAS program is submitted at the beginning of a new SAS session:

data sasuser.one;
   x=1;
   y=27;
   output one;
run; 
Select one:

A.
The data set Sasuser.One is created with 2 variables and 3 observations

B.
The data set Sasuser.One is created with 2 variables and 0 observations

C.
The DATA step does not execute

D.
The data set Sasuser.One is created with 2 variables and 1 observation

```The OUTPUT statement is told to use Work.One, but it is not a data set that is specified on the DATA statement. This generates a syntax error and stops the execution of the DATA step. At compile time, a data set Sasuser.One with 2 variables and 0 observations would be created, but only if it did not already exist. A pre-existing Sasuser.One would not be affected by this DATA step.

The correct answer is: The data set Sasuser.One is created with 2 variables and 0 observations
```

7. The LENGTH statement only gives the variable Name a predefined maximum length.
The variable Name in the data set Employee has a $CHAR10. format. The variable Name in the data set Sales has a $CHAR15. format. 

The following SAS program is submitted:

data both;
   length name $ 20;
   merge sales employee;
   by id; 
run;
What is the format for the variable Name in the data set Both?
 
Select one:

A.
$20


B.
$CHAR10

**C.
$CHAR15**


D.
$CHAR20
The first attribute seen for a variable is the one used in the current data step. Given that the Work.Sales data set is positioned first on the MERGE statement, the variable Name would have a format of $CHAR15. in the new data set Work.Both. 
 
8. DO loop is increased at the bottom of the loop and evaluated at the top.
