## Overview

The Database created for this project is an RDS instance powered by MySQL 8. Any updates to MySQL will run automatically and a backup will be preformed on a weekly basis. Connecting to the Database requires a few additional steps so consult with the backend engineer if you require access. At the moment, all data is stored within two databases and the lambda functions created access the necessary data.

## Creating a Database - Steps to follow in order to replicate the DEV/TEST SErver instances created currently.

#### Selecting the tier
<img width="1280" alt="screen shot 2019-01-16 at 2 33 37 pm" src="https://user-images.githubusercontent.com/20977403/51273911-d70ba280-199b-11e9-8e24-8777da820fd2.png">

#### Settings
The RDS is running MySQL 8.1 and is stored under our VPC within a datalayer security group.

#### Connecting to the MySQL Workbench after creation

Step-by-step instructions can be found at https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ConnectToInstance.html. 

Make sure that you have your IP address whitelisted in the **DATALAYER** security group. I you are unsure of this then consult with your backend engineer and ask them to whitelist it for you. Any changes should go through the backend engineer since the RDS instance is 

