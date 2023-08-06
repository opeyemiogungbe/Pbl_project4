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

