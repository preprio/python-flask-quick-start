# Flask Python Quick Start
The Flask Python quick start project launches a page app with content from Prepr.


## Set up the project locally

Open the terminal and set up a quick virtual environment like the following:

```
python3 -m venv venv;
. venv/bin/activate;
pip install --upgrade pip
```

Now, you're ready to install dependencies for your project with pip:

```
pip install flask requests
```


You've now installed Flask, a microframework that you'll use for the simple web app to wrap data sent from the GraphQL API.


## Set up the Flask app

To configure the Flask app location, set up an environment variable with the name of your application (say, api.py file):

```
export FLASK_APP=api.py
```


In this `api.py` file, create the simple Flask setup like the following:


```
from flask import Flask

app = Flask(__name__)

@app.route("/get_page")
def get_page():
    return {"page title text": "data from the API"}
```


Type flask run in the terminal and open the browser on localhost:5000/get_page endpoint. A simple JSON with the "page title text" key is returned.



## Query data from Prepr

To authenticate your app on Prepr CMS, you need to know the API URL and the GraphQL query you want to send to the request.

To get the endpoint of your Prepr environment, navigate to Settings -> Access Tokens and click the token you want to use. Copy the endpoint under API Url.


What's left is the GraphQL query that you want to pass to the request. Click `Open in API Explorer` to open the explorer in which you can experiment with GraphQL queries. Write this query on the playground:


```
query Page {
  Page(slug: "home") {
    title   
  }
}
```


Now, you're ready to authenticate your app. Open the api.py, and your project is now like the following:

```python
import requests
import json
import os
from flask import Flask

query_page = """query Page {
  Page(slug: "home") {
    title   
  }
}
"""

url = "https://graphql.prepr.io/your_token"  # Paste your earlier copied API URL
app = Flask(__name__)

@app.route("/get_page")
def get_page():
    payload = {"query": query_page}
    result = requests.post(url, json=payload)
    json_data = result.json()
    return {"page title text": json_data["data"]["Page"]["title"]}
```



- The result object contains the response of the API request that you sent.
- The json_data is a JSON conversion from the result Python object
- Finally, the response coming from the query:

```json
{
  "data": {
    "Page": {
      "title": "Home page"
    }
  }
}
```


Run the Flask app with flask run and open the localhost on the get_page endpoint. You'll see a response with the following:

```
{
  "page title text": "Home page"
}
```
