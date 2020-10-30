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
