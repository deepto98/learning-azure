
Serverless - Code you write that runs on servers a cloud provider manages.
1. What is Azure Functions?<br>
Azure Functions is a serverless application platform. 
It enables developers to host business logic that can be executed without provisioning infrastructure. 
https://docs.microsoft.com/en-us/learn/modules/create-serverless-logic-with-azure-functions/2-decide-if-serverless-computing-is-right-for-your-business-need<br>
2. What is a function app?<br>
Functions are hosted in an execution context called a function app. 
You define function apps to logically group and structure your functions and a compute resource in Azure. <br>
3. Steps to create a function app:<br>
  i. Go to https://portal.azure.com/, choose Function App and click Create<br>
  ii. Fill in the details:<br><br>
    ![image](https://user-images.githubusercontent.com/91651033/161237924-20a61492-640d-4d82-bc94-a2440b7c7ec5.png)<br><br>
  iii. Click Review+Create>Create<br>
  iv. Wait for deployment, then select Go to resource. The Function App pane for your escalator function appears.<br>
  v. In the Essentials section, select the URL link to open it in a browser<br><br>
  ![image](https://user-images.githubusercontent.com/91651033/161242369-ec54ee2f-36fb-4ba3-8087-54713bc29bd2.png)<br><br>
  ![image](https://user-images.githubusercontent.com/91651033/161242571-443e1892-2b99-483a-8af3-d864a94f8cf9.png)	
4. Function Basics:<br>
  i.Triggers<br>
    Functions are event driven, which means they run in response to an event. 
    The type of event that starts a function is called a trigger. 
    Each function must be configured with exactly one trigger.
    Azure services for which triggers can be defined:
      Blob Storage,Azure Cosmos DB, Event Grid, HTTP, Microsoft Graph Events, Queue Storage, Service Bus, Timer	<br>
   ii. Bindings<br>
      A binding is a declarative way to connect data and services to your function. 
      Bindings interact with various data sources, which means you don't have to write the code in your function to connect to data sources and manage connections. 
      The platform takes care of that complexity for you as part of the binding code. 
      Each binding has a direction--your code reads data from input bindings, and writes data to output bindings.
      Each function can have zero or more bindings to manage the input and output data processed by the function.
      A trigger is a type of input binding that has the ability to initiate execution of some code.<br>
      eg :  Let's say we want to write a new row to Azure Table storage whenever a new message appears in Azure Queue Storage. 
			This scenario can be implemented using an Azure Queue Storage trigger and an Azure Table storage output binding.<br><br>
			function.json
      ```
   	{
     "bindings": [
      {
        "name": "order",
        "type": "queueTrigger",
        "direction": "in",
        "queueName": "myqueue-items",
        "connection": "MY_STORAGE_ACCT_APP_SETTING"
      },
      {
        "name": "$return",
        "type": "table",
        "direction": "out",
        "tableName": "outTable",
        "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
      }
    ]
    }
    ```
5. Create a function:<br>
		(For Windows deployments, functions can be edited from Azure Portal, for Linux ones it has to be done through VS Code)<br>
	i. On Function App Page: Functions > Create to see instructions<br>
	ii. In new dir on local, run:<br>
			`npm install -g azure-functions-core-tools@4 --unsafe-perm true`<br>
	iii. Install Azure Functions extension in VS Code https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions<br>
	iv. Sign in<br>
	v. Click the Create New Project… icon in the Azure: Functions panel.<br>
	vi. Click the Create Function… icon in the Azure: Functions panel, choose a function, eg HTTP Trigger<br>
	vii. Important files - <br>
				function.json - has input and output bindings<br>
				index.js - logic to proccess request and send response, use context.log("Test") fo logging<br>
	viii. To run function:
				`npm start ` The runtime will output a URL for any HTTP functions, which can be copied and run in your browser's address bar.<br><br>
![image](https://user-images.githubusercontent.com/91651033/161309978-03f113ab-0e86-4154-876a-bc01b499db9a.png)
	ix. To deploy the function choose `Deploy to Function App` and choose the App created earlier<br>
	x. Once deployed, we can see it in the Functions pane<br>
	xi. To get the url, click on Get Function URL<br><br>
6. Authorization Levels - stored in function.json as authLevel<br>
		When creating the function, we're prompted with 3 choices:<br>
			i. Function - requires a function specific API key<br>
			ii. Admin  -  global "master" key<br>
			iii. Anonymous - no key<br><br>
		To get the key, under Developer, select Function Keys. The Function Keys pane for your function opens.<br><br>
![image](https://user-images.githubusercontent.com/91651033/161318964-5acc90f4-0adb-4fd5-a82b-4fe57ed55d09.png)<br><br>
		If your Authorization level is set to Function, you can use either a function or a host key. If your Authorization level is set to Admin, you must supply a host key.<br><br>
		This key has to be sent as a query string parameter named code, or as an HTTP header (preferred) named x-functions-key, along with the function url.
