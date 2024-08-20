# Large-Scale-Basket-Analysis
This is a consulting project I worked on for a parts distrbutor. I was tasked with performing basket analysis on a years worth of records from one of their distribution sites so they could redesign their storage systems to group items that were commonly purchased and shipped together. For confidentiality reasons, the datasets they provided me and the further analysis I performed pertaining to the location of these items was removed from the notebook. However, this code shows how to perform basket analysis on datasets with millions of records.

The transaction history I recieved from the company contained over 200,000 items and over 2.8 million transactions - therefore, performing the BA calculations in a standard tabular format would be too computationally intensive. In fact, when I tried this with even a tenth of the data, my python kernel died within 45 seconds. Therefore, I converted the data into a sparse matrix, as a vast majority of the products have no relationship with each other, which means that a majority of the values in your data will be 0 and don't need to be stored. 

When the baskets are finally generaated, you will find a vast majority of them to be redundant. This is because for every large basket, the Apriori algorithm also identifies every single permutations of smaller baskets composed of the same items. So if a basket has 8 items, it also identifies every possible basket with 7 of those items, and 6, and 5 and so on, also with every possible variation of which of those items are antecedents and which are consequents. To solve this, I created sets of all the largest unique baskets and then pruned all the smaller sets who were contained in the larger ones. This made my final dataframe go down from 3 million identified baskets to around 17,000 unique baskets. This is a crucial step, as otherwise 99% of your resulting data will be redudant, especially with datasets as large as these. 
