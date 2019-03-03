## Overview

The API is created in an agnostic language through AWS. AWS uses API's through their service called the `API Gateway`. Here you can create various API's or endpoints with different methods all to one API. To get to the API Gateway, you will need to search for the API Gateway in the services section of the console. 

**Important**
If you are planning on hooking up a new lambda function, you must first create the API and then hook it into the new Lambda function. We will go over this in greater detail later on.

## Current Architecture

Currently, there is only one API created for the webpage called `emailfwd-API`. I originally created this API as a test for the email forwarding aspect of the API following the instructions that can be found at https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-create-api.html. Here AWS walks through how to create a REST API within AWS as it is much different than using Django, Flask, or ASP.NET Core.

## Creating a new API

AWS makes this process very simple. 

1) First click on the `Create API` button as shown below
<img width="650" alt="screen shot 2019-01-15 at 12 56 30 pm" src="https://user-images.githubusercontent.com/20977403/51199661-59756300-18c5-11e9-84cb-6a5e36241f16.png">

2) After you will be prompted with some settings of the API. You will want to select `REST API` and **NOT** `WebSocket`. Second, you will have the choice of either creating this API from scratch, cloning one of the existing API's, or importing from Swagger. I would ignore the last two unless you have a good handle on Swagger and API's. Plus, you might want to play around with the options of creating an API from scratch here in AWS to get more familiar with the options.


## Adding a Stage 

In AWS, endpoints are called `stages`. In the example shown below, the email forward API (which will need to be refactored later once we have more endpoints to create one REST endpoint for the application) has one called `default`.
<img width="1130" alt="screen shot 2019-01-15 at 1 18 21 pm" src="https://user-images.githubusercontent.com/20977403/51200722-4ca63e80-18c8-11e9-9d62-c1613f3317c4.png">

To create a new stage, click the `Create` button when you have one of the stages highlighted. Once you click on the `Create` button, you will need to specify the stage name (prod, beta, test, etc.) Generally, you wont be creating a new stage unless the API requires backend changes without impacting the production enviornment that users will be interacting with. 

#### Exporting

When we get to a place where testing of the endpoints and API is required, we can export the stage under the `Export` tab. Under this you will have a few options, but I would recommend to export as `Swagger + Postman Extensions` This will allow testing through Postman (an API GUI that will be much cleaner and simpler to use than testing within AWS).


# Creating from Scratch. **The above was a special case for the contact us page
**
## Adding a Method

To add a method to a stage, navigate to the left tabs and select `Resources`. Once there you will have access to creating an endpoint and a the various resources to each.
<img width="690" alt="screen shot 2019-01-15 at 1 42 27 pm" src="https://user-images.githubusercontent.com/20977403/51201950-6eed8b80-18cb-11e9-82de-7348405c5975.png">

When creating a Method, take into consideration the `ANY` field and what roles might need to be applied to them. For example, the method shown below has a role of `AWS_IAM` since there is authorization needed for the `POST` process to go through.

When you are creating a new resource, be sure to have the `/` highlighted or else the new method/resource will be a sub-method/resource of the one that you had selected. AWS acts in dot directory notation much like UNIX if you familiar with those.

## Hooking it into the lambda function

AWS makes hooking up a lambda function into an API gateway very straight forward. First you want to navigate to the designer of the lambda function. 

* Figure 1
<img width="983" alt="screen shot 2019-01-15 at 2 29 33 pm" src="https://user-images.githubusercontent.com/20977403/51204773-5b91ee80-18d2-11e9-93e5-df34348f5f20.png">

In Figure 1, you see how there are multiple triggers than can kick off a lambda function. For this demonstration however, we will only focus on the API Gateway. Once you drag the API Gateway as a trigger of the lambda, select it to launch into the settings of the API gateway.

<img width="1160" alt="screen shot 2019-01-15 at 2 36 05 pm" src="https://user-images.githubusercontent.com/20977403/51204998-f25eab00-18d2-11e9-9dd0-37d87906c1bc.png">

Shown above are the settings of the API Gateway in the lamdba function. Once here, you can remove methods that were imported that you no longer need. If a new method/resource is added in then you will need to follow the steps above again and import the API once more as a trigger.

## Creating A New Resource

A resource is a new endpoint within the main API. The basic layout is `baseURL/<resource>` much like what we've seen when interacting with the Twitter, Flickr, or Reddit APIs. To create a new resource, first you will want to navigate to the API Gateway within the AWS Console. Next you will select the main API we use (in this case the `emailfwd-API`) and click on `Resources` on the left sidebar. After this, make sure you have the top `/` highlighted before clicking on the `Actions` button and selecting `Create Resource`. This will create the resource as a child under the baseURL shown below.

![createresource0](https://user-images.githubusercontent.com/20977403/53697247-94602700-3d9d-11e9-9294-02bba4bf2e2c.png)

Next you will give your resource a name and then click `Finish`. 

![ccreateresource1](https://user-images.githubusercontent.com/20977403/53697335-5adbeb80-3d9e-11e9-9bdc-6eff69d82b5b.png)

## Adding a Method

Now that we have the new Resource created, we are going to add a new method to the new resource. In this case we are going to add a `GET` since the main purpose of this function is to retrieve and send back data to the webpage. First you want to highlight the resource. Next, click on `Actions` and select `Create Method` (shown below)
![createmethod0](https://user-images.githubusercontent.com/20977403/53697341-64655380-3d9e-11e9-9d14-71619d7c54c6.png)

After you have the method added, navigate to the drop down selection and select which type of method you intend to create. Like I stated above, I created a `GET` as the purpose was to retrieve data. There are a host of different ones such as `POST`, `PUT`, `ANY`, etc. These all follow the traditional methods for APIs. After selecting `GET` we now need to configure the method. In this case we want to hook up the trigger to the lambda function for pulling data. Because of this, I have selected `Lambda Function` and searched for the one I want to add to it. This automatically adds the trigger to the lambda function. 

![createmethod1](https://user-images.githubusercontent.com/20977403/53697429-f0777b00-3d9e-11e9-94d2-880d1fac33ba.png)

## Deployment
Now that we have the new Resource created with the methods for our purpose, we can deploy the API. Navigate to the `Actions` button and select `Deploy API`. 
![deployapi](https://user-images.githubusercontent.com/20977403/53697442-2288dd00-3d9f-11e9-8650-05a23b2125df.png)

At this point you will be asked which stage you want to deploy it to. For our purposes, we have `default` set up as the production enviornment since we don't require a test/beta stage at this point. 
You can now test if the endpoint works as intended by navigating to the `Stages` section on the left sidebar. Select the `default` stage, click on the new resource + method combo, then click on the endpoint URL at the top. This URL invokes the function in your web browser. If it all works correctly, you should see your data from the query (in this case for `GET`) in your web browser.