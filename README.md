I'll help you create a simple web app using AWS Lambda with function URLs. Here are the straightforward steps:

Step 1: Create the Lambda Function
Go to AWS Console

Log into AWS Management Console

Search for "Lambda" and click on it

Create Function

Click "Create function"

Choose "Author from scratch"

Function name: SimpleWebApp

Runtime: Python 3.9 (or any version you prefer)

Click "Create function"

Step 2: Write Simple Code
Replace the default code with this simple Python code:

python
import json

def lambda_handler(event, context):
    # Get the HTTP method
    http_method = event.get('requestContext', {}).get('http', {}).get('method', 'GET')
    
    if http_method == 'GET':
        return {
            'statusCode': 200,
            'headers': {
                'Content-Type': 'text/html'
            },
            'body': '''
            <html>
                <head><title>Simple Web App</title></head>
                <body>
                    <h1>Hello from AWS Lambda!</h1>
                    <p>This is a simple web app running on Lambda</p>
                    <form method="POST">
                        <input type="text" name="message" placeholder="Enter a message">
                        <button type="submit">Submit</button>
                    </form>
                </body>
            </html>
            '''
        }
    
    elif http_method == 'POST':
        # Simple form processing
        body = event.get('body', '')
        return {
            'statusCode': 200,
            'headers': {
                'Content-Type': 'text/html'
            },
            'body': f'''
            <html>
                <head><title>Response</title></head>
                <body>
                    <h1>Form Submitted!</h1>
                    <p>You posted: {body}</p>
                    <a href="/">Go Back</a>
                </body>
            </html>
            '''
        }
Click "Deploy" to save your code

Step 3: Create Function URL
Configure Function URL

In your Lambda function, click "Configuration" tab

Click "Function URL" in left sidebar

Click "Create function URL"

Set URL Settings

Auth type: NONE (for simplicity, but use AWS_IAM for production)

CORS: Configure if needed, or leave default for now

Click "Save"

Step 4: Test Your Web App
