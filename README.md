# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...

Lesson 1: Installing Your Environment and Setting Up the Project
In this lesson, you will install a web development environment on your computer. We will be using a tool called vagrant, which will allow us to install a web development environment rapidly. Once our development environment is installed, we'll run through the steps to start a new project from scratch.



Step 1 - Installing the Tools
Firehose Install Guide
Installing a professional web development environment on your machine usually takes a full day. You can get it done in 45 minutes, if you use the Firehose Installation Guide and do the following:

Be detail oriented: read all the instructions and don't rush through the installation.
Go step-by-step: start with step 1, then step 2, then step 3, and so on.
Follow each step precisely: if you miss a single command, things will fail and you may have to start over. Make sure you pay attention to each instruction in the installation guide.

Start the Installation Guide on Github
Step 2 - Get your environment running
Launch vagrant. If you've restarted your machine, you may need to relaunch vagrant.

Open two terminal windows inside vagrant: We want to have two vagrant windows open (the ones with the blue [Web Dev]). These web dev windows will allow us to interact with and run commands in our coding environment.

Close any Ruby on Rails servers you have running. Make sure if you go to localhost:3030 in your browser you don't see anything come up (not even the "Yay You're on Rails!" Page). During the install process, we had you run a Ruby on Rails server in a test application. If the test application is still running, find the web dev window it is running in and hold CTRL+C. This will close the server.

Full Vagrant Crash Course
If you want to get a full refresher on how to launch vagrant, connect to the environment, etc., make sure to read our vagrant web-dev environment crash course .

Step 3 - Set up the Project
To set up our new project, we'll need to run commands inside one of the web dev windows that we have open. So bring up that window, and let's do stuff with it.

Change the directory to where your code will live - remember, every time you see the gray box with a dollar sign ($) at the very beginning, it means you should run the command inside your terminal window where you also see the dollar sign.

Now, type the following without the actual dollar sign:

$ cd /vagrant/src
Type ls to see a list of all the other projects you have:

$ ls
Create a new application that uses postgres. I'm going to call my application splurty, but you can call your application anything you want, so long as there are no spaces in the name.
$ rails new splurty --database=postgresql
Now let's open up our newly created Splurty web application code with our Sublime Text Editor.

Inside Sublime Text, go to the menu and click File>Open... (or Open Folder on Windows). Then browse to your Desktop and navigate to Desktop/vagrant/src/your-app-name and open up this folder.

Adjust database.yml

We need to tell our rails application how to connect to our database. We'll need to adjust the username and password, and add a section called host. The reason we need to do this is the Firehose Project install process sets our database up with these usernames, passwords and hosts. Change config/database.yml so it looks exactly like the code below:

default: &default
  adapter: postgresql
  encoding: unicode
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: postgres
  password: password
  host: localhost

development:
  <<: *default
  database: splurty_development

test:
  <<: *default
  database: splurty_test

production:
  <<: *default
  database: splurty_production
  # username: splurty
  # password: <%= ENV['SPLURTY_DATABASE_PASSWORD'] %>
 
 
 
 
 
Then make sure to save the file.

Common Gotcha
Common gotchas
1 - Make sure the database adapter already says postgresql when you open this file. If it doesn't, you didn't create the application with the --database=postgres command. If this happened, delete this whole folder that was created and go back to the step above where you ran rails new, and continue from there.

2 - The database.yml file is whitespace sensitive. Make sure your indentation between lines is consistent.

3 - Make sure you comment out or delete the two lines under production that say username and password.

Learn about your Terminal
Before we finish setting up our project, let's first get a little bit more comfortable with navigating and using the terminal.

Let's return to the same place we started in the web dev window by running this command. This command "puts us in" or "changes the directory" to be the vagrant folder we started with.

$ cd /vagrant
Go into your web dev terminal window and list out all the files and folders by typing the following:

$ ls
After running the ls command, you should see all the files that are listed inside your vagrant folder. This is pretty much the same way you would see your files if you were to navigate to the vagrant folder by pointing and clicking on it. In fact, if you look below, you can see how things match up between the terminal and the actual Finder window on a Mac:

ls
Right now, we're inside our vagrant folder. If we want to change the directory or move into a different folder, we need another command. Let's say we want to move into the src folder. We can do this by running the following command:

$ cd src
Now let's run our ls command to see everything that's inside our src folder:

$ ls
We see two folders listed out: One is called firehose-test-app and the other one is called splurty. The firehose-test-app folder contains the app we built during the installation process to test that your system is working properly. The splurty folder contains all the files we'll be using to build our actual Splurty Web Application.

If you ever get lost in the terminal, look between the [Web Dev]: and the $ to see which folder you are currently in. Right now, since we changed our directory to the src directory, we see the details like this:

terminal
If we want to navigate back a folder (go into the parent folder, or the folder that contains the current folder), we can do that by running the following command:

$ cd ..
After typing cd .. and hitting enter, we can type ls again to see that we're now outside of our src folder.

Create your initial database
Change directory into your project

Important: Whenever we want to work with our project, we need to make sure we're inside of our project folder. (We're going to need to do this every time we open up a new web dev window). If we're not inside our project folder, most of the commands will not work.

In our case, the folder we want to be in is the splurty folder.

If we're not inside our splurty folder, our machine doesn't know what to do. So make sure you always navigate inside your splurty folder when working on the Splurty web application.

We can get into the splurty folder, which has the full location of /vagrant/src/splurty by running:

$ cd /vagrant/src/splurty
Create your initial database

At the beginning of each new web application, we need to create our initial and empty database so we have a place to store information. For this one time, do this:

$ rake db:create
This command outputs that it's creating your development and test environments. Once it is done, it will return the dollar sign:

Created database 'splurty_development'
Created database 'splurty_test'
If it says they exist already then that is a good thing. If it gives you any error message, check your database.yml file with the example in this lesson.

Start your server
Now that we have the database.yml file configured and our initial database created, it's time to fire up our server and start up our web application.

We can start our server by running the following command:

$ rails server -b 0.0.0.0 -p 3000
The web dev window where you just ran the rails server -b 0.0.0.0 -p 3000command will look like it's running forever because it doesn't return the $ sign. That's a good thing, since we want our server to be running all the time so we can see our Splurty web application all the time in our browser.

One thing you'll notice is that the rails server -b 0.0.0.0 -p 3000 command basically eats our dollar sign, so we can no longer run commands or do anything with this web dev terminal window.

Since we can't use our original web dev terminal window anymore, let's always make sure to have two, separate web dev terminal windows open. If you only have one open, open another web dev terminal window, and follow the "Change directory into your project" step, or simply run the following in your second web dev terminal window:

cd /vagrant/src/splurty
Test that everything works
Go to http://localhost:3030 in your browser. You should see something like this:

High-five!
