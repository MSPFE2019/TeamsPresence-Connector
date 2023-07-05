# TeamsPresence-Connector
The custom connector has been explicitly programmed to retrieve a user's Teams Presence information - data that indicates the user's availability and status to other users on Microsoft Teams. This encompasses statuses such as Available, Busy, Do Not Disturb, and Away, among others. This information can be accessed by providing the unique user ID number associated with each individual Teams user.


# Azure Application Registration & Granting Rights to Teams User Presences Information

This guide will walk you through the process of creating an Azure Application Registration and granting it rights to access Microsoft Teams user presence information.

## Prerequisites
- An active Azure account with the necessary privileges to create an application registration.
- An active Microsoft 365 account with Teams for testing.

## Steps

### 1. Registering a new Azure App
1. Log in to your Azure account and navigate to the Azure Active Directory section.
2. From the left sidebar, select "App registrations".
3. Click "New registration" to start creating a new application.
4. Enter your application's name, choose the supported account types and redirect URI (if applicable).
5. Click "Register" to finalize the creation of your app.
6. After your app has been created, you will be redirected to your app's dashboard. Here, take note of the Application (client) ID and Directory (tenant) ID as you'll need them later.

### 2. Granting API Permissions
1. From the left sidebar in your app's dashboard, select "API permissions".
2. Click on the "Add a permission" button.
3. In the panel that opens, choose "Microsoft Graph".
4. Choose the type of permission your app needs. For accessing Teams user presence information, you'll most likely need "Delegated permissions".
5. In the search box, enter "Presence.Read.All" to find the necessary permission.
6. Check the box next to "Presence.Read.All" and click "Add permissions" at the bottom of the panel.
7. Back on the "API permissions" page, click "Grant admin consent for {your_directory}".

### 3. Creating Client Secret
1. From the left sidebar in your app's dashboard, select "Certificates & secrets".
2. Click on the "New client secret" button.
3. Enter a description for the client secret, select its expiry duration and click "Add".
4. After the secret is created, make sure to copy its value and store it securely. You will not be able to retrieve it after leaving the page.

### 4. Configuring and Testing Your App
Now, with your Application (client) ID, Directory (tenant) ID, and client secret, you can authenticate your app and make API calls to Microsoft Graph API to fetch Teams user presence information.

**Note:** Ensure your Teams users have the necessary permissions set to allow your application to access their presence information.

## Conclusion
By following these steps, you should now have an Azure App with rights to access Microsoft Teams user presence information. This guide is written with GitHub Markdown in mind, you can add more images and links as you find necessary for your documentation.

For more information, you may refer to the official [Microsoft Documentation](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app).

**Disclaimer:** Be sure to handle sensitive information such as client secrets with care. Never expose these values in public repositories, logs, or other insecure locations.
