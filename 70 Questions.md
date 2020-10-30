4. 
[Characters That Cause Misinterpretation When Following a Character Constant](https://support.sas.com/documentation/cdl/en/lrcon/62955/HTML/default/viewer.htm#a000780334.htm#a002154623)

5. Which statement specifies that records 1 through 10 are to be read from the raw data file customer.txt?

A. infile ‘customer.txt’ 1-10;
B. input ‘customer.txt’ stop@10;
**C. infile ‘customer.txt’ obs=10;**
D. input ‘customer.txt’ stop=10;

```
data d;
infile datalines firstobs = 2 obs = 5;
input x;
input y;
datalines;
1
2
3
4
5
6
7
8
9
10
;
run;
两行record组成一个observation。生成的data set应为：

Obs	x	y
1	2	3
2	4	5
最后，INPUT statement中不存在STOP这个argument。
```

6. After a SAS program is submitted, the following is written to the SAS log:
101 data WORK.JANUARY;
102 set WORK.ALLYEAR(keep=product month num_Sold Cost);
103 if Month=’Jan’ then output WORK.JANUARY;
104 Sales=Cost * Num_Sold;
105 keep=Product Sales;
-----
22
ERROR 22-322: Syntax error, expecting one of the following: !,!!, &, *, **, +, -, , <=, <>, =, >, >=, AND, EQ, GE, GT, IN, LE, LT, MAX, MIN, NE, NG, NL,NOTIN, OR, ^=, |, ||, ~=.
106 run;

What changes should be made to the KEEP statement to correct the errors in the LOG?
A. keep=(Product Sales);
B. keep Product, Sales;
C. keep=Product, Sales;
**D. keep Product Sales;**

7. Which of the following choices is an unacceptable ODS destination for producing output that can be viewed in Microsoft Excel?

A. MSOFFICE2K
B. EXCELXP
C. CSVALL
**D. WINXP**

```注解：MSOFFICE2K用于生成XLS文件，EXCELXP生成XML文件，CSVALL生成CSV文件，以上三种都可以用Excel打开。最后，不存在WINXP这种ODS destination。```

8. The SAS data set named WORK.SALARY contains 10 observations for each department,and is currently ordered by Department. The following SAS program is submitted:

data WORK.TOTAL;
set WORK.SALARY(keep=Department MonthlyWageRate);
by Department;
if First.Department=1 then Payroll=0;
Payroll+(MonthlyWageRate*12);
if Last.Department=1;
run;

Which statement is true?
A. The by statement in the DATA step causes a syntax error.
B. The statement Payroll+(MonthlyWageRate*12); in the data step causes a syntax error.
**C. The values of the variable Payroll represent the monthly total for each department in the WORK.SALARY data set.**
D. The values of the variable Payroll represent a monthly total for all values of WAGERATE in the WORK.SALARY data set.

9. The following SAS program is submitted:

data WORK.RETAIL;
Cost=’20.000′;
Discount=.10*Cost;
run;

What is the result?

A. The value of the variable Discount in the output data set is 2000.No messages are written to the SAS log.
B. The value of the variable Discount in the output data set is 2000.A note that conversion has taken place is written to the SAS log.
**C. The value of the variable Discount in the output data set is missing.A note in the SAS log refers to invalid numeric data.**
D. The variable Discount in the output data set is set to zero.No messages are written to the SAS log.
```sas会尽力把变量转化为数值型变量以便进行数值运算，但是由于有$ notation，无法转化为数值，故无法运算```

10. Given the existing SAS program:

proc format;
value agegrp
low-12 =’Pre-Teen’
13-high = ‘Teen’;
run;

proc means data=SASHELP.CLASS;
var Height;
class Sex Age;
format Age agegrp.;
run;

Which statement in the proc means step needs to be modified or added to generate the following results:

Analysis Variable : Height
Sex	Age	N Obs	Minimum	Maximum	Mean
F	Pre-Teen	3	51.3	59.8	55.8
 	Teen	6	56.5	66.5	63.0
M	Pre-Teen	4	57.3	64.8	59.7
 	Teen	6	62.5	72.0	66.8
A. var Height / nobs min max mean maxdec=1;
B. proc means data=SASHELP.CLASS maxdec=1 ;
**C. proc means data=SASHELP.CLASS min max mean maxdec=1;**
D. output nobs min max mean maxdec=1;
```
PROC MEANS默认会输出非missing观测值个数、均值、标准差、最小值和最大值。
题目只需要输出最小值（MIN）、最大值（MAX）和均值（MEAN），并显示小数点后一位（MAXDEC）。
其中N Obs是观测值个数（包括missing和非missing），要去掉的话使用NONOBS，即proc means data = XXXX nonobs。
```

11. The following SAS program is submitted:

data WORK.TEST;
set WORK.MEASLES(keep=Janpt Febpt Marpt);
array Diff{3} Difcount1-Difcount3;
array Patients{3} Janpt Febpt Marpt;
run;

What new variables are created?
**A. Difcount1, Difcount2 and Difcount3**
B. Diff1, Diff2 and Diff3
C. Janpt, Febpt, and Marpt
D. Patients1, Patients2 and Patients3
```ARRAY statement用于定义Array内的元素。题目中，Janpt, Febpt和Marpt是来自于Measles data set的旧变量，仅有Difcount1, Difcount2和Difcount3是新建立的变量。```

14. Which of the following programs correctly invokes the DATA Step Debugger:

A.
data WORK.TEST debug;
set WORK.PILOTS;
State=scan(cityState,2,’ ‘);
if State=’NE’ then description=’Central’;
run;

B.
data WORK.TEST debugger;
set WORK.PILOTS;
State=scan(cityState,2,’ ‘);
if State=’NE’ then description=’Central’;
run;

**C.
data WORK.TEST / debug;
set WORK.PILOTS;
State=scan(cityState,2,’ ‘);
if State=’NE’ then description=’Central’;
run;**

D.
data WORK.TEST / debugger;
set WORK.PILOTS;
State=scan(cityState,2,’ ‘);
if State=’NE’ then description=’Central’;
run;

15. Which statement is true concerning the SAS automatic variable _ERROR_?

A. It cannot be used in an if/then condition.
B. It cannot be used in an assignment statement.
C. It can be put into a keep statement or keep= option.
D. It is automatically dropped.
```
_ERROR_是DATA step中SAS生成的Automatic Variable，当程序运行正常时_ERROR_的值为0，出错时为1。_ERROR_仅在DATA step的执行过程中存在，
在执行完一次DATA step输出数据时，SAS自动丢弃该变量，即输出的data set中不会出现_ERROR_这一变量。在DATA step的执行过程中，_ERROR_可以当作IF/THEN的条件，
可以将其值赋给其它变量输出到data set中，但KEEP无法作用于_ERROR_。
```


[understanding PDV and Data Step](https://www.sas.com/content/dam/SAS/en_ca/User%20Group%20Presentations/TASS/Mehatab-DataStepPDV.pdf)

16. The following SAS program is submitted:

data WORK.DATE_INFO;
X=’04jul2005’d;
DayOfMonth=day(x);
MonthOfYear=month(x);
Year=year(x);
run;

What types of variables are DayOfMonth, MonthOfYear, and Year?

A. DayOfMonth, Year, and MonthOfYear are character.
**B. DayOfMonth, Year, and MonthOfYear are numeric.**
C. DayOfMonth and Year are numeric. MonthOfYear is character.
D. DayOfMonth, Year, and MonthOfYear are date values.
```
d的作用是将“数字day + 英文month前三个字母 + 数字year”格式的日期，转化成SAS日期，即以1960年1月1日为0，2005年7月4日则为16621。
DAY, MONTH, YEAR这三个function则是分别返回一个SAS格式日期的日，月，年，并且返回的值均为数值型。
```

17. Given the following data step:

data WORK.GEO;
infile datalines;
input City $20.;
if City=’Tulsa’ then
State=’OK’;
Region=’Central’;
if City=’Los Angeles’ then
State=’CA’;
Region=’Western’;
datalines;
Tulsa
Los Angeles
Bangor
;
run;

After data step execution, what will data set WORK.GEO contain?

**A.

Obs	City	State	Region
1	Tulsa	OK	Western
2	Los Angeles	CA	Western
3	Bangor		Western**
B.

Obs	City	State	Region
1	Tulsa	OK	Western
2	Los Angeles	CA	Western
3	Bangor		
C.

Obs	City	State	Region
1	Tulsa	OK	Central
2	Los Angeles	CA	Western
3	Bangor		Western
D.

Obs	City	State	Region
1	Tulsa	OK	Central
2	Los Angeles	CA	Western
3	Bangor	

```
if/then只能有一个then， 如果需要多语句，则用 if/then/do/end。
if City=’Tulsa’ then do;
State=’OK’;
Region=’Central’;
end;
故此题中region不受then影响，而是赋值两次。
```

18. Which statement describes a characteristic of the SAS automatic variable _ERROR_?

A. The _ERROR_ variable maintains a count of the number of data errors in a DATA step.
B. The _ERROR_ variable is added to the program data vector and becomes part of the data set being created.
**C. The _ERROR_ variable can be used in expressions in the DATA step.**
D. The _ERROR_ variable contains the number of the observation that caused the data error.

19. The SAS data set WORK.ONE contains a numeric variable named Num and a character variable named Char:

Num	Char
1	23
2	23
1	77
The following SAS program is submitted:

proc print data=WORK.ONE;
where Num=’1′;
run;

What is output?

A.

Obs	Num	Char
1	1	23
B.

Obs	Num	Char
1	1	23
3	1	77
C.

Obs	Num	Char
1	1	23
2	2	23
3	1	77
**D. No output is generated.**
```where 无法自动转换字符型为数值型，Log中会显示”ERROR: WHERE clause operator requires compatible variables.”```
[Auto Character-to-numeric Conversion](https://v8doc.sas.com/sashtml/lrcon/z0780416.htm)

20. The data set WORK.REALESTATE has the variable LocalFee with a format of 9. and a variable CountryFee with a format of 7.;

The following SAS program is submitted:

data WORK.FEE_STRUCTURE;
format LocalFee CountryFee percent7.2;
set WORK.REALESTAT;
LocalFee=LocalFee/100;
CountryFee=CountryFee/100;
run;

What are the formats of the variables LOCALFEE and COUNTRYFEE in the output dataset?
A. LocalFee has format of 9. and CountryFee has a format of 7.
B. LocalFee has format of 9. and CountryFee has a format of percent7.2
**C. Both LocalFee and CountryFee have a format of percent7.2**
D. The data step fails execution; there is no format for LocalFee.
```FORMAT statement可以一次改变多个变量的format```
21. Given the SAS data set WORK.PRODUCTS:

ProdId	Price	ProductType	Sales	Returns
K12S	95.50	OUTDOOR	15	2
B132S	2.99	CLOTHING	300	10
R18KY2	51.99	EQUIPMENT	25	5
3KL8BY	6.39	OUTDOOR	125	15
DY65DW	5.60	OUTDOOR	45	5
DGTY23	34.55	EQUIPMENT	67	2
The following SAS program is submitted:

data WORK.OUTDOOR WORK.CLOTH WORK.EQUIP;
set WORK.PRODUCTS;
if Sales GT 30;
if ProductType EQ ‘OUTDOOR’ then output WORK.OUTDOOR;
else if ProductType EQ ‘CLOTHING’ then output WORK.CLOTH;
else if ProductType EQ ‘EQUIPMENT’ then output WORK.EQUIP;
run;

How many observations does the WORK.OUTDOOR data set contain?
A. 1
**B. 2**
C. 3
D. 6
```set流程是，读入一条语句后就执行if，if为真才执行后面语句。```

22. Which step displays a listing of all the data sets in the WORK library?
A. proc contents lib=WORK run;
B. proc contents lib=WORK.all;run;
C. proc contents data=WORK._all_; run;
D. proc contents data=WORK _ALL_; run;

```在PROC CONTENTS statement中，libref._ALL_用于显示libref这一SAS library下所有data set的信息。D缺了个“.”，如果libref是work的话，可以省略work，即data = _all_```

23. Which is a valid LIBNAME statement?
A. libname “_SAS_data_library_location_”;
B. sasdata libname “_SAS_data_library_location_”;
**C. libname sasdata “_SAS_data_library_location_”;**
D. libname sasdata sas “_SAS_data_library_location_”;
```正确格式为：LIBNAME  libref  ‘文件路径’。```

24. Given the following raw data records:

----|----10---|----20
Susan*12/29/1970*10
Michael**6

The following output is desired:

Obs	employee	bdate	years
1	Susan	4015	10
2	Michael	.	6
Which SAS program correctly reads in the raw data?
A.
data employees;
infile ‘file specification’ dlm=’*’;
input employee $ bdate : mmddyy10. years;
run;

B.
data employees;
infile ‘file specification’ dsd=’*’;
input employee $ bdate mmddyy10. years;
run;

C.
data employees;
infile ‘file specification’ dlm dsd;
input employee $ bdate mmddyy10. years;
run;

***D.
data employees;
infile ‘file specification’ dlm=’*’ dsd;
input employee $ bdate : mmddyy10. years;
run;***
``` dsd: dlm: same as base (2) ```
```$指明其前面的那个变量是字符型的```

25. Given the following code:

proc print data=SASHELP.CLASS(firstobs=5 obs=15);
where Sex=’M’;
run;

How many observations will be displayed?

A. 11
B. 15
C. 10 or fewer
**D. 11 or fewer**
``` same as base (5)```

26. Which step sorts the observations of a permanent SAS data set by two variables and stores the sorted observations in a temporary SAS data set?

A.
proc sort out=EMPLOYEES data=EMPSORT;
by Lname and Fname;
run;

**B.
proc sort data=SASUSER.EMPLOYEES out=EMPSORT;
by Lname Fname;
run;**

C.
proc sort out=SASUSER.EMPLOYEES data=WORK.EMPSORT;
by Lname Fname;
run;

D.
proc sort data=SASUSER.EMPLOYEES out=SASUSER.EMPSORT;
by Lname and Fname;
run;
```
DATA指定需要被排序的data set，OUT指定存放排序后数据的data set，
1. 如果省略OUT，SAS则会用排序后的数据替换原始数据。
2. BY statement后直接列出需要排序的变量名，并以空格隔开。
3. WORK library中的dataset都为临时data set，即关闭SAS后这些数据都将被移除，以WORK.dataset表示，其中WORK可以省略，例如：WORK.EMPSORT或EMPSORT。其他library中的都为永久data set，以libref.dataset表示，例如：SASUSER.EMPLOY
```

27. Given the SAS data set WORK.TEMPS:

Day	Month	Temp
1	May	75
15	May	70
15	June	80
3	June	76
2	July	85
14	July	89
The following program is submitted:

proc sort data=WORK.TEMPS;
by descending Month Day;
run;

proc print data=WORK.TEMPS;
run;

Which output is correct?

A.

Obs	Day	Month	Temp
1	2	July	85
2	14	July	89
3	3	June	76
4	15	June	80
5	1	May	75
6	15	May	70
B.

Obs	Day	Month	Temp
1	1	May	75
2	2	July	85
3	3	June	76
4	14	July	89
5	15	May	70
6	15	June	80
**C.

Obs	Day	Month	Temp
1	1	May	75
2	15	May	70
3	3	June	76
4	15	June	80
5	2	July	85
6	14	July	89**
D.

Obs	Day	Month	Temp
1	15	May	70
2	1	May	75
3	15	June	80
4	3	June	76
5	14	July	89
6	2	July	85
```
1. temporary table在程序完全结束后消失。
2. DESCENDING只作用于紧跟着它的那一个变量。
3. SAS并不知道May是5月，June是6月，SAS只知道May的第一个字母是M，而June的第一个字母是J。
4. 字符型变量的排序在采用不同编码表的操作系统中略有不同。

采用ASCII编码的系统，例如Windows，Linux和MAC OS中，各字符从小到大的排列顺序为：
空格 ! ” # $ % & ‘ ( ) * + , – . /0 1 2 3 4 5 6 7 8 9 : ; < = > ? @
A B C D E F G H I J K L M N O P Q R S T U V W X Y Z[ ] ˆ_
a b c d e f g h i j k l m n o p q r s t u v w x y z { } ~

采用EBCDIC编码的系统，例如z/OS，各字符从小到大的排列顺序为：
空格 . < ( + | & ! $ * ) ; ¬ – / , % _ > ?: # @ ‘ = “
a b c d e f g h i j k l m n o p q r ~ s t u v w x y z
{ A B C D E F G H I } J K L M N O P Q R S T U V W X Y Z
0 1 2 3 4 5 6 7 8 9
```

28. Given the SAS data set WORK.P2000:

Location	Pop2000
Alaska	626931
Delaware	783595
Vermont	608826
Wyoming	493782
and the SAS data set WORK.P2008:

State	Pop2008
Alaska	686293
Delaware	873092
Wyoming	532668
The following output is desired:

Obs	State	Pop2000	Pop2008	Difference
1	Alaska	626931	686293	59362
2	Delaware	783595	873092	89497
3	Wyoming	493782	532668	38886
Which SAS program correctly combines the data?

A.
data compare;
merge WORK.P2000(in=_a Location=State)
WORK.P2008(in=_b);
by State;
if _a and _b;
Difference=Pop2008-Pop2000;
run;

B.
data compare;
merge WORK.P2000(rename=(Location=State))
WORK.P2008;
by State;
if _a and _b;
Difference=Pop2008-Pop2000;
run;

**C.
data compare;
merge WORK.P2000(in=_a rename=(Location=State))
WORK.P2008(in=_b);
by State;
if _a and _b;
Difference=Pop2008-Pop2000;
run;**

D.
data compare;
merge WORK.P2000(in=_a) (rename=(Location=State))
WORK.P2008(in=_b);
by State;
if _a and _b;
Difference=Pop2008-Pop2000;
run;
```
1. MERGE statement的语法格式，MERGE dataset1 dataset2 (option1 option2);
2. RENAME option的作用是重新对变量命名，格式为：RENAME = (旧变量名 = 新变量名)；
3. MERGE的作用是将来自于多个data set中的观测值合并为一个观测值（相当于SQL中的JOIN）。
IN option用于生成一个布尔型变量，变量名为等号右边的变量（题目中分别为_a和_b），此过程在pdv中
当Merge后的观测值有来自于当前data set的数据时，该变量的值为1，否则为0。比如题目中新data set的第一个观测值的State为Alaska，
WORK.P2000和WORK.P2008中均有Alaska这个观测值，那么_a和_b在第一次DATA step循环中均为1。
以下程序可以显示各个DATA step中_a和_b的值（由于_a和_b并不会被输出到新的data set中，需要把其值赋值给新的变量，
```


29. The following SAS program is sumbitted:

data WORK.INFO;
infile ‘DATAFILE.TXT’;
input @1 Company $20. @25 State $2. @;
if State=’ ‘ then input @30 Year;
else input @30 City Year;
input NumEmployees;
run;

How many raw data records are read during each iteration of the DATA step?

A. 1
**B. 2**
C. 3
D. 4
```
1. @1 @25 @30 代表列数；第二个input以前全在一行data中；
2. 默认情况下，每出现一次INPUT，SAS都会去新的一行读取数据，而@的作用是让SAS继续在当前行读取数据；
3. @@：两次调用同一个input
```

30.You’re attempting to read a raw data file and you see the following messages displayed in the SAS Log:

NOTE: Invalid data for Salary in line 4 15-23.
RULE:     ----|----10---|----20---|----30---|----40---|----50-
4         120104   F    46#30     11MAY1954 33
Employee_Id=120104 employee_gender=F Salary=. birth_date=-2061 _ERROR_=1 _N_=4
NOTE: 20 records were read from the infile ‘c:employees.dat’.
      The minimum record length was 33.
      The maximum record length was 33.
NOTE: The data set WORK.EMPLOYEES has 20 observations and 4 variables.

What does it mean?
A. A compiler error, triggered by an invalid character for the variable Salary.
**B. An execution error, triggered by an invalid character for the variable Salary.**
C. The 1st of potentially many errors, this one occurring on the 4th observation.
D. An error on the INPUT statement specification for reading the variable Salary.
```
1. Compiler error是指SAS在编译代码时出错，例如代码写错了。不会输出data set。
2. Execution error是指代码没错，但是在执行代码是发生错误，例如试图将字符复制给数值型变量。依然会输出data set。
```

31. Given the following raw data records in DATAFILE.TXT:

----|----10---|----20---|----30
Kim,Basketball,Golf,Tennis
Bill,Football
Tracy,Soccer,Track

The following program is submitted:

data WORK.SPORTS_INFO;
length Fname Sport1-Sport3 $ 10;
infile ‘DATAFILE.TXT’ dlm=’,’;
input Fname $ Sport1 $ Sport2 $ Sport3 $;
run;

proc print data=WORK.SPORTS_INFO;
run;

Which output is correct based on the submitted program?

A.

Obs	Fname	Sport1	Sport2	Sport3
1	Kim	Basketball	Golf	Tennis
2	Bill	Football		
3	Tracy	Soccer	Track	
B.

Obs	Fname	Sport1	Sport2	Sport3
1	Kim	Basketball	Golf	Tennis
2	Bill	Football	 Football	 Football
3	Tracy	Soccer	Track	 Track
**C.

Obs	Fname	Sport1	Sport2	Sport3
1	Kim	Basketball	Golf	Tennis
2	Bill	Football	Tracy	Soccer**
D.

Obs	Fname	Sport1	Sport2	Sport3
1	Kim	Basketball	Golf	Tennis
2	Bill	Football	
```
sas读取data record原则
1. 当一行数据中变量值的数量少于变量的数量时，SAS会去下一行接着读取数据。
2. 当所有变量都得到赋值之后，无论该行数据中是否还有未使用的变量值，SAS都会前往下一行开始新的DATA step，即开始读取新的观测值。
当SAS在执行第二次DATA step时，由于第二行数据只有2个值，SAS会去第三行寻找值并赋给Sport2和Sport3。
当4个变量都得到赋值之后，SAS忽略第三行中余下的值Track。如果这时DATAFILE.TXT中还有第四行的话，SAS就会前往第四行开始读取第三个观测值。
```

32. Consider the following data step:

data WORK.NEW;
set WORK.OLD;
Count+1;
run;

The variable Count is created using a sum statement. Which statement regarding this variable is true?
A. It is assigned a value 0 when the data step begins execution.
B. It is assigned a value of missing when the data step begins execution.
**C. It is assigned a value 0 at compile time.**
D. It is assigned a value of missing at compile time.
```
1. Count + 1为一个Sum Statement，等价于：
RETAIN Count 0;
Count = SUM(Count, 1);
2. RETAIN的作用是初始化一个变量，并且在每次进入新的DATA step时，保留该变量的值。
值得注意的是，RETAIN statement在编译代码时执行，即在执行DATA step（读取数据）之前，所以RETAIN statement只执行一次。
3. SUM function的作用是求合，并且忽略missing value。
上面程序第一句的意思为初始化一个叫Count的变量，并且其初始值为0。
第二行的作用是将Count的值增加1，与Count = Count + 1类似，但两者有一个重要的区别，SUM function会忽略missing value，而后一种表达式则不会。
假设Count的值为missing，Sum(Count, 1)的结果为1，而Count + 1的结果则为missing，missing value加上一个值其结果还是missing。
```

33. The following SAS program is submitted:

data WORK.TEST;
set WORK.PILOTS;
if Jobcode=’Pilot2′ then Description=’Senior Pilot’;
else Description=’Unknown’;
run;

The value for the variable Jobcode is: PILOT2. What is the value of the variable Description?
A. PILOT2
**B. Unknown**
C. Senior Pilot
D. ‘ ‘ (missing character value)
```
字符串的大小写是有区别的，所以PILOT不等于Pilot，执行ELSE之后的表达式。
```

34. A user-defined format has been created using the FORMAT procedure.How is it stored?
**A. in a SAS catalog**
B. in a memory resident lookup table
C. in a SAS dataset in the WORK library
D. in a SAS dataset in a permanent SAS data library
```
存储自定义FORMAT的文件格式叫作catalog。FORMAT的存储位置和名字可以通过PROC FORMAT statement中的LIBRARY option设定，缩写为LIB，格式为：LIBRARY = lebref.catalog_name。例如：
PROC FORMAT LIBRARY = SASLIB.self_defined_format;
会在SASLIB library中建立名为self_defined_format的catalog。如果不定义libref，默认library为WORK。
如果不定义catalog_name，默认名字为Formats。如果不设置LIBRARY option，FORMAT会存储在WORK library下，文件名为Formats。
```
35. given the SAS data set SASDATA.TWO:

X	Y
5	2
3	1
5	6
The following SAS program is submitted:

data SASUSER.ONE SASUSER.TWO OTHER;
set SASDATA.TWO;
if X eq 5 then output SASUSER.ONE;
if Y lt 5 then output SASUSER.TWO;
output;
run;

What is the result?

**A.
data set SASUSER.ONE has 5 observations
data set SASUSER.TWO has 5 observations
data set WORK.OTHER has 3 observations**

B.
data set SASUSER.ONE has 2 observations
data set SASUSER.TWO has 2 observations
data set WORK.OTHER has 1 observations

C.
data set SASUSER.ONE has 2 observations
data set SASUSER.TWO has 2 observations
data set WORK.OTHER has 5 observations

D. No data sets are output. The DATA step fails execution due to syntax errors.
```
1. DATA statement可以一次建立多个data set，可以通过OUTPUT statement来指定所需写入数据的data set。如果程序中没有出现OUTPUT statement，那么SAS会自动在DATA step的最后加入OUTPUT，即一下2个程序是一样的：

data d;
infile datalines;
input x;
output;
datalines;
1
;
run;	data d;
infile datalines;
input x;
datalines;
1
;
run;
2. 本题中，出现了3个OUTPUT，第一个将SASDATA.TWO中X等于5的观测值写入SASUSER.ONE中（2个观测值），
第二个将SASDATA.TWO中Y小于5的观测值写入SASUSER.TWO中（2个观测值）。
第三个OUTPUT statement等价于：
OUTPUT SASUSER.ONE SASUSER.TWO OTHER;
```
36. Given the contents of the raw data file ‘EMPLOYEE.TXT’:

----|----10---|----20---|----30--
Xing           2 19 2004 ACCT
Bob            5 22 2004 MKTG
Jorge          3 14 2004 EDUC

The following SAS program is submitted:

data WORK.EMPLOYEE;
infile ‘EMPLOYEE.TXT’;
input
@1 FirstName $
@15 StartDate
@25 Department $;
run;

Which SAS informat correctly completes the program?
A. date9.
B. mmddyy10.
C. ddmmyy10.
D. mondayyr10.
```
FORMAT是指用于输出数据（例如：PROC PRINT）的格式，而INFORMAT则是读取数据采用的格式。
’ 2 19 2004’这种格式的日期，月日年由MMDDYY.读取，10则告诉SAS一共有10个字符，其中包括3个空格，2前面一个，19前面一个，2004前面一个。
程序中的@用于指定读取数据的位置，@n指从第n个字符开始读。StartDate是从第15个字符开始读，而第15个字符是一个空格，2是第16个字符，这就解释了为什么在读入的日期里，2前有会有一个空格。
```
[formate vs informate](https://blog.csdn.net/cyxlxp8411/article/details/7897767)

37. The SAS data set Fed.Banks contains a variable Open_Date which has been assigned a permanent label of “Open Date”. Which SAS program temporarily replaces the label “Open Date” with the label “Starting Date” in the output?

A.
proc print data=SASUSER.HOUSES label;
label Open_Date “Starting Date”;
run;

**B.
proc print data=SASUSER.HOUSES label;
label Open_Date=”Starting Date”;
run;**

C.
proc print data=SASUSER.HOUSES;
label Open_Date=”Starting Date”;
run;

D.
proc print data=SASUSER.HOUSES;
Open_Date=”Starting Date”;
run;
```
1. LABEL variable = ‘label‘;
2. PROC PRINT中的LABEL argument则是告诉SAS在打印数据时，输出该变量的label，而非默认的变量名。
```

38. Given the SAS data set WORK.ONE:

X	Y	Z
1	A	27
1	A	33
1	B	45
2	A	52
2	B	69
3	B	70
4	A	82
4	C	91
The following SAS program is submitted:

data WORK.TWO;
set WORK.ONE;
by X Y;
if First.Y;
run;
proc print data=WORK.TWO noobs;
run;

Which report is produced?

A.

X	Y	Z
1	B	45
2	A	52
2	B	69
3	B	70
4	A	82
4	C	91
**B.

X	Y	Z
1	A	27
1	B	45
2	A	52
2	B	69
3	B	70
4	A	82
4	C	91**
C.

X	Y	Z
1	A	33
1	B	45
2	A	52
2	B	69
3	B	70
4	A	82
4	C	91
D. The PRINT procedure fails because the data set WORK.TWO is not created in the DATA step.
```
by 将各个分组中的第一个观测值输入到WORK.TWO
```

39. The following SAS program is submitted:

data WORK.AUTHORS;
array Favorites{3} $ 8 (‘Shakespeare’,’Hemingway’,’McCaffrey’);
run;

What is the value of the second variable in the dataset WORK.AUTHORS?
A. Hemingway
**B. Hemingwa**
C. ‘ ‘ (a missing value)
D. The program contains errors. No variables are created.

40. The following SAS program is submitted:

data WORK.PRODUCTS;
Prod=1;
do while(Prod LE 6);
Prod + 1;
end;
run;

What is the value of the variable Prod in the output data set?

A. 6
**B. 7**
C. 8
D. . (missing numeric)

41. Given the raw data record in the file phone.txt:

----|----10---|----20---|----30---|
Stevens James SALES 304-923-3721 14

The following SAS program is submitted:

data WORK.PHONES;
infile ‘phone.txt’;
input EmpLName $ EmpFName $ Dept $ Phone $ Extension;
<_insert_code_>
run;

Which SAS statement completes the program and results in a value of “James Stevens” for the variable FullName?

**A. FullName=CATX(‘ ‘,EmpFName,EmpLName);**
B. FullName=CAT(‘ ‘,EmpFName,EmpLName);
C. FullName=EmpFName||EmpLName;
D. FullName=EmpFName + EmpLName;
```
CAT function用于连接括号内的字符串，字符串头部和尾部的空格会得到保留。例如：
data _null_;
x = ‘ SAS ‘;
y = ‘ R Python.’;
z = cat(x, y);
put z $char.;
run;
‘SAS’前面和后面的空格，’R’前面的空格都会得到保留。在LOG中会输出以下结果（不包括标尺）：
----|----10---|
 SAS  R Python.

CATX function在连接字符串时，会在各字符串之间插入一个设定好的分隔符，并且去掉字符串头部和尾部的空格。例如：
data _null_;
x = ‘ SAS ‘;
y = ‘ R Python.’;
z = catx(‘*’, x, y);
put z $char.;
run;
输出的结果为：
----|----10---|
SAS*R Python.

||为concatenation operator，起作用几乎相当于CAT，即CAT(a, b)和a||b输出相同的结果。唯一的区别是，接收合并后字符串的那个变量的默认长度（Length），例如以下程序：
data d;
x = ‘ SAS ‘;
y = ‘ R Python.’;
z1 = cat(x, y);
z2 = x||y;
put z1 $char.;
put z2 $char.;
run;
如果z1和z2的长度都没有预先定义，z1的长度为200，而z2的长度为x的长度加上y的长度。以下为PROC CONTENTS的输出结果：

Alphabetic List of Variables and Attributes
#	Variable	Type	Len
1	x	Char	5
2	y	Char	10
3	z1	Char	200
4	z2	Char	15
```

42. The following SAS program is submitted:

data WORK.ONE;
Text=’Australia, US, Denmark’;
Pos=find(Text,’US’,’i’,5);
run;

What value will SAS assign to Pos?

A. 0
B. 1
C. 2
D. 12
```
FIND function用于寻找字符串中某一个特定字符串片段的启示位置。题目中为：从’Australia, US, Denmark’中的第5个字符开始寻找’US’，’i’的作用是忽略大小写。
忽略大小写之后，’Australia, US, Denmark’中有2处’US’，但由于是从第5个字符开始找，所以第一次出现’US’的位置是第12个字符（从’A’开始数，包括逗号空格）。
```

43. Given the SAS data set WORK.ORDERS:

order_id	customer	shipped
9341	Josh Martin	02FEB2009
9874	Rachel Lords	14MAR2009
10233	Takashi Sato	07JUL2009
The variable order_id is numeric; customer is character; and shipped is numeric, contains a SAS date value,and is shown with the DATE9. format.

A programmer would like to create a new variable, ship_note,that shows a character value with the order_id,shipped date, and customer name.

For example, given the first observation ship_note would have the value “Order 9341 shipped on 02FEB2009 to Josh Martin”.

Which of the following statement will correctly create the value and assign it to ship_note?

A. ship_note=catx(‘ ‘,’Order’,order_id,’shipped on’,input(shipped,date9.),’to’,customer);
B. ship_note=catx(‘ ‘,’Order’,order_id,’shipped on’,char(shipped,date9.),’to’,customer);
C. ship_note=catx(‘ ‘,’Order’,order_id,’shipped on’,tranwrd(shipped,date9.),’to’,customer);
**D. ship_note=catx(‘ ‘,’Order’,order_id,’shipped on’,put(shipped,date9.),’to’,customer);**
```
put - numeric to character new_variable = PUT(source_value, format);即format指定的是new_variable的格式。比如题目中，将一个SAS date（距1960年1月1日的天数），用date9.0的格式表示。
input - character to numeric new_variable = INPUT(source_value, informat);即informat用于告诉SAS source_value的格式。
data d;
today1 = ’18Nov2014’d;
new_today1 = put(today1, ddmmyy10.);
today2 = ’18/11/2014′;
new_today2 = input(today2, ddmmyy10.);
run;

Obs	today1	new_today1	today2	new_today2
1	20045	18/11/2014	18/11/2014	20045

CHAR function的作用是返回字符串中某一字符的位置，比如char(‘SAS’, 3)，返回的值为’S’，char(‘SAS’, 4)则返回missing。
TRANWRD function用于替换字符串中的某些字符，比如tranwrd(‘SAS&R’, ‘R’, ‘Python’)，返回的值为’SAS&Python’。
```
44. The following SAS program is submitted:

data ONE TWO SASUSER.TWO
set SASUSER.ONE;
run;

Assuming that SASUSER.ONE exists, how many temporary and permanent SAS data sets are created?

A. 2 temporary and 1 permanent SAS data sets are created
B. 3 temporary and 2 permanent SAS data sets are created
C. 2 temporary and 2 permanent SAS data sets are created
**D. there is an error and no new data sets are created**
```Semicolon!!!```

45. The following SAS program is submitted:

ods csvall file=’c:test.csv’;
proc print data=WORK.ONE;
var Name Score Grade;
by IdNumber;
run;
ods csvall close;

What is produced as output?

A. A file named test.csv that can only be opened in Excel.
**B. A text file named test.csv that can be opened in Excel or in any text editor.**
C. A text file named test.csv that can only be opened in a text editor.
D. A file named test.csv that can only be opened by SAS.
```
ODS，全称Output Delivery System，用于导出SAS中数据和分析结果。开启ODS格式：
ODS destination file = ‘想要保存文件的路径+文件名.扩展名’;
关闭ODS格式：
ODS destination CLOSE;
其中destination用于定义导出文件的类型，比如题目中的CSVALL、HTML、PDF等。本题的程序输出的是CSV文件，可以用Excel和任意本文编辑器打开。
```

46. Given the SAS data set WORK.ONE:

Obs	Revenue2008	Revenue2009	Revenue2010
1	1.2	1.6	2
The following SAS program is submitted:

data WORK.TWO;
set WORK.ONE;
Total=mean(of Rev:);
run;

What value will SAS assign to Total?

A. 3
**B. 1.6**
C. 4.8
D. The program fails to execute due to errors.
```
本题使用了Variable List，Rev:是指选取所有以Rev开头的变量，并且在对变量列使用function时，要在变量列之前加上OF。
mean(of Rev:)等价于 mean(Revenue2008, Revenue2009, Revenue2010)，MEAN function用于求这三个值的均值。
```

47. The following output is created by the FREQUENCY procedure:

Frequency
Percent
Row Pct
Col Pct	
Table of region by product
region	product
corn	cotton	oranges	Total
EAST	
2
22.22
50.00
50.00	
1
11.11
25.00
33.33	
1
11.11
25.00
50.00	
4
44.44
SOUTH	
2
22.22
40.00
50.00	
2
22.22
40.00
66.67	
1
11.11
20.00
50.00	
5
55.56
Total	
4
44.44	
3
33.33	
2
22.22	
9
100.00
Which TABLES option(s) would be used to eliminate the

row and column counts and just see the frequencies and percents?

A. norowcount nocolcount
B. freq percent
**C. norow nocol**
D. nocounts
```
RPOC FREQ statement用于生成Frequency Table。题目要求不显示Row Percent和Column Percent这个统计量，这仅需要在TABLES statement后加上NOROW和NOCOL选项，程序为：
proc freq data = dataset;
tables region * product / nocol norow;
run;
```

48. The following SAS program is submitted:

data WORK.TEST;
drop City;
infile datalines;
input Name $ 1-14 / Address $ 1-14 / City $ 1-12 ;
if City=’New York ‘ then input @1 State $2.;
else input;
datalines;
Joe Conley
123 Main St.
Janesville
WI
Jane Ngyuen
555 Alpha Ave.
New York
NY
Jennifer Jason
666 Mt. Diablo
Eureka
CA
;
run;

What will the data set WORK.TEST contain?

**A.

Obs	Name	Address	State
1	Joe Conley	123 Main St.	
2	Jane Ngyuen	555 Alpha Ave.	NY
3	Jennifer Jason	666 Mt. Diablo	**

B.

Obs	Name	Address	City	State
1	Joe Conley	123 Main St.	Janesville	
2	Jane Ngyuen	555 Alpha Ave.	New York	NY
3	Jennifer Jason	666 Mt. Diablo	Eureka	
C.

Obs	Name	Address	State
1	Jane Ngyuen	555 Alpha Ave.	NY
D. No observations, there is a syntax error in the data step.
```
1. $表示这是一个字符型变量；
2. 1-14表示将该行的第1-14个字符写进变量；
3. /表示将指针移动到下一行的第一个字符，即之后的变量将从下二行的第一个字符开始读取。
4. INPUT statement默认自动前往下一行，当INPUT后没有申明任何变量名时，其起到的作用和/类似，但两者的工作原理不同，具体请查看官方手册中INPUT statement的Without Arguments部分。
```

49. The following SAS program is submitted:

data WORK.TOTALSALES(keep=MonthSales{12});
set WORK.MONTHLYSALES(keep=Year Product Sales);
array MonthSales{12};
do i=1 to 12;
MonthSales{i}=Sales;
end;
drop i;
run;

The program fails execution due to syntax errors.
What is the cause of the syntax error?
**A. An array cannot be referenced on a keep= data set option.**
B. The keep= data set option should be (keep=MonthSales*).
C. The keep= data set option should be the statement KEEP MonthSales{12}.
D. The variable MonthSales does not exist.
```
1. MonthSales{12}为数组；
2. KEEP和DROP的对象不能是数组，只能是变量；
3. 如果希望去掉数组中的变量，可以直接引用该变量的名字。
例如题目中，希望仅保留数组中第12个元素，即MonthSales{12}，可以使用以下KEEP option: KEEP = MonthSales12，如果想保留整个数组：KEEP = MonthSales1 – MonthSales12。
4. ARRAY statement must be defined in the Data Step prior to any references to the array in outher Data Step statements.
```
50. Given the SAS data set WORK.ONE:

Id	Char1
111	A
158	B
329	C
644	D
and the SAS data set WORK.TWO:

Id	Char2
111	E
538	F
644	G
The following program is submitted:

data WORK.BOTH;
set WORK.ONE WORK.TWO;
by Id;
run;

What is the first observation in SAS data set WORK.BOTH?

**A.

Id	Char1	Char2
111	A	**
B.

Id	Char1	Char2
111	E	
C.

Id	Char1	Char2
111	A	 E
D.

Id	Char1	Char2
644	D	G
```
1. SET statement的作用是将多个data set合并，但不会对观测值进行合并。ascending
题目中，新data set BOTH中将包含ONE和TWO中所有的变量.
2. BY statement作用是使新data set根据ID升序排列
所以ONE中的第一条数据将成为BOTH中的第一条数据，由于该观测值中没有Char2变量，所以输出结果中显示为missing。完整的BOTH为：
Obs	Id	Char1	Char2
1	111	A	
2	111		E
3	158	B	
4	329	C	
5	538		F
6	644	D	
7	644		G
```

51. The following program is submitted:

proc contents data=_all_;
run;

Which statement best describes the output from the submitted program?

A. The output contains only a list of the SAS data sets that are contained in the WORK library.
B. The output displays only the contents of the SAS data sets that are contained in the WORK library.
C. The output displays only the variables in the SAS data sets that are contained in the WORK library.
**D. The output contains a list of the SAS data sets that are contained in the WORK library and displays the contents of those data sets.**
```
1. The CONTENTS procedure shows the contents of a SAS data set and prints the directory of the SAS library. 
2. As the libref is omitted, SAS uses the default library WORK, and  _ALL_ represents all data sets in that library. 
SAS lists the data sets in WORK library followed by the contents of each data set.
```

52. Given the SAS data set WORK.EMP_NAME:

Name	EmpID
Jill	1864
Jack	2121
Joan	4698
John	5463
Given the SAS data set WORK.EMP_DEPT:

EmpID	Department
2121	Accounti
3567	Finance
4698	Marketin
5463	Accounti
The following program is submitted:

data WORK.ALL;
merge WORK.EMP_NAME(in=Emp_N)
WORK.EMP_DEPT(in=Emp_D);
by Empid;
if (Emp_N and not Emp_D) or (Emp_D and not Emp_N);
run;

How many observations are in data set WORK.ALL after submitting the program?

A. 1
**B. 2**
C. 3
D. 5

53. The following SAS program is submitted:

data WORK.TOTAL_SALARY;
retain Total;
set WORK.SALARY;
by Department;
if First.Department
then Total=0;
Total=sum(Total, Wagerate);
if Last.Total;
run;
What is the initial value of the variable Total?

A. 0
**B. Missing**
C. The value of the first observations Wagerate
D. Cannot be determined from the information given
```
RETAIN Count 0;
Count = SUM(Count, 1);
sum 可以处理missing，=不可以
```

54. Consider the following data step:

data WORK.TEST;
set SASHELP.CLASS(obs=5);
retain City ‘Beverly Hills’;
State=’California’;
run;

The computed variables City and State have their values assigned using two different methods, a RETAIN statement and an Assignment statement. Which statement regarding this program is true?

A. The RETAIN statement is fine, but the value of City will be truncated to 8 bytes as the LENGTH statement has been omitted.
B. Both the RETAIN and assignment statement are being used to initialize new variables and are equally efficient. Method used is a matter of programmer preference.
C. The assignment statement is fine, but the value of City will be truncated to 8 bytes as the LENGTH statement has been omitted.
**D. City’s value will be assigned one time, State’s value 5 times.**
```
Both RETAIN statement and Assignment (=) statement can be used to assign values, but there are a few differences.

1. As RETAIN statement assigns the value at compile time, the code will be executed once and only once. Assignment statement, however, respecifies the value in every iteration.
2. SAS automatically sets variables that are assigned values by an assignment statement to missing before each iteration of the DATA step. On the contrary, RETAIN statement retains the value from one iteration to the next.

AS this program reads the first 5 observations (5 iterations) in CLASS data set,  the value of State is specified 5 times, and the variable is reset to missing when SAS begins to read the next observation. City is initialized as ‘Beverly Hills’ before DATA step and won’t be reset to missing.
```

55. The following SAS program is submitted:

data WORK.DATE_INFO;
X=”01Jan1960″D ;
run;

Variable X contains what value?

**A. the numeric value 0**
B. the character value “01Jan1960”
C. the date value 01011960
D. the code contains a syntax error and does not execute.
```
d is case insensitive.
```

56. The following output is created by the FREQUENCY procedure:

Frequency
Percent
Row Pct
Col Pct	
Table of Region by Product
Region	Product
Corn	Cotton	Oranges	Total
East	
2
22.22
50.00
50.00	
1
11.11
25.00
33.33	
1
11.11
25.00
50.00	
4
44.44
South	
2
22.22
40.00
50.00	
2
22.22
40.00
66.67	
1
11.11
20.00
50.00	
5
55.56
Total	
4
44.44	
3
33.33	
2
22.22	
9
100.00
Which TABLES statement was used to completed the following program
that produced the output?

proc freq data=sales;
<_insert_code_>
run;

A. tables region product;
B. tables region,product;
C. tables region/product;
**D. tables region*product;**

57. Given the SAS data set WORK.ONE:

N	BeginDate
1	09JAN201
2	12JAN201
The following SAS program is submitted:

data WORK.TWO;
set WORK.ONE;
Day=<_insert_code_>;
format BeginDate date9.;
run;

The data set WORK.TWO is created, where Day would be 1 for Sunday, 2 for Monday, 3 for Tuesday, … :

N	BeginDate	Day
1	09JAN2010	7
2	12JAN2010	3
Which expression successfully completed the program and creates the variable Day?

A. day(BeginDate)
**B. weekday(BeginDate)**
C. dayofweek(BeginDate)
D. getday(BeginDate,today())

```
1. WEEKDAY function  returns an integer that corresponds to the day of the week, where 1=Sunday, 2=Monday, …, 7=Saturday, from a SAS date value. 
2. DAY function returns the day of the month. 
3. There is no function called DAYOFWEEK or GETDAY in SAS.
```

58. The following program is submitted:

proc format;
value salfmt. 0 -< 50000 = ‘Less than 50K’ 50000 – high = ’50K or Greater’;

options fmterr nodate pageno=1;
title ‘Employee Report’;

proc print data=work.employees noobs;
var fullname salary hiredate;
format salary salfmt. hiredate date9.;
label fullname=’Name of Employee’ salary=’Annual Salary’ hiredate=’Date of Hire’;
run;

Why does the program fail?

A. The PAGENO option is invalid in the OPTIONS statement.
B. The RUN statement is missing after the FORMAT procedure.
**C. The format name contains a period in the VALUE statement.**
D. The LABEL option is missing from the PROC PRINT statement.
``` .是用来区别变量名和格式名
```

59.Given the contents of the raw data file TYPECOLOR.DAT:

—-+—-10—+—-20—+—-30
daisyyellow

The following SAS program is submitted:

data FLOWERS;
infile ‘TYPECOLOR.DAT’ truncover;
length
Type $ 5
Color $ 11;
input
Type $
Color $;
run;

What are the values of the variables Type and Color?

A. Type=daisy, Color=yellow
B. Type=daisy, Color=w
C. Type=daisy, Color=daisyyellow
**D. Type=daisy, Color=**

```
读取数据default delimiter是space，题目中daisyyellow 是一个value被读取，如需强行读取两个数据，可采取以下形式：
data FLOWERS;
infile ‘TYPECOLOR.DAT’;
length
Type $ 5
Color $ 11;
input
Type $ 1-5
Color $ 6-11;
run;
```

60. Given the SAS data set WORK.PRODUCTS:
ProdId Price ProductType Sales Returns
------ ----- ----------- ----- -------
K12S 95.50 OUTDOOR 15 2
B132S 2.99 CLOTHING 300 10
R18KY2 51.99 EQUIPMENT 25 5
3KL8BY 6.39 OUTDOOR 125 15
DY65DW 5.60 OUTDOOR 45 5
DGTY23 34.55 EQUIPMENT 67 2
The following SAS program is submitted:
data WORK.REVENUE(drop=Sales Returns Price);
set WORK.PRODUCTS(keep=ProdId Price Sales Returns);
Revenue=Price*(Sales-Returns);
run;
How many variables does the WORK.REVENUE data set contain?
**A. 2**
B. 3
C. 4
D. 6

61. Consider the data step:
data WORK.TEST;
infile 'c:\class1.csv' dsd;
input Name $ Sex $ Age Height Weight;
if Age NE 16 and Age NE 15 then Group=1;
else Group=2;
run;
Which statement produces a functionally equivalent result for assigning Group a value?
**A. if Age not in(15,16) then Group=1; else Group=2;**
B. if (Age NE 16) or (Age NE 15) then Group=1; else Group=2;
C. where Age not between 15 and 16 then Group=1; else Group=2;
D. both A or C will work.
```
WHERE 不能与THEN连用
```

62. The following SAS program is submitted:
<_insert_ods_code_>
proc means data=SASUSER.SHOES;
where Product in ('Sandal' , 'Slipper' , 'Boot');
run;
<_insert_ods_code_>
Which ODS statements, inserted in the two locations above,create a report stored in an html file?
A.
ods html open='sales.html';
ods html close;
B.
ods file='sales.html' / html;
ods file close;
**C.
ods html file='sales.html';
ods html close;**
D.
ods file html='sales.html';
ods file close;

63. The following SAS program is submitted:
data WORK.OUTDS;
do until(Prod GT 6);
Prod + 1;
end;
run;
What is the value of the variable Prod in the output data set?
A. . (missing)
B. 6
**C. 7**
D. Undetermined, infinite loop.

64. The following SAS program is submitted:   
data work.accounting;        
length jobcode $ 12;        
set work.department; 
run; 
The WORK.DEPARTMENT SAS data set contains a character variable named JOBCODE with a length of 5. Which of the following is the length of the variable JOBCODE in the output data set? 
A. 5 
B. 8 
C. 12 
D. The length can not be determined as the program fails to execute due to errors. 
```
LEGTH规定的是变量的字节长度，不是格式，不能含小数点。 LENGTH variable-specification(s) <DEFAULT=n> 其中，DEFAULT=n是规定新建的数值变量的默认长度8改为n。 
1. 数值变量 对于数值变量，LENGTH范围为3-8字节。LENGTH可放在任意位置。 在PROC SQL中ALERT不能改变数值变量长度。
2. 字符变量 对于字符变量，LENGTH范围为1-32767字节，空格占一个字符。LENGTH必须放在SET语句之前。实际上，较少使用LENGTH语句，而是通过PROC SQL中ALERT改变字符变量长度。 
```

65. The following SAS program is submitted:
data WORK.ACCOUNTING;
set WORK.DEPARTMENT;
label Jobcode='Job Description';
run;
Which statement is true about the output dataset?
A. The label of the variable Jobcode is Job (only the first word).
B. The label of the variable Jobcode is Job Desc (only the first 8 characters).
**C. The label of the variable Jobcode is Job Description.**
D. The program fails to execute due to errors. Labels must be defined in a PROC step.

66. The following SAS program is submitted:
data WORK.SALES;
do Year=1 to 5;
do Month=1 to 12;
X + 1;
end;
end;
run;
How many observations are written to the WORK.SALES data set?
A. 0
**B. 1**
C. 5
D. 60

```
循环结束之后x才输入到数据集中。可加入output
data WORK.SALES;
do Year=1 to 5;
do Month=1 to 12;
X + 1;
end;
end;
data WORK.SALES;
do Year=1 to 5;
do Month=1 to 12;
X + 1;
output;
end;
end;

run;
```

67. Consider the following data step:
data WORK.NEW;
set WORK.OLD(keep=X);
if X < 10 then X=1;
else if X >= 10 AND X LT 20 then X=2;
else X=3;
run;
In filtering the values of the variable X in data set WORK.OLD, what value new value would be assigned to X if
its original value was a missing value?
**A. X would get a value of 1.**
B. X would get a value of 3.
C. X would retain its original value of missing.
D. This step does not run because of syntax errors.
```
缺失值默认为最小
```

68. The following SAS program is submitted:
data WORK.ACCOUNTING;
set WORK.DEPARTMENT;
length EmpId $6;
CharEmpid=EmpId;
run;
If data set WORK.DEPARTMENT has a numeric variable EmpId,which statement is true about the output
dataset?
A. The type of the variable CharEmpid is numeric.
B. The type of the variable CharEmpid is unknown.
C. The type of the variable CharEmpid is character.
**D. The program fails to execute due to errors.**
```两个数据集中empid格式存在冲突```

69. Given the data set WORK.EMPDATA:
Employee_ Manager_
ID Job_Title Department ID
------- ---------------------- ---------------- ------
120101 Director Sales Management 120261
120102 Sales Manager Sales Management 120101
120103 Sales Manager II Sales Management 120101
120104 Administration Manager Administration 120101
120105 Secretary I Administration 120101
Which one of the following where statements would display observations with job titles containing the word
'Manager'?
A. where substr(Job_Title,(length(Job_Title)-6))='Manager';
B. where upcase(scan(Job_Title,-1,' '))='MANAGER';
C. where Job_Title='% Manager ';
**D. where Job_Title like '%Manager%';**

70.After a SAS program is submitted, the following is written to the SAS log:
105 data WORK.JANUARY;
106 set WORK.ALLYEAR(keep=Product Month Quantity Cost);
107 if Month='JAN' then output WORK.JANUARY;
108 Sales=Cost * Quantity;
109 drop=Month Quantity Cost;
22
ERROR 22-322: Syntax error, expecting one of the following: !,
!!, &, *, \**, +, -,
, <=, <>, =, >, >=,
AND, EQ, GE, GT, IN, LE, LT, MAX, MIN, NE, NG, NL,
NOTIN, OR, ^=, |, ||, ~=.
110 run;
What data set option could be attached to WORK.JANUARY to replace the DROP statement that generated the
error in the log?
A. (drop Month Quantity Cost)
B. (drop Month, Quantity, Cost)
C. (drop=Month, Quantity, Cost)
**D. (drop=Month Quantity Cost)**
