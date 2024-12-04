# Data-Mining-II-T3

#Market Basket Analysis: Task 3 - Customer Behavior Patterns in Market Basket Analysis

Part I: Research Question
A.  Describe the purpose of your data mining report by doing the following:
1.  Propose one question relevant to a real-world organizational situation that you will answer using market basket analysis.


What are the most frequently purchased items together?
This question is relevant because knowing which items are often bought together can help with keeping track of inventory and help boost  sales of certain items . 


2.  Define one goal of the data analysis. Ensure your goal is reasonable within the scope of the selected scenario and is represented in the available data.


One of the goals of this analysis is to identify combinations of items that are frequently purchased together. According to Chaudhary (n.d.), "Market basket analysis is a data mining technique that analyzes patterns of co-occurrence and determines the strength of the link between products purchased together. It is also referred to as frequent itemset mining or association analysis." Using market basket analysis, I aim to uncover patterns in customer purchasing behavior that can inform sales strategies. This goal is reasonable because the dataset contains enough items to detect patterns. 
Part II: Market Basket Justification
B.  Explain the reasons for using market basket analysis by doing the following: 
1.As Srishti Chaudhary explains, “This type of market basket analysis offers actionable insights based on historical data. It is a frequently used approach that does not make any predictions but rates the association using statistical techniques between the products.”This unsupervised learning method helps reveal patterns, enabling companies to take targeted action without relying on predefined outcomes.


2.  Provide one example of transactions in the data set.


By using example_transaction = df.iloc[1], I was able to extract and provide one example of a transaction from my dataset.
    
   **Let’s breakdown in depth on what the transaction shows**
There are 20 items which are the columns, and the rows are a transaction. Therefore, customer 1 had 20 items which is 1 row and 20 columns that we see here. At this point of the data cleaning, I could not use [0] because the entire row was empty. I will further elaborate how I handled this. 
I used the function, df_cleaned = df.iloc[1::2]  # Keep rows from index 1 and take every second row. Which made it possible to get rid of all the empty rows. 

I then had to convert the  dataset into a binary matrix format suitable for market basket analysis. 

I prepared the dataset for market basket analysis by converting each of the 7,501 transactions into a list representing the 20 items purchased. Using the TransactionEncoder from the mlxtend library, I transformed this list into a binary matrix where rows indicate transactions and columns represent products. 
 3.  Summarize one assumption of market basket analysis.
One key assumption in market basket analysis is that you do not need to worry about variables correlating in the same way as in linear regression. Instead, MBA focuses on patterns between variables based on how frequently they occur together in transactions. Tan, Steinbach, and Kumar (2006) state that “support counting is the process of determining the frequency of occurrence for every candidate itemset that survives the candidate pruning step of the apriori-gen function” (p. 341). However, including unrelated variables can reduce the focus on patterns in the variables we want to analyze. This happens due to the volume of transactions MBA considers when detecting frequencies. Tan, Steinbach, and Kumar (2006) further explain that “for applications such as document analysis or market basket analysis, the measure is expected to remain invariant under the null addition operation. Otherwise, the relationship between words may disappear simply by adding enough documents that do not contain both words” (p. 380).
    
 Part III: Data Preparation and Analysis
C.  Prepare and perform market basket analysis by doing the following:
1.  Transform the data set to make it suitable for market basket analysis. Include a copy of the cleaned data set.
cleaned_df.to_csv('df_cleanmba1.csv',index=False)
Clean_data 


2.  Execute the code used to generate association rules with the Apriori algorithm. Provide screenshots that demonstrate that the code is error free.


I executed the Apriori algorithm to generate frequent itemsets from the dataset using the following code. The frequent itemsets were filtered with a minimum support threshold of 0.02, and I included screenshots to confirm that the code executed successfully without any errors.
#frequent item set 
frequent_itemsets = apriori(df, min_support=0.02, use_colnames=True).round(3)

 frequent_itemsets.head(5)
To generate association rules from the frequent itemsets obtained using the Apriori algorithm, I used the association_rules function with a lift metric and a minimum threshold of 1. Keep in mind that anything above 1 is a positive association which is why I set the min to 1.  This approach allowed me to identify significant relationships between products based on their co-occurrence in transactions. The resulting rul_table contains the first 20 association rules, showcasing the strength of the associations as measured by lift.


rul_table = association_rules(frequent_itemsets, metric='lift', min_threshold=1)
rul_table.head(20)
3.  Provide values for the support, lift, and confidence of the association rules table.


Since I provided the screenshots in the previous question, I will include this table of a few variables from the rul_table.
4.  Explain the top three relevant rules generated by the Apriori algorithm. Include a screenshot of the top three relevant rules.
            To better understand the results, it's important to define key concepts from Market Basket Analysis (MBA). As summarized from Kharwal (2023), antecedents are the starting point or "if" part of the association rule, representing items that initiate the rule. Consequents, on the other hand, are the items likely to be associated with the antecedents or the "then" part of the rule.


            Top Three Relevant Rules Based on Confidence:
Rule 1: (10ft iPhone Charger Cable 2 Pack) → (Dust-Off Compressed Gas 2 pack)
Confidence: 45.10%
This rule indicates that when customers purchase the 10ft iPhone Charger Cable 2 Pack, there is a 45.10% chance they will also buy the Dust-Off Compressed Gas 2 pack. This suggests a moderately strong association between these two products.
Rule 2: (FEIYOLD Blue light Blocking Glasses) → (Dust-Off Compressed Gas 2 pack)
Confidence: 42.42%
Customers buying the FEIYOLD Blue Light Blocking Glasses are likely to purchase the Dust-Off Compressed Gas 2 pack 42.42% of the time. This implies a noteworthy relationship that could inform marketing strategies.
Rule 3: (SanDisk Ultra 64GB Card) → (Dust-Off Compressed Gas 2 pack)
Confidence: 41.84%
There is a 41.84% chance that customers who buy the SanDisk Ultra 64GB card will also buy the Dust-Off Compressed Gas 2 pack, indicating a meaningful link in purchasing behavior.
Top Three Relevant Rules Based on Lift:
Rule 1: (SanDisk Ultra 64GB Card) → (VIVO Dual LCD Monitor Desk Mount)
Lift: 2.29
This rule has a lift of 2.29, meaning customers who buy the SanDisk Ultra 64GB card are 2.29 times more likely to buy the VIVO Dual LCD Monitor Desk Mount than expected if the purchases were independent. 
Rule 2: (VIVO Dual LCD Monitor Desk Mount) → (SanDisk Ultra 64GB Card)
Lift: 2.29
This indicates  that customers purchasing the VIVO Dual LCD Monitor Desk Mount are more likely to buy the SanDisk Ultra 64GB card.
Rule 3: (FEIYOLD Blue Light Blocking Glasses) → (VIVO Dual LCD Monitor Desk Mount)
Lift: 2.00
A lift of 2.00 shows that customers who  buy the FEIYOLD Blue Light Blocking Glasses are 2 times more likely to buy  the VIVO Dual LCD Monitor Desk Mount. 
Top Three Relevant Rules Based on Support:
Rule 1: (Dust-Off Compressed Gas 2 pack) → (VIVO Dual LCD Monitor Desk Mount)
Support: 6.00%
This indicates that 6.00% of all transactions include both the Dust-Off Compressed Gas 2 pack and the VIVO Dual LCD Monitor Desk Mount. This means that this is a frequent purchase combination.
Rule 2: (VIVO Dual LCD Monitor Desk Mount) → (Dust-Off Compressed Gas 2 pack)
Support: 6.00%
The support is the same as the first rule, showing that these two items are often bought together.
Rule 3: (HP 61 Ink) → (Dust-Off Compressed Gas 2 pack)
Support: 5.30%
This indicates that 5.30% of transactions involve both the HP 61 ink and the Dust-Off Compressed Gas 2 pack, suggesting it’s another common purchase combination.


Part IV: Data Summary and Implications
D.  Summarize your data analysis by doing the following:
1.  Summarize the significance of support, lift, and confidence from the results of the analysis.




Support measures how frequently a combination of antecedents and consequent appears in the dataset, indicating how often certain items (or variables) occur together. Confidence quantifies the probability of a consequent occurring given the antecedent, showing the likelihood of the relationship between the two. Lastly, lift measures the strength of the association between antecedents and consequents, with a value greater than 1 indicating a positive correlation (Kharwal, 2023).


In the figure below, I created two pie charts, one is the support percentages of the top 3 rules and another pie chart showing the top 3 rules for confidence. 


2.  Discuss the practical significance of your findings from the analysis.


The market basket analysis shows  the importance of identifying patterns of purchases. This can significantly   improve inventory management and organizing  popular item combinations on the shelves. 


The analysis identified a significant association between the "10ft iPhone Charger Cable 2 Pack" and "Dust-Off Compressed Gas 2 Pack," which has a support of 0.023 and a confidence of 0.450980, indicating that approximately 45% of customers who buy the charger also purchase the Dust-Off. The lift value being over 1 signifies a strong association between these items. Additionally, the "SanDisk Ultra 64GB Card" has a higher support of 0.041 when purchased alongside the Dust-Off, further indicating its complementary nature. These insights can inform strategic decisions to enhance sales.


3.  Recommend a course of action for the real-world organizational situation from part A1 based on the results from part D1.


 Based on the market basket analysis, I recommend offering discounts on items that may not be as popular such as “10ft iPHone Charger Cable 2 Pack” but are frequently purchased alongside more popular products. Additionally, placing these frequently purchased items together in-store or on the website can enhance customer convenience and encourage higher sales. Providing incentives for customers to maintain multiple services can also encourage continued streaming subscriptions while helping to keep overall monthly costs lower.




GeeksforGeeks. (2022, February 22). How to make a table in Python? Retrieved from https://www.geeksforgeeks.org/how-to-make-a-table-in-python/
Medium. (n.d.). Market Basket Analysis. Retrieved from https://medium.com/@rifatalkausar/market-basket-analysis-using-mlxtend-library-in-python-7e56bd41a56
Raschka, S. (n.d.). Association rules generation from frequent itemsets using association_rules in mlxtend. Retrieved from https://rasbt.github.io/mlxtend/user_guide/frequent_patterns/association_rules/

Chaudhary, S. (n.d.). Market Basket Analysis: Anticipating Customer Behavior. Turing. Retrieved from https://www.turing.com/kb/market-basket-analysis
Kamara, K.(n.d) Market Basket Analysis. D212,Western Governors University, 2024. Lecture.
Kharwal, A. (2023, October 16). Market Basket Analysis using Python. The Clever Programmer. Retrieved from https://thecleverprogrammer.com/2023/10/16/market-basket-analysis-using-python/#google_vignette
Tan, P.-N., Steinbach, M., & Kumar, V. (n.d.). Introduction to Data Mining. CEOM. Retrieved from https://www.ceom.ou.edu/media/docs/upload/Pang-Ning_Tan_Michael_Steinbach_Vipin_Kumar_-_Introduction_to_Data_Mining-Pe_NRDK4fi.pdf






