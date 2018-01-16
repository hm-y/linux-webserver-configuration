# linux-webserver-configuration

### UDACITY FSND Part 5: Project Description

> **Project Overview**  
> You will take a baseline installation of a Linux server and prepare it to host your web applications. You will secure your server from a number of attack vectors, install and configure a database server, and deploy one of your existing web applications onto it.  
>   
> **Why this Project?**  
> A deep understanding of exactly what your web applications are doing, how they are hosted, and the interactions between multiple systems are what define you as a Full Stack Web Developer. In this project, you’ll be responsible for turning a brand-new, bare bones, Linux server into the secure and efficient web application host your applications need.  
>   
> **What will I Learn?**  
> You will learn how to access, secure, and perform the initial configuration of a bare-bones Linux server. You will then learn how to install and configure a web and database server and actually host a web application.  
>   
> **How does this Help my Career?**  
> - Deploying your web applications to a publicly accessible server is the first step in getting users  
> - Properly securing your application ensures your application remains stable and that your user’s data is safe  

## Information for the Reviewer  
  
**SSH Login: ssh grader@18.217.182.173 -p 2200 -i udacity_key**  
IP Address: [18.217.182.173](http://18.217.182.173/)  
Port: 2200  
Username: grader  
  
The server runs [the catalog application](https://github.com/hm-y/catalog-app).  
All necessary environment packages are added such as Flask and PostgreSql.  

## Project Steps, Configurations, Changes...  
  
**1. Create an instance of Ubuntu Server on Amazon Lightsail**  

Picture comes here  
  
**2. Securing the server**  
  
- Updating the installed packages:  
sudo apt-get update  
sudo apt-get upgrade  

- Changing the SSH port from 22 to 2200  
- Configuring UFW to only allow SSH (port 2200), HTTP (port 80), and NTP (port 123)  
  
Picture here  
  
**3. Creating "grader" account with sudo access and SSH key pair**  
  
- Creating new user:  
adduser grader  
usermod -aG sudo grader  
  
- Generating key pair for "grader", locating the file and authorizing the key  
  
**4. Preparing for the app**  
  
- Setting the local time to UTC  
sudo dpkg-reconfigure tzdata  

- Installing Apache & mos_wsgi  
sudo apt-get install apache2  
sudo apt-get install libapache2-mod-wsgi  

-  Configuring Apache to handle requests using the WSGI module  
Add "WSGIScriptAlias / /var/www/html/myapp.wsgi" into "/etc/apache2/sites-enabled/000-default.conf"  
and then "sudo apache2ctl restart"

- Installing PostgreSQL, Disabling remote acces & creating db user  
Install:  sudo apt-get install postgresql  
Log in to psql:  "sudo su - postgres" and "psql"
Create user and db: "CREATE USER catalog WITH PASSWORD 'password'; CREATE DATABASE catalog OWNER catalog;"  

**5. Seeting up the app**  


