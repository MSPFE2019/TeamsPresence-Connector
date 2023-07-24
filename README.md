Here is your revised text with added links to official Microsoft documents:

The custom connector has been explicitly programmed to retrieve a user's Teams Presence information - data that indicates the user's availability and status to other users on Microsoft Teams. This encompasses statuses such as Available, Busy, Do Not Disturb, and Away, among others. This information can be accessed by providing the unique user ID number associated with each individual Teams user.

[Azure Application Registration](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app) & Granting Rights to Teams User Presences Information
This guide will walk you through the process of creating an Azure Application Registration and granting it rights to access Microsoft Teams user presence information.

Prerequisites
- An active Azure account with the necessary privileges to create an application registration.
- An active Microsoft 365 account with Teams for testing.

Steps
1. Registering a new Azure App
   - Log in to your Azure account and navigate to the Azure Active Directory section.
   - From the left sidebar, select "App registrations".
   - Click "New registration" to start creating a new application.
   - Enter your application's name, choose the supported account types and redirect URI (if applicable).
   - Click "Register" to finalize the creation of your app.
   - After your app has been created, you will be redirected to your app's dashboard. Here, take note of the Application (client) ID and Directory (tenant) ID as you'll need them later.

2. Granting API Permissions
   - From the left sidebar in your app's dashboard, select "API permissions".
   - Click on the "Add a permission" button.
   - In the panel that opens, choose "Microsoft Graph".
   - Choose the type of permission your app needs. For accessing Teams user presence information, you'll most likely need "Delegated permissions".
   - In the search box, enter "Presence.Read.All" to find the necessary permission.
   - Check the box next to "Presence.Read.All" and click "Add permissions" at the bottom of the panel.
   - Back on the "API permissions" page, click "Grant admin consent for {your_directory}".

3. Creating Client Secret
   - From the left sidebar in your app's dashboard, select "Certificates & secrets".
   - Click on the "New client secret" button.
   - Enter a description for the client secret, select its expiry duration and click "Add".
   - After the secret is created, make sure to copy its value and store it securely. You will not be able to retrieve it after leaving the page.

4. Configuring and Testing Your App
   - Now, with your Application (client) ID, Directory (tenant) ID, and client secret, you can authenticate your app and make API calls to Microsoft Graph API to fetch Teams user presence information.
   - Download the custom connector files. To import the custom connector files into Power Platform, follow these steps:
       - In Power Automate, go to Data > Custom connectors.
       - Click New custom connector.
       - Select "Import an OpenAPI file".
       - Set Connector Name
       - Browse to the directory where you downloaded the custom connector file.
       - Upload the "Teams-Presence-API.swagger" file
       - Click Import.
       - On the general tab ensure that the host has "graph.microsoft.com" listed, add if missing.
       - Proceed to the "Security" tab
       - Authentication type should be "OAuth 2.0"
       - Under OAuth 2.0 section here are the values you check and fill out
           - Id Provider is "Azure Active Directory"
           - Client ID (from your app registration)
           - Authorization Url - https://login.microsoftonline.com
           - Common - skip
           - Resource URL - https://graph.microsoft.com
       - After all the blocks have been filled out, click "Create connector" in the top right-hand side.
       - Copy the redirect URL value, you need this for App registration.
       - Please proceed to the Test Tab.
       - Create a new connection.
       - Under User Presence paste ID number of users from Azure AD.
       - Test Operation, if you get a 200 with the users' status, setup is complete.
       - Click on "Update connector" and "Close" once saving is completed.

You are now able to use this connector in your environment for any power app or power automate. Please note you only need to pass the user's Azure AD id number to the connector to return data.


Disclaimer: Be sure to handle sensitive information such as client secrets with care. Never expose these values in public repositories, logs, or other insecure locations.
