# E2E COURIER CHARGES ACCURACY ANALYSIS WITH PYTHON
<div align="center">
  <img src="Young Woman Pay Delivery Charges.png" alt="My Project Logo" width="auto" height="auto">
</div>

## Background Story:
<details>
  <summary>Click to expand</summary>
  <br>
Courier Companies also known as Logistics Companies are businesses that specialize in transporting packages, documents, and other goods from one location to another.  They offer a range of services, from same-day delivery within a city to international shipping across continents.  They manage the entire process, including pickup, transportation, tracking, and delivery, often using a combination of transportation modes like trucks, airplanes, ships, and trains.  They play a vital role in facilitating commerce and connecting businesses and individuals globally.
  
Courier charges are the fees you pay to a courier company for their services, which primarily involve picking up a package from one location and delivering it to another.
  
In today’s fast-paced e-commerce industry, fast and efficient order delivery is crucial to business success. To ensure seamless order fulfilment, businesses often partner with courier companies to ship their products to customers. However, managing the charges collected by these courier companies can be difficult, especially when dealing with a high volume of orders. It is one of the real-time problems Enterprise to Enterprise businesses experience when their estimated charges for the same invoice don’t match. In this project, I will take you through a solution to this problem statement based on this E2E Courier Charges Accuracy Analysis using Python.
</details>

## Project Objective:
<details>
  <summary>Click to expand</summary>
 <br>This project focuses on assessing the accuracy of fees charged by courier companies for the delivery of goods in E2E transactions. The goal is to ensure that companies are billed appropriately for the services provided by courier companies.
</details>

## Data Overview:
<details>
  <summary>Click to expand</summary>
 <br>This dataset provides a comprehensive view of courier operations and is comprised of five Excel files. These files contain detailed information on:

- Courier company rates
- Invoices
- Order reports
- Pincodes
- SKU master data

### Definitions:
<details>
  <summary>Click to expand</summary>
 <br>
  
- fwd_a_fixed: (Fixed Forward Charge), a fixed cost for shipping a package from the origin to the destination. It's the primary fee for the courier service.
  
- fwd_a_additional: (Additional Forward Charge), an additional charge added to the standard shipping cost due to specific circumstances or service requirements such as special handling, remote area delivery, faster delivery service, fuel surcharge, etc.
  
- rto_a_fixed: (Return To Origin Fixed Charge), a fixed fee charged by the courier when a package has to be returned to the sender.  It's an extra cost incurred due to the failed delivery and the return process.
  
- rto_a_aditional: (Return To Origin Additional Charge), The key difference from "rto_a_fixed" is that this charge is not a fixed amount.  It's a variable charge added to the cost of returning the package and it only applies if an RTO occurs. Because it's not "fixed," the amount of the RTO charge will vary depending on some factors like distance of return, weight or dimension of package, courier policies, courier pricing structures, etc.
  
- AWB Code: (Air WayBill Code), a unique identification number assigned to each air shipment, like a tracking number for your package.  It contains vital information about the shipment and allows it to be tracked throughout its journey.

- ORDER ID: A unique number assigned to a specific order written in an invoice or shipping label.
  
- Charged Weight: Shipping costs are primarily determined by weight and size. Couriers use the "charged weight" to account for both the weight and size of your package and use it to decide how much to charge you for shipping.
  
- Warehouse Pincode: This is the pincode of the warehouse where the shipment originates. It's the starting point of the package's journey.
  
- Customer Pincode: This is the pincode of the customer's delivery address, where the package needs to be delivered. It's the destination of the shipment.
  
- Zone: Shipping zones are geographical areas that carriers use to calculate shipping rates and estimate delivery times. They are typically defined by distance from the origin of the shipment.
  
- Type of Shipment: The type of charges accrued based on the type of shipment being done. e.g forward charges or RTO charges.
  
- Billing Amount: Refers to the total amount the customer is charged for a shipment. It's the sum of all applicable charges.
  
- ExternOrderNo: Same as ORDER ID
  
- SKU(Stock Keeping Unit): It's a unique identifier assigned to a specific product or service to track all the products a retailer, wholesaler, or manufacturer has in stock, waiting to be purchased by customers.
  
- Order Qty: Order Quantity tells you how many of a particular product or item a customer has requested in their order.
  
- Weight: Weight is a primary factor in calculating shipping costs. Heavier packages generally cost more to ship.
</details>
</details>

## Tools Used:
<details>
  <summary>Click to expand</summary>
 <br>
I used the following tools and librabries:
  
- Jupyter Notebook: Writing and Executing Codes
- Pandas Python Library: Data Manipulation and Analysis
- Plotly Python Library: Data Visualization
</details>

## Data Cleaning and Preparation:
<details>
  <summary>Click to expand</summary>
 <br>
  
In the initial data preparation phase, I performed the following tasks:
  
1. I imported the necessary python libraries and the datasets.
2. Checked for missing values.
3. Data cleaning and formatting
</details>

## Exploratory Data Analysis:
<details>
  <summary>Click to expand</summary>
 <br>
I used EDA to answer questions like:
  
- Total Orders where ABC has been correctly charged.
- Total Orders where ABC has been overcharged.
- Total Orders where ABC has been undercharged.
</details>

## Data Analysis:
<details>
  <summary>Click to expand</summary>
 <br>
 Here are some major interesting codes aand functions I worked with:

```python
pd.merge() : # A Pandas function used for merging DataFrames.
```
```python
sigma_courier = pincode_mapping.drop_duplicates(subset=['Customer Pincode'])
courier_sigma= courier_invoice[['Order ID', 'Customer Pincode','Type of Shipment']]
pincodes= courier_abc.merge(abc_courier,on='Customer Pincode')
print(pincodes.head())

# The code above was used to merge the courier invoice and pincode mapping dataset.
```

```python
def weight_slab(weight):
    i = round(weight % 1, 1)
    if i == 0.0:
        return weight
    elif i > 0.5:
        return int(weight) + 1.0
    else:
        return int(weight) + 0.5

merged2['Weight Slab (KG)'] = merged2['Weights (Kgs)'].apply(weight_slab)
courier_invoice['Weight Slab Charged by Courier Company']=(courier_invoice['Charged Weight']).apply(weight_slab)

# The above function is the The weight_slab() function which is defined to determine the weight slab based on the weight of the shipment.
```

```python
total_expected_charge = []

for _, row in merged2.iterrows():
    fwd_category = 'fwd_' + row['Delivery Zone As Per SIGMA']
    fwd_fixed = courier_company_rates.at[0, fwd_category + '_fixed']
    fwd_additional = courier_company_rates.at[0, fwd_category + '_additional']
    rto_category = 'rto_' + row['Delivery Zone As Per SIGMA']
    rto_fixed = courier_company_rates.at[0, rto_category + '_fixed']
    rto_additional = courier_company_rates.at[0, rto_category + '_additional']

    weight_slab = row['Weight Slab As Per SIGMA']

    if row['Type of Shipment'] == 'Forward charges':
        additional_weight = max(0, (weight_slab - 0.5) / 0.5)
        total_expected_charge.append(fwd_fixed + additional_weight * fwd_additional)
    elif row['Type of Shipment'] == 'Forward and RTO charges':
        additional_weight = max(0, (weight_slab - 0.5) / 0.5)
        total_expected_charge.append(fwd_fixed + additional_weight * (fwd_additional + rto_additional))
    else:
        total_expected_charge.append(0)

merged2['Expected Charge as per SIGMA'] = total_expected_charge
print(merged2.head())

'''
The code above is a block of code that iterates through a Pandas DataFrame (merged2) and calculates an "Expected Charge as per SIGMA" based on several factors, including:
Delivery zone
Weight slab
Type of shipment
Courier company rates (from courier_company_rates DataFrame)
'''
```
</details>

## Results & Findings:
<details>
  <summary>Click to expand</summary>
 <br>

These are the three major things I found out concerning our courier companies charges:

| Description                                         | Count | Amount (NGN.) |
|-----------------------------------------------------|-------|---------------|
| Total Orders where SIGMA has been correctly charged | 0     | 0.0           |
| Total Orders where SIGMA has been overcharged       | 354   | 23742040.0    |
| Total Orders where SIGMA has been undercharged      | 47    | -1242780.0     |
</details>

## Recommendations:
<details>
  <summary>Click to expand</summary>
 <br>
  
Here are my recommendations for these courier companies and their courier charges:

 1. Investigate Overcharging Discrepancies:
 - Conduct a thorough investigation into the 354 overcharged orders.
 - Identify the root causes of the overcharging (e.g., incorrect weight calculations, incorrect zone assignments, system errors).
 - Analyze the patterns in the overcharged orders (e.g., specific delivery zones, package types, courier services).

 2. Implement Corrective Actions:
- Develop and implement corrective measures to prevent future overcharging.
- This may involve:
  - Auditing and improving the accuracy of weight and dimension calculations.
  - Verifying and correcting zone assignments.
  - Enhancing system checks and validations.
  - Providing additional training to staff involved in charge calculations.
  - Consider implementing automated checks to verify charges against expected rates.
   
 3. Address Undercharging:
- While the undercharging amount is less significant, investigate the 47 undercharged orders to ensure there are no systematic errors.
- Consider if the undercharging is due to any promotional activities.

 4. Improve Transparency and Communication:
- Provide clear and detailed invoices to customers, showing how charges are calculated.
- Establish a process for customers to dispute charges and resolve discrepancies promptly.
- Consider publishing the rate calculation methodology.

 5. Strengthen Internal Controls:
- Implement stronger internal controls to ensure the accuracy of courier charges.
- Conduct regular audits of courier charge calculations.
- Consider implementing a system for independent verification of charges.

 6. Negotiate with Courier Companies:
- Use the analysis findings to negotiate better rates or service level agreements with the courier companies.
- If systematic errors are found with a specific courier, consider switching to a more reliable provider.

 7. System Improvements:
- If the data is entered manually, look at the UI/UX for ease of use, and reduce manual errors.
- Look at the API connection to the courier companies to ensure data is transferred correctly.

 8. Focus on Customer Satisfaction:
- Overcharging can lead to customer dissatisfaction and loss of business.
- Prioritize accuracy in courier charges to improve customer trust and loyalty.
</details>

## Limitations:
<details>
  <summary>Click to expand</summary>
 <br>
    
- Data Inconsistency and Preparation: The original datasets exhibited inconsistencies in column naming conventions. To ensure data organization and completeness, it was necessary to rename several columns. For example, 'ExternOrderNo' in the Order Report Dataset was renamed to 'Order Id' to align with other datasets. Similarly, 'Zone' and 'Weight Slab (KG)' columns were renamed to provide more descriptive and consistent labels across the dataframes.
  
- Data Preprocessing: A significant portion of the project involved data preprocessing to address inconsistencies in column naming. This step was crucial for accurate data merging and analysis. Notable changes included renaming 'ExternOrderNo' to 'Order Id' and standardizing zone and weight slab column names.
  
- Challenges Faced: Data integration presented challenges due to variations in column naming across datasets. To overcome this, columns such as 'ExternOrderNo' (Order Report) and 'Zone' (Courier Invoice, merged2) were renamed to ensure uniformity and facilitate data analysis.
</details>


