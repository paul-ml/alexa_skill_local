# Alexa skill using ngrok
*  server is running on local machine
*  so whenever ngrok connection is restarted, endpoint has to be changed in amazon developer console
*  Alternate for ngrok ? go for  aws lamba function creation. 

## Expected Output: (Example)
`User invocation`: listen to me <br>
`Alexa speaks`: Welcome to Alexa Skill. Would you like to hear a joke?<br>
`User`: Yes/No <br>
`Alexa`: speaks joke if Yes<br>

## requirements
> Flask 
- Flask is a micro web framework written in Python
```
pip install flask
```
> Flask Ask
- Flask-Ask is a Flask extension that makes building Alexa skills for the Amazon Echo easier and much more fun.
```
pip install flask_ask
```
> ngrok
- Is a `command-line program` that opens a secure tunnel to localhost and exposes that tunnel behind the HTTPS
- `steps`
    - please `follow step 1 to step 3` from following link:
      https://ngrok.com/download
    - fire ngrok up
    ```
    ./ngrok http 5000 
    (5000 is the port number in which python script will be running)
    ```
    * `COPY` https link obtained from ngrok (will be used later)


> Start python script
```
python index.py
```
* now python script running in localhost can be accessed by using the https link obtained from ngrok

## Install Flask-Ask dependencies
- Created a virtualenv for python3.6.5 and activate venv
  - `virtualenv -p python3.6 venv`
  - `source bin/activate`
- Install the dependecies in venv
  - `pip install aniso8601==1.2.0 Flask==0.12.1 cryptography==2.1.4 pyOpenSSL==17.0.0 PyYAML==3.12 six==1.11.0` 
## What next ?
- Lets create a new skill in amazon developer console

### Signup to Amazon developer console
* https://www.amazon.com/ap/register?openid.pape.max_auth_age=1&openid.return_to=https%3A%2F%2Fdeveloper.amazon.com%2Fap_login.html&prevRID=GTTTSX8MVP5Z1BT4MT2R&openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&openid.assoc_handle=mas_dev_portal&openid.mode=checkid_setup&prepopulatedLoginId=&failedSignInCount=0&language=ja_JP&openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&pageId=amzn_developer_portal&openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0
### Go to alexa console and create a new skill
* https://developer.amazon.com/alexa/console/ask?
    * `model` : custom (default selection)
    * `template`: start from scratch
### Add invocation name
* as name suggests its used to invoke our skill 
    * example: add `listen to me` to invocation and save it
        * now`listen to me ` is used to invoke alexa skill
 
### Create Intents
* check we are using 2 intents (please check `index.py`)
    * `YesIntent` and `No Intent`
* create 2 intents in console with same name 
* Add sample utterances for intents
    * example `yes`, `yes please`, `yup` (these are the expected responses from user)

### Add endpoints
* add `HTTPS` endpoint obtained from ngrok 
* change `SSL certificate type`: my development environment is a subdomain of domain that has a wildcard certficate from a certificate authority

### Save and build model 
* click on `save endpoints` 
* click on `build` on model

## Ready to fire Alexa Skill?

### Test skill on developer console
- go to `Test`
- type the `invocation word` created 
- click `enter` button 

*** check `ngrok` to see the response status code *** 

### Test using smartphone/ iphone
- Go to `Playstore/App store` 
- `Download` Amazon Alexa app
- `SignIn` using the same email id and password used for creating alexa skill
- `fire it up` using invocation word




