#AWS EC2 Flask site

Introduction
This was my first project and attempt to launch a static website through AWS EC2. 

I built a simple Flask web application locally through VS Code, then deployed it on an AWS EC2 Linux server, and finally pushed the code to GitHub for version control and portfolio building.

This process helped me understand the full lifecycle of a cloud-hosted application.

Local Development (VS Code)
2.1 Inital backend code

I began by creating my project in Visual Studio Code (VS Code). My project structure was simple:

mywebsite/ app.py

2.2 First Flask Application

I wrote a basic Flask app:

from flask import Flask

app = Flask(name)

@app.route("/") def home(): return "Hello World!"

if name == "main": app.run(debug=True)

2.3 First Challenge (Python Environment Issue)

I immediately faced my first real debugging issue:

ModuleNotFoundError: No module named 'flask'

2.4 What I Learned

I learned that:

Python libraries are environment-specific VS Code must use the correct interpreter

2.5 Fix applied pip install flask

Then I selected the correct Python interpreter in VS Code.

Outcome

My Flask app successfully ran on:

http://127.0.0.1:5000

Introduction to AWS EC2 Deployment
After local success, I moved to cloud deployment using Amazon EC2, which simulates a real production Linux server.

I launched an EC2 instance and accessed it via a browser-based terminal.

This was my first real exposure to:

Linux terminal Cloud virtual machines Remote server management

EC2 Setup and Linux Environment
4.1 Installing Required Tools

On the EC2 server, I installed Python and pip:

sudo dnf update -y sudo dnf install python3 python3-pip -y

4.2 Second Challenge (Flask Missing Again)

I encountered another error:

ModuleNotFoundError: No module named flask

4.3 What I Learned

This taught me:

EC2 is a completely separate environment from my system and all dependencies must be installed again on the server even if initial code i prepared installed the dependencies. 

4.4 Fix Applied

python3 -m pip install flask 

Outcome
Flask installed successfully and was verified.

Deploying Flask on EC2
5.1 Writing the server application

I created a Flask app that can operate and be accessed on other systems

from flask import Flask

app = Flask(name)

@app.route("/") def home(): return "Hello from AWS EC2!"

if name == "main": app.run(host="0.0.0.0", port=5000)

5.2 Running the Application python3 app.py

5.3 First Successful Cloud Deployment

I accessed the application using:

http://EC2_PUBLIC_IP:5000

This was my first cloud-hosted web application.

Networking and Security Understanding
However, I still could not access the site on my browser. I then realised that you have to configure the EC2 security group inbound rules to allow public access. 

To make the site accessible, I had to configure:

Open port 5000 Allow public access (0.0.0.0/0 for testing)

This helped me understand basic cloud networking concepts.

Git & Version Control Learning
7.1 Initial Git Setup

git init git add . git commit -m "first flask website" 

7.2 Learning Branch Concepts

I encountered errors when using in the terminal:

master main

Learning Outcome

I understood:

Git branches are just pointers to commits modern GitHub uses main by default

Fix:

git branch -M main

GitHub Integration Challenges

8.1 First Issue: Merge Conflicts

The GitHub repository I initially created was created with a README, causing:

This created two different instances of the repository, one in EC2 and one in the orignal GitHub repository, therfore Git was unable to perform a merge between the two repositiories. 

Fix:

git pull origin main --allow-unrelated-histories

This command allowed me to merge the two independent versions of the repository into a single history.

8.2 Second Issue: Authentication Failure

I encountered:

403 Permission denied

Password requested for pushing to Git. 

Fix: Personal Access Token (PAT)

I generated a PAT and used it instead of a password during push, I used classic token and ensured that the PAT gave repo permissions.

git push -u origin main

Key Skills Learned
Through this project, I gained experience in:

Setting up AWS EC2 instance and deploying a Flask application to the cloud

Using Linux command line on EC2 terminal to push application to GitHub

Using python to create simple Flask static web application 

Git version control GitHub repositories deployment 

Challenges Faced 
Flask module missing environment isolation EC2 setup confusion Linux server basics port not accessible Cloud networking rules Git branch mismatch version control understanding GitHub authentication error Security using PAT

Final Outcome

I successfully:

Built a Flask web application deployed it on AWS EC2 Made it publicly accessible, pushed it to GitHub and learned to debug when errors arose. 

**Update - to ensure page runs when Secure Shell is not running on host EC2 machine 

nohup flask run --host=0.0.0.0 > flask.log 2>&1 &

this prevents Linux from sending the hangup signal (SIGHUP) when SSH disconnects, and logs both stream 1(regular messages) and stream 2(error messages) into the same log file. 
