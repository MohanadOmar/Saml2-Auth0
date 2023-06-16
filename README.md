# Configure Auth0
When you signed up for Auth0, a new application was created for you, or you could have created a new one. You will need some details about that application to communicate with Auth0. You can get these details from the Application Settings section in the Auth0 dashboard.
You need the following information:
- Domain
- Client ID
- Client Secret
## Configure Callback URLs
A callback URL is a URL in your application where Auth0 redirects the user after they have authenticated. The callback URL for your app must be added to the Allowed Callback URLs field in your Application Settings. If this field is not set, users will be unable to log in to the application and will get an error.
##Configure Logout URLs
A logout URL is a URL in your application that Auth0 can return to after the user has been logged out of the authorization server. This is specified in the returnTo query parameter. The logout URL for your app must be added to the Allowed Logout URLs field in your Application Settings. If this field is not set, users will be unable to log out from the application and will get an error.

##Install dependencies
- flask>=2.0.3
- python-dotenv>=0.19.2
- authlib>=1.0
- requests>=2.27.1
