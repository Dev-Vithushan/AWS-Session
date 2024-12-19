### **Create a DynamoDB Table and Add Data via API Gateway**

This guide explains how to create a DynamoDB table and a Lambda function that adds data to the table when triggered by an API Gateway endpoint.

---

### **Steps**

#### **Step 1: Create a DynamoDB Table**
1. Go to the **DynamoDB Console**.
2. Click **Create Table** and configure:
   - **Table Name**: `ItemsTable`.
   - **Partition Key**: `id` (String).
   - Leave other settings as default and create the table.

---

#### **Step 2: Create a Lambda Function**
1. Navigate to the **Lambda Console**.
2. Create a new Lambda function:
   - **Name**: `AddItemFunction`.
   - **Runtime**: Python 3.x or Node.js.
3. Use the following code depending on your preferred runtime:

---

##### **Python Code**
```python
import json
import boto3
import uuid

# Initialize DynamoDB resource
dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('ItemsTable')

def lambda_handler(event, context):
    try:
        # Parse incoming request
        body = json.loads(event['body'])
        item = {
            'id': str(uuid.uuid4()),  # Generate a unique ID
            'name': body['name'],
            'description': body['description']
        }
        
        # Add item to DynamoDB
        table.put_item(Item=item)
        
        return {
            'statusCode': 200,
            'body': json.dumps({'message': 'Item added successfully!', 'item': item})
        }
    except Exception as e:
        return {
            'statusCode': 500,
            'body': json.dumps({'error': str(e)})
        }
```

---

##### **Node.js Code**
```javascript
const AWS = require('aws-sdk');
const dynamodb = new AWS.DynamoDB.DocumentClient();

exports.handler = async (event) => {
    try {
        const body = JSON.parse(event.body);
        const item = {
            id: AWS.util.uuid.v4(), // Generate a unique ID
            name: body.name,
            description: body.description,
        };
        
        // Add item to DynamoDB
        await dynamodb.put({
            TableName: 'ItemsTable',
            Item: item,
        }).promise();
        
        return {
            statusCode: 200,
            body: JSON.stringify({ message: 'Item added successfully!', item }),
        };
    } catch (error) {
        return {
            statusCode: 500,
            body: JSON.stringify({ error: error.message }),
        };
    }
};
```

4. Deploy the function and attach the necessary IAM role with **DynamoDB full access** permissions.

---

#### **Step 3: Create an API Gateway**
1. Go to the **API Gateway Console** and create a new REST API.
2. Create a resource (e.g., `/addItem`).
3. Add a **POST method** to the resource:
   - Integration type: **Lambda Function**.
   - Link the method to your Lambda function (`AddItemFunction`).
4. Deploy the API:
   - Click **Deploy API**.
   - Create a new stage (e.g., `dev`).

---

#### **Step 4: Test the API**
1. Use a tool like **Postman** or **cURL** to send a POST request to the API endpoint.
2. Example POST request body:
   ```json
   {
       "name": "Laptop",
       "description": "A high-performance laptop"
   }
   ```
3. Verify the response and check if the item is added to the DynamoDB table.

---

### **Deliverables**
- **API Endpoint URL**.
- **Screenshot of DynamoDB Table with Data**.
- **Test Results** from Postman or cURL.

