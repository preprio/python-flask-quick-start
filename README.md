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

Type `flask run` in the terminal and open the browser on `localhost:5000/get_page` endpoint. A simple JSON with the "page title text" key is returned.
