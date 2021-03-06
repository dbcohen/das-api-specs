<!---
  © Copyright IBM Corp. 2017
  
  Licensed under the Apache License, Version 2.0 (the "License"); 
  you may not use this file except in compliance with the License. 
  You may obtain a copy of the License at:
  
  http://www.apache.org/licenses/LICENSE-2.0 
  
  Unless required by applicable law or agreed to in writing, software 
  distributed under the License is distributed on an "AS IS" BASIS, 
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or 
  implied. See the License for the specific language governing 
--->

# Node.js samples using the DAS Mail API
Sample code showing use of Domino Access Services (DAS) with Swagger
generated client code.  You can use this code to test mail API client
code generated by
[Swagger Codegen](https://github.com/swagger-api/swagger-codegen).

### Prerequisites
- A Domino server with the mail API installed and enabled.
- A Node.js runtime environment.
- A Node.js package generated from **mail.yaml**.  For example,
  you can use the [online Swagger editor](http://editor2.swagger.io)
  to import **mail.yaml** and then generate a "Javascript" client.

# Instructions
These instructions show how to install and run [messagelisttest.js](messagelisttest.js).
To run a different mail API client sample, follow these same instructions
and substitute file names where appropriate.

First create a root folder and two sub-folders as shown below:

```
/tests
/tests/ibm_domino_mail_api
/tests/messagelisttest
```

The root folder name is not important.  Choose a name other than
**/tests** if necessary.

### Unzip the generated client code
Next unzip the generated code to **/tests/ibm_domino_mail_api**.
When you are finished, the contents of the folder should look
something like this:

```
docs
src
test
.swagger-codegen-ignore
.travis.yml
git_push.sh
mocha.opts
package.json
README.md
```

### Create your Node.js application
Now use **npm** to initialize your Node.js application. Use a Node.js 
command shell to execute the following commands:

```
cd /tests/messagelisttest
npm init
```

The **npm** command will prompt you for information about your
application.  Be sure to specify **messagelisttest.js** as the
entry point.  Otherwise, you can accept the default values
as shown below:

```
name: (messagelisttest)
version: (1.0.0)
description: Domino mail API test
entry point: (index.js) messagelisttest.js
test command:
git repository:
keywords:
author:
license: (ISC)
```

Use **npm** to make your application dependent on **ibm_domino_mail_api**
(the generated client code):

```
npm install --save ../ibm_domino_mail_api
```

Download [messagelisttest.js](messagelisttest.js) to the **/tests/messagelisttest** folder.
Then open your local copy of **messagelisttest.js** in your favorite text editor
and customize the following values for your environment:

```javascript
// IMPORTANT: Change these values to match your test environment:
//
// - basePath is the base URL for your Domino server.
//   The mail service MUST be installed and enabled
//   on the server.  Be sure to change the protocol to
//   http if your server doesn't support https.
//
// - username is the name of a user who has access to a
//   mail file on your Domino server
//
// - password is the user's password
//
// - folder is the mail file folder name relative to the Domino
//   data directory.  Use '.' if the mail file is in the data
//   directory itself.
//
// - database is the mail file name.
//
var basePath = 'http://yourserver.yourorg.com';
var username = 'First Last';
var password = 'password';
var folder = 'mail';
var database = 'database.nsf';
```

### Run your Node.js application
After saving your local changes, return to the Node.js command shell to run 
your application:

```
node messagelisttest
```

The following is some sample output from a successful run:

```
/tests/messagelisttest> node messagelisttest
Reading inbox from dlawson.nsf ...
Request succeeded. Response follows ...

Message 0
  subject: Re: Test from Swagger UI
  date: 2017-03-14T17:47:09Z
  from: Dean Melnyk

Message 1
  subject: Accepted: API test
  date: 2017-03-14T13:01:02Z
  from: Room 1001

Message 2
  subject: Pi Day celebration
  date: 2017-03-14T12:59:07Z
  from: Raymond Chan

Message 3
  subject: Accepted: API test
  date: 2017-03-14T12:56:22Z
  from: Room 1001
```

In other words, the **messagelisttest.js** application lists up to
five messages in the specified inbox.  You can specify a different view
on the command line.  The following command lists messages in the
sent view:

```
node messagelisttest sent
```

The application accepts the following view names: `inbox`, `sent`, 
`drafts`, and `trash`.