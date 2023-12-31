# Secure Dev Ops Sample App
As at November 2023.
This is a sample MEAN stack application with no particular functionality.
It was first created to demonstrate code snippets for another coding subject.

## What does it do
The app

## Development Stack
    - Angular (Version 16)
    - Node 
    - Express
    - Mongo ( Local install or Mongo Atlas cloud server)

## Installation
### Server
    > cd sample-app-server
    > npm install
### Front End
    > cd sample-app-angular
    > npm install

### Generate SSL certificate
#### generate a SSL certificate authority and cert.
- openssl req -x509 -nodes -new -sha256 -days 1024 -newkey rsa:2048 -keyout RootCA.key -out RootCA.pem -subj "/C=US/CN=My-Root-CA"
- openssl x509 -outform pem -in RootCA.pem -out RootCA.crt
- openssl req -new -nodes -newkey rsa:2048 -keyout localhost.key -out localhost.csr -subj "/C=US/ST=YourState/L=YourCity/O=Example-Certificates/CN=localhost.local"
- openssl x509 -req -sha256 -days 1024 -in localhost.csr -CA RootCA.pem -CAkey RootCA.key -CAcreateserial -extfile domains.ext -out localhost.crt

move localhost.key and localhost.crt that were generated to the ssl directory.

## Mongo Database
Install a local instance of a mongo database https://127.0.0.1:27017 or configure a mongo Atlas cloud instance.

Import 

## Running the APP

In development mode
    > cd sample-app-angular
    > ng serve

    > cd sample-app-server
    > nodemon server.js

In production mode
    > cd sample-app-angular
    > ng build

    > cd sample-app-server
    > nodemon server.js

### Environment Variables
    PORT = 3000 
    DEVPORT = 4200 
    SERVER = "https://localhost"
    DEVSERVER = "http://localhost"
    MONGODB_URL = "mongodb://127.0.0.1:27017"
    BUILD = "dev" 

These environment variables provide a convience to switch between a development mode using the angular convience web server "ng serve" to host the angular front end or having the express server host the website from a built/compiled version of the angular front end. If not environment variables are provided then default values will be used. The server will look for a file called ".env" in the sample-app-server directory for these variables.

**PORT** - Used for production mode. This is the Port number as expected from the express server used to host the website. The express server is configured with a static directory that will point to a built version of the angular application. This will be in the "WWW" directory.
*default value - 3000*

**DEVPORT** - Used for development mode. This is the port number used by the angular convience server "ng serve" for hosting a pre-built version of the app. Angular automatically restarts this server whenever a file is saved and this saves having to build the app manually each time you make a chnage to the angular code. This server will be using http and not https. 
*default value - 4200*

**SERVER** - Used to define the URL to access the app. In production this is using SSL. It will work in combination with the PORT variable.
*default value - https://localhost*

**DEVSERVER** - Used to define the URL to access the app. It will work in combination with the DEVPORT variable.
*default value - http://localhost*

**MONGODB_URL** - Used to define the URL to the mongo database. This could be a local install or a link to a Mongo Atlas Cloud instance.
*default value - mongodb://127.0.0.1:27017*

**BUILD** - used to note if the app should be using development (dev) or Production (prod)
*default value - prod*


