# Deploying Your App to Production

When your app is ready to work in production, please follow the RingCentral app graduation process. The process is designed to ensure that your RingCentral integration works properly and will not cause any bad experience for RingCentral users.

## Step 1: Apply for Production

You will be able to click the 'Apply for production' button as soon as your app meets the following graduation requirements which cover the **last two days** (UTC timezone) &#x2014; yesterday and today. The following requirements are necessary to apply for production:

1. **5+ successful API calls per each endpoint used (20+ in total)**

    Your app is required to send 5 or more successful API requests to each endpoint it uses, but the total number of successful API requests should be 20 or more.

    !!! note "For Example"
        Suppose your app uses only two endpoints:
            
        * `.../extension/{extensionId}/call-log`
        * `.../extension/{extensionId}/presence`
       
        You will need to make 5+ successful requests to each of these endpoints within the last two days, and the total number of requests within these two days should be at least 20.
    
        Let's say yesterday you have made 3 requests to call-log endpoint, and 3 requests to presence endpoint. Then today you can make 2 requests to call-log endpoint (to make it 5) and 12 requests to presence endpoint (to make it 20 in total) to pass.
    
        Please note: OAuth 2.0 requests are not included in these API counts.

2. **Less than 5% of API calls result in 4xx errors**

    Please make sure that you receive `4xx` errors (`400`, `404`, `429`, etc.) in response to **less than 5%** of your API requests during the last two days.

3. **Exercise of all requested permissions**

    We ask you to have made API calls for using all the permissions you have requested, which mean that your app should make at least 1 API call per each permission it has along the minimum API calls per endpoint above.

    You can set and edit the scope/permissions of your app upon app creation and during the development process. It is recommended to only request the permissions your app will actually use.
    
    !!! warning "Editing App Permissions"
        Once your application is published to production, a.k.a. "graduation," you will no longer be able to edit your app's permissions.

    !!! info "For Example"
        You have requested three permissions when you created your app: `ReadCallLog`, `SMS` and `ReadMessages`. After you have completed development, you realized that your app uses `SMS` and `ReadMessages` permissions, but you are not going to be using `ReadCallLog` permission in the first version of your app.

        To graduate your app, you should remove the `ReadCallLog` permission from your app and make at least one API call per each of the permissions you need (within the last two days).

All the requirements above are calculated automatically. You can check your app performance against them in the Status &amp; Review section:
    
<img class="img-fluid" src="../../img/console-status-review.png" style="max-width: 500px">

Once your app meets the above requirements you will be able to apply for production.

## Step 2: Review and Approval

Upon clicking the "Apply for Production" button, your app will officially be submitted for review, at which time a RingCentral staff member will review your application. Reviews are conducted Monday-Friday, for each prior business day's production application requests. Weekend and holiday requests will be reviewed the next available business day.

!!! warning "Editing App Settings"
    You will not be able to change your app settings after you apply, so please check that they are all set to proper values. Make sure that your app has a detailed description, listing its integration purposes and use cases.

!!! note "Facilitating the Review Process"
    Public apps undergo more rigorous testing and review since they can be distributed to many RingCentral accounts. To ensure a smooth review process:
    
    * Include a full and comprehensive description of your app.
    * Provide at least two screenshots when applicable. 
    * Test your application. Consider recruiting beta testers. 

## Step 3. Deployment

Once your app is approved for production, you will receive an email. After that, make sure to change API server URLs and credentials you have been using for sandbox development to production ones (see Credentials section), and you are all ready to go!

