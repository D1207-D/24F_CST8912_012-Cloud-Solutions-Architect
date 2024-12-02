
# CST8912 – Cloud Solution Architecture

## Cloud Development and Operations  
**CST8912_013 Cloud Solution Architecture**  
**Lab 10_Week 13**

### Prepared By:  
Daniyal Shahid (041110791)  

### Submitted to:  
Prof. Ragini Madan  

---

## Graded Lab Activity #10

### Problem Statement:
I have a storage account in Azure. In the container, we are storing various data files. The files are stored in a tree hierarchy of folders (Parent -> year -> month -> day). Each day, new files get uploaded to the specific day folder. If the file for that specific day is not uploaded, I would like to drop an email notification.

---

## Task 1:
1. Create a Logic App (choose consumption-based plan) and an SQL database instance in the Canada Central region.  

![Lab10](./images/1.png)

![Lab10](./images/2.png)

![Lab10](./images/3.png)

![Lab10](./images/4.png)

![Lab10](./images/5.png)

![Lab10](./images/6.png)

2. Create an `alerts` table in the SQL database using the query editor.  

![Lab10](./images/7.png)


3. Insert records into the `alerts` table using the query:

```sql
Insert into [dbo].[Alerts] (ToAddress,MailSubject,MailBody,EmailSent) 
values ('youremail','demoApp1','This is message body1',0)
go

Insert into [dbo].[Alerts] (ToAddress,MailSubject,MailBody,EmailSent) 
values ('youremail','demoApp2','This is message body2',0)
go

Insert into [dbo].[Alerts] (ToAddress,MailSubject,MailBody,EmailSent) 
values ('youremail','demoApp3','This is message body3',0)
go
```

![Lab10](./images/8.png)


4. Select rows from the `alerts` table to verify the records inserted in the table.

![Lab10](./images/9.png)


5. Go to the Logic App created in the lab.  
6. Use the Recurrence trigger and define values for interval (3) and frequency (minute).  

![Lab10](./images/10.png)


7. Add a new step named “SQL Server,” and use “Get Rows” as the action.  
8. Enter the credentials (in the background, connectors are getting created). Enter your server name (FQDN), database name, username, and password.  

![Lab10](./images/11.png)

![Lab10](./images/12.png)

![Lab10](./images/13.png)

9. Add a new step `For-Each` in the Logic App.  
10. Select the `Value` parameter from Dynamic Content.  
11. Add a `Send Mail` action.  
12. Enter the details from Dynamic Content (refer to values from columns defined in the `alerts` table).  
13. Save the Logic App.  
14. Wait for some time, and you will receive an email.  

![Lab10](./images/14.png)

![Lab10](./images/15.png)


---

## Task 2:
### Design a logic to trigger an email notification in your Outlook when the file for a specific folder does not get uploaded by a specific time.
1. Create a storage account in the Canada Central region.  

![Lab10](./images/16.png)

![Lab10](./images/17.png)


2. Create a sample container, and within that container, create a folder in the format of `yyyy-mm-dd`. 
 
![Lab10](./images/18.png)

![Lab10](./images/19.png)

![Lab10](./images/20.png)


3. Create a trigger to schedule this logic every day at 6 PM.  

![Lab10](./images/21.png)
![Lab10](./images/22.png)
![Lab10](./images/23.png)
![Lab10](./images/24.png)

4. Use `List Blob` to check every file in the folder. To check the file in the folder, you can use the expression like:  
   ```
   concat('/', utcNow('yyyy/MM/dd'))
   ```  
   If the file in the path does not exist, `List Blob` will fail.  

![Lab10](./images/25.png)

![Lab10](./images/26.png)


5. Send an email to your email address in Outlook if `List Blob` fails.  

---

## Task 3:
Monitor workflows in Azure Logic Apps.

![Lab10](./images/27.png)


---

## Task 4:
Clean all the resources created during this lab and record all the steps with screenshots in the lab report.


![Lab10](./images/28.png)


