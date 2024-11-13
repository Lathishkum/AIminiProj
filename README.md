# Ex.No: 13 Learning – Use Supervised Learning  
### DATE: 24.10.24                                                                           
### REGISTER NUMBER : 212221040087
### AIM: 
To write a program to train the classifier for Comparative Insights for Mutual Fund 
Choices Using ML.
###  Algorithm:
1.Load Data: Load the dataset containing mutual fund details.
2.Filter Selected Fund: If one fund is selected, compare it with two randomly chosen funds from the same category.
3.Compare Two Funds: If two funds are selected, compare them directly.
4.Calculate Best Fund: Determine the best fund based on 1-year returns.
5.Visualize Comparison: Display a bar plot for visual comparison of the selected funds.

### Program: 
# Function to compare selected fund(s) 
def compare_funds(fund_names): 
if len(fund_names) == 1: 
selected_fund_name = fund_names[0] 

# Filter the dataset for the selected fund 
selected_fund_data = data[data['scheme_name'] == 
selected_fund_name] 

# Check if the selected fund exists 
if selected_fund_data.empty: 
print("Selected fund not found.") 
return 

# Get the category of the selected fund 
fund_category = selected_fund_data['category'].values[0] 
# Get a list of other funds in the same category excluding the 
selected one 
other_funds = data[(data['category'] == fund_category) & 
(data['scheme_name'] != selected_fund_name)] 
# Randomly select two other funds 
if len(other_funds) < 2: 
print("Not enough funds in the category to compare.") 
return random_funds = other_funds.sample(n=2, 
random_state=42) 
funds_to_compare = pd.concat([selected_fund_data, 
random_funds]) 
elif len(fund_names) == 2: 
# If two fund names are provided, compare those directly 
fund_data = [] 
for fund_name in fund_names: 
fund_data_single = data[data['scheme_name'] == fund_name] 
if fund_data_single.empty: 
print(f"Fund '{fund_name}' not found.") 
return 
fund_data.append(fund_data_single) 
funds_to_compare = pd.concat(fund_data) 
else: 
print("Please provide either one or two fund names.") 
return DataFrame 
comparison = funds_to_compare[['scheme_name', 'returns_1yr', 
'sd', 'sortino', 'expense_ratio']] 
# Identify the best fund based on 1-year returns 
best_fund = comparison.loc[comparison['returns_1yr'].idxmax()] 
# Print the best fund details 
print("\nBest Fund Based on 1-Year Returns:") 
print(best_fund) 
# Visualization 
plt.figure(figsize=(12, 6)) 
sns.barplot(data=comparison, x='scheme_name', y='returns_1yr', 
color='blue', alpha=0.6) 
plt.axhline(y=best_fund['returns_1yr'], color='red', linestyle='--', 
label='Best Fund') 
plt.title('Comparison of Selected Fund(s) with Other Funds') 
plt.xlabel('Fund Name') 
plt.ylabel('1-Year Returns') 
plt.xticks(rotation=45) 
plt.legend() 
plt.show()

# Get user input for the selected fund(s) 
user_input = input("Enter the scheme names of the selected funds 
(comma separated): ") 
fund_names = [name.strip() for name in user_input.split(',')] 

# Call the comparison function 
compare_funds(fund_names)

### Output:
![aiproj](https://github.com/user-attachments/assets/33d1a432-9d73-4c96-bbef-f33b50d25f26)

### Result:
Thus the system was trained successfully and the prediction was carried out.
