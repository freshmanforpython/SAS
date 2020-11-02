1. sas分为data步和proc步；
2. data步

**data** table1(**drop=var3:**) table2 /debug; #数据集名称必须以字母开头，最长不超过8个字符

  **set** table(**keep=**);
  
  **keep** var1 var2;
  
  length v1 $10 v2 $15; #LENGTH statement only gives the variables a predefined maximum length.
  
  a1=**input**(substr(a, 4),7.3); #from char to numeric
  
  **if** then output table1 do;
  
  v1=strip(substr(v1, 1, find(v1,'abcd')-1));
  
  **else if** then output table2;
  
  v3=**catx**(' ',v1,v2);
  
  if v1 **=:** 'abcd' then delete; /* =: starts with */
  
  **where**  ;
  
  run;
  
  
  data table1;
  
  infile card dsd; # delimiter sensitive data; missover:从下一个数据行中读入数据，未赋值的变量就是缺失值；dlm=：delimiter
    
  input v1 v2 v3;
  
  input; # skip the row
    
  datalines;
    
  a
    
  b
    
  c
  ;
  run;
  
  
  data count;
    
  set table;
    
  **by** origin;
    
  if first.origin then count=0;
    
  count+1;
    
  if last.origin;
    
  run;
  
  data new-data-set;
 
set old-data-set;

file ‘file-path’;

put variable-list; /* similar as input statement */

run;

output both a SAS data file ‘new-data-set’ and a raw data file ‘file-path’.

  
3. PROC步

1) PROC statements

**proc transpose** <data=input-data-set>  <NAME=name> <OUT=output-data-set> <PREFIX=prefix>;

 BY <DESCENDING> variable-1 <...<DESCENDING> variable-n> <NOTSORTED>;  #使输入数据集分组转置，分组变量被包括在输出数据集中。 
 
COPY  variable(s); 

 ID variable; #转置后变量名
 
 IDLABEL variable; #转置后变量标签
 
VAR variable(s); #被转置的变量

 run;
 
 **proc import** datafile = 'file_path' out=data_set;
 
 DBMS= identifier # xls, xlsx, excel; csv, tab(.txt), dlm
 
 replace;
 
 sheet='sheet name';
 
 range='sheet name$UL:LR';
 
 getnames=no; *not take variables name from the first row
 
 guessingrows=n;
 
 mixed=yes;
 <br/>
 **proc contents** data=dataset;

 run;
 
 <br/>
 **proc means** data=dataset statistic_keywords options;
 * statistic_keywords include: max, mean, min, mode, sum, sumwgt, n, nmiss, median, range, stddev, stderr, var etc.;
 
 * If you do not specify any summary statistics, SAS will print the number of n, the mean, stddev, mim, max for each variable. 
 
 * options include: missing, maxdec, noprint, alpha=n;

 var v1;
 
 by v2;
 
 class v3;
 
 title 'text';
 
 output out='filename';
 
 tun;
 
 <br/>
 **proc freq** data=dataset;
 
 table v1/options;
 
 table v1*v2/options;
 
 table v1*v2*v3/options;
 
 table v1*(v2 v3)/options; * two two-way tables 
 
 run;
 
 * options1 include: missing missprint ncum nopercent noprint;
 
 * options2 include: options1, plus crosslist (display crosstabulation in list format with totals), list (display crosstabulation in list format without totals), nocol (suppress column percentages in crosstabulation), norow (suppress row percentages in crosstabulation);
 
 <br/>
 **proc print** data=dataset noobs lable;
 
 label v1='s1' v2='s2';
 
 where ;
 
 by v1;
 
 id variable_list;
 
 sum variable_list;
 
 var variable_list;
 
 format v1 v2 dollar8.2 v3 mmddyy8.;
 
 title 't1';
 
 title2 't2';
 
 title3 't3';
 
 footnote 'f1';
 
 footnote2 'f2';
 
 footnote3 'f3';
 
 run;
 
 <br/>
 
 **proc report** data=dataset;
 
 <br/>
 
 **proc format**;
 
 value format_name 1-50='fail';
 
 run;
 
 'A' = 'Asia'
 
1, 3, 5, 7, 9 = 'Odd'

500000 - HIGH = 'Not Affordable'

13 -< 20 = 'Teenager'

0 <- HIGH = 'Positive Non Zero'

OTHER = 'Bad Data’
<br/>


4. others

1) placing before variables:

/ move the pointer to the next line

#5 move the pointer to line 5

@5 move the pointer to column 3

@'string' move the pointer after 'string'

2) placing after variables:

v1:$20 stops reading v1 when it encounters a space or the end of data line.

v1 & $20 stops reading when encounters two or more spaces in a row.

@@ prevents SAS from automatically going to a new line of raw data for next observation

@ holds the line of data until it reaches either the end of DATA step or INPUT statement that does not end with @.


3) functions

 **label** v1='string1' v2='string2'
 
 lable v1='' # clear the label
 
 merge table1 (in=a1 rename=(v1=v2))
        table2 (in=a2);
        
 by commonv;
      
 **keep** v1 v2;
 
 **drop** v1 v2;
 
 data table1 (keep=v1 v2);
 
 set table2 (drop=v1 v2);
 
 <br/>
 
