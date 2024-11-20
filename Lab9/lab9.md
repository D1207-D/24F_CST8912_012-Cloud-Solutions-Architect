# CST8912 – Cloud Solution Architecture

## Cloud Development and Operations
**CST8912_013 Cloud Solution Architecture**  
**Lab 9_Week 12**  

### Prepared By:  
Daniyal Shahid (041110791)  

### Submitted to:  
Prof. Ragini Madan  

---

## Graded Lab Activity #9

### Instructions:

### Task 1: Deploy an Azure SQL Database

#### Method 1:
1. Configure Azure SQL database for the Canada Central region under your resource group `cst8912-demo`.  
   Choose **Single Database** under SQL Databases in SQL deployment options.  

2. Enter the following values in the Create Database page (keep other properties at their default settings):  

   - **Subscription**: Select your Azure subscription.  
   - **Resource group**: `CST8912demo`.  
   - **Database name**: `db8912`.  
   - **Server**: Select **Create New** and create a new server with:  
     - Unique name in any Canada Central location.  
     - SQL Authentication.  
     - Specify your name as the server admin login.  
     - Use a suitably complex password (`dfguyt@234!`).  

     Example:  
     - **Server Name**: `db8912demo`.  
     - **Username**: `db8912yourname`.  
     - **Password**: `dfguyt@234!`.  

   - **Want to use SQL Elastic Pool?**: No.  
   - **Workload environment**: Development.  
   - **Compute + Storage**: Leave unchanged.  
   - **Backup storage redundancy**: Locally-redundant backup storage.  

3. On the Create SQL Database page:  
   - Select **Next: Networking >**.  
   - In the **Network Connectivity** section, select **Public Endpoint**.  
   - Set **Yes** for both options under Firewall rules to allow access to your database server from Azure services and your current client IP address.  

4. Select **Next: Security >** and set **Enable Microsoft Defender for SQL** to **Not now**.  

5. Select **Next: Additional Settings >** and set **Use Existing Data** to **Sample** (this will create a sample database to explore later).  

6. Select **Review + Create**, and then click **Create** to create your Azure SQL database.  

---

### Task 2: Configure Advanced Data Protection

1. On the SQL server blade, in the **Security** section, click **Microsoft Defender for Cloud** and select **Enable Microsoft Defender for SQL**.  

2. On the SQL server blade, in the **Security** section, on the **Microsoft Defender for Cloud** page, configure the **Microsoft Defender for SQL** option at the subscription level.  

3. On the Server Settings blade, review details about:  
   - Pricing and trial periods.  
   - **Vulnerability Assessment Settings**.  
   - **Advanced Threat Protection Settings**.  

4. Review **Recommendations** and **Security Alerts** on the Microsoft Defender for Cloud blade.  

---

### Task 3: Configure Data Classification

1. On the SQL server blade, in the **Settings** section, click **SQL Databases**.  
2. On the SQL database blade, in the **Security** section, click **Data Discovery & Classification**.  
3. On the **Data Discovery & Classification** blade, click the **Classification** tab.  
4. Click the text message:  
   *We have found 15 columns with classification recommendations* (displayed on a blue bar at the top).  
5. Review the listed columns and their recommended sensitivity labels.  
6. Select all and click **Accept Selected Recommendations**.  
7. After completing your review, click **Save**.  
8. On the **Overview** tab, verify that the classification information has been updated.  

---

### Task 4: Configure Auditing

1. Navigate back to the **SQL Server** blade.  
2. In the **Security** section, click **Auditing**.  
3. Set **Enable Azure SQL Auditing** to **ON**.  
4. Enable **Storage** and create a new storage account if necessary.  
5. Set **Retention (days)** to `5`.  
6. Save the auditing settings.  

#### Database-level Auditing:  
7. On the **SQL Database** blade, enable auditing.  
8. On the database **Overview** page, use the **Query Editor (Preview)**:  
   - Test failed login attempts (check firewall and password issues).  
   - Test successful logins and execute queries.  

9. Check **Audit Logs** under the **Auditing** section.  

---

### Task 5: Clean Up Resources  
- Delete all the resources created during this lab.  
- Document the steps with screenshots in the lab report.  

---

## Conclusion

In this lab, we explored how Microsoft Azure provides powerful tools to secure databases and protect sensitive information. By deploying an Azure SQL Database and leveraging features like Microsoft Defender for SQL, data classification, and auditing, we created a robust and compliant environment. These tools not only shield against threats like unauthorized access and SQL injection but also help meet privacy standards like GDPR. Auditing keeps an eye on database activities to catch unusual behavior, while data classification ensures sensitive information is properly handled. Wrapping up by cleaning resources helps keep costs down and Azure environments organized.  

---

### Business Use Case: Safeguarding Customer Data in Banking

Imagine a bank managing sensitive data like account details and personal information. With strict regulations like GDPR and PCI DSS to follow, it also needs to ensure customer trust by protecting against breaches. Azure SQL Database offers the tools to do just that:  

- **Classify Sensitive Data**: Automatically flag critical information for secure handling.  
- **Audit Activity**: Track database use to catch unauthorized access.  
- **Stay Ahead of Threats**: Real-time alerts help prevent attacks like SQL injections.  
- **Encrypt Data**: Keep stored information secure, even if hardware is compromised.  

By using these features, the bank can confidently protect its customers, meet compliance requirements, and maintain trust while controlling costs.  


