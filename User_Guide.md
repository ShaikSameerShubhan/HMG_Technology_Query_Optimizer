AWS Redshift + AI Optimization POC
🎯 What We're Building
A system where AI assistants help optimize your database queries and reduce costs - all running on Amazon's cloud infrastructure.
📚 Background Knowledge (5-minute read)
What is Amazon Redshift?

Think of it as a giant Excel spreadsheet in the cloud that can handle millions of rows
Companies use it to analyze business data (sales, customers, inventory, etc.)
It's expensive if not optimized properly - that's where AI helpers come in!

What are AI Sub-Agents?

Instead of one general AI, you have specialized AI assistants
Each one is an expert in one area:

Query Optimizer: Makes slow database searches faster
Cost Saver: Finds ways to reduce your AWS bill
Schema Advisor: Suggests better ways to organize your data
Data Validator: Checks if your data is correct



🛠️ Step 1: Set Up Your AWS Account (15 minutes)
1.1 Create AWS Account

Go to aws.amazon.com
Click "Create an AWS Account"
Follow the signup process (you'll need a credit card)
Important: AWS offers free tier, but Redshift costs money (~$0.25/hour for small cluster)

1.2 Set Up Billing Alerts

Go to AWS Console > Billing Dashboard
Set up a billing alert for $50/month (so you don't get surprised)

🗄️ Step 2: Create Your First Redshift Cluster (20 minutes)
2.1 Navigate to Redshift

In AWS Console, search for "Redshift"
Click "Amazon Redshift"

2.2 Choose Redshift Serverless (Easier for beginners)

Click "Create" > "Serverless"
Give it a name: my-first-redshift-cluster
Set admin username: admin
Set password: MyPassword123! (write this down!)
Click "Create workgroup"

2.3 Wait for Setup (5-10 minutes)

AWS will create your database cluster
Status will show "Available" when ready

📊 Step 3: Load Sample Data (15 minutes)
3.1 Connect to Your Database
You'll use the "Query Editor" in AWS Console:

Go to Redshift > Query Editor v2
Connect to your cluster using the credentials you created

3.2 Create Sample Tables
Copy and paste this SQL code:
sql-- Create a customers table
CREATE TABLE customers (
    customer_id INTEGER PRIMARY KEY,
    customer_name VARCHAR(100),
    email VARCHAR(100),
    city VARCHAR(50),
    signup_date DATE
);

-- Create a sales table
CREATE TABLE sales (
    sale_id INTEGER PRIMARY KEY,
    customer_id INTEGER,
    product_name VARCHAR(100),
    sale_amount DECIMAL(10,2),
    sale_date DATE
);

-- Insert sample data
INSERT INTO customers VALUES 
(1, 'John Doe', 'john@email.com', 'New York', '2023-01-15'),
(2, 'Jane Smith', 'jane@email.com', 'Los Angeles', '2023-02-20'),
(3, 'Bob Johnson', 'bob@email.com', 'Chicago', '2023-03-10'),
(4, 'Alice Brown', 'alice@email.com', 'Houston', '2023-04-05'),
(5, 'Charlie Wilson', 'charlie@email.com', 'Phoenix', '2023-05-12');

INSERT INTO sales VALUES
(1, 1, 'Laptop', 1200.00, '2023-06-01'),
(2, 1, 'Mouse', 25.00, '2023-06-02'),
(3, 2, 'Monitor', 300.00, '2023-06-03'),
(4, 3, 'Keyboard', 80.00, '2023-06-04'),
(5, 2, 'Webcam', 150.00, '2023-06-05'),
(6, 4, 'Laptop', 1200.00, '2023-06-06'),
(7, 5, 'Tablet', 400.00, '2023-06-07'),
(8, 1, 'Headphones', 200.00, '2023-06-08');
3.3 Test Your Data
Run this query to make sure everything works:
sqlSELECT c.customer_name, s.product_name, s.sale_amount
FROM customers c
JOIN sales s ON c.customer_id = s.customer_id
ORDER BY s.sale_amount DESC;
🔐 Step 4: Set Up AWS Secrets Manager (10 minutes)
4.1 Store Database Credentials Securely

Go to AWS Console > Secrets Manager
Click "Store a new secret"
Choose "Credentials for Amazon Redshift cluster"
Enter:

Username: admin
Password: MyPassword123!
Select your Redshift cluster


Name it: redshift-credentials
Click "Store"
