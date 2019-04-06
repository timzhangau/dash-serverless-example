# dash-serverless-example
dash serverless deployment to AWS lambda


## THINGS TO NOTE ON AWS API GATEWAY PATHNAME
AWS lambda has different stages, the pathname will mess up the communication between front end and back end.
to avoid that, need to set a pathname prefix equal to the environment name corresponding to AWS API gateway


## steps to create and deploy flask app to AWS lambda
- detailed instruction is from:
https://medium.com/@Twistacz/flask-serverless-api-in-aws-lambda-the-easy-way-a445a8805028

1. make sure you already have AWS account and have awscli installed on your machine

2. install serverless
    ```bash
    npm install -g serverless
    ```

3. create python project and virtual environment. (NOTE: use virtualenv to create virtual environment as the python3 
default venv is not working properly with serverless deployment)
    ```bash
    # create new dir and jump in
    $ mkdir quotes
    $ cd quotes/
    # create virtualenv, activate it
    $ virtualenv venv -p python3
    $ . venv/bin/activate.fish
    # install Flask and freeze requirements
    $ (venv) pip install Flask
    $ (venv) pip freeze > requirements.txt
    ```

4. write your flask codes

5. create a serverless config yaml file with the following format as example:
    ```yaml
    service: quotes
    
    provider:
      name: aws
      runtime: python3.6
      stage: dev
      region: us-east-1
      memorySize: 128
    ```

6. install two additional sls plugins.
    ```bash
    $ sls plugin install -n serverless-wsgi
    $ sls plugin install -n serverless-python-requirements
    ```

7. test app locally with
    ```bash
    sls wsgi serve
    ```

8. if good, deploy with
    ```bash
    sls deploy
    ```

Additional documentation on serverless can be found at
https://serverless.com/framework/docs/


## update existing deployment
- use deploy function or package for existing project for speedier deployment
    ```bash
    sls deploy function --function myFunction
    ```
    or
    ```bash
    sls deploy --package path-to-package
    ```
