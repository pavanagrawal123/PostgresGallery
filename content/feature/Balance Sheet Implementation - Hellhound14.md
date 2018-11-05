|Date|Profit ($)|Loss ($)|Monthly Earnings ($)|Total ($)|
|----|----------|--------|--------------------|---------|
|"2018-01-28"|576|543|33|33|
|"2018-02-28"|675|521|154|187|
|"2018-03-28"|432|653|-221|-34|
|"2018-04-28"|765|321|444|410|


### Description
Creating A Table On A SQL Server Can Help You. `How You Ask?` Well….
Microsoft Softwares Like `MS Excel Cannot Do Things Postgresql Can`. Let’s Say You Wanna Create And Share Your Financial Conditions Depicted Through A Table To Someone Far Away From You, But You Don’t Want To Fuss Over The Work Of Making A Copy Of The File And Sending It Through An E-Mail. You Can Just Create The Same Table In Postgresql Which Will `Automatically Update The Data On It To A Public Server`, Which Can Be Accessed Easily By Anyone With The `Server Name And Password`.
It Also Makes It Easier For People To Add The Values And Then Have Them Automatically Calculated Through A `Press Of A Button`.
I Bet MS Excel Doesn’t Do That!
But Wait There Is More Did I Tell You That You Can Even Share Your `Server With A Large Group Of People`. This Makes Your Work Even `More Quick and Easy`.

### Code
CREATE TABLE table1 (“Date” date, “Profit ($)” integer, “Loss ($)” integer, “Monthly Earnings ($)” integer);


INSERT INTO public.table1 (
	"Date", "Profit ($)", "Loss ($)", "Monthly Earnings ($)", "Total")
	VALUES ('2018-01-28', 576, 543, 0, 0),
     ('2018-02-28', 675, 521, 0, 0),
     ('2018-03-28', 432, 653, 0, 0), 
     ('2018-04-28', 765, 321, 0, 0);

UPDATE public.table1
	SET "Monthly Earnings ($)"="Profit ($)"-"Loss ($)", 
"Total"= (SELECT LAG ("Monthly Earnings ($)”, 1, 0) OVER (ORDER BY "Monthly Earnings ($)")) +"Monthly Earnings ($)";


### Code Breakdown and Explanation

The `CREATE TABLE` statement creates a new table with the name `“table1”` and adds the columns `“Date”, “Profit ($)”, “Loss ($)” and “Earnings ($)”` of the defined data types.

In the newly formed “table1”, using the statement `INSERT INTO` new `VALUES` are added.

Finally, the `UPDATE` statement updates the values of the `“Earnings ($)”` column by subtracting the values of the `“Loss ($)”` column from the `“Profit ($)”` one.

It also `SETS` the value of `“Total”` column by adding the previous row values with (Calculated through LAG function) the `“Monthly Earnings ($)”` column.
