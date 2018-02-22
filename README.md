# Guide to create a memo site

**Memo site**

Azure Web App hosted on Azure App Service, the site can scale on high load maintaining availability. The App Service enables schedule scaling, on demand scaling as well as automated scaling.

**Queue Service**

Azure Storage Queue queues messages and save it in Azure storage.

**Triggering email**

Azure functions enables server-less trigger calls to send out alerts. Azure function allows code portability if design is to be hosted on premise.

**Redis Cache**

Redis cache enables faster data stream and improve data load time

**Database**

Storing data in Azure SQL DB enables portability and cost saving compared to maintaining a database in VM. Storing data in one database also enables the database to scale easily.

**Document Storage**

Azure App Service streams request to Azure Blob Storage for storing completed memo and corresponding documents. Recommended for better security and easier management.

**Logging**

Resource monitoring made easy using Azure Monitor. It allows easy monitoring of resources health and can be configured to send out alerts.

|   | **Features** | **Description** | **Tasks** |
| --- | --- | --- | --- |
| 1 | Storing attached documents | Store into blob storage | Code to authenticate, verify and store using REST API [https://docs.microsoft.com/en-us/azure/storage/common/storage-rest-api-auth](https://docs.microsoft.com/en-us/azure/storage/common/storage-rest-api-auth) Alternatively, you can use Shared Access Token SAS [https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1](https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1) |
|   | Retrieving attached documents | Retrieve from blob storage | Code to allow authenticated user to read document file from blob storage (HTTP Handler) [https://farooqmdotcom.wordpress.com/2012/09/06/http-handlers-and-windows-azure-web-roles](https://farooqmdotcom.wordpress.com/2012/09/06/http-handlers-and-windows-azure-web-roles) |
| 2 | Queue user memo (Read) | Queue message for storage | Azure function to read message from queue [https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-storage-queue-triggered-function](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-storage-queue-triggered-function) |
|   | Queue user memo (Write) | Queue message for storage | Code to send message to queue, verify &amp; store in Azure storage [https://docs.microsoft.com/en-us/azure/architecture/best-practices/retry-service-specific](https://docs.microsoft.com/en-us/azure/architecture/best-practices/retry-service-specific)  |
| 3 | Trigger function | Function to send to queue | Create code to send message to Queue in an Azure Function [https://docs.microsoft.com/en-us/azure/azure-functions/functions-integrate-storage-queue-output-binding](https://docs.microsoft.com/en-us/azure/azure-functions/functions-integrate-storage-queue-output-binding) |
|   |   | Function to check mail server | Create a Timer based Azure function to &#39;check&#39; the mail Server.... Write to monitor. Business logic to be completed later [https://contos.io/monitoring-exchange-activesync-with-azure-functions-34fc4d13401c](https://contos.io/monitoring-exchange-activesync-with-azure-functions-34fc4d13401c) |
|   |   | Configure CI CD | Configure Continuous Integration deployment from Git for the Azure Functions [http://gaunacode.com/azure%20functions/ci/cd/devops/2018/01/02/CICDAzureFunctions.html](http://gaunacode.com/azure%20functions/ci/cd/devops/2018/01/02/CICDAzureFunctions.html) |
| 4 | Caching | Caching from database | Lazy load REDIS Cache from SQL DB **Using Node.js** [https://docs.microsoft.com/en-us/azure/redis-cache/cache-nodejs-get-started](https://docs.microsoft.com/en-us/azure/redis-cache/cache-nodejs-get-started) **Using .NET** [https://docs.microsoft.com/en-us/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache](https://docs.microsoft.com/en-us/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache) |
| 5 | Logging | Create logs | Sample code to write to Azure Monitoring log from both Website and Azure function**Azure monitor walkthrough** [https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-get-started](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-get-started) |
|   |   | Create log rules | Configure example Monitoring rules and alerts in Azure Monitoring  **Creating an alert** [https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitor-quick-resource-metric-alert-portal](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitor-quick-resource-metric-alert-portal) |
|   |   | Storing logs | Configure log storage in a container  **Archiving monitor data to storage** [https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitor-tutorial-archive-monitoring-data](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitor-tutorial-archive-monitoring-data) |
| 6 | Storing data | Deploying database | Deploy DB to a Basic Elastic Pool for DevTest [https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-pool](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-pool)  |
|   |   | Read &amp; write to database | Read &amp; write to DB with appropriate schema |
| 7 | MyMemo Site deployment | Deploying web app | Deploy App to Basic App Service with two instances  **Deploy with Git** [https://docs.microsoft.com/en-us/azure/app-service/app-service-deploy-local-git](https://docs.microsoft.com/en-us/azure/app-service/app-service-deploy-local-git)  |
|   |   | Configure web app | Configure app to have two deployments one for &#39;Development&#39; one for &#39;Staging&#39; [https://docs.microsoft.com/en-us/azure/app-service/web-sites-staged-publishing](https://docs.microsoft.com/en-us/azure/app-service/web-sites-staged-publishing) |
|   |   | Configure CI CD | Configure app to have continuous integration deployment for &#39;Development&#39; one for &#39;Staging&#39; [https://blogs.msdn.microsoft.com/mvpawardprogram/2017/05/16/deploy-app-azure-app-service/](https://blogs.msdn.microsoft.com/mvpawardprogram/2017/05/16/deploy-app-azure-app-service/) |
|   |   | Configure CI CD | Configure Continuous Integration deployment from Git for the Azure Web App [https://docs.microsoft.com/en-us/azure/app-service/web-sites-staged-publishing](https://docs.microsoft.com/en-us/azure/app-service/web-sites-staged-publishing) |
| 8 | Code repo | Create code repository | Provision and configure bitbucket for code repository and integration with Jenkins  **Bitbucket** [https://confluence.atlassian.com/get-started-with-bitbucket/set-up-a-repository-861178557.html](https://confluence.atlassian.com/get-started-with-bitbucket/set-up-a-repository-861178557.html) **Jenkins** [https://jenkins.io/doc/pipeline/tour/hello-world/](https://jenkins.io/doc/pipeline/tour/hello-world/)  |