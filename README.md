# MEAN STACK DEPLOYMENT TO UBUNTU IN AWS

The MEAN stack is a JavaScript-based framework for developing web applications. MEAN is named after MongoDB, Express, Angular, and Node, the four key technologies that make up the layers of the stack. It is a relatively new but highly popular full-stack software bundle2. It uses JavaScript technologies and is used for developing web applications. In other words, this is a JavaScript-based tech stack, with both frontend and backend tools, used to build fast and efficient full-stack web applications2.

### Step 1: Install NodeJs
In this step we are going to update, upgrade, add the necessary certificate and install Node.js with the commands below:
```
sudo apt update
sudo apt upgrade -y
sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates

curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs
```

### Step 2: Install MongoDB
Mongodb is a software package that serve as database to store our data. i'll be adding book records to MongoDB that contain book name, isbn number, author, and number of pages.

Import the Public Key used by Package Management System
```
sudo apt-get install gnupg curl
curl -fsSL https://pgp.mongodb.com/server-6.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-6.0.gpg --dearmor
```
i'll be creating a List file For MongoDB for ubuntu 22.04
```
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-6.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
```

next ill be reloading the local packages, install Mongodb, start and enable mongodb services and verify that it's up and running with the following command:
```
sudo apt-get update

sudo apt-get install -y mongodb-org

sudosystemctl start mongod

sudosystemctl enable mongod

sudo systemctl status mongod
```

![Screenshot 2023-07-22 100229](https://github.com/opeyemiogungbe/Pbl_project4/assets/136735745/378468b4-4f3b-4547-aa78-2a87dd543efa)

Next i'll Install body-parser package (body-parser’ package is needed to help process JSON files passed in requests to the server).
```
sudo npm install body-parser
```
Next i'll reate a folder named Books and go into the book directory 
```
mkdir Books && cd Books
```
In the Books directory, i'll be starting my npm project.
```
npm init
```
![Screenshot 2023-07-22 100725](https://github.com/opeyemiogungbe/Pbl_project4/assets/136735745/18779eec-249c-44b0-bc8b-0ba41c6d626a)


i'll be adding a file named server.js and Vi into ito it to put in the necessary code.

![Screenshot 2023-07-22 101340](https://github.com/opeyemiogungbe/Pbl_project4/assets/136735745/40561135-c7d6-4ddd-abfc-66a89d646543)

### Step 3: Installing Express and set up routes to the serve
Express is a flexible Node.js web application framework that provides features for web and mobile applications. i will use Express in to pass book information to and from MongoDB database. i will use mongoose to establish a schema for the database to store data of my book register.
```
sudo npm install express mongoose
```
In books folder, i'll create a folder named apps and change directory into it:
```
mkdir apps && cd apps
```
i'll create a file named routes.js in the app folder and vi into it and paste in the necessary code in it.
```
vi routes.js
```
![Screenshot 2023-07-22 101553](https://github.com/opeyemiogungbe/Pbl_project4/assets/136735745/6f9e178c-bdf7-4f7b-9113-89c93e81e80b)

In the apps folder, i'll be creating another folder named models and change directory into it
```
mkdir models && cd models
```
I'll create a file named book.js, vi into it and put in all the necessary code

`vi book.js`

```
var mongoose = require('mongoose');
var dbHost = 'mongodb://localhost:27017/test';
mongoose.connect(dbHost);
mongoose.connection;
mongoose.set('debug', true);
var bookSchema = mongoose.Schema( {
  name: String,
  isbn: {type: String, index: true},
  author: String,
  pages: Number
});
var Book = mongoose.model('Book', bookSchema);
module.exports = mongoose.model('Book', bookSchema);
```
### Step 4 – Access the routes with AngularJS
AngularJS provides a web framework for creating dynamic views in web applications. i'll be using AngularJS to connect my web page with Express and perform actions on my book register.

I'll be changing the directory back to Books, create a folder name public and change directory into it
```
cd ../..
mkdir public && cd public
```
I'll add a file named script.js and vi into it
`Vi script.js`

![Screenshot 2023-07-22 102119](https://github.com/opeyemiogungbe/Pbl_project4/assets/136735745/6aa3fd29-b6fe-4113-99c3-58cec40ffcfe)

In public folder also i'll create a file named index.html, vi into it and paste the necessary code.

`Vi index.html`

![Screenshot 2023-07-22 102333](https://github.com/opeyemiogungbe/Pbl_project4/assets/136735745/f661a76d-7fb5-42ba-9e35-f207c4673eaf)

i'll change the directory back up to Books start the server by running this command:
```
cd ..
node server.js
```
Now that our server is up and running, i'll open up the tcp port 3300 on AWS Web Console for EC2 Instance. I'll access my Book Register web application from the internet with a browser using Public IP address or Public DNS name.

