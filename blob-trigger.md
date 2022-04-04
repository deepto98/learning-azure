1. What is a blob trigger?<br>
  A blob trigger is a trigger that executes a function when a file is uploaded or updated in Azure Blob storage. <br>
  To create a blob trigger, you create an Azure Storage account and provide a location that the trigger monitors. <br>

2. Azure Blob Storage Basics?<br>
  Azure Blob storage is an object storage solution that's designed to store large amounts of unstructured data. <br>
  Bindings are optional and can be input bindings, output bindings, or both. <br>
  There are three types of blobs: <br>
    i. Block blobs are the most common type. They allow you to store text or binary data efficiently. <br>
    ii. Append blobs are like block blobs, but they're designed more for append operations like creating a log file 
       that's being constantly updated. <br>
    iii. Page blobs are made up of pages and are designed for frequent random read and write operations. <br>
	Path:
	Path tells the blob trigger where to monitor to see if a blob is uploaded or updated. By default, the Path value is:<br>
	`samples-workitems/{name}`: samples-workitems is the blob container that the trigger monitors,
	 {name} means that every type of file will cause the trigger to invoke the function<br>
	 `samples-workitems/{name}.png` - only png files will cause the trigger to invoke the function
	 Azure function receives the filename as a string through a parameter called `name`.
