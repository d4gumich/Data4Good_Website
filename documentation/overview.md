# Overall

 The documents contained in this folder outline how the backend of the webpage is created and where the webpage is located. Details in each file will show how you can make changes to the webpage and all the various backend components of the Data4Good.center webpage.
 
# Folders

## css
Contains all the code pertaining to the CSS elements of the webpage

## Documentation
### Backend
Here you will find all the documents outlining the architecture of the webpage in AWS from a backend persepctive. Most of the documentation contains links that helped in the construction of the backend hookups. Please consult your backend engineer if there are other questions that you have about AWS specifically. The documentation from AWS is pretty robust, however I tried to outline everything I found to be useful when creating the backend.

## img
These are pretty self explanitory, but this directory contains all the images for the webpage (i.e. static images and banner video).

## js
Contains all the javascript files for the dinamic assets such as contact us and the bubble chart.

## libs
Contains the various libraries used for the charts with `.js` and `.css`. Shouldn't need to modify these moving forward.

## mail
I believe we can get rid of this, however, I don't want to just yet until I get more familiar with the code. This PHP script should be legacied with the AWS Lambda function I created and hooked up in the `contact.html` page.

## vendor
Contains all the bootstrap elements, fonts, and jquery.

# Files
## 404
HTML for if the webpage was not reached/down.

## about
Contains the mission statement, our pictures, descriptions, mainly anything relating back to about us

## audience
**IN PROGRESS**. This contains data, queries, projects, pertaining to what has been worked on. Selection of the role dictates what the user would be getting back. 

## blog-home-1 & 2
**IN PROGRESS**. This will be where we release projects to the public. 

## contact
Contains the `Contact Us` elements that fires off the lambda function created. More details on this can be found under `documentation/backend/email.md`.

## data
**IN PROGRESS**. Where datasets will be realeased from in the future.

## events
Code contains the embedding of the UMSI calendar and what events are coming up.

## faq
Goes without saying this contains Frequently Asked Questions

## index
This is the main landing of the webpage. The index.html is what the user sees if the go to data4good.center in their browser. All changes to this page will be reflected across the webpage.

## sidebar
Sidebar elements


