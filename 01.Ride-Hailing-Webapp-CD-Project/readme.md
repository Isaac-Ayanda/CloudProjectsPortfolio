# Ride-Hailing Web App Continuous Delivery Project
### A ficticious company has approached us with a requirement to build a continous delivery Ride-hailing web application, like Uber; in this case, cars are referred to as Unicorns. The application should incorporate user registration and login, and Map functionalities that allows users to click on a location and request a unicorn ride. Credit: AWS

<!-- ## Architechture -->
![App Architecture](./images/architecture.png)

AWS services used: AWS CodeCommit, AWS Identity & Access Management (IAM), AWS 
## Project requirements & analysis
+ An Account and access to AWS Console
+ Knowledge of AWS Services
+ A free ArcGIS account (arcgis.com)
+ The need to store/update/pull code
+ The need to handle permissions for code
+ The need to host website and make updates
+ User registration and login
+ Ride sharing functionality
+ The need to store/return ride results
+ Invoking ride sharing functionality

### Code Setup
We use AWS CodeCommit to:
+ store/update/pull the wep application source code
+ handle permissions for the source code
+ Side note: There is need to be consistent in the AWS region we are working in.
+ The App source code is made availale by AWS in a public S3 bocket
+ We create a CodeCommit Repo
+ + Create an empty repository in CodeCommit
![Create repo on CodeCommit](./images/codecommitrepo.png)
![Create repo on CodeCommit](./images/createrepo.png)
.
+ Add a policy to your IAM user so that you can access CodeCommit. It is best practise to login as an IAM user with administrative acces not with root credentials. 
<!-- Go to IAM> Users> Permissions policy> Add permissions> Attach policies directly> search for AWS CodeCommitPowerUSer> Next> Add permissions -->
![Create repo on CodeCommit](./images/add-permissions.png)
![Create repo on CodeCommit](./images/attach-policy.png)
.
+ Create GIT credentials for your IAM user to allow HTTPS connections to CodeCommit 
<!-- IAM>Users>Security credentials>HTTPS Git Credentials for AWS CodeCommit>Generate credentials> Then download the credential -->
![Create GIT credentials](./images/git-credentials.png)
![Create GIT credentials](./images/git-credentials2.png)
![Create GIT credentials](./images/git-credentials3.png)
.
+ Clone the repository (create an empty folder for future code)
<!-- CodeCommit>Repositories>Create repository> select repo you earlier created>Clone URL>Clone HTTPS>open cloud shell at the top> then type: git clone the url> Then enter the user name & password generated earlier -->
![Clone empty repo for source code](./images/clone-repo2.png)
.
+ Copy the project code from the S3 bucket and commit it to the new repo. In cloud shell cd into the empty repo folder and copy source code from S3 to this folder.
<!-- cd wildrydes-site2 > aws s3 cp s3:// (ensure to change the region to your region) then add the files to the git repository, when prompted for email and user name use the details of the IAM user not the details for HTTPS, Commit and push> followed by the HTTPS credentials -->
![Clone source code from S3 bucket](./images/clone-repo3.png)
![Clone source code from S3 bucket](./images/clone-repo4.png)
![Clone source code from S3 bucket](./images/clone-repo5.png)

<!-- We can then view the source code files at CodeCommit> Repositories> Wildrydes-site -->
![View source code in repo](./images/source-code.png)
.
### Host the Website & allow continuous delivery
We use AWS Amplify to:
+ connect with the CodeCommit repository and pull the source code
+ host the website so that user can easily access it.
+ easily deliver updates to the website
<!-- Applify>New app> Host app> select CodeCommit>continue>select the repo created earlier> click next> ensure to click the checkbox to allow AWS applify to automatically deploy all files..as continous deployment> click create a new service role>next>review>save and deploy -->
![View source code in repo](./images/applify-app.png)
![View source code in repo](./images/applify-app1.png)
<!-- Amplify is serverless and no need to provision EC2 servers-->
![View source code in repo](./images/applify-app2.png)
![View source code in repo](./images/app-page.png)
.
+ Test that continous deployment is working by making some changes to the source code and see if amplify automatically effect the changes
<!-- CodeCommit> Repositories>repo name> Edit index.html> Update some of the text>Commit the changes with Author name, email -->
![Amplify CD](./images/applify-cd.png)
![CD of changes](./images/amplify-cd2.png)

### Implement User Access
We use AWS Cognito to:
+ enable users to register and login with their credential or external identity systems.
+ enable user authentication
 Amplify studio lets us setup cognito on the deployed app easily: But first we setup a user pool from  cognito be performing configuration changes in amplify <!--.i.e Amazon Cognito> User pools> Create user pool> Choose attibutes that users will use to sign in (User name, Email, Phone number)>Next>Configure Security requirements(Password Policy)>MFA setup>defaults for user account recovery>Next>Configure sign-up experience> Enable self registration and maintain defaults> Next> Configure message delivery: Email Provider(send with congito to test)> defaults for from and reply to emails adderss>Next>Integrate your app: add user pool name, add app client name, the rest defaults>Next> Review and create: Create user pool> Access user pool and copy User pool ID, Client ID under - app clients and analytics - App authentication -->
![Cognito setup](./images/cognito-user-pool.png)
![Amplify Studio](./images/applify-studio.png)
.
+ Then update the config file in the application to point to this user pool.  
<!-- CodeCommit>Code>js>config.js> Edit and update userpoolid, clientid and region the commit changes -->
![Update IDs](./images/update-ids.png)

+ Refresh the web page and test the login functionality with email and password. The Cognito email service will send a confirmation email with verification code to the registered email to login. Cognito user pool takes care of signin functionality to the app. After successfully login it takes you to the ride.html page that has the map functionality

![Test login](./images/test-login.png)
![verification  successful](./images/verification-successful.png)

+ 