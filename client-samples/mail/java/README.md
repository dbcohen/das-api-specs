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

# Java samples using the DAS Mail API
Sample code showing use of Domino Access Services (DAS) with Swagger
generated client code.  You can use this code to test mail API
client code generated by
[Swagger Codegen](https://github.com/swagger-api/swagger-codegen).

### Prerequisites
- A Domino server with the mail API installed and enabled.
- A Java development kit (JDK).  Java 7 is the minimum required
  version.
- Apache Maven to build the Java code and automatically manage
  dependencies.
- A Java client package generated from **mail.yaml**.  For example,
  you can use the [online Swagger editor](http://editor2.swagger.io)
  to import **mail.yaml** and then generate a "Java" client.
  (*Note:* This repository does not include the generated code.)
  
### Required JARs
The generated client package includes a Maven project object module 
(**pom.xml**) identifying several required JARs.  Therefore, we
recommend you use Maven to automatically build
the project and manage its dependencies.  If you choose not to
use Maven, the list of required JARs is as currently follows:  

- gson-2.6.2.jar
- joda-time-2.9.3.jar
- logging-interceptor-2.7.5.jar
- okhttp-2.7.5.jar
- okio-1.6.0.jar
- swagger-annotations-1.5.9.jar

This list depends on the version of Swagger Codegen and is subject
to change without notice.  (In other words, you really should use
Maven!)

# Instructions
These instructions show how to build and run
[MessageTest.java](client/mail/test/MessageTest.java).  To run
a different mail client sample, follow these same instructions
and substitute file names where appropriate.

First create a root folder and sub-folder as shown below:

```
/tests
/tests/swagger-java-client
```

The root folder name is not important.  Choose a name other than
**/tests** if necessary.

### Unzip the generated client code
Unzip the generated code to **/tests/swagger-java-client**.  When you
are finished, the contents of the folder should look something like
this:

```
docs
gradle
src
.gitignore
.swagger-codegen-ignore
.travis.yml
build.gradle
build.sbt
git_push.sh
gradle.properties
gradlew
gradlew.bat
pom.xml
README.md
settings.gradle
```

### Use Maven to build the generated client code
Build the generated client code and install it to your local Maven
repository:

```
cd /tests/swagger-java-client
mvn install
```

This step may take several seconds to complete.  Move on to
the next step only when you are sure you have a successful build:

```
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 4.896 s
[INFO] Finished at: 2017-02-22T14:26:49-05:00
[INFO] Final Memory: 20M/34M
[INFO] ------------------------------------------------------------------------
```

### Create your mail API test project
Now run the following two commands:

```
cd /tests
mvn archetype:generate -DgroupId=client.mail.test -DartifactId=client-mail-test -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

That second command is complicated, but when successful,
it automatically creates a new Maven project based on a common
template.  The new project is in a folder called
**/tests/client-mail-test**.  You might want to take a
moment to explore the contents of the new folder now.

### Customize your test project
Look for a file named **pom.xml** in the
**/tests/client-mail-test** folder.  Open **pom.xml**
in your favorite text editor and add the following lines
inside the existing `<dependencies>` element:

```
<dependency>
    <groupId>io.swagger</groupId>
    <artifactId>swagger-java-client</artifactId>
    <version>1.0.0</version>
    <scope>compile</scope>
</dependency>
```

Save your changes to **pom.xml**.

Now download [MessageTest.java](client/mail/test/MessageTest.java)
to the **/tests/client-mail-test/src/main/java/client/mail/test**
folder.  Then open your local copy of **MessageTest.java** in a text
editor and customize the following values for your environment:

```java
// IMPORTANT: Change these values to match your test environment:
//
// - basePath is the base URL for your Domino server.
//   The mail service MUST be installed and enabled
//   on the server. Be sure to change the protocol to
//   https if necessary.
//
// - folder is the mail file database folder. The folder is relative
//   to the Domino data directory.  Use "." if the mail file
//   is in the data directory itself.
//
// - database is the mail file database name.
//
// - user is the user name of the owner of the mail file specified by
//   /{folder}/{database}.
//
// - password is the user's password.
//
// - sendTo is the email address of a recipient
//
String basePath = "http://yourserver.yourorg.com";
String folder = "mail";
String database = "database.nsf";
String user = "First Last";
String password = "password";
String sendTo = "recipient@yourorg.com";
```

### Build your test project
Run the following two commands:

```
cd /tests/client-mail-test
mvn package
```

If your build is successful, you should see the following:

```
[INFO]
[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ client-mail-test ---
[INFO] Building jar: /tests/client-mail-test/target/client-mail-test-1.0-SNAPSHOT.jar
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1.870 s
[INFO] Finished at: 2017-02-22T15:04:06-05:00
[INFO] Final Memory: 15M/25M
[INFO] ------------------------------------------------------------------------
```

### Run your test project
On Linux run the following command (note the use of *colons* to
separate folders in the classpath):

```
java -cp "target/*:../swagger-java-client/target/*:../swagger-java-client/target/lib/*" client.mail.test.MessageTest
```

On the other hand, if you are using Windows run the following
(note the use of *semicolons* to separate folders in the
classpath):

```
java -cp "target/*;../swagger-java-client/target/*;../swagger-java-client/target/lib/*" client.mail.test.MessageTest
```

Either way, the above commands run the **MessageTest** class with
a classpath that includes the **client-mail-test** JAR (`target/*`),
the generated client code (`../swagger-java-client/target/*`), and its
dependencies (`../swagger-java-client/target/lib/*`).

A successful run looks something like this:

```
Sending message from mail/database.nsf ...
Send message request succeeded.  Location is http://yourserver.yourorg.com:80/mail/database.nsf/api/mail/messages/2A3C4E50234ADA95852580E600534390

Reading message 2A3C4E50234ADA95852580E600534390 from mail/database.nsf ...
Read message request succeeded.  Response follows ...
  subject: Test message from Swagger generated Java client code
  date: 2017-03-17T15:09:27Z

  contentType: text/plain
  data: This is a test.

  contentType: text/html
  data: <html><body>This is a test.<p><b>This is only a test!</b></body></html>
```

In other words, the **MessageTest** class sends a test message to
the specified recipient.  Then it reads the sent message and dumps its
contents to the console.  The **MessageTest** class does this with relatively
simple calls into the generated client code.

### Next steps
Here are some other things to try:

- Review **MessageTest.java** to better understand how it uses
  the generated client code.  You might even want to step
  through the code in a debugger.
  
- **MessageTest** sends a message in **multipart/alternative**
  format, but the mail API allows you to represent virtually any
  MIME structure in JSON format.  Try changing the contents of the
  test message.
  
- Add other test classes to the **client-mail-test**
  project.  For example, see
  [DraftMessageTest.java](client/mail/test/DraftMessageTest.java) and
  [MessageListTest.java](client/mail/test/MessageListTest.java).
  As you add each new class, be sure to customize it for
  your test environment and rebuild the test project.  Then
  run the new class and see what it does.

- Explore the generated code in more detail.  You might even
  want to write your own application to integrate with the Domino
  mail API.
