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
   



















