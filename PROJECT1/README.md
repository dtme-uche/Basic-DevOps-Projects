# Deploying a static website from GitHub to an AWS EC2 Instance using APACHE2

This project entails the detailed process of Deploying a static website from GitHub to an AWS EC2 Instance using APACHE2

The very first step includes copying and pushing your static website from your local machine to GitHub
this achieved by:
```
Creating a repository on GitHub with or without a README.md file
Cloning the repository to your local machine through the command line:
git clone https://github.com/<github-username>/<repo-name>.git
Copy your static website files and folders(if available) into this newly cloned repository

By running the following commands you will be able to Add your files to GitHub, Configure Username and Usermail of your Github
account on the command line, Commit changes made and Push your static website unto GitHub:

git add .							to add all your files at once or
git add <filename>						to add files individually
git config --global user.name <github-username>			sync and configure your github account locally
git config --global user.email <github-usermail>		sync and configure your github account locally
git commit -m "commit message"					a comit message detailing a task you performed(more like subject of a mail)
git push							push all changes unto GitHub
```

## Hurray!! We have finally pushed our Static website from our local machine to Github

### WHATS NEXT? Launch EC2 Instance on AWS UI
Navigate to the [AWS UI](https://signin.aws.amazon.com/signin?redirect_uri=https%3A%2F%2Feu-north-1.console.aws.amazon.com%2Fcloudwatch%2Fhome%3Fregion%3Deu-north-1%26state%3DhashArgs%2523logsV2%253Alog-groups%26isauthcode%3Dtrue&client_id=arn%3Aaws%3Aiam%3A%3A015428540659%3Auser%2Fcloudwatch&forceMobileApp=0&code_challenge=0_L-Mwvj9fajJo8MUS-nq4h7iAR90kvki-nPQqvBLU8&code_challenge_method=SHA-256)
```
Sign in or Sign UP
Navigate to EC2 Instance > Instance > Launch Instance
Chose an Instance name  eg. my-website
Select an AMI Image eg Amazon Linux, Ubuntu, MacOs, RedHat.
Choose a free-tier instance type eg t2.micro or t3.micro
Create and downlaod a Keypair to securely connect to your instance.
Use default VPC for network setting.
Edit the Security group by allowing HTTPS traffic from the internet
Lanch your Instance.
```

## Next?  SSH to the Instance on your local machine

Get the Public Ip Adress of the newly created instance on AWS
On your terminal navigate to the download folder or where you have your keypair saved
Run this command on your keypair file 
```
chmod 400 keypair.pem
```
The chmod 400 command is used to set the permissions on a file so that it is readable only by the file's owner
To SSH to your AWS Instance do:
```
ssh -i ssh -i /path/to/keypair.pem username@ec2-public-ip
```
If you are on the download folder or whereever you have your keypair saved you can simply run:
```
ssh -i keypair.pem username@ec2-public-ip
```
### Now you're Logged in
## Clone your Git Repo to your Instance
```
git clone https://github.com/<github-username>/<repo-name>.git
```

## Update Ubuntu packages and Install Apache Webserver
```
sudo apt-get update
sudo apt-get install apache2
```
This commands updates the Ubuntu packages and also Installs the Apache WebServer with which we'll be deploying our static website
Apache Web Server will only read webisites files located in this folder:
```
/var/www/html
```
Therefore we need to copy every file from our cloned repository to the above folder. To achieve this, do:
```
cd repo-name			to move into the cloned repo directory
cp -r * /var/www/html		copy all files from the repo-directory to the /var/www/html folder
```

## Lastly
We need to check the state of our Apache Webserver. it need to be in the enabled state to host our static website.
```
sudo systemctl start apache2
sudo systemctl enable apache2
sudo systemctl status apache2
```
The following group of commands will start Apache2 service, enable and check for its status.

## Finally
our website have now been successfully deployed on the AWS EC2 Instance and we can view it using our Instance public IP
```
http://<AWS-EC2-Instance-Public-Ip-Address>
```

We've come to the end of our first project. if you have any suggestions do let me know.
You can try out this project by forking this repo and replicating the following commands.
If you encounter any challenge do let me know here or on [LinkedIn](https://www.linkedin.com/in/uche-francis-6803b080/)
Thank you.
