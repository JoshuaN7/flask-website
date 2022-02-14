# project setup

## Create an AWS account

Head over to https://aws.amazon.com/ and create an account

## Create a PostgreSQL database on AWS Lightsail

Source: https://lightsail.aws.amazon.com/ls/docs/en_us/articles/amazon-lightsail-creating-a-database

## Install Postgres.app and connect to the database

1. Head over to https://postgresapp.com/ to install Postgres CLI tools by following the steps
2. Head over to https://lightsail.aws.amazon.com/ls/docs/en_us/articles/amazon-lightsail-connecting-to-your-postgres-database to connect to the PostgreSQL database on AWS Lightsail

## Setup local environment

Source: https://www.youtube.com/watch?v=4tDjVFbi31o&t=787s

### Create virtual environment

```sh
python3 -m venv venv
```

### Activate virtual environment

```sh
source venv/bin/activate
```

## Verify that pip list is clean

```sh
pip list
```

## Upgrade pip

```sh
/Users/simontran/coding/stamps-website/venv/bin/python3 -m pip install --upgrade pip
```

### Install modules (simon)

```sh
pip install flask
```

### Direct pip3 installed modules and their versions into requirements.txt file 

```sh
pip freeze > requirements.txt
```

### Create application.py file

The main file should be called application.py for seamless integration with AWS Elasticbeanstalk.

```sh
touch application.py
```

## Add simple code

```py
from flask import Flask
application = Flask(__name__)
app = application

@app.route('/')
def hello_world():
    return 'Hello World'
```

## Test the flask website locally

1. Temporarily add application.py to PATH

```sh
export FLASK_APP="application.py"
```
2. Run the flask website

```sh
flask run
```

Then open the link after "Running on" to view the website. 

If everything looks good, hit `CTRL+C`to terminate the process.

3. Push the code to Github

```sh
git add .
git commit -m "Test deploy"
git push origin main
```

## Create AWS Elasticbeanstalk environment

Source: https://www.youtube.com/watch?v=4tDjVFbi31o&t=787s

1. Open Elastic Beanstalk tab
2. Click `Create a new environment`
3. Select `Web server environment`
4. Under `Application name`, input "flask-website"
5. Under `Platform`, select `Managed platform`, `Python` as the Platform, `Pyhon 3.8 running on 64bit Amazon Linux 2`as the Platform branch, and `3.3.10 (Recommended)`as the Platform version
6. Under `Application code`, select `Sample application`
7. Then click `Create environment`

Wait until the environment is created

## Create CodePipeline

Source 1:
Source 2: https://docs.aws.amazon.com/dtconsole/latest/userguide/connections-create-github.html

1. Open CodePipeline tab
2. Click `Create pipeline``
3. Under `Pipeline name`, input "flask-website"
4. Under `Service role`, select `New service role` then click `Next`
5. Under `Source provider`, select `Github (Version 2)``
6. Under `Connection`, select `Connect to Github``
7. Under `Connection name`, input "flask-website-connection", then click on `Connect to Github``
8. Under `Github Apps`, click `Install a new app`, then select `ccfo-informatique`, and scroll down to `Repository access`and select `Only select repositories`. From there, select the `flask-website` repo and hit `Save`
9. Click `Connect`to finalize the Github connection
10. Under `Repository name`, select `flask-website``
11. Under `Branch name`, select `main``
12. Under `Output artifact format`, select `CodePipeline default`, and hit `Next`
13. Under `Add build stage`, click `Skip build stage`, and `Skip` to confirm
14. Under `Deploy`, select `AWS Elastic Beanstalk` as the `Deploy provider`, `Canada (Central)` as the `Region`, `flask-website` as the `Application name`, and `Flaskwebsite-env` as the `Environment name`, then hit `Next`
15. Select `Create pipeline` and wait until it gets deployed
16. Once the deployment is done, under `Deploy`, click `AWS Elastic Beanstalk`, then under `URL`, click on that link to open the website