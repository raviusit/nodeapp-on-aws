This repo can be used an example how you handle infrastructure day-to-day. 

This is a coding exercise for someone who works as an Infrastructure Engineering 
This whole work can be completed in around 1-2 hours. 

Things that you'll learn by this repo - 

An ability to handle code like a software engineer
Maintainability of solutions
Containers
Infrastructure as Code
Monitoring
Consideration of CI/CD
Resilience
Ability to develop applications locally in a consistent environment
Concise documentation (please include a README)
As you must only be interested in the code, I didn't let this project running and in order not to incur any aws costs.


Okay, let's begin - 

We are going to create a simple 'Hello World' web application (for example, node.js) and deploy it to a Cloud Infrastructure, such as an AWS account, using appropriate tools and best practices. When deployed, the root url should display 'Hello World'.

PS - Changed output to "Hello" :) 

Click here - http://test-lb-tf-1964796265.us-east-2.elb.amazonaws.com


# Prerequisites
* AWS account - used free tier account
* Node - v14.6.0
* Docker 
* Terraform  -  v0.12.29

# Overview of the Solution

* Created a simple Node app
* Dockerize the Node app.
* Push the image to AWS ECR 

Used Terraform to - 
* provision network resources
* provision an AWS ECS cluster
* Create an AWS ECS task
* Create an AWS ECS service
* Create a load balancer

### Step 1 - Created the Node App
create and navigate to application’s directory:

$ mkdir nodeapp-on-aws-CondeNast


$ cd nodeapp-on-aws-CondeNast


created an npm project:
$ npm init --y

Install Express:
$ npm install express

Created node.js file :

```sh 
'use strict';
const express = require('express');
// Constants
const PORT = 3000;
const HOST = '0.0.0.0';
// App
const app = express();
app.get('/', (req, res) => {
  res.send('Hello Condé Nast');
});
app.listen(PORT, HOST);
console.log(`Running on http://${HOST}:${PORT}`);
```

$ node node.js
app should be running at - http://localhost:3000/

### Step 2 - Dockerize the Node App
created a Dockerfile

```sh
FROM node:14-slim
WORKDIR /app
COPY package.json .
RUN yarn
COPY . .
EXPOSE 3000
CMD [ "node", "node.js" ]
```

### Step 3 - Pushed the Node App image to AWS ECR

### Step 4 Run terraform to provision network and infrastructure components 
```
Apply complete! Resources: 15 added, 0 changed, 0 destroyed.

Outputs:

App_URL = test-lb-tf-1964796265.us-east-2.elb.amazonaws.com  

ramaurya@ramaurya-mac nodeapp-on-aws (master)*$ curl http://test-lb-tf-1964796265.us-east-2.elb.amazonaws.com
Hello World
```

### Directory structure 

```sh
ramaurya@ramaurya-mac nodeapp-on-aws (master) $ tree
.
├── Dockerfile
├── main.tf
├── node.js
├── package.json
├── providers.tf
└── README.md
└── variables.tf
```

