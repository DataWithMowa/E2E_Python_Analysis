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
- fwd_a_fixed:(Fixed Forward Charge), a fixed cost for shipping a package from the origin to the destination. It's the primary fee for the courier service.
  
- fwd_a_additional:(Additional Forward Charge), an additional charge added to the standard shipping cost due to specific circumstances or service requirements such as special handling, remote area delivery, faster delivery service, fuel surcharge, etc.
  
- rto_a_fixed:(Return To Origin Fixed Charge), a fixed fee charged by the courier when a package has to be returned to the sender.  It's an extra cost incurred due to the failed delivery and the return process.
  
- rto_a_aditional:(Return To Origin Additional Charge), The key difference from "rto_a_fixed" is that this charge is not a fixed amount.  It's a variable charge added to the cost of returning the package and it only applies if an RTO occurs. Because it's not "fixed," the amount of the RTO charge will vary depending on some factors like distance of return, weight or dimension of package, courier policies, courier pricing structures, etc.
  
- AWB Code:(Air WayBill Code), a unique identification number assigned to each air shipment, like a tracking number for your package.  It contains vital information about the shipment and allows it to be tracked throughout its journey.

- ORDER ID:A unique number assigned to a specific order written in an invoice or shipping label.
  
- Charged Weight: Shipping costs are primarily determined by weight and size. Couriers use the "charged weight" to account for both the weight and size of your package and use it to decide how much to charge you for shipping.
  
- Warehouse Pincode:This is the pincode of the warehouse where the shipment originates. It's the starting point of the package's journey.
  
- Customer Pincode:This is the pincode of the customer's delivery address, where the package needs to be delivered. It's the destination of the shipment.
  
- Zone:Shipping zones are geographical areas that carriers use to calculate shipping rates and estimate delivery times. They are typically defined by distance from the origin of the shipment.
  
- Type of Shipment:The type of charges accrued based on the type of shipment being done. e.g forward charges or RTO charges.
  
- Billing Amount:Refers to the total amount the customer is charged for a shipment. It's the sum of all applicable charges.
  
- ExternOrderNo: Same as ORDER ID
  
- SKU(Stock Keeping Unit):It's a unique identifier assigned to a specific product or service to track all the products a retailer, wholesaler, or manufacturer has in stock, waiting to be purchased by customers.
  
- Order Qty:Order Quantity tells you how many of a particular product or item a customer has requested in their order.
  
-Weight:Weight is a primary factor in calculating shipping costs. Heavier packages generally cost more to ship.
</details>
</details>

## Tools used:
<details>
  <summary>Click to expand</summary>
 <br>
 - Jupyter NoteBook - Writing and Executing Codes
 - Pandas Python Library - Data Manipulation and Analysis
 - Plotly Python Library - Data Cleaning
</details>

## Data Cleaning and Preparation
<details>
  <summary>Click to expand</summary>
 <br>
 

