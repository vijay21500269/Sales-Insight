# Sales-Insight
## Problem Statement:
A Computer Hardware Manufacuturer Company faces certain problems with respect to it's Bussiness Sales.
Let's say that there is a company named 'A' who supplies computer hardware and peripheral to many clients across India, let's say they have there headquaters in Delhi,India. The sales director of the company is facing so many challenges as the market is growing dynamically. He is facing issues in tracking the sales in regional markets , he's having issues regarding to the insights of the bussiness and therfore he has some regional managers (North India , South india, Central India ) working for his company. Whenever he wants the insights regarding these three region he would approach them and get the details. 

The problem is that these conversations are verbal.Even though the managers come up with excel files , its a hugh number of data for the sales director to go through and figure out the need.

The sales director just expects the managers to give a statistical data which are in simpler terms inorder to focus on the weak area that they need to work on inorder to grow their bussiness further.

## Approach towards End goal : 
Project Planning : We will be using AIMS Grid to tackle the problem and find the strategy to solve the problem.Followed by Data discovery , Data cleaning , Data merging and finally generating an interactive dashboard in Power BI.
![Screenshot 2023-09-24 231726](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/2e85bc95-ad71-41bd-9c7c-7f9537400c80)

## DataSet : 
We are provided with a database named "sales".

The database has five tables namely customers , date , markets , products and transactions. 

### Customer table : 
![a1](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/f78c96af-97e3-4f5c-8e10-2d0f40ac9be1)

### Date table :
![a2](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/39eaf6e4-d577-4a1e-a75a-5af6c6c6b214)

### Markets table :
![a3](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/afb8b151-d36d-495c-9301-40af5d3ba03d)

### Products table :
![a4](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/4509b86e-1898-40ad-a59c-eb2f1c50dfa9)

### Transaction tables : 
![a5](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/318e9d2b-5189-4315-ba13-05714843c034)

## Data Model :

Building the data model for analysis.

Once the data tables are loaded into the PowerBI , it creates a data model that establish the realtion among differnt tables between the coulmns present in the table. This helps the data analyst to analyse the data in a better rate and come up with efficient results.

![11](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/e600e599-6cb9-49d6-ac2d-9620bc806aaa)

## Data wrangling and Data munging :

1 . The above tables may contain some null values.

2 . It might contain some inappropriate values like negative and zero values.

3 . It might have duplicate records.

4 . It might have terms expressed in differnt formats ( example : the monetary terms can vary based on international sales exports).

Inorder to handle all these issues we need to clean the data first. In simple terms , if we resolve the above issues our data tables will be cleaned and secure enough to produce the correct results during data processing.

### Removing the Null values from Markets table (column - zone): 

![ab](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/56bfe2e2-c57e-4658-a436-b279fd5a6686)

![b1](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/00309bcf-f80c-4989-a7ad-6a611f3dc761)
### Removing values that are less than and equal to 0 from transaction table (column - sales_amount):
```
SELECT * FROM sales.transactions where transactions.sales_amount<=0;
SET SQL_SAFE_UPDATES = 0;
DELETE FROM sales.transactions WHERE sales_amount <= 0;
select * from sales.transactions;
```
![b4](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/24095504-a549-4e7e-a27a-8aef509c8c89)

### Converting monetary terms from USD to INR : 
```
SELECT * FROM sales.transactions where currency = "USD" or currency = "USD\r";
```
![aa1](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/c81788b0-31e5-4b1f-8c89-3602d16f52ea)

```
Table.AddColumn(#"Cleanup currency", "normalize_sales_amount", each if [currrency]="USD#(cr)" then [sales_amount]*75 else [sales_amount])
```
![c2n](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/4aef6211-df8c-4c45-b421-3540d6ac153c)


## PowerBI : 

### Interface for creating Report : Data Visualization is done here.

![page](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/8561f2b0-6ff1-48a4-82a9-b595789098ec)

For our problem statement , we need to analyse the market status in different areas or zones to get the inference on the sales. And based on the sales insight and the trends the sales director will implement some ideas and solution to make the weak areas into stronger ones.
### Revenue and Sales - Card :

Revenue and Sales Quantity are created and used as the Base Measures inorder to polt differnt UI elements.

Revenue is gonna be the sum of sales_amount column from the tarnasaction table, this gives the Total Revenue across every year.

![1rev](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/5c0c5b92-a11d-44c6-9898-7389c8474bec)

Sales Quantity is gonna be the sum of sales_qty column from the transaction table, this gives the total number of sales over the years.

![1sale](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/b5b8d95c-4685-4a15-8c72-2523db448a7e)

### Revenue By Market - Horizontal Bar Chart :

This bar chart gives the visulaization of the revenue based on the markets available in the table .

![1revmar](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/cb643870-e766-4d68-930f-423986fd3824)

![a1n](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/5f289e29-8adb-4866-bcf8-b9727ad437ae)

From this we infer that the Revenue obtained in the market Mumbai is 150.08 Million.

### Sales Quantity By Market -  Horizontal Bar Chart : 

This bar chart gives the visulaization of the Number of sales based on the markets available in the table .

![1salemar](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/cb38e0a9-0057-4bab-b4b5-491194327ce5)

![a2](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/8a1078cc-8a2a-47d8-a2aa-42ec483bc901)

From this we can infer that the number of sales occured in Nagpur is 262094.

### Time Scale - Slicer : 

#### YEAR

Inorder to view the revenue based on year, we can use cy_date column in our dashborad.

![1year](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/6a2a68c3-b5c2-4e2b-82e5-43bd09bd3725)

##### The Revenue trend and status in the year 2018 

![2018](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/e4bf91a7-ed5e-4224-bc6b-a0d89ee029d6)

##### The Revenue trend and status in the year 2020

![2020](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/299d5fb5-55a4-4964-a735-1291c036b136)
#### DATE

Inorder to view the revenue based on date, we can use cy_date column in our dashborad.

![1date](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/7e9d01fb-3dcb-499e-aba3-377860949d31)

##### The Revenue status at the beginning of the year 2019 (Jan)

![2019](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/5009b877-d30d-4e02-898c-63c2e79782d2)

##### The Revenue status at the ending of the year 2019 (Dec)

![2019dec](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/a035af78-76fa-4ec1-aaf3-2111da72a53a)

From the data , we infer that there is a decrement in the revenue by 8.93 Million.

### Top 5 Customers : 

Using filtering Options , we can visualize only the top 5 customers by revenue who contribute more to the sales of the company.

![15cus](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/abf00e6b-5a45-4ea6-8d05-341af517230c)

![a5t](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/b31185c8-d20b-44f2-88c2-f0873ab36b51)

### Top 5 Products : 

Using filtering Options , we can visualize only the top 5 products by revenue over the sales period.

![15pro](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/697a3fe8-1b75-489c-ade4-a416abe41819)

![a5ta](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/bb478d4e-bd5a-4ffe-8749-c3224ab817f0)

### Revenue Trend - Line chart : 

This revenue trend chart is build vs revenue and date to detect the increment and decrement in the revenue.

![1trend](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/ec9305b0-ebe6-4350-901f-b207191af336)

##### Overall Revenue - Oct 

![revb](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/80316a65-afcf-4282-87cb-a63b79bda550)

##### Overall Revenue - Jan

![revm](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/9977ec9e-9a95-403b-ae15-7c403bf8d0e0)

##### Overall Revenue - Jun

![reve](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/831e9a36-ecd6-4dfc-a63b-ff6c8fb7d4c8)

### Final Report : 
Thus in this way an interactive PowerBI can be built.

Previously the engineer team will spend money and time creating these kinds of dashboard. But by using these visualization tools like PowerBI , it becomes easy for the analyst to segregate data and visualize them. And the sales director is much more pleased and clear with the sales insights of his company by just interacting with the PowerBI dashboard.

![report](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/d57fc7c5-4149-4b55-8bd6-93fb7ac7e496)

## Validation \ Cross Checking : 

Lets check where the PowerBI dashboard yeilds the accurate results as in the dataset.

The overall revenue in the year 2020 is 142.22M - this is the number given by PowerBI

![val1](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/2f9429e4-24e0-4216-a549-f5419d8437c1)

Using sql queries we can check the revenue yeild in the year 2020

```
SELECT SUM(transactions.sales_amount)
FROM sales.transactions
INNER JOIN date ON transactions.order_date = date.date
WHERE date.year = 2020 AND (transactions.currency = 'INR\r' OR transactions.currency = 'USD\r');

```
![val1a](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/8adb4575-4a3c-45ff-9f72-7b0bbaf9c276)

## End goal :

By using this interative PowerBi DashBoard the sales director is able to 

#1 . track revenue numbers and sales quantity numbers over the years .

#2 . track revenue breakdown by regional states.

#3 . track revenue trends.

Enabling him to finally work on the weak areas and come up with new ideas and grow their bussiness in a effective and efficient manner.

## Mobile Interface :
![mobile](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/e8835415-2438-4ce6-bd3d-17bc5267d59e)
![mobile2019](https://github.com/SOWMIYA2003/Sales-Insight/assets/93427443/b588b6df-683e-402f-81ab-4ae4e69511ef)

## Links :
##### SQL DOWNLOAD LINK :
```
https://dev.mysql.com/downloads/file/?id=520407
```
##### POWERBI DOWNLOAD LINK : 
```
https://aka.ms/pbidesktopstore
```
