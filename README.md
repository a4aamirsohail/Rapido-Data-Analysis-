This project contains a series of SQL queries designed to analyze ride-booking data from the Rapido table. It performs various operations such as:

Filtering successful bookings to retrieve all completed rides.

Calculating average ride distance for each vehicle type.

Counting customer cancellations of rides.

Identifying top 5 most frequent customers based on ride count.

Counting driver cancellations due to personal or car-related issues.

Finding maximum and minimum driver ratings specifically for Prime Sedan bookings.

Filtering rides paid via UPI payment method.

Calculating average customer ratings per vehicle type.

Summing total booking value of all successful rides.

Listing incomplete rides and their reasons for better incident tracking.

Below are the code that i use for cleaning the data 


--1. Retrieve all successful bookings

Select * from Rapido
where Booking_Status = 'Success'


--#2. Find the average ride distance for each vehicle type:

Select Vehicle_Type,
Avg(Ride_Distance) as Avg_Ride from Rapido
Group By Vehicle_Type


--#3. Get the total number of cancelled rides by customers:

Select Count(*) from Rapido
Where Booking_Status = 'Canceled by Customer'

--#4. List the top 5 customers who booked the highest number of rides:

SELECT TOP 5 Customer_ID,
       COUNT(*) AS Total_rides
FROM Rapido
GROUP BY Customer_ID
ORDER BY Total_rides DESC;

--#5. Get the number of rides cancelled by drivers due to personal and car-related issues:

Select Count(*) as Cancel_Ride from Rapido
where Canceled_Rides_by_Driver = 'Personal & Car related issue'

--#6. Find the maximum and minimum driver ratings for Prime Sedan bookings:

Select Max(Driver_Ratings) as Max_Ratings,
Min(Driver_Ratings) as Min_Ratings
from Rapido
where Vehicle_Type = 'Prime Sedan'


--#7. Retrieve all rides where payment was made using UPI:

Select * from Rapido
Where Payment_Method = 'UPI'

--#8. Find the average customer rating per vehicle type:

Select Vehicle_Type,
AVG(Customer_Rating) as Avg_customer_rating
from Rapido
Group by Vehicle_Type

--#9. Calculate the total booking value of rides completed successfully

Select Sum(Booking_Value) as Total_successful_ride_value
from Rapido
Where Booking_Status = 'Success'


--#10. List all incomplete rides along with the reason

-- Assuming Yes = 1 and No = 0
SELECT Booking_ID, Incomplete_Rides_Reason
FROM Rapido
WHERE Incomplete_Rides = 1;
