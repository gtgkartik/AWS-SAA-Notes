# AWS SAA

### Cross Origin

this basically allows you to use resources from other site into your site

The webbrowser cannot make API calls to another domain other than its origin

Once filled a google form the data cannot be sent to some other domain it must be stored in googles servers 

By enabling cross origin on AWS services will send API calls to each other, in interacting to build a great App !

# IAM in AWS

- IAM stands for Identity Access Management
- it is a global service (Which means it is avilable in all countries)

### What is a Root Account ?

This account is created whenever you have created and Account on AWS, this account password cannot be shared with anyone because it is the root and it will have full access to the AWS account.

The better alternative is login in to the aws account from the root credentials and create AWS IAM credentials for and attatch policies to the IAM credentials and share it with the **Users**. 

**Users** are the people within a organizations and can be grouped.

### Example Scenario:

We have 6 people in an organization

- Alice
- bob
- charles
- David
- Edward
- Fred

In an organization there can be many teams

- Developer Team
- Operations Team
- Audit Team
- and many more

### Why do we create Users and why do we create Groups ?

We want to allow the organizations memebrs to use AWS account !

And to do so we need to give them permissions

We can give permissions to both Users and Groups

Users and groups can be given permission by attaching a document called a policy.

The policy is in the format of a JSON document. 

This JSON Document contains what a User is allowed to do or what a group is allowed to do. 

If a policy is attached to a group and this policy will be applied to evry user present in this group.

### AWS IAM on AWS Console

when you open AWS IAM service on you AWS Management Console you will see on the top right it will show “Global” which means AWS IAM do not have any Region selection and it is global 

### Create IAM User on AWS

when you are creating AWS IAM user you can create a user group and attatchpolocies to this user group and again this user group will be attahced with a policy and when a new IAM user is created they can be added to this user group and thus this new user in the user group will inherit all the permissions of the user group

Example: I can create a IAM user group with admininstrator access policy attatched tho this group 

and when I am creating a new user I can add him to this group and this user will inherit the policy adminstrator access via the user group.

This will be easy to manage Policies and permissions to large number of users in a group. Instead of adding policies to users with same previlage again and again.

### Alias for AWS IAM

After creating user this user will have to use a url present in the csv file to access the IAM console of the organization. so this url can have a alias name 

![Untitled](AWS%20SAA%20e747ade1a4344759a43bfb9f6c3fbba3/Untitled.png)

![Untitled](AWS%20SAA%20e747ade1a4344759a43bfb9f6c3fbba3/Untitled%201.png)

### IAM Policy Structure

Policies/permission can be applied on 

- Users (By creating IAM User)
- Services (By creating IAM Role)

Policies in AWS are basically for Users, Services and resources to define access control !!

A service like AWS lamda when created must be granted permission in order to interact with other services

Similirly when a IAM user uses AWS they must be granted access to a some services to use it

Policies will help us acheive this task

```jsx
{
  "Version": "2012-10-17",
  "Id": "Policy1497053408897",
  "Statement": [
    {
      "Sid": "Stmt1497053406813",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::<your bucket name>/*"
    }
  ]
}
```

A policy is a Document in JSON format and here it consist of a object inside which we will have 

- Policy Version (Policy version) (what is a policy Version?)
- ID (Policy Identifier)
- Statement

**Statement (an array of objects, each object is a statement)**

A statement Consists of 

- SID: An Identifier for the statement
- Effect: Effect will take in values like “allow” or “deny”.
- Principal: The account/User/role to which this policy is applied to.
- Action: List of actions this policy allows or denies
- Condition: Condition for which this statement will be in effect

### IAM MFA

you can use Multi factor authentication for both the root account as well at the IAM accounts you have created, It is very important to keep your credentials secured

MFA can be unables using many devices 

- Virtual MFA Device (Third party Apps like Authy, Google Authenticator… etc)
- Universal 2nd factor Security Key  (Like a pendrive)
- Hardware key mob security device (a physical device that displays numbers)
- Hardware Key fob MFA Device for AWS GovCloud (USA)

**Enable MFA for IAM Users / Root User**

- Login to AWS Management Console
- Top right on the name click
- select security credentials
- enable MFA

### Password Policy

You can add the password rules against the passwords that are set by the IAM users.

you can set rules like 

- 8 digit passwrd length
- special character
- number
- uppercase letter
- lowercase letter
- etc…
- Allow all IAM users to change passwords after some days (Password expiration)
- Prevent Password Re use

**Set Password Policy Rules**

- login to aws Management console
- search and select the IAM service
- on the left handside in the sidebar choose the Account Settings

### Different ways to access AWS ?

So far we have used AWS Management Console to access AWS

But there are otherways to access AWS 

To access AWS you have 3 options

- AWS Management Console (Protected by Password +MFA)
- AWS Command Line Interface (CLI) (Protected by Access Keys)
- AWS Software Development Kit (This is used whever you want to call AWS from the application code, using API’s) (Protected by access Keys)

**Access Keys**

Access keys are ofcourse generated from the AWS Management Console.

Access Keys are just like a password it cannot be shared with anyone

Access Keys consists of Access Key and Access ID 

Access ID is like a Username 
and Access Key is like a Password

**What’s the AWS CLI?**

- A tool that enables you to interact with AWS services using commands in
your command-line shell
- Direct access to the public APIs of AWS services
- Alternative to using AWS Management Console

**How to Create Access Keys**

You can create Access Keys for a user by going to IAM service in the Management console.

- go to IAM console
- Click on the User to which you want to create Access Keys
- Create Access Keys by searching for “Access Keys” heading somewhere
- You have many options where you can create access keys for, “Applications outside aws” but for now choose “CLI”
- You can add tags
- you can download Access Keys which will be in a CSV File.

**How to use these Access Keys in you CLI**

These Access keys can now be used in your local Command Prompt

After downloading the Access Keys it will look something like this below:

![Untitled](AWS%20SAA%20e747ade1a4344759a43bfb9f6c3fbba3/Untitled%202.png)

- Open Command Line in your computer
- run the below command

```jsx
aws configure
```

- The above command will request you to enter your keys
- it will ask you the region that you wanted to use you have to mention the right region name
- And click enter
- Now in the terminal run the below command

```jsx
aws iam list-users
```

- this command will list all the users in the IAM
- If this command do not work that mean the Access Keys that are associated with the User do not have permissions to access the IAM
- you can manage the permissions/Policies of this user back in the IAM console from your AWS Root Account.

**Another ALTERNATIVE of Accesing AWS using CLI is using Cloudshell**

Cloudshell is a inbuild command line interface in AWS, you do not have to use Access Keys.

Firstly Cloudshell is only avilable in few Regions you can check it here

[https://docs.aws.amazon.com/cloudshell/latest/userguide/supported-aws-regions.html](https://docs.aws.amazon.com/cloudshell/latest/userguide/supported-aws-regions.html)

### IAM roles for Services

Do you know how the API Gateway on AWS keeps performing some actions in your absence ? 

Its gets the data from the frontend and pass it to the backend. This is a automatic process,

AWS lambda is also works on its own when it is triggered. 

Dynamo DB on AWS stores data when a PUT request is initiated and here Dynamo DB will perform write action in its database. and all of this happens in the absence

We understand that some services on AWS will keep working when they triggered in the absence of users.

To enable Services to take action on our behalf automatically we need to grant them permission/Policies.

Example: AWS Gateway API can perform PUT operation on Dynamo DB, so to do this AWS Gateway API must be granted with a write access to the Dynamo DB. so we need to Create a Policy and attatch it to the AWS Gateway API

Now we can create a IAM Role here which can be attatched to services

so do u realise we are using the word “IAM Role”, there is a difference between an “IAM Role” and “IAM User”

“IAM User” credentials will be used by a physical Human being

Whearas “IAM Role” contains a set of polocies and this Role can be attached to a Service.

Example: EC2 instance may want to perform some actions on AWS we need to give it some permissions, to give permissions we need to create a IAM role with the policies atattched.

**Common Roles** 

- EC2 Instance Role
- Lambda Function Role
- Roles for cloud formation

### IAM Security Tools

There are two major tools

- IAM Credentials Report (account-level)
    
    This will list out all the IAM Users and more detials about the MFA whether it is active or not, Password, last active etc…
    
    And most importantly this works on account level, or the root level
    
    which means you can download the credentials report by loggining in as the root user.
    
    To look at the credentials report you have to follow few steps
    
    - open AWS Management Console
    - open IAM service
    - select the credentials report on the left hand sidebar under access reports
    - click download, and a csv file will be downloaded
- IAM Access Advisor (user-level)
    
    Access advisor shows the service permissions granted to a user and when those
    services were last accessed.
    
    To look at the Access Advisor 
    
    - Open AWS Management Console
    - Open IAM Service
    - Select the Usrs on the left hand side sidebar
    - choose the user who’s Access Advisior you want to look at
    - Select the Access Advisor tab
    - you will notice the list of polocies that have been attatched to this user and the last time it has been used.

### IAM Best Practises

- Do not use root account except for AWS setup
- Assign users to groups and assign permissions to groups, working with user groups should be easy and the best practise if you are working has a huge team
- Use and enforce MFA (Multi Factor Authentication) On all  IAM Users as well as the root account. You cannot add MFA to users instead advice them to do it
- Create roles whenever you want to give access to services
- Use access keys for programmatic access to AWS (SDK/CLI)
- Audit permission that are given to the users by using the IAM Security tools like, Access Advisor and downloading the Credentials report

### IAM Summary

- **Users**: mapped to a physical user, has a password for AWS Console
- **Groups**: contains users only
- **Policies**: JSON document that outlines permissions for users or groups
- **Roles**: for EC2 instances or AWS services
- **Security**: MFA + Password Policy
- **AWS CLI**: manage your AWS services using the command-line
- **AWS SDK**: manage your AWS services using a programming language
- **Access Keys**: access AWS using the CLI or SDK
- **Audit**: IAM Credential Reports & IAM Access Advisor