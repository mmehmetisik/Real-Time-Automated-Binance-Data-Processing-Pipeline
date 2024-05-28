# Real-Time Automated Binance Data Processing Pipeline

## Architecture Diagram
![image](https://github.com/mmehmetisik/Real-Time-Automated-Binance-Data-Processing-Pipeline/assets/64706956/fe4d24c5-99c2-4abd-aae9-81334cad10d4)


## Project Overview
The aim of this project is to fetch real-time data from the Binance API, process and store it using AWS infrastructure. This project ensures efficient collection, processing, and storage of high-volume data. The process creates an automated and scalable data pipeline using AWS services.

This project utilizes the following AWS services or technologies:
1. VPC
2. EC2 Instance
3. Lambda Function
4. IAM Role
5. S3 Bucket
6. SQS
7. DynamoDB
8. NoSQL Workbench

## Architecture
The system architecture is designed to demonstrate real-time data handling using AWS services. The following AWS services are utilized:
- **VPC:** To create an isolated network environment.
- **EC2 Instance:** For running the application and managing data buffers.
- **Lambda Function:** To process data and interact with other AWS services.
- **IAM Role:** To securely manage access to AWS services.
- **S3 Bucket:** To store the .tsv files that contain the data to be processed.
- **SQS:** To queue the data before it is inserted into DynamoDB.
- **DynamoDB:** For storing the processed data in a NoSQL database.
- **NoSQL Workbench:** To query and analyze the data stored in DynamoDB.

## Technologies Used
- **Python:** The programming language used for writing Lambda functions.
- **AWS Services:** Including but not limited to VPC, EC2, Lambda, IAM, S3, SQS, DynamoDB, and NoSQL Workbench for comprehensive cloud-based operations and data management.

## How It Works
1. **Data Storage on EC2:**
   - TSV files containing data are fetched from the Binance API every minute and stored on an EC2 instance.

2. **Triggering Lambda Function from S3:**
   - When a .tsv file is uploaded to the S3 bucket from the EC2 instance, the first Lambda function is triggered.
   - This Lambda function reads the first 5 rows of the .tsv file and sends each row as a message to the SQS queue.

3. **Triggering Lambda Function from SQS:**
   - The second Lambda function is triggered when a new message is added to the SQS queue.
   - This Lambda function reads the messages from the SQS queue and writes the data to the DynamoDB table `ProcessedData`.

4. **Data Verification with NoSQL Workbench:**
   - After all processes are completed, NoSQL Workbench is used to connect to the DynamoDB table and verify if the data has been correctly inserted.

## Important Considerations
### Counter:
- A counter mechanism between S3 and the first Lambda function ensures that the process only runs for three TSV files. After processing the third TSV file, the first Lambda function stops.

### Throttle:
- A throttle mechanism between SQS and the second Lambda function ensures controlled data processing by gradually feeding data to the Lambda function from the SQS queue.

## Step-by-Step Instructions
### Part 1:
1. Create a VPC.
2. Create an IAM Role (EC2 to S3).
3. Launch an EC2 instance.
4. Create an S3 Bucket (with a folder named `data_1_min`).
5. Test the first part by verifying if .tsv files are uploaded to the S3 Bucket.

### Part 2:
6. Set up SQS.
7. Create the first Lambda Function.
8. Add code to the first Lambda Function.
9. Add an S3 Bucket trigger to the first Lambda Function.
10. Attach the IAM Role to the first Lambda Function.
11. Test and verify if the first Lambda Function is working correctly by checking if messages are sent to the SQS queue.

### Part 3:
12. Create the second Lambda Function.
13. Add code to the second Lambda Function.
14. Attach the IAM Role to the second Lambda Function.
15. Add an SQS trigger to the second Lambda Function.
16. Create a table in DynamoDB.
17. Use NoSQL Workbench to connect to the DynamoDB table and verify if the data is correctly inserted.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

This README file provides a comprehensive guide to setting up and running the Real-Time Automated Binance Data Processing Pipeline using AWS services.
