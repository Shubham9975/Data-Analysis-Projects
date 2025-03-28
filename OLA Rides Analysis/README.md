# 🚖 OLA Data Analyst Project

## 📌 Overview
This project focuses on analyzing ride data for Ola in Bengaluru over a one-month period. It combines dataset generation, SQL queries, and Power BI visualizations to uncover insights into booking trends, cancellations, customer and driver behavior, and overall revenue.

---

## 📊 Dataset Description
The dataset simulates ride booking data for Bengaluru with **1,00,000 rows**, including the following attributes:

### 📅 Core Columns
1. **📆 Date**: Date of booking.
2. **⏰ Time**: Time of booking.
3. **🆔 Booking ID**: A unique 10-digit identifier for each booking.
4. **📌 Booking Status**: Indicates whether the ride was:
   - ✅ Successful
   - ❌ Cancelled by Customer
   - ❌ Cancelled by Driver
   - ⚠️ Incomplete  
5. **👤 Customer ID**: Unique ID assigned to each customer.  

### 🚗 Ride Details
6. **🚘 Vehicle Type**: Categories such as Auto, Prime Sedan, Mini, Bike, eBike, Prime SUV, and Prime Plus.  
7. **📍 Pickup & Drop Locations**: 50 predefined areas within Bengaluru used as dummy data.  
8. **⏳ VTAT (Vehicle Arrival Time)**: Time taken for the vehicle to arrive.  
9. **⏳ CTAT (Customer Arrival Time)**: Time taken for the customer to reach the pickup point.  
10. **📏 Ride Distance**: Distance covered during the ride (in kilometers).  

### ❌ Cancellation Information
11. **🚫 Cancelled Rides by Customer**: Reasons include:
   - 🚖 Driver not moving toward the pickup location.
   - 🔄 Driver requested cancellation.
   - ❄️ Non-functional AC (for 4-wheelers only).
   - 🔀 Change of plans.
   - 📍 Incorrect address.
12. **🚫 Cancelled Rides by Driver**: Reasons include:
   - 🚗 Personal or vehicle-related issues.
   - 👥 Customer-related problems.
   - 🤒 Customer was coughing or appeared sick.
   - 👨‍👩‍👦 More passengers than allowed.  

### ⚠️ Additional Information
13. **❌ Incomplete Rides**: Includes rides that started but did not complete, along with reasons like:
   - 🏁 Customer demand.
   - 🛠️ Vehicle breakdown.
   - ❓ Other issues.  
14. **💰 Booking Value**: The fare of each ride (in INR).  
15. **⭐ Driver Ratings**: Feedback from customers about drivers (1-5 scale).  
16. **⭐ Customer Ratings**: Feedback from drivers about customers (1-5 scale).  
17. **💳 Payment Method**: Options include Cash, UPI, Credit/Debit Cards, etc.

---

## ⚙️ Key Data Constraints
1. **✅ Successful Bookings**: Maintained at **62%** of total bookings.
2. **🚫 Customer Cancellations**: Restricted to **≤ 7%**.
3. **🚫 Driver Cancellations**: Limited to **≤ 18%**.
4. **⚠️ Incomplete Rides**: Less than **6%**.
5. **📊 Weekend and Event Behavior**:
   - 📈 Higher booking volume on weekends.
   - 💸 Higher booking value on weekends and event days.  

---

## 🛠️ SQL Analysis

### 🔍 Key Queries
1. Retrieve all successful bookings:
   ```sql
   SELECT * FROM bookings WHERE Booking_Status = 'Success';
   ```

2. Calculate the average ride distance per vehicle type:
   ```sql
   SELECT Vehicle_Type, AVG(Ride_Distance) AS avg_distance 
   FROM bookings 
   GROUP BY Vehicle_Type;
   ```

3. Get the total number of cancelled rides by customers:
   ```sql
   SELECT COUNT(*) AS total_cancelled_by_customers 
   FROM bookings 
   WHERE Booking_Status = 'Cancelled by Customer';
   ```

4. List the top 5 customers with the highest number of rides:
   ```sql
   SELECT Customer_ID, COUNT(Booking_ID) AS total_rides 
   FROM bookings 
   GROUP BY Customer_ID 
   ORDER BY total_rides DESC 
   LIMIT 5;
   ```

5. Find incomplete rides and their reasons:
   ```sql
   SELECT Booking_ID, Incomplete_Rides_Reason 
   FROM bookings 
   WHERE Incomplete_Rides = 'Yes';
   ```

6. Retrieve rides where payment was made via UPI:
   ```sql
   SELECT * 
   FROM bookings 
   WHERE Payment_Method = 'UPI';
   ```

7. Calculate the total booking value for successful rides:
   ```sql
   SELECT SUM(Booking_Value) AS total_successful_value 
   FROM bookings 
   WHERE Booking_Status = 'Success';
   ```

---

## 📈 Power BI Visualizations
The project includes dashboards for analyzing booking trends and insights:

1. **📅 Ride Volume Over Time**:
   - A time-series chart showing daily or weekly ride volumes.
2. **📊 Booking Status Breakdown**:
   - A pie chart or doughnut chart visualizing the proportions of success, cancellations, and incomplete rides.
3. **🚘 Top Vehicle Types by Ride Distance**:
   - A bar chart ranking vehicle types by total ride distance.
4. **⭐ Average Customer Ratings by Vehicle Type**:
   - A column chart showcasing average ratings for different vehicle categories.
5. **🚫 Cancelled Rides Analysis**:
   - A segmented bar chart highlighting reasons for cancellations by customers and drivers.
6. **💳 Revenue by Payment Method**:
   - A stacked bar chart visualizing revenue distribution across payment methods.
7. **🏆 Top 5 Customers by Booking Value**:
   - A leaderboard ranking customers based on total spending.
8. **📊 Driver Ratings Distribution**:
   - A box plot analyzing driver ratings across vehicle types.
9. **📉 Customer vs. Driver Ratings**:
   - A scatter plot comparing customer and driver ratings for completed rides.

---
![Power BI Visualizations](https://github.com/Shubham9975/Data-Analysis-Projects/blob/main/OLA%20Rides%20Analysis/Vizualizations.gif?raw=true)

