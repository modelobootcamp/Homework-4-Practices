
### Heroes Of Pymoli Data Analysis
* Of the 1163 active players, the vast majority are male (84%). There also exists, a smaller, but notable proportion of female players (14%).

* Our peak age demographic falls between 20-24 (44.8%) with secondary groups falling between 15-19 (18.60%) and 25-29 (13.4%).

### Note
* Instructions have been included for each segment. You do not have to follow them exactly, but they are included to help you think through the steps.


```python
# Dependencies and Setup
import pandas as pd
import numpy as np

# File to Load (Remember to Change These)
#purchase_data.csv = "Resources/purchase_data.csv"

# Read Purchasing File and store into Pandas data frame
# import a CSV file and rename csv for ease of use
data = pd.read_csv("purchase_data.csv")
```

##  Player Count

* Display the total number of players
* Cleaner formatting Player Count


```python
SN = {'Total Player':[len(data['SN'].value_counts())]}
SN1 = pd.DataFrame(SN)
SN1
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Player</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>576</td>
    </tr>
  </tbody>
</table>
</div>



## Purchasing Analysis (Total)
 
* Run basic calculations to obtain number of unique items, average price, etc.
* Create a summary data frame to hold the results
* Optional: give the displayed data cleaner formatting
* Display the summary data frame


```python
it = (data['Item ID'].nunique())
print(it)
```

    183
    

** Average price


```python
average_price = (data['Price'].mean())
print(average_price)
```

    3.050987179487176
    


```python
purchased_number = (data['SN'].count())
print(purchased_number)
```

    780
    


```python
total_revenue = (data['Price'].sum())
print(total_revenue)
```

    2379.77
    

** Cleaner formatting Player Count


```python
#Number of Unique Items
UniqueItems = len(data['Item Name'].value_counts())
#Average Purchase Price
AvPurchPrice = round(data['Price'].mean(),2)
#Total Purchase Value
TotalPurchases = round(data['Price'].sum(),2)
#Purchasing Analysis (Total)
PurchasingAnalysis= {'Unique Items':[UniqueItems],'Average Price':[AvPurchPrice],'Number of Purchases': [len(data)],'Total Purchases':[TotalPurchases]}
PurchasingAnalysis1 =pd.DataFrame(PurchasingAnalysis)
PurchasingAnalysis1 = PurchasingAnalysis1[['Unique Items','Average Price','Number of Purchases','Total Purchases']]
PurchasingAnalysis1
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unique Items</th>
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Total Purchases</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>179</td>
      <td>3.05</td>
      <td>780</td>
      <td>2379.77</td>
    </tr>
  </tbody>
</table>
</div>



## Gender Demographics
* Percentage and Count of Male Players
* Percentage and Count of Female Players
* Percentage and Count of Other / Non-Disclosed


```python
total_count = len(data["SN"].unique())

#Percentage and Count of Male Players
#Male = data.loc[data['Gender'] =='Male',:]
Male1= data.groupby(['Gender']).get_group(('Male'))
Male2= len(Male1['SN'].unique())
MalePercent= round((Male2/total_count)*100,2)

#Percentage and Count of Female Players
Female1= data.groupby(['Gender']).get_group(('Female'))
Female2= len(Female1['SN'].unique())
FemalePercent= round((Female2/total_count)*100,2)

#Percentage and Count of Other / Non-Disclosed Players
Other1= data.groupby(['Gender']).get_group(('Other / Non-Disclosed'))
Other2= len(Other1['SN'].unique())
OtherPercent= round((Other2/total_count)*100,2)

#Make it into a Gender DataFrame
gender1 = {'Percent of Players':[MalePercent,FemalePercent,OtherPercent],'Gender':["Male",'Female','Other'],'Gender Count':[Male2,Female2,Other2]}
gender2 =  pd.DataFrame(gender1)
gender2= gender2.set_index('Gender')
gender2= gender2[['Gender Count','Percent of Players']]
gender2
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender Count</th>
      <th>Percent of Players</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>484</td>
      <td>84.03</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>81</td>
      <td>14.06</td>
    </tr>
    <tr>
      <th>Other</th>
      <td>11</td>
      <td>1.91</td>
    </tr>
  </tbody>
</table>
</div>



## Purchasing Analysis (Gender)

* Run basic calculations to obtain number of unique items, average price, etc.
* Create a summary data frame to hold the results
* Optional: give the displayed data cleaner formatting
* Display the summary data frame


** Purchasing Analysis (Gender)


```python
# Average Total Purchase Sum
FemaleAverageTotalPurchaseSum = len(Female1)
MaleAverageTotalPurchaseSum = len(Male1)
OtherAverageTotalPurchaseSum = len(Other1)

#Purchase Count
FemalePurchaseCount = len(Female1)
MalePurchaseCount = len(Male1)
OtherPurchaseCount = len(Other1)

#Total Purchase Value
FemaleTotalPurchase = round(Female1['Price'].sum(),2)
MaleTotalPurchase = round(Male1['Price'].sum(),2)
OtherTotalPurchase = round(Other1['Price'].sum(),2)

# Purchase Count
# Female / Male / Other
NormFemale = round((FemaleTotalPurchase/FemalePurchaseCount), 2)
NormMale = round((MaleTotalPurchase/MalePurchaseCount), 2)
NormOther = round((OtherTotalPurchase/OtherPurchaseCount), 2)

#Average Purchase Price
FemaleAvgPrice= round((Female1["Price"].sum())/len(Female1["Price"]),2)
MaleAvgPrice =round((Male1["Price"].sum())/len(Male1["Price"]),2)
OtherAvgPrice= round((Other1["Price"].sum())/len(Other1["Price"]),2)


# Avg Total Purchase Count Per Person
#FemaleAvgPrice= round((Female1["Price"].sum())/len(Female1["Price"]),2)
#MaleAvgPrice =round((Male1["Price"].sum())/len(Male1["Price"]),2)
#OtherAvgPrice= round((Other1["Price"].sum())/len(Other1["Price"]),2)


# Average Total Purchase Sum Per Person
FemaleAverageTotalPurchaseSum= round((total_revenue)/len(Male1["Price"]),2)
MaleAverageTotalPurchaseSum = round((total_revenue)/len(Male1["Price"]),2)
#OtherAverageTotalPurchaseSum= round((total_revenue)/len(Other1["Price"]),2)

# index by gender
ResultBySex = {"Purchase Count":[FemalePurchaseCount, MalePurchaseCount, OtherPurchaseCount],
                    "Gender":["Female","Male","Other / Non-Disclosed"],
                    "Average Purchase Price":[FemaleAvgPrice,MaleAvgPrice,OtherAvgPrice],
                    "Total Purchase Value":[FemaleTotalPurchase,MaleTotalPurchase,OtherTotalPurchase],
                    "Normalized Totals":[NormFemale,NormMale,NormOther],
#                    "Avg Total Purchase Per Person ":[FemaleAverageTotalPurchaseSum,MaleAverageTotalPurchaseSum,OtherAverageTotalPurchaseSum]}
ResultBySex1= pd.DataFrame(ResultBySex)
ResultBySex1= ResultBySex1.set_index('Gender')
ResultBySex1= ResultBySex1[['Purchase Count','Average Purchase Price','Total Purchase Value','Normalized Totals', 'Avg Total Purchase Per Person']]
ResultBySex1
```


      File "<ipython-input-23-5936ecb4b733>", line 46
        ResultBySex1= pd.DataFrame(ResultBySex)
                    ^
    SyntaxError: invalid syntax
    


## Age Demographics

* Establish bins for ages
* Categorize the existing players using the age bins. Hint: use pd.cut()
* Calculate the numbers and percentages by age group
* Create a summary data frame to hold the results
* Optional: round the percentage column to two decimal points
* Display Age Demographics Table


```python
#Age Demographics
MaxAge = data['Age'].max()
print(MaxAge)
```


```python
#Age Demographics
MinAge = data['Age'].min()
print(MinAge)
```

* Categorize the existing players using the age bins. Hint: use pd.cut()

pandas.cut(x, bins, right=True, labels=None, retbins=False, precision=3, include_lowest=False, duplicates='raise')


```python
#bins of 4 years (i.e. <10, 10-14, 15-19, etc.)
bins = [0,10,14,19,24,29,34,39,46]
Agelabels = ["<10","10-14","15-19","20-24","25-29","30-34","35-39","40+"]
data['Age Summary'] = pd.cut(data['Age'],bins,labels= Agelabels)
print(bins)
```


```python
data.columns
```


```python

```


```python

```


```python

```


```python

```


```python
#Purchase Count
Bin1 = data.groupby(['Age Summary']).get_group(('<10'))
pc1 = len(Bin1['SN'].unique())
PerBin1 = (pc1/total_count)*100

Bin2 = data.groupby(['Age Summary']).get_group(('10-14'))
pc2 = len(Bin2['SN'].unique())
PerBin2 = (pc2/total_count)*100

Bin3 = data.groupby(['Age Summary']).get_group(('15-19'))
pc3 = len(Bin3['SN'].unique())
PerBin3 = (pc3/total_count)*100

Bin4 = data.groupby(['Age Summary']).get_group(('20-24'))
pc4 = len(Bin4['SN'].unique())
PerBin4 = (pc4/total_count)*100

Bin5 = data.groupby(['Age Summary']).get_group(('25-29'))
pc5 = len(Bin5['SN'].unique())
PerBin5 = (pc5/total_count)*100

Bin6 = data.groupby(['Age Summary']).get_group(('30-34'))
pc6 = len(Bin6['SN'].unique())
PerBin6 = (pc6/total_count)*100

Bin7 = data.groupby(['Age Summary']).get_group(('35-39'))
pc7 = len(Bin7['SN'].unique())
PerBin7 = (pc7/total_count)*100

Bin8 = data.groupby(['Age Summary']).get_group(('40+'))
pc8 = len(Bin8['SN'].unique())
PerBin8 = (pc8/total_count)*100
```

* Calculate the numbers and percentages by age group


```python
PlayerBinsCount=[pc1,pc2,pc3,pc4,pc5,pc6,pc7,pc8]
PercentBins= [PerBin1,PerBin2,PerBin3,PerBin4,PerBin5,PerBin6,PerBin7,PerBin8]
PercentBins= [round(x,2) for x in PercentBins]
print(PlayerBinsCount)
```


```python
AgeDem = {"Age Summary":Agelabels,"Total Player Count":PlayerBinsCount,"Percentage Of Players":PercentBins}
AgeDem1 = pd.DataFrame(AgeDem)
AgeDem1 = AgeDem1.set_index('Age Summary')
AgeDem1
```

## Purchasing Analysis (Age)

* Bin the purchase_data data frame by age
* Run basic calculations to obtain purchase count, avg. purchase price, avg. purchase total per person etc. in the table below
* Create a summary data frame to hold the results
* Optional: give the displayed data cleaner formatting
* Display the summary data frame


```python
#Age Demographics
MaxAge = data['Age'].max()


#Age Demographics
MinAge = data['Age'].min()


#bins of 4 years (i.e. <10, 10-14, 15-19, etc.)
bins = [0,10,14,19,24,29,34,39,46]
Agelabels = ["<10","10-14","15-19","20-24","25-29","30-34","35-39","40+"]
data['Age Summary'] = pd.cut(data['Age'],bins,labels= Agelabels)


PlayerBinsCount=[pc1,pc2,pc3,pc4,pc5,pc6,pc7,pc8]
PercentBins= [PerBin1,PerBin2,PerBin3,PerBin4,PerBin5,PerBin6,PerBin7,PerBin8]
PercentBins= [round(x,2) for x in PercentBins]


#Purchase Count
Bin1 = data.groupby(['Age Summary']).get_group(('<10'))
pc1 = len(Bin1['SN'].unique())
PerBin1 = (pc1/total_count)*100

Bin2 = data.groupby(['Age Summary']).get_group(('10-14'))
pc2 = len(Bin2['SN'].unique())
PerBin2 = (pc2/total_count)*100

Bin3 = data.groupby(['Age Summary']).get_group(('15-19'))
pc3 = len(Bin3['SN'].unique())
PerBin3 = (pc3/total_count)*100

Bin4 = data.groupby(['Age Summary']).get_group(('20-24'))
pc4 = len(Bin4['SN'].unique())
PerBin4 = (pc4/total_count)*100

Bin5 = data.groupby(['Age Summary']).get_group(('25-29'))
pc5 = len(Bin5['SN'].unique())
PerBin5 = (pc5/total_count)*100

Bin6 = data.groupby(['Age Summary']).get_group(('30-34'))
pc6 = len(Bin6['SN'].unique())
PerBin6 = (pc6/total_count)*100

Bin7 = data.groupby(['Age Summary']).get_group(('35-39'))
pc7 = len(Bin7['SN'].unique())
PerBin7 = (pc7/total_count)*100

Bin8 = data.groupby(['Age Summary']).get_group(('40+'))
pc8 = len(Bin8['SN'].unique())
PerBin8 = (pc8/total_count)*100
```


```python
data.columns
```


```python
AgeDem = {"Age Summary":Agelabels,"Total Player Count":PlayerBinsCount,"Percentage Of Players":PercentBins}
AgeDem1 = pd.DataFrame(AgeDem)
AgeDem1 = AgeDem1.set_index('Age Summary')
AgeDem1
```


```python

```


```python

```

## Top Spenders

* Run basic calculations to obtain the results in the table below
* Create a summary data frame to hold the results
* Sort the total purchase value column in descending order
* Optional: give the displayed data cleaner formatting
* Display a preview of the summary data frame


```python
#SN
SN = data.groupby(data["SN"])
ScreenName = SN["SN"].unique()

#Purchase Count
SNCount = SN['Age'].count()

#Average Purchase Price
SNAverage = round(SN['Price'].mean(),2)

#Total Purchase Value
SNTotal = SN['Price'].sum()


TopSpend = {"SN":ScreenName,"Purchase Count":SNCount,
                 "Average Purchase Price":SNAverage,"Total Purchase Value":SNTotal}
TopSpend1= pd.DataFrame(TopSpend)
TopSpend1= TopSpend1.set_index('SN')
TopSpend1 = TopSpend1.sort_values("Total Purchase Value",ascending=False)
TopSpend1 = TopSpend1[['Purchase Count', 'Average Purchase Price', 'Total Purchase Value']]

TopSpend1.iloc[:5]
```

## Most Popular Items

* Retrieve the Item ID, Item Name, and Item Price columns

* Group by Item ID and Item Name. Perform calculations to obtain purchase count, item price, and total purchase value

* Create a summary data frame to hold the results

* Sort the purchase count column in descending order

* Optional: give the displayed data cleaner formatting

* Display a preview of the summary data frame


```python
#Item ID
ItemId = data.groupby(data['Item ID'])
Items = ItemId['Item ID'].unique()
#Item Name

ItemName = ItemId["Item Name"].unique()

#Purchase Count
ItemPurCount = ItemId['Age'].count()

#Item Price
ItemPrice= ItemId['Price'].unique()


#Total Purchase Value
ItemTotalPurchase = ItemId['Price'].sum()

ItemTable = {'Item ID':Items,'Item Name':ItemName,'Item Price':ItemPrice,'Item Count':ItemPurCount,'Total Purchase':ItemTotalPurchase}
ItemTable1 = pd.DataFrame(ItemTable)
ItemTable1 = ItemTable1.set_index('Item ID')
ItemTable1= ItemTable1.sort_values('Item Count', ascending=False)
ItemTable1 = ItemTable1[['Item Name','Item Count','Item Price','Total Purchase']]
ItemTable1.iloc[:5]
```

## Most Profitable Items

* Sort the above table by total purchase value in descending order
* Optional: give the displayed data cleaner formatting
* Display a preview of the data frame


```python
MostProfit= ItemTable1.sort_values('Total Purchase', ascending=False)
MostProfit[:5]
```


```python

```


```python

```


```python

```
