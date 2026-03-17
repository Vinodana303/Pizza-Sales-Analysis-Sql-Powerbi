#  &nbsp;&nbsp;&nbsp;&nbsp; PIZZA SALES ANALYSIS
![delicious-pizza-studio_23-2151846547](https://github.com/user-attachments/assets/8e61443c-8c84-4427-9243-cb957a48534b)

<h3>Tools used : Excel,MS SQL Server,Power BI</h3>

[Dataset used](https://github.com/Vinodana303/Pizza-Sales-Analysis-Sql-Powerbi/blob/main/pizza_sales.csv)

[SQL Analysis-code](https://github.com/Vinodana303/Pizza-Sales-Analysis-Sql-Powerbi/blob/main/PIZZA%20SALES%20SQL%20QUERIES.docx)

[Power BI Dashboard- click to view](https://github.com/Vinodana303/Pizza-Sales-Analysis-Sql-Powerbi/blob/main/pizza_report1.png)

[Power BI Dashboard- click to interact](https://github.com/Vinodana303/Pizza-Sales-Analysis-Sql-Powerbi/blob/main/pizza_data_report.pbix)

<h2>Business Problem</h2>

A pizza company needs a robust and scalable data analytics solution to handle the vast amount of data(approximately 50k rows of data combined) to effectively analyze and extract meaningful insights like trends, order patterns, menu performance, customer preferences and other key business metrics. Visualizations must also be created to identify trends and insights related to daily and monthly order volume, sales by pizza type and size, and top/bottom sellers. The end goal is to equip the business with data-driven insights that inform strategic decisions to improve operations and profitability.
<h2>Solution Plan</h2>

- In helping the pizza company gain valuable insights from their sales data CSV file, I will utilize SQL and data visualization with Power BI to extract relevant information and conduct insightful analyses. Data cleaning/processing, data transformation and analysis shall be done.

- By leveraging SQL's functions, I can uncover key metrics like total revenue, average order size, and best/worst selling menu items.

- Once the data has been extracted and prepared, I will leverage Power BI to present the findings through interactive visualizations. This will allow stakeholders at the pizza company to gain actionable insights into sales trends, order patterns, and menu performance through visually compelling charts, graphs, and reports.

- I plan on creating a dynamic Power BI dashboard that enables users to explore details on daily order volume, sales by pizza type/size, or top/bottom selling items. The end goal is equipping the business with data-driven insights to inform strategic decisions that improve operations and profitability.

<h2>Execution</h2>
Questions Answered from the Dataset

1) What are the Key Performance Indicators obtained from the Dataset?

   - Total Revenue:

SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;

<img width="287" height="131" alt="image" src="https://github.com/user-attachments/assets/c4cff35d-5d65-41d7-8ae7-b5fe353ff421" />

This metric provides a clear measure of the overall financial performance of the pizza sales. It indicates the total amount of money generated from pizza orders over a specific period, reflecting the revenue potential of the business.

- Average Order Value:

    SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales

 <img width="305" height="133" alt="image" src="https://github.com/user-attachments/assets/dab58483-2ae8-4825-a9ac-4240a97d4b0f" />

Average order value helps in understanding customer spending habits and the effectiveness of marketing strategies. A higher average order value indicates that customers are spending more per transaction, which can contribute to increased revenue and profitability.

- Total Pizzas Sold:

  SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales

<img width="311" height="135" alt="image" src="https://github.com/user-attachments/assets/27df90b5-034c-4198-b423-61ae2c78a437" />

Total pizzas sold is a fundamental metric that directly reflects product demand. It provides insights into consumption patterns and helps in inventory management and production planning. Understanding total pizzas sold enables businesses to meet customer demand efficiently.

- Total Orders:

  SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales

<img width="315" height="128" alt="image" src="https://github.com/user-attachments/assets/e77cac93-aba9-42c1-9c65-46b84ef8f433" />

Total orders represent the volume of transactions processed within a specific period. Tracking total orders helps in evaluating sales performance and identifying trends in customer behavior. It provides a basis for assessing business growth and operational efficiency.

- Average Pizzas Per Order:

   SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) /   
   CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))  
    AS Avg_Pizzas_per_order  
    FROM pizza_sales

<img width="325" height="141" alt="image" src="https://github.com/user-attachments/assets/d7b296eb-ecbd-47f2-8be8-a81bd515c1a1" />

Average pizzas per order indicates the average quantity of pizzas purchased in each transaction. This metric offers insights into customer preferences and ordering behavior. Higher average pizzas per order may indicate upselling opportunities or popular menu items.


2) Daily Trend for Total Orders

    SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders   
    FROM pizza_sales  
    GROUP BY DATENAME(DW, order_date)

  <img width="367" height="325" alt="image" src="https://github.com/user-attachments/assets/4ea72f8a-7f32-4f58-ac91-3798e24c8bac" />
 
By analyzing the daily trend of total orders over a specific time period, we can identify patterns and fluctuations in order volumes on a daily basis. This helps in understanding the demand patterns throughout the week or month, enabling better inventory management and resource allocation. 

3) Monthly Trend for Orders

   select DATENAME(MONTH, order_date) as Month_Name, COUNT(DISTINCT order_id) as Total_Orders  
    from pizza_sales  
    GROUP BY DATENAME(MONTH, order_date)

<img width="400" height="475" alt="image" src="https://github.com/user-attachments/assets/3408c892-a04a-42ee-9a55-bf26a7b180d5" />

The monthly trend of total orders offers insights into the overall order activity throughout the month. Identifying peak periods of high order activity can aid in resource allocation, production planning, and promotional efforts. By recognizing monthly trends, businesses can adjust their operations to capitalize on high-demand periods and optimize efficiency during slower periods.

4) % of Sales by Pizza Category
   
    SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,  
    CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT  
    FROM pizza_sales  
    GROUP BY pizza_category

<img width="601" height="275" alt="image" src="https://github.com/user-attachments/assets/f381e6aa-a93e-4b09-9716-7a2dd64603ee" />

The distribution of sales across different pizza categories helps in understanding the popularity of each category and its contribution to overall sales. This insight informs menu optimization strategies, marketing campaigns, and inventory management decisions to maximize revenue and customer satisfaction.

5) % of Sales by Pizza Size

    SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,  
    CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT  
    FROM pizza_sales  
    GROUP BY pizza_size  
    ORDER BY pizza_size
   

<img width="549" height="318" alt="image" src="https://github.com/user-attachments/assets/92663636-a1d6-4232-a8bf-5f4d11f6577f" />

The chart depicting the percentage of sales attributed to different pizza sizes provides insights into customer preferences regarding pizza size. Understanding these preferences allows for better inventory management and menu optimization to meet customer demand effectively.

6) Total Pizzas Sold by Pizza Category

    SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold  
    FROM pizza_sales  
    WHERE MONTH(order_date) = 2  
    GROUP BY pizza_category  
    ORDER BY Total_Quantity_Sold DESC
   
<img width="565" height="271" alt="image" src="https://github.com/user-attachments/assets/e9c5e239-161b-4a91-8152-bf96ca382e81" />

The metric showing total number of pizzas sold for each pizza category enables comparison of sales performance across different categories. This visualization helps in identifying popular and less popular pizza options, informing marketing strategies and menu adjustments accordingly.

7) Top 5 Pizzas by Revenue

    SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue  
    FROM pizza_sales  
    GROUP BY pizza_name  
    ORDER BY Total_Revenue DESC

<img width="516" height="242" alt="image" src="https://github.com/user-attachments/assets/7a3eaeb4-3a5e-4289-9113-fa55885a55bd" />

The chart highlighting the top 5 best-selling pizzas based on revenue, total quantity, and total orders identifies the most popular pizza options. This insight aids in understanding customer preferences and allows for targeted promotions or menu enhancements to capitalize on high-demand items.

8) Bottom 5 Pizzas by Revenue

    SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
    FROM pizza_sales
    GROUP BY pizza_name
    ORDER BY Total_Revenue ASC

 <img width="560" height="211" alt="image" src="https://github.com/user-attachments/assets/443f9e0f-c619-4f49-9b00-9c7b3f3fc52e" />
  
Conversely, the chart showcasing the bottom 5 worst-selling pizzas based on revenue, total quantity, and total orders helps identify underperforming or less popular pizza options. This information is valuable for making strategic decisions such as discontinuing unpopular items or adjusting pricing and marketing strategies to boost sales.

9) Top 5 Pizzas by Quantity

    SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold  
    FROM pizza_sales  
    GROUP BY pizza_name  
    ORDER BY Total_Pizza_Sold DESC

<img width="716" height="283" alt="image" src="https://github.com/user-attachments/assets/81f23f56-c7e5-45d2-bae2-fed539805731" />

Identifying the top 5 pizzas by quantity sold provides insight into the most popular pizza varieties among customers. This information helps in understanding customer preferences and allows for targeted marketing efforts or menu optimizations to capitalize on high-demand items.

10) Bottom 5 Pizzas by Quantity

    SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold  
    FROM pizza_sales  
    GROUP BY pizza_name  
    ORDER BY Total_Pizza_Sold ASC

<img width="667" height="305" alt="image" src="https://github.com/user-attachments/assets/23aa2fc9-e7aa-40e3-87c0-a9d9e290242b" />

Conversely, identifying the bottom 5 pizzas by quantity sold highlights less popular or underperforming pizza options. This insight can inform menu adjustments, promotional strategies, or inventory management decisions to minimize waste and maximize profitability.

11) Top 5 Pizzas by Total Orders

    SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders  
    FROM pizza_sales  
    GROUP BY pizza_name  
    ORDER BY Total_Orders DESC

<img width="516" height="264" alt="image" src="https://github.com/user-attachments/assets/fc3ef1ce-7812-4ec0-9f8d-9575d6f11f31" />

Identifying the top 5 pizzas by total orders sheds light on the most frequently ordered pizza varieties. This information helps in understanding customer behavior and preferences, enabling businesses to tailor marketing campaigns and menu offerings to meet customer demand effectively.


12) Bottom 5 Pizzas by Total Orders


    SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders  
    FROM pizza_sales  
    GROUP BY pizza_name  
    ORDER BY Total_Orders ASC  

<img width="508" height="215" alt="image" src="https://github.com/user-attachments/assets/140dc7ad-869a-40c3-8138-0b582683cc1c" />

Identifying the bottom 5 pizzas by total orders reveals less popular or niche pizza options that may require attention or adjustments. Understanding these trends allows businesses to make informed decisions regarding menu adjustments, promotional strategies, or inventory management to optimize sales and customer satisfaction  


13) Generated various Charts and Visuals on Power BI to identify trends/patterns and gain more insights into the data.





   
