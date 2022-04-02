1. What is a trigger?<br>
  A trigger is an object that defines how an Azure Function is invoked. <br>
  For example, if you want a function to execute every 10 minutes, you could use a timer trigger.<br><br>
  Every function must have exactly one trigger associated with it. If you want to execute a piece of logic that runs under multiple conditions,
you need to create multiple functions that share the same core function code.

2. What is a binding?<br>
  A binding is a connection to data within your function. <br>
  Bindings are optional and can be input bindings, output bindings, or both. <br>
  An input binding is the data that your function receives. An output binding is the data that your function sends. <br>
  Unlike a trigger, a function can have multiple input bindings and output bindings.<br><br>

3. Timer Trigger Basics<br>
A timer trigger is a trigger that executes a function at a consistent interval. <br>
To create a timer trigger, you need to supply two pieces of information:<br>
  i. A Timestamp parameter name, which is simply an identifier to access the trigger in code.<br>
  ii. A Schedule, which is a CRON expression that sets the interval for the timer.<br>
      The order of the six fields in Azure is: {second} {minute} {hour} {day} {month} {day of the week}.<br>
      eg :`0 */5 * * * *` - every five minutes<br><br>
      ![image](https://user-images.githubusercontent.com/91651033/161362876-f99555d1-0991-41d6-bad6-947ae78f5d5b.png)<br><br>
 4.Creating the function:<br>
  i. Create Function > Timer Trigger > Name > Cron Expression<br>
  ii. Deploy the function<br>
  iii. Now the function runs as per the cron schedule, to see the output, go to Function page > Monitor > Logs:<br><br>
![image](https://user-images.githubusercontent.com/91651033/161363684-41d01253-4112-4b17-915a-e7107b6d5d71.png)

