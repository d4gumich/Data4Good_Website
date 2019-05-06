## Overview

The Database created for this project is an RDS instance powered by MySQL 8. Any updates to MySQL will run automatically and a backup will be preformed on a weekly basis. Connecting to the Database requires a few additional steps so consult with the backend engineer if you require access. At the moment, all data is stored within two databases and the lambda functions created access the necessary data.

## Creating a Database - Steps to follow in order to replicate the Production Server instance created currently.

#### Selecting the tier
<img width="1280" alt="screen shot 2019-01-16 at 2 33 37 pm" src="https://user-images.githubusercontent.com/20977403/51273911-d70ba280-199b-11e9-8e24-8777da820fd2.png">

#### Settings
The RDS is running MySQL 8.1 and is stored under our VPC within a datalayer security group.

#### Connecting to the MySQL Workbench after creation

Step-by-step instructions can be found at https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ConnectToInstance.html. 

Make sure that you have your IP address whitelisted in the **DATALAYER** security group.

#### Whitelisting IP

**This step should be only touched by the backend engineer. If you require access to the API please consult them first before touching any of this**

First you will want to navigate to the `VPC` reosurce on the AWS console. Now that you are in the `Virtual Private Cloud (VPC)` settings, select `Security Groups` on the left sidebar (found under `Security`). Select the VPC name `PROD-DataLayer`. At the bottom of your screen you should see four tabs like the image below. Click on `Inbound Rules` and click `edit`. The top IP address with the description that states to "change this as needed" is the one you can modify. **DO NOT TOUCH THE OTHER ONE**.
![screen shot 2019-03-03 at 11 01 26 am](https://user-images.githubusercontent.com/20977403/53697887-f3c13580-3da3-11e9-9e71-c55fd713b99c.png)

The simple way to add your IP address is to select the `Source` tab and select `My IP`. This will automatically fill in your IP address to the Inbound whitelist rules. Click save to complete the changes and you are all set. 

#### Using the terminal to access the RDS

`mysql -h <RDS_HOST_NAME> -P <PORT> -u <MASTER_USERNAME> -p`

* <RDS_HOST_NAME>: Can be found in the RDS instance
* <PORT>: Can be found in the RDS instance
* <MASTER_USERNAME>: Get from your team
* -p: This is the password to get into the RDS instance. Get from your team.
  
#### Dumping SQL.dump File into RDS

`mysql -h <RDS_HOST_NAME> -P <PORT> -u <MASTER_USERNAME> -p <DATABASE_NAME> < <PATH/TO/DUMP.SQL>`

* <RDS_HOST_NAME>: Can be found in the RDS instance
* <PORT>: Can be found in the RDS instance
* <MASTER_USERNAME>: Get from your team
* -p: This is the password to get into the RDS instance. Get from your team.
* <DATABASE_NAME>: The database you want to dump new data into
* <PATH/TO/DUMP.SQL>: Path to where you have the dump.sql file stored

