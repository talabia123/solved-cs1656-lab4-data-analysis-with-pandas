Download Link: https://assignmentchef.com/product/solved-cs1656-lab4-data-analysis-with-pandas
<br>
<h1></h1>

So far we have encountered basic data manipulation with pandas Dataframes including row and column selection, boolean indexing, working with missing values, groupby and aggregate functions such as mean().But there are many other powerful data manipulation and analysis techniques available in pandas. In this lab, we will learn some more advanced ways for data anylsis in Python using Dataframes.

Begin by importing pandas package.

In [1]: import pandas as pd

Next load the dataset that we will be playing arround with.

In [2]: df = pd.read_csv(‘http://data.cs1656.org/coffee-chain.csv’) df.head()

Out[2]:     Area Code Market        Market Size        Product Product Line  0                985 South Small Market Colombian          Beans 1 985 South Small Market Chamomile            Leaves

2 985 South Small Market Chamomile Leaves 3 985 South Small Market Decaf Irish Cream Beans

4                          985 South Small Market                                         Lemon                 Leaves

Product Type                  State                         Type Inventory Budget COGS Budget Margin 

<table width="549">

 <tbody>

  <tr>

   <td width="316">0                          Coffee Louisiana Regular</td>

   <td width="105">845</td>

   <td width="105">50</td>

   <td width="23">90</td>

  </tr>

  <tr>

   <td width="316">1 Herbal Tea Louisiana                            Decaf</td>

   <td width="105">540</td>

   <td width="105">80</td>

   <td width="23">110</td>

  </tr>

  <tr>

   <td width="316">2 Herbal Tea Louisiana                            Decaf</td>

   <td width="105">552</td>

   <td width="105">90</td>

   <td width="23">120</td>

  </tr>

  <tr>

   <td width="316">3                       Coffee Louisiana                Decaf</td>

   <td width="105">851</td>

   <td width="105">70</td>

   <td width="23">90</td>

  </tr>

  <tr>

   <td width="316">4 Herbal Tea Louisiana                            Decaf</td>

   <td width="105">599</td>

   <td width="105">60</td>

   <td width="23">80</td>

  </tr>

 </tbody>

</table>

Budget Profit Budget Sales COGS Margin Marketing Profit Sales 

<table width="526">

 <tbody>

  <tr>

   <td width="203">0                                 70</td>

   <td width="105">140          49</td>

   <td width="90">71</td>

   <td width="53">13</td>

   <td width="53">68</td>

   <td width="23">128</td>

  </tr>

  <tr>

   <td width="203">1                                 70</td>

   <td width="105">190          94</td>

   <td width="90">120</td>

   <td width="53">31</td>

   <td width="53">114</td>

   <td width="23">228</td>

  </tr>

  <tr>

   <td width="203">2                                 80</td>

   <td width="105">210 101</td>

   <td width="90">130</td>

   <td width="53">33</td>

   <td width="53">126</td>

   <td width="23">246</td>

  </tr>

  <tr>

   <td width="203">3                                 80</td>

   <td width="105">160          48</td>

   <td width="90">70</td>

   <td width="53">13</td>

   <td width="53">67</td>

   <td width="23">126</td>

  </tr>

  <tr>

   <td width="203">4                                 30</td>

   <td width="105">140          67</td>

   <td width="90">83</td>

   <td width="53">25</td>

   <td width="53">37</td>

   <td width="23">160</td>

  </tr>

 </tbody>

</table>

Total Expenses

<ul>

 <li>25</li>

 <li>43</li>

 <li>45</li>

 <li>25</li>

 <li>58</li>

</ul>

Let’s get the subset of the dataframe we need.

In [3]: df_small = df[[‘Area Code’,’Market’, ‘Market Size’, ‘Product’, ‘Product Line’, ‘Product df_small.head()

Out[3]:     Area Code Market        Market Size        Product Product Line  0                985 South Small Market Colombian          Beans 1 985 South Small Market Chamomile            Leaves

2          985 South Small Market Chamomile         Leaves 3               985 South Small Market Decaf Irish Cream         Beans

4                          985 South Small Market                                         Lemon                 Leaves

Product Type                  State                      Type Profit Total Expenses

<table width="436">

 <tbody>

  <tr>

   <td width="293">0                          Coffee Louisiana Regular</td>

   <td width="128">68</td>

   <td width="15">25</td>

  </tr>

  <tr>

   <td width="293">1 Herbal Tea Louisiana                            Decaf</td>

   <td width="128">114</td>

   <td width="15">43</td>

  </tr>

  <tr>

   <td width="293">2 Herbal Tea Louisiana                            Decaf</td>

   <td width="128">126</td>

   <td width="15">45</td>

  </tr>

  <tr>

   <td width="293">3                       Coffee Louisiana                Decaf</td>

   <td width="128">67</td>

   <td width="15">25</td>

  </tr>

  <tr>

   <td width="293">4 Herbal Tea Louisiana                            Decaf</td>

   <td width="128">37</td>

   <td width="15">58</td>

  </tr>

 </tbody>

</table>

<h1>1.3       Slicing &amp; Indexing</h1>

What we saw above was slicing. Slicing uses the [] operator selects a set of rows and/or columns from a DataFrame. <strong>Slicing rows</strong>

To slice out a set of rows, you use the following syntax: data[start:stop]. When slicing in pandas the start bound is included in the output.

In [4]: df_small[0:3]

Out[4]:                Area Code Market           Market Size                     Product Product Line Product Type 

<table width="526">

 <tbody>

  <tr>

   <td width="383">0                             985 South Small Market Colombian</td>

   <td width="143">Beans                      Coffee</td>

  </tr>

  <tr>

   <td width="383">1                            985 South Small Market Chamomile</td>

   <td width="143">Leaves Herbal Tea</td>

  </tr>

  <tr>

   <td width="383">2                            985 South Small Market ChamomileState                      Type Profit Total Expenses0 Louisiana Regular 68 25 1 Louisiana Decaf 114 432 Louisiana                  Decaf             126                                   45</td>

   <td width="143">Leaves Herbal Tea</td>

  </tr>

 </tbody>

</table>

<h2>Slicing vs Copying</h2>

We might have thought that we were creating a fresh copy of df_small when we did slicing. However the statement y = x doesn’t create a copy of our DataFrame. It creates a new variable y that refers to the same object x refers to. This means that there is only one object (the DataFrame), and both x and y refer to it. To create a fresh copy of the DataFrame you can use the syntax y=x.copy(). We will see the effect of slicing but not copying in later steps.

** Indexing **

We can select specific ranges of our data in both the row and column directions using either label or integer-based indexing.

<ul>

 <li>loc: indexing via labels or integers or mixed</li>

 <li>iloc: indexing via integers only</li>

</ul>

To select a subset of rows AND columns from our DataFrame, we can use the iloc method. For example,

In [5]: df_small.loc[0:3, ‘Market’: ‘Product’]

Out[5]: Market Market Size Product 0 South Small Market Colombian

<ul>

 <li>South Small Market Chamomile</li>

 <li>South Small Market Chamomile</li>

 <li>South Small Market Decaf Irish Cream In [6]: df_small.iloc[0:4, 1:4]</li>

</ul>

Out[6]: Market Market Size Product 0 South Small Market Colombian

<ul>

 <li>South Small Market Chamomile</li>

 <li>South Small Market Chamomile 3 South Small Market Decaf Irish Cream</li>

</ul>

Notice that indexing in loc is inclusive whereas indexing in iloc is exlusive of the end index

<h1>1.4      Statistical Technqiues</h1>

<h2>1.4.1      Cross-tabulation</h2>

Cross tabultaion computes a frequency table of two or more factors. Let’s start by making a crosstab with two variables first.

In [7]: df_crosstab = pd.crosstab(df_small[“Market”],df_small[“Market Size”],margins=True) df_crosstab

Out[7]: Market Size Major Market Small Market All

Market

Central 696 648 1344 East 552 336 888 South 168 504 672 West 288 1056 1344

All                                              1704                            2544 4248

Let’c check the type of the cross-tab

In [8]: type(df_crosstab)

Out[8]: pandas.core.frame.DataFrame

Now let’s check the value counts of one of our cross-tab’s dimensions and see if the totals match?

In [9]: pd.value_counts(df_small[‘Market Size’])

Out[9]: Small Market      2544 Major Market             1704

Name: Market Size, dtype: int64

Now let’s make a cross-tab with three variables.

In [10]: pd.crosstab(df[“Product Type”], [df[“Market”],df[“Market Size”]],margins=True)

Out[10]: Market                                     Central                                                          East                                                        South 

Market Size Major Market Small Market Major Market Small Market Major Market Product Type

<table width="579">

 <tbody>

  <tr>

   <td width="458">Coffee                                          192                         192                            96</td>

   <td width="98">72</td>

   <td width="23">48</td>

  </tr>

  <tr>

   <td width="458">Espresso                                      144                         144                          144</td>

   <td width="98">96</td>

   <td width="23">72</td>

  </tr>

  <tr>

   <td width="458">Herbal Tea                                  192                         144                          144</td>

   <td width="98">72</td>

   <td width="23">48</td>

  </tr>

  <tr>

   <td width="458">Tea                                                168                         168                          168</td>

   <td width="98">96</td>

   <td width="23">0</td>

  </tr>

  <tr>

   <td width="458">All                                                  696                         648                          552Market                                                                       West                                         AllMarket Size Small Market Major Market Small MarketProduct TypeCoffee 144 72 240 1056 Espresso 216 72 288 1176 Herbal Tea 144 72 240 1056Tea                                                     0                            72                             288 960All                                                  504                         288                         1056 4248</td>

   <td width="98">336</td>

   <td width="23">168</td>

  </tr>

 </tbody>

</table>

<h2>1.4.2       Binning Data</h2>

We can bin our data into categorirs by specifying bin widths. Let’s define equal width bins as shown below. The bins array specifies 4 bins from -800 to -400, -400 to 0, 0 to 400, 400 to 800. We will also specify a group names to assign as labels to each of our bins later.

In [11]: bins = [-800,-400, 0, 400, 800] group_names = [‘Low’, ‘Okay’, ‘Good’, ‘Great’]

Now lets bin the data into the categories and add it as a column to the dataframe

In [12]: df_small[‘Categories’] = pd.cut(df_small[‘Profit’], bins=bins, labels=group_names) df_small.head(20)

Out[12]:      Area Code Market Market Size             Product Product Line  0                985 South Small Market               Colombian          Beans 1 985 South Small Market Chamomile          Leaves

2       985 South Small Market Chamomile         Leaves 3               985 South Small Market Decaf Irish Cream      Beans 4 985 South Small Market Lemon  Leaves

<ul>

 <li>985 South Small Market Decaf Irish Cream Beans</li>

 <li>985 South Small Market Lemon Leaves 7               985 South Small Market Chamomile          Leaves</li>

 <li>985 South Small Market Caffe Mocha Beans</li>

 <li>985 South Small Market Caffe Latte Beans 10 985 South Small Market Caffe Latte Beans 11 985 South Small Market Decaf Irish Cream Beans 12 985 South Small Market Decaf Espresso Beans 13 985 South Small Market Lemon Leaves</li>

</ul>

14 985 South Small Market Decaf Espresso Beans 15 985 South Small Market Lemon Leaves 16 985 South Small Market Caffe Mocha Beans

<ul>

 <li>985 South Small Market Caffe Latte Beans</li>

 <li>985 South Small Market Caffe Mocha Beans</li>

 <li>985 South Small Market Decaf Espresso Beans</li>

</ul>

Product Type                  State                         Type Profit Total Expenses Categories

<table width="526">

 <tbody>

  <tr>

   <td width="301">0                            Coffee Louisiana Regular</td>

   <td width="128">68</td>

   <td width="68">25</td>

   <td width="30">Good</td>

  </tr>

  <tr>

   <td width="301">1                Herbal Tea Louisiana                Decaf</td>

   <td width="128">114</td>

   <td width="68">43</td>

   <td width="30">Good</td>

  </tr>

  <tr>

   <td width="301">2                Herbal Tea Louisiana                Decaf</td>

   <td width="128">126</td>

   <td width="68">45</td>

   <td width="30">Good</td>

  </tr>

  <tr>

   <td width="301">3                         Coffee Louisiana               Decaf</td>

   <td width="128">67</td>

   <td width="68">25</td>

   <td width="30">Good</td>

  </tr>

  <tr>

   <td width="301">4                Herbal Tea Louisiana                Decaf</td>

   <td width="128">37</td>

   <td width="68">58</td>

   <td width="30">Good</td>

  </tr>

  <tr>

   <td width="301">5                         Coffee Louisiana               Decaf</td>

   <td width="128">87</td>

   <td width="68">26</td>

   <td width="30">Good</td>

  </tr>

  <tr>

   <td width="301">6                Herbal Tea Louisiana                Decaf</td>

   <td width="128">43</td>

   <td width="68">58</td>

   <td width="30">Good</td>

  </tr>

  <tr>

   <td width="301">7                Herbal Tea Louisiana                Decaf</td>

   <td width="128">48</td>

   <td width="68">26</td>

   <td width="30">Good</td>

  </tr>

  <tr>

   <td width="301">8                        Espresso Louisiana Regular</td>

   <td width="128">61</td>

   <td width="68">35</td>

   <td width="30">Good</td>

  </tr>

  <tr>

   <td width="301">9                        Espresso Louisiana Regular</td>

   <td width="128">4</td>

   <td width="68">81</td>

   <td width="30">Good</td>

  </tr>

  <tr>

   <td width="301">10                     Espresso Louisiana Regular</td>

   <td width="128">1</td>

   <td width="68">86</td>

   <td width="30">Good</td>

  </tr>

  <tr>

   <td width="301">11                       Coffee Louisiana               Decaf</td>

   <td width="128">70</td>

   <td width="68">25</td>

   <td width="30">Good</td>

  </tr>

  <tr>

   <td width="301">12                  Espresso Louisiana                Decaf</td>

   <td width="128">56</td>

   <td width="68">39</td>

   <td width="30">Good</td>

  </tr>

  <tr>

   <td width="301">13 Herbal Tea Louisiana                            Decaf</td>

   <td width="128">62</td>

   <td width="68">65</td>

   <td width="30">Good</td>

  </tr>

  <tr>

   <td width="301">14                  Espresso Louisiana                Decaf</td>

   <td width="128">61</td>

   <td width="68">40</td>

   <td width="30">Good</td>

  </tr>

  <tr>

   <td width="301">15 Herbal Tea Louisiana                            Decaf</td>

   <td width="128">26</td>

   <td width="68">59</td>

   <td width="30">Good</td>

  </tr>

  <tr>

   <td width="301">16                     Espresso Louisiana Regular</td>

   <td width="128">31</td>

   <td width="68">35</td>

   <td width="30">Good</td>

  </tr>

  <tr>

   <td width="301">17                     Espresso Louisiana Regular</td>

   <td width="128">-3</td>

   <td width="68">79</td>

   <td width="30">Okay</td>

  </tr>

  <tr>

   <td width="301">18                     Espresso Louisiana Regular</td>

   <td width="128">58</td>

   <td width="68">41</td>

   <td width="30">Good</td>

  </tr>

  <tr>

   <td width="301">19                  Espresso Louisiana                Decaf</td>

   <td width="128">31</td>

   <td width="68">36</td>

   <td width="30">Good</td>

  </tr>

 </tbody>

</table>

To find out the value counts for each bin of category, we can use value_counts like we did earlier.

In [13]: pd.value_counts(df_small[‘Categories’])

Out[13]: Good                 3648

Okay               544

Great                40

Low                    16

Name: Categories, dtype: int64

<h2>1.4.3      Quantiles</h2>

Pandas allows an easy way of computing percentiles or quartiles. Let’s first specify the quantiles we want to calculate,

In [14]: quants = [0.0, 0.05, 0.25, 0.5, 0.75, 0.95, 1.0]

To compute the quantiles of Profit and Total Expenses,

In [15]: q = df_small[[‘Profit’,’Total Expenses’]].quantile(quants) q

Out[15]:                           Profit Total Expenses

<table width="210">

 <tbody>

  <tr>

   <td width="173">0.00 -638.0</td>

   <td width="38">10.0</td>

  </tr>

  <tr>

   <td width="173">0.05 -13.0</td>

   <td width="38">17.0</td>

  </tr>

  <tr>

   <td width="173">0.25            17.0</td>

   <td width="38">33.0</td>

  </tr>

  <tr>

   <td width="173">0.50            40.0</td>

   <td width="38">46.0</td>

  </tr>

  <tr>

   <td width="173">0.75            92.0</td>

   <td width="38">65.0</td>

  </tr>

  <tr>

   <td width="173">0.95 232.0</td>

   <td width="38">125.0</td>

  </tr>

  <tr>

   <td width="173">1.00 778.0</td>

   <td width="38">190.0</td>

  </tr>

 </tbody>

</table>

<h2>1.4.4        Groupby &amp; Apply</h2>

Groupby allows grouping or clustering the dataframe by a particular categorical attribute. Apply can be used to apply a function to a group or the entire dataframe. Let’s first define the function that we want to apply,

In [16]: def get_stats(group): return {‘min’: group.min(), ‘max’: group.max(), ‘count’: group.count(), ‘mean’: gro

This can be applied to a Dataframe or a grouping of the dataframe as shown below

In [17]: df_group = df_small[‘Profit’].groupby(df_small[‘Categories’]).apply(get_stats) df_group

<table width="323">

 <tbody>

  <tr>

   <td width="158">Out[17]: Categories</td>

   <td width="60"> </td>

   <td width="105"> </td>

  </tr>

  <tr>

   <td width="158">Low</td>

   <td width="60">count</td>

   <td width="105">16.000000</td>

  </tr>

  <tr>

   <td width="158"> </td>

   <td width="60">max</td>

   <td width="105">-404.000000</td>

  </tr>

  <tr>

   <td width="158"> </td>

   <td width="60">mean</td>

   <td width="105">-510.562500</td>

  </tr>

  <tr>

   <td width="158"> </td>

   <td width="60">min</td>

   <td width="105">-638.000000</td>

  </tr>

  <tr>

   <td width="158"> </td>

   <td width="60">sum</td>

   <td width="105">-8169.000000</td>

  </tr>

  <tr>

   <td width="158">Okay</td>

   <td width="60">count</td>

   <td width="105">544.000000</td>

  </tr>

  <tr>

   <td width="158"> </td>

   <td width="60">max</td>

   <td width="105">0.000000</td>

  </tr>

  <tr>

   <td width="158"> </td>

   <td width="60">mean</td>

   <td width="105">-45.630515</td>

  </tr>

  <tr>

   <td width="158"> </td>

   <td width="60">min</td>

   <td width="105">-392.000000</td>

  </tr>

  <tr>

   <td width="158"> </td>

   <td width="60">sum</td>

   <td width="105">-24823.000000</td>

  </tr>

  <tr>

   <td width="158">Good</td>

   <td width="60">count</td>

   <td width="105">3648.000000</td>

  </tr>

  <tr>

   <td width="158"> </td>

   <td width="60">max</td>

   <td width="105">397.000000</td>

  </tr>

  <tr>

   <td width="158"> </td>

   <td width="60">mean</td>

   <td width="105">74.514529</td>

  </tr>

  <tr>

   <td width="158"> </td>

   <td width="60">min</td>

   <td width="105">1.000000</td>

  </tr>

 </tbody>

</table>

sum                271829.000000

Great count 40.000000 max 778.000000 mean 517.650000 min 402.000000 sum 20706.000000

Name: Profit, dtype: float64

The width format of the output above can be fixed by using the unstack() function as shown below.

In [18]: df_group.unstack()

Out[18]:                                       count          max                   mean         min                 sum

Categories

Low 16.0 -404.0 -510.562500 -638.0 -8169.0 Okay      544.0     0.0 -45.630515 -392.0 -24823.0 Good       3648.0 397.0 74.514529         1.0 271829.0

Great                                40.0 778.0 517.650000 402.0                 20706.0

<h2>1.4.5      Sorting</h2>

Pandas allows nested sorting over mutliple columns of the Dataframe easily as shown below.

In [19]: data_sorted = df_small.sort_values([‘Total Expenses’, ‘Profit’], ascending=False) data_sorted[[‘Total Expenses’,’Profit’]].head(20)

Out[19]:                           Total Expenses Profit

<table width="210">

 <tbody>

  <tr>

   <td width="45">959</td>

   <td width="135">190</td>

   <td width="30">49</td>

  </tr>

  <tr>

   <td width="45">2334</td>

   <td width="135">189</td>

   <td width="30">50</td>

  </tr>

  <tr>

   <td width="45">2352</td>

   <td width="135">189</td>

   <td width="30">-284</td>

  </tr>

  <tr>

   <td width="45">3432</td>

   <td width="135">181</td>

   <td width="30">-266</td>

  </tr>

  <tr>

   <td width="45">966</td>

   <td width="135">180</td>

   <td width="30">45</td>

  </tr>

  <tr>

   <td width="45">2224</td>

   <td width="135">180</td>

   <td width="30">45</td>

  </tr>

  <tr>

   <td width="45">632</td>

   <td width="135">178</td>

   <td width="30">370</td>

  </tr>

  <tr>

   <td width="45">1429</td>

   <td width="135">178</td>

   <td width="30">370</td>

  </tr>

  <tr>

   <td width="45">631</td>

   <td width="135">178</td>

   <td width="30">368</td>

  </tr>

  <tr>

   <td width="45">1605</td>

   <td width="135">178</td>

   <td width="30">368</td>

  </tr>

  <tr>

   <td width="45">753</td>

   <td width="135">177</td>

   <td width="30">357</td>

  </tr>

  <tr>

   <td width="45">1622</td>

   <td width="135">177</td>

   <td width="30">357</td>

  </tr>

  <tr>

   <td width="45">1454</td>

   <td width="135">177</td>

   <td width="30">68</td>

  </tr>

  <tr>

   <td width="45">285</td>

   <td width="135">176</td>

   <td width="30">69</td>

  </tr>

  <tr>

   <td width="45">4086</td>

   <td width="135">176</td>

   <td width="30">-392</td>

  </tr>

  <tr>

   <td width="45">3420</td>

   <td width="135">168</td>

   <td width="30">-367</td>

  </tr>

  <tr>

   <td width="45">1461</td>

   <td width="135">167</td>

   <td width="30">62</td>

  </tr>

  <tr>

   <td width="45">3278</td>

   <td width="135">167</td>

   <td width="30">62</td>

  </tr>

  <tr>

   <td width="45">1269</td>

   <td width="135">166</td>

   <td width="30">511</td>

  </tr>

  <tr>

   <td width="45">1596</td>

   <td width="135">166</td>

   <td width="30">511</td>

  </tr>

 </tbody>

</table>

<h1>1.5     Tasks</h1>

For your tasks, use the data file http://data.cs1656.org/bank-data.csv.

<strong>Task 1 </strong>Compute the mean income of males versus females.

<strong>Task 2 </strong>Create a cross-tab of save_acct and mortgage.

<strong>Task 3 </strong>Convert the frequencies in cross-tab to percentages. (Hint: use apply and indexing)