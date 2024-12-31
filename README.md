# Deployment of MarketPeak E-Commerce Website

## Objective:
The objective of this project was to deploy the **MarketPeak E-Commerce** platform, utilizing a pre-existing e-commerce template. The focus was on setting up the website using a template, deploying it to AWS, and maintaining a continuous integration and deployment (CI/CD) workflow.

## Step 1: Obtain and Prepare the E-Commerce Website Template

### 1.1 Downloading the Template
To avoid the complexities of developing the website from scratch, I decided to use a pre-existing e-commerce website template. I visited **Tooplate** (a resource for free templates) and selected a template suitable for the **MarketPeak** e-commerce platform. This template required minimal adjustments, allowing me to focus on the deployment and operational aspects.

### 1.2 Preparing the Template
Once the template was downloaded, I extracted it into my project directory called `MarketPeak_Ecommerce`. I made minor customizations, including:
- Updating the logo to reflect the MarketPeak branding.
- Modifying the color scheme to align with MarketPeak’s brand identity.
- Editing text content to suit the marketplace.

### 1.3 Stage and Commit the Template to Git
To manage version control and collaboration, I added the website files to a **Git** repository. I set up my Git configuration by running:

```bash
git config --global user.name "sabhayor"
git config --global user.email "sabhayor@gmail.com"
```

Then, I committed the changes to the repository with a clear message:

```
git add .
git commit -m "Initial commit with basic e-commerce site structure"
```

### 1.4 Push the Code to GitHub
Next, I created a remote repository on GitHub named MarketPeak_Ecommerce and linked it to my local repository. After adding the remote repository URL, I pushed the code to GitHub:

```
git remote add origin https://github.com/sabhayor/MarketPeak_Ecommerce.git
git push -u origin main
```
This ensured that my code was stored on GitHub and ready for deployment.


## Step 2: AWS Deployment

### 2.1 Set Up an AWS EC2 Instance
To host the website, I logged into the AWS Management Console and launched an EC2 instance using an Amazon Linux AMI. After the instance was set up, I connected to it via SSH to begin the deployment.

### 2.2 Clone the Repository on the EC2 Instance
To deploy the website, I cloned the GitHub repository onto my EC2 instance. I chose the HTTPS method for cloning the repository, as it didn’t require SSH key setup. The cloning command was:

```bash
git clone https://github.com/sabhayor/MarketPeak_Ecommerce.git
```
This step ensured that the EC2 instance had the latest version of the website files.

### 2.3 Install a Web Server on EC2
Next, I installed Apache HTTP Server (httpd) to serve the website. Using the following commands, I updated the Linux server and installed Apache:

```bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```
These commands ensured that Apache was installed, running, and set to start automatically on system boot.

### 2.4 Configure Apache for the Website
I then configured Apache to serve the MarketPeak_Ecommerce website. The default web directory for Apache is /var/www/html/. To point Apache to the correct directory, I first removed the default files and copied the website files from my project directory:
```
sudo rm -rf /var/www/html/*
sudo cp -r ~/MarketPeak_Ecommerce/* /var/www/html/
```
Once the files were in place, I reloaded Apache to apply the changes:
```
sudo systemctl reload httpd
```

### 2.5 Access the Website from Browser
Finally, I accessed the public IP of the EC2 instance from a web browser to view the live MarketPeak Ecommerce platform. The website was successfully deployed and accessible on the internet.


## Step 3: Continuous Integration and Deployment Workflow
To maintain a smooth development and deployment process, I set up a CI/CD workflow to handle ongoing changes and updates to the website.

### 3.1 Developing New Features and Fixes
I began by creating a development branch to isolate new features and bug fixes from the main production branch. This step ensured that the main website remained stable during updates:

```bash
git branch development
git checkout development
```
I then implemented changes, which included adding a new product page and enhancing the design.

### 3.2 Version Control with Git
After making the changes, I staged and committed them to the development branch:

```bash
git add .
git commit -m "Added a new product page"
```
I then pushed the changes to GitHub:

```bash
git push origin development
```
### 3.3 Pull Requests and Merging to Main Branch
Once the changes were pushed, I created a pull request on GitHub to merge the development branch into the main branch. After reviewing the pull request and ensuring everything was working as expected, I merged it into the main branch:

```bash
git checkout main
git merge development
```
I then pushed the merged changes to GitHub:

```bash
git push origin main
```

### 3.4 Deploying Updates to the Production Server
To deploy the updates to the live website, I SSH'd into the EC2 instance and pulled the latest changes from the main branch:

```bash
git pull origin main
```
I restarted the Apache server to apply the changes:
```bash
sudo systemctl reload httpd
```
### 3.5 Testing the New Changes
Finally, I tested the new features on the live site by accessing the public IP address of the EC2 instance. The updates were successfully deployed and worked as expected.


