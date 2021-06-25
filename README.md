# EmailApi
A django project to read a email's via using email api
First you need a Python3.6 or above version install on your system.
then Go throught this link and create the google developer account 
https://developers.google.com/workspace/guides/create-project
by using this documentation you should be able to create a project on googel work space.
After then 
Authorization credentials for a desktop application. To learn how to create credentials for a desktop application, refer to https://developers.google.com/workspace/guides/create-credentials
Then you should need A Google account with Gmail enabled
# Now let's jump our coding part.
Step 1: Install the Google client library
To install the Google client library for Python, run the following command:
  pip install --upgrade google-api-python-client google-auth-httplib2 google-auth-oauthlib
  
  
Step 2: Configure the sample
To configure the sample:

In your working directory, create a file named quickstart.py.
Include the following code in quickstart.py:
#example


from __future__ import print_function
import os.path
from googleapiclient.discovery import build
from google_auth_oauthlib.flow import InstalledAppFlow
from google.auth.transport.requests import Request
from google.oauth2.credentials import Credentials
SCOPES = ['https://www.googleapis.com/auth/gmail.readonly']
def main():
    """Shows basic usage of the Gmail API.
    Lists the user's Gmail labels.
    """
    creds = None
    # The file token.json stores the user's access and refresh tokens, and is
    # created automatically when the authorization flow completes for the first
    # time.
    if os.path.exists('token.json'):
        creds = Credentials.from_authorized_user_file('token.json', SCOPES)
    # If there are no (valid) credentials available, let the user log in.
    if not creds or not creds.valid:
        if creds and creds.expired and creds.refresh_token:
            creds.refresh(Request())
        else:
            flow = InstalledAppFlow.from_client_secrets_file(
                'credentials.json', SCOPES)
            creds = flow.run_local_server(port=0)
        # Save the credentials for the next run
        with open('token.json', 'w') as token:
            token.write(creds.to_json())

    service = build('gmail', 'v1', credentials=creds)

    # Call the Gmail API
    results = service.users().labels().list(userId='me').execute()
    labels = results.get('labels', [])

    if not labels:
        print('No labels found.')
    else:
        print('Labels:')
        for label in labels:
            print(label['name'])

if __name__ == '__main__':
    main()
 
 
Step 3: Run the sample
To run the sample:

From the command-line, execute the following command:
python quickstart.py

(optional). If this is your first time running the sample, the sample opens a new window prompting you to authorize access to your data:

If you are not already signed in to your Google account, you are prompted to sign in. If you are signed in to multiple Google accounts, you are asked to select one account to use for the authorization.
Click Accept. The app is authorized to access your data.
The sample executes.

#for more informations click on this link
https://developers.google.com/gmail/api/quickstart/python

#Note
for security reason i have delete my token.json and token.pickle file .
you should have to use yours.
