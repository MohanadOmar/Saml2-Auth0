# Configure Auth0
When you signed up for Auth0, a new application was created for you, or you could have created a new one. You will need some details about that application to communicate with Auth0. You can get these details from the Application Settings section in the Auth0 dashboard.
You need the following information:
- Domain
- Client ID
- Client Secret
## Configure Callback URLs
A callback URL is a URL in your application where Auth0 redirects the user after they have authenticated. The callback URL for your app must be added to the Allowed Callback URLs field in your Application Settings. If this field is not set, users will be unable to log in to the application and will get an error.
## Configure Logout URLs
A logout URL is a URL in your application that Auth0 can return to after the user has been logged out of the authorization server. This is specified in the returnTo query parameter. The logout URL for your app must be added to the Allowed Logout URLs field in your Application Settings. If this field is not set, users will be unable to log out from the application and will get an error.

# Install dependencies
- flask>=2.0.3
- python-dotenv>=0.19.2
- authlib>=1.0
- requests>=2.27.1

# Configure your .env file
📁 .env -----

AUTH0_CLIENT_ID=[YOUR AUTH0_CLIENT_ID FROM YOUR APPLICATION SETTINGS]
AUTH0_CLIENT_SECRET=[YOUR AUTH0_CLIENT_ID FROM YOUR APPLICATION SETTINGS]
AUTH0_DOMAIN=[YOUR AUTH0_DOMAIN FROM YOUR APPLICATION SETTINGS]
APP_SECRET_KEY=(Generate a suitable string for APP_SECRET_KEY using openssl rand -hex 32 from your shell.)

# Setup your application
### Now you're ready to start writing your application. Create a server.py file in your project directory - this file will hold all of your application logic.

Begin by importing all the libraries your application will be making use of:
📁 server.py -----

import json
from os import environ as env
from urllib.parse import quote_plus, urlencode

from authlib.integrations.flask_client import OAuth
from dotenv import find_dotenv, load_dotenv
from flask import Flask, redirect, render_template, session, url_for

### Next, your application will need to load the configuration .env file you made in the previous step:
👆 We're continuing from the steps above. Append this to your server.py file.

ENV_FILE = find_dotenv()
if ENV_FILE:
    load_dotenv(ENV_FILE)

### Now you can configure Flask for your application's needs:
👆 We're continuing from the steps above. Append this to your server.py file.

app = Flask(__name__)
app.secret_key = env.get("APP_SECRET_KEY")

### Finally, you can now configure Authlib to handle your application's authentication with Auth0:
👆 We're continuing from the steps above. Append this to your server.py file.

oauth = OAuth(app)

oauth.register(
    "auth0",
    client_id=env.get("AUTH0_CLIENT_ID"),
    client_secret=env.get("AUTH0_CLIENT_SECRET"),
    client_kwargs={
        "scope": "openid profile email",
    },
    server_metadata_url=f'https://{env.get("AUTH0_DOMAIN")}/.well-known/openid-configuration'
)


