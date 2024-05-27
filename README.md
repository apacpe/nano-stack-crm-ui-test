# nano-stack-crm-ui-1
# Nano Stack Developer Training - CRM UI Extensions
The following are instructions to create a simple CRM UI card and deploy it to HubSpot. The CRM UI card will be built with React and Node.js. 

## Pre-requisites
You will need the following installed on your local machine:
1. [version 20 or higher of NodeJS](https://nodejs.org/)
2. Code editor program such as [Sublime](https://www.sublimetext.com/download), [Atom](https://atom.io/). If you install [Visual Studio Code](https://code.visualstudio.com/download), it comes with an in-built terminal.
3. Terminal program such as [Git Bash](https://gitforwindows.org/), [Hyper](https://hyper.is/) 

You will need to 
1. Check that your portal is on the [CRM Development Tools beta](https://developers.hubspot.com/docs/platform/crm-development-tools-overview#:~:text=If%20you%27re%20not%20currently%20enrolled%20in%20the%20CRM%20development%20tools%20beta%2C%20you%20can%20join%20directly%20form%20your%20HubSpot%20account%3A)

## Deploy a template CRM UI extension to HubSpot
### Install and connect the HubSpot CLI
1. In your local machine, create a directory and change your active directory to it
```
mkdir nano-stack-crm-ui
cd nano-stack-crm-ui
```
2. Install the HubSpot CLI using `npm install -g @hubspot/cli@latest`
3. Connect to your HubSpot portal with `hs init`

4. Follow the prompts to create a personal access key in your web browser. Please check the options under "Sandboxes" and "Serverless Functions"

4. Copy and paste the personal access key into your terminal to authorize the CLI on your local machine to interact with your HubSpot account.


### Create a project and upload a template 

1. Create a project in your portal with `hs project create` and follow the prompts to name your project

***NEED TO DOUBLE CHECK THE USER FLOW FOR THIS SECTION*** 

2. Select the `Use basic CRM extension card sample project (files only)` template

3. Change your active directory and load the dependencies required to start local development server.
```
cd <your sub-folder name>
npm install
```
4. Run `hs project dev` in this sub-folder and choose to create and deploy to a sandbox or deploy to your main account.

5. Upload your files to the project with `hs project upload --account=[your account name]` 

6. In your HS portal, go to Contacts Settings and add the CRM UI card to the middle column of your contact records. You should see the template CRM card appear on any contact record. 

### Project directory structure
Your final project directory should have the following structure:
```
/nano-stack-crm-ui
    |__ /node_modules
    |__ /src            
         |__ app
              |__ app.functions
                   |__ serverless.json
                   |__ example-function.js
              |__ extensions
                   |__ example-card.json
                   |__ Example.jsx
    |__ readme.md
    |__ package.json
    |__ package-lock.json

```
Review the contents of example-card.json, Example.jsx, serverless.json and example-function.js in a code editor program.

*** POINT OUT HOW FILES ARE CONNECTED ***

### Modify your CRM UI extension

1. Install the HubSpot UI extensions npm package in the app/extensions folder
```
cd ./app/extensions
npm i @hubspot/ui-extensions
```
2. Open the Example.jsx file in the app/extensions folder, in a code editor program and XXXX
```
const express = require('express');
const app = express();
app.listen(3000, function()
  {console.log("Server started on port 3000");}
);
```
3. Test it by running the app using `node app.js` in your terminal and access localhost:3000 on your browser, you should see 'Cannot GET /'
4. Press Ctrl + C in the terminal to stop running the app

### Write Express routes in application file
1. Add a get route to the app.js file 

```
const express = require('express');
const app = express();
app.get("/", function(req, res){
  res.send('Hello world');
});
app.listen(3000, function()
  {console.log("Server started on port 3000");}
);
```
2. Run the app again using `node app.js` and access localhost:3000, you should see 'Hello world' now
3. Press Ctrl + C in the terminal to stop running the app

### Install some useful dependencies to the app
1. Install [nodemon](https://www.npmjs.com/package/nodemon) so that the server restarts automatically when you make changes to the files `npm install nodemon`
2. Install a template engine that can be used to serve page content such as [EJS](https://www.npmjs.com/package/ejs) `npm install ejs` 

### Configure the app to use EJS templates
Add this line of code in your app.js file:
```
app.set("view engine", "ejs");
```

### Create a page template
1. In your terminal, create a new directory called *views* in the portfolio-app directory and change directory into it
```
mkdir views
cd views
```
2. Create a new page template using `touch home.ejs`
3. Go back to the root directory /portfolio-app `cd ..`
4. In your code editor, open up home.ejs and insert basic HTML codes for a page
```
<html>
  <head>
    <title>Portfolio App</title>
  </head>
  <body>
    <p>This is a test page!</p>
  </body>
</html>
```

### Update application file to serve page template
1. In your code editor, open up app.js and alter the get route to serve the page template you created
```
app.get("/", function(req, res){
  res.render('home');
});
```
2. In your terminal, run the app using `node app.js` or `nodemon app.js` if you installed nodemon package
3. Access localhost:3000 on your browser and it should display a page based on the HTML codes you inserted in the page template
4. Press Ctrl + C in the terminal to stop running the app if you used `node app.js` to start the app


### Update package.json file to point to app.js

By default, package.json sets the "Main" field as "index.js". The "Main" field is the module ID that is the entry point to your app. We will need to update this to "app.js" instead.

1. In your code editor, open the package.json file
2. Change the following line
```
 "main": "index.js",
```
to
```
 "main": "app.js",
```

### Git set up

1. In your terminal, set your Git user name and email address.
```
git config --global user.name "John Doe"
git config --global user.email "johndoe@example.com"
```

### Deploy to HubSpot
1. Upload your updated files with `hs project upload --account=[your account name]`
2. Review the changes on your CRM 
