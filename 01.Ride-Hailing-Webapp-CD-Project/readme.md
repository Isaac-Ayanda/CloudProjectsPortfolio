# Ride-Hailing Web App Continuous Delivery Project
### A ficticious company has approached us with a requirement to build a continous delivery Ride-hailing web application, like Uber; in this case, cars are referred to as Unicorns. The application should incorporate user registration and login, and Map functionalities that allows users to click on a location and request a unicorn ride. Credit: AWS

<!-- ## Architechture -->
![App Architecture](./images/architecture.png)

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
<!-- IAM>Users>Security credentials>HTTPS Git Credentials for AWS CodeCommit>Generate credentials -->
![Create GIT credentials](./images/git-credentials.png)