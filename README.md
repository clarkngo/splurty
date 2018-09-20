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

Lesson 2: Setting up the Web Development Pipeline
In the previous lesson, we setup our initial project structure. We're going to use a few different tools in the course of this application and this lesson will initialize our project to use each of them. These tools are: git, GitHub and Heroku. We will cover what these tools are and how to use them in future lessons. Once we setup our project with these tools, we will be able to start working on our specific project.

Classmates working on this track:
         

Before we move forward with coding, let's do what every web developer does first and set up our web development pipeline so we can back up our code frequently and push changes to our application live onto our server on the internet.

With that in mind, let's start our new project by setting up our pipeline and connecting it to GitHub (to keep our code safe) and Heroku (our server, to go live onto the internet).

First, make sure you are in the directory for Splurty. In your terminal you should see:

[Web Dev]: /vagrant/src/splurty $
If you don't, type the following command:

$ cd /vagrant/src/splurty
Step 1 - Set Up Git
The next command is the command that we'll run a single time so that our project will use git.

Again, we see the dollar sign ($), so we need to type this into the terminal window, without the actual dollar sign.

$ git init
This gets everything in the current folder ready to be tracked by git.

$ git add --all
This takes the first commit, or snapshot of our application code.

$ git commit -am "Initial commit"

Common Gotcha
Common gotcha
You may see what looks like an error message come up after you run git commit if you messed up a step in the install guide. If it spits out a bunch of lines with stuff like git config --global user.name "Your Name" at you, check this post about how to fix the problem.

Step 2 - Set Up GitHub
Go to GitHub.com. Log in and click on the green "New repository" button.

Enter a repository name, and make sure the 'Public' radio button is selected (this is the default in GitHub).

Important: DO NOT check 'Initialize this repository with a README.'
Now, go on and press the Create repository button.

First, click on the button in the top that says "SSH." This tells GitHub we want to authenticate using what are known as SSH Keys, or basically just password files (see the image below).

Second, scroll down and follow the instructions to "Push an existing repository from the command line." Copy and paste both of the lines that you see on the GitHub page: git remote add ... and git push ... one at a time into the terminal (make sure the terminal is in the directory for Splurty first). It's important to take these from the GitHub page because they will be pre-populated with information specific to your account.

You may see the following warning message:

Warning: Permanently added the RSA host key for IP address '$IP' to the list of known hosts.
It tells you that you're connecting to an IP address for github.com that you haven't used before. It is nothing to worry about.


Refresh the page in GitHub and watch as the page changes and our web application folders are listed on the page.

Common Gotcha
Common gotcha
If you refresh the page and it doesn't change to show all the files, and you look in your web dev window where you ran the command and see something like this:


What happened is you missed the step where you select the "SSH Key" authentication. This means every time you send your code to GitHub, you'll be prompted with this and you'll have to enter your GitHub username and password when it asks you to. That's ok, but make sure to enter your username and password here when it prompts you for it.

Step 3 - Opening our Text Editor
Next, let's open our text editor. We suggest you use the Sublime Text editor, so open up that program. When you first open the program, it's probably going to look like this:


First thing we want to do is set some preferences so our code is indented properly. Indentation is very important when it comes to coding. It makes code more readable and much easier to locate bugs and typos. Be sure to follow the directions for the version of Sublime Text you're using (2 or 3).

Sublime Text 2
For Mac, go to: Sublime Text 2 > Preferences > Settings - Default 
For Windows, go to: Preferences > Settings - Default 

You should see something like this:


Now we want to scroll down until we find the setting "tab_size" and the setting "translate_tabs_to_spaces". Once you find those, change the "tab_size" to have a value of 2, and change the "translate_tabs_to_spaces" value to true. (Be sure not to use quotes for the values) 

Your two settings should now look like this:



Sublime Text 3
For Mac, go to: Sublime Text 3 > Preferences > Settings - User 
For Windows, go to: Preferences > Settings - User 

You should see something like this:


Add the following lines of code:

"tab_size": 2,
"translate_tabs_to_spaces": true
For Both Versions
Now save the file and close sublime text. Now open sublime text back up. When you open it up you should see in the bottom right pane "Spaces: 2". This tells you that your tabs are converted to spaces and they use 2 spaces. If this says something otherwise you can click on the pane and change the settings for each file there. 

Here is an image of what the bottom pane should look like:



We have our settings configured, so now what we want to do is open our whole web application folder in Sublime. This will give us easy access to all our files.

In the menu, go to File>Open... (File>Open Folder on Windows) and select your app folder, then press the "Open" button:


This will open up a coding environment with all the files listed on the left-hand side. Now to open a file, all you need to do is click on the file name in the project explorer on the left.


Our Sublime Text editor, where we'll be coding, has an indicator of whether the file we're working with has been saved or not. If the file has been saved, there will be a grey 'x' in the top of the tab. If there is a grey circle in the top of the tab, it indicates the file has been changed, but not yet saved.



Step 4 - Deploying to Heroku
Now we'll need to create a project in Heroku. Everyone will need to have a different name, so adjust the name so your project name is unique.

$ heroku create splurty-firstname-lastname
Now push it up to Heroku with the following command:

$ git push heroku master
It should take a few moments to run, and when it finishes it should say "Launching..." along with a URL.

To easily see our heroku url we can type:

$ heroku apps:info
Copy this URL and paste it into your browser.

When you go to this URL, it will initially tell you, 'The page you were looking for doesn't exist.' This is because we haven't built our application yet. That's the next step.

One thing that's important to note is that our web application has two environments. One is "localhost," or your very own machine/computer that we will test our code on locally. (Another name for this environment is your development environment). Then, we have our application that is live on the internet on Heroku. (Another name for this is production).

How does this save me time?
As we build out our application, we want to treat our localhost as separate from our real, live environment. This means we shouldn't spend time entering data into localhost, because that data won't ever make it into production. Our Heroku app is the environment we'll take the time to put all our good quotes into.

Lesson 3: Wireframing our web application
In this lesson, we will take a moment to take a step back and think through the application we're setting out to build. We will do this with a practice that is known as wireframing.

Classmates working on this track:
         

Before we start coding, we always need to have a good idea of what we're actually building. To get our idea across visually, we use a technique called wireframing.

Quickly drawing out what we want our application to look like, and which features we're actually building is really important. Going through this wireframing exercise at the beginning of each web development project ensures that we always have a place we can refer to and double-check we're still building what we set out to build in the first place. In short: all good developers do this, so you should do it too.


Let's take a look at the wireframes that we will turn into a fully functional web application in a step-by-step process:

Let's start with the homepage where we can show all the quotes/sentences to any visitor that comes to our page.

Splurty Homepage

Then, let's build a form where users can add a quote. Rather than having our form on a separate page, let's put it inside of a fancy-looking modal (basically a popup box).

Adding a Quote

The last page is a quick about page where the world can learn a bit more about you and your awesome app.

About Page

Customizing your web application
Important: We want you to use your own creativity and build your very own quote-splurting web app. So make your app splurt out advice about something that you're passionate about or something that's funny and will crack your friends up when you share the app with them.

Here are a few different ways you can think about customizing your own Splurty app.

You know you're an urban planner when...
I love Boston, but I really hate that...
Startup advice for entrepreneurs...

Awesome - now that we have a solid idea of what we want to build, let's get cranking and write some more code!

Lesson 4: Setting up the Homepage
In the previous lessons, we've setup a blank project. Right now, our project shows us the default Yay! You're on Rails! message. In this lesson, we'll change this to just show the message of Welcome to my Awesome Web App on the main page of our web application.

This lesson will introduce the concepts of: controllers, routes and views. Follow along, but if it seems like a lot to process, know that after we build the full splurty web application, we will present a series of video overviews that explains how these different components interact in our application.

Classmates working on this track:
         

How to go through these lessons
Before we start coding, here's some advice about how best to go through all the lessons.

Each lesson will give you clear instructions for when to write what kind of code and run commands in the terminal. At first, you might think copying and pasting is the way to go, but that's not really true. While copying and pasting might make you feel like you're making a lot of progress quickly, it actually hurts your learning, because coding is best learned by doing. This means, the more code you type, the more you will retain and be able to reproduce later on when you build your next web application.

Common Gotcha
One rule to always follow:
Type out every line of code!
We care about your learning and believe the best way to absorb all the information here is to type every line out. Otherwise, unless we explicitly tell you to copy and paste a particular section of code you should type it into your terminal and text editor.

Now let's get started building our first page, the homepage!

The very first step - getting our coding environment ready
To start with, we need to make sure our coding environment is ready for us to start coding. Make sure you have those two web dev terminal windows open like we set up in Lesson 1. Also, make sure you have your server running in one of them, and that when you go to http://localhost:3030 it takes you to the "Yay You're on Rails!" page. The terminal windows will allow us to send commands to our web development environment.

Next, let's open our text editor. For a refresher on how to do that, you can refer to the Opening our Text Editor step in Lesson 2.

Let's get coding!
If we look back at the wireframes, we see that the homepage should be the page that displays a random quote. Our homepage is also the page that a user sees as the very first page. So when we type in the URL and it doesn't have anything after the .com, .net, .org, etc. (for example http://awesomeURL.com), we get to see the homepage. In web developer talk, the homepage is also called the root of the app.

Throughout this guide, we're going to type commands that look like rails generate ... into our project a lot. If you think back to one of the very first steps we took, we ran rails new ..., which built up a blank rails web app for us. That single command wrote a ton of code for us and set us up with a full, blank web application that was ready for us to start changing and adding code to. So in short, using rails generate ... commands will always save us a lot of time, because it writes standard code for us automatically.

To start building our homepage, we need a few different pieces. One of the most important pieces is called a controller. To build this new controller, we want to run a single command in the terminal (without the $ sign):

$ rails generate controller quotes
Now, what just happened? The rails generate command will automatically write a bunch of code for you. The part of this that looks like rails generate tells Ruby on Rails it's time to write some code for us. The next thing we specify is what we want to generate, which in this case is a "controller" (we'll explain what a controller is a little bit later), and then the last thing we do is give the thing we are generating a name. So in this case, we're telling Ruby on Rails to write code to build us a blank controller called "quotes."

We're going to be doing this a lot, so even if it's a little fuzzy now, as you continue to run this command throughout the project it will start becoming a lot clearer. Hang in there for now.

Common Gotcha
A common gotcha
Don't forget the s at the end of quotes in the rails generate controller quotes command. Rails assumes the controller names are in the plural form.

Continue setting up the quotes controller
After we've set up our quotes controller, we need to do a few more things before we can view our page.

First, open up config/routes.rb and add this line someplace after the line that saysRails.application.routes.draw do, and before the line that says end.

Make sure the line doesn't start with a hashtag and the text inside the Sublime editor is not grey:

Rails.application.routes.draw do
  root 'quotes#index'
end 
Then save the file.

Next, open up your quotes controller in app/controllers/quotes_controller.rb and adjust the file to look like this:

class QuotesController < ApplicationController
  def index
  end
end
 
 
Save this file as well.

And finally, we need to create a new file inside our app/views/quotes folder. This folder was automatically created when we ran our rails generate command.

In Sublime Text, go to app/views/quotes/ in the file-tree view on the left part of the application. Right-click (or CTRL+click) on the quotes folder and create a new file. Save this file and name it index.html.erb.

Inside the index.html.erb file, add the following line:

<h1>Welcome to my Awesome Web App</h1>
Before we move on, one thing we can notice here is that the file ends in .html.erb. Most of the other files we've dealt with end in .rb. The file extension .rb means it's only ruby code that's in the file.

The files that end in html.erb are HTML files that can pull in ruby code to run alongside regular HTML.

So what are HTML files? In short, HTML files describe the content that exists on a page. There tend to be things wrapped in angle brackets and these are known as HTML tags. For example, in the code we just wrote, we added <h1>Welcome to my Awesome Web App</h1>. This line of code is nothing more than a little section that starts an h1 - or a big headline - and fills it up with the text "Welcome to my Awesome Web App" and then closes the headline.

We're going to use a lot of different HTML tags throughout the tutorial, and you'll learn them best by using them with us in practice.

Awesome, now if you go to http://localhost:3030 you'll see the text, "Welcome to my Awesome Web App." Nice :)

Common Gotcha
Common Gotcha
If you refresh localhost:3030 and it continues to display the "Yay You're on Rails!" page, this is usually because you have the wrong project running in the server window. See this comment for more information on how to fix that.


Git Commit
Let's make a git commit for this step so we can back up our code on GitHub and don't have to worry about losing anything if our computer crashes.

If you jump over to our git workflow guide here, you can get all the individual steps on how to run through the git commit workflow.


Lesson 5: Setting up the database for Quotes
In the previous lesson, we changed our application to show a custom message. Currently, we've hardcoded the message to Welcome to my Awesome Web App. In other words, our code contains the message the user sees explicitly. Eventually, we will want users who visit our application to enter custom user-generated data on our application. To support this behavior we're going to need to use a database. In this lesson, we will setup our database.

This lesson will introduce the concepts of: models, database tables and database migrations. Follow along, but if it seems like a lot to process, know that after we build the full splurty web application, we will present a series of video overviews that explains how these different components interact in our application.

Classmates working on this track:
         

Before we move on and continue to style and design our homepage, we should put on our web developer hats and write some code that will make it possible to store an actual quote inside our database.

If we go back and take a look at our wireframes, we can see that our web application has a form, where a user can fill in two different form fields to save a quote. The fields are for the actual quote and for the name of the author.

Adding a Quote

For our web application to work, we need to set up our database with a table that can hold those two form fields for every single entry. (Picture an Excel spreadsheet in your mind, where quotes and author are the columns and all the different quotes are in separate rows.) For now, let's call the two form fields inside our form the following:

saying
author
Those are the same fields that we want to have available in our database (again, think of it just like 2 columns in an Excel sheet).

When using Ruby on Rails, we first need to create a model (which is like a translator that helps us talk to our database) whenever we want to create a new table in our database.

Run the following in the terminal:

$ rails generate model quote
This will create the model and a migration file (don't worry about what a migration file is just yet) for us.

The first step is to edit our new migration file. The last command we ran (that rails generate one) built up the template of a file for us. The file it made us is located in our project at db/migrate/XXXXX_create_quotes.rb, where XXXXX represents the date and time when you ran that command to generate the model.

We'll want to adjust the file to look like this:

class CreateQuotes < ActiveRecord::Migration[5.0]
  def change
    create_table :quotes do |t|
      t.string :saying
      t.string :author
      t.timestamps
    end
  end
end
 
 
Then save this file (saving the file now is VERY important).

After we've filled out our migration file, we can create our two columns inside the database table by what's called "running the migration."

We run our migration and create two fields in our database table with the following command in the terminal:

$ rake db:migrate
Awesome. Even though it doesn't look like much just yet, we now have a database and a model for our web application and are ready to store author names and quotes (or "sayings") in our database.

Common Gotcha
A common gotcha
If you forgot to save the file, or you immediately realize you want to change the migration to do something like add another field, you can undo the last migration with rails db:rollback and adjust the migration file to be how you want it. Then, save the migration file and re-run rake db:migrate.


Run through a git commit
Since we finished this step, let's make a commit by following the standard git workflow.

Lesson 6: Show a Quote from our Database on our Page
In the previous lesson, we've introduced the structure of a database. In this lesson, we'll interact with our database in our application and will show items that exist in the database on the main page of our web application.

Classmates working on this track:
         

The first thing we'll want to do in order to show a single quote on our homepage is actually pull the very first quote from our database and store it in a variable. What we'll do is create and load a variable in our quotes controller with the first quote in our database.

Open app/controllers/quotes_controller.rb and make the index method look like this:

def index
  @quote = Quote.first
end 
Now, the first quote that we have in our database is stuffed into the variable called @quote.

Save this file and open back up app/views/quotes/index.html.erb. Change the welcome message we put in this file to look like this:

<h1><%= @quote.inspect %></h1>
Then save the file. Now if we go to http://localhost:3030 and view our page, we'll see something that looks like this:


Ok, that looks pretty bad and I promise we'll fix things up in no time, but before we put on our web design hats, we need to keep rocking our web developer hats and make our database work.

What is happening on our homepage is our web application is listing out the first Quote in our database in a very "developery" but readable way. As you can see, we don't have any quotes in our database table yet (that's why it says nil, which basically means blank), so let's add them by using a fancy developer tool called rails console.

Go into your terminal and type:

$ rails console
Now we can directly add an item to our database by using the rails console without the need for a silly form (that's for non-developers). I'm going to run code that looks like this to add a quote about entrepreneurship to my database. Adjust your code accordingly to add a quote that fits in with your application (don't paste in the ">").

> Quote.create(saying: 'Work like there is someone working twenty-four hours a day to take it all away from you.', author: 'Mark Cuban')
You may have a problem running the command to add the quote directly into your database. Whether you have problems or not, read the section One Common Gotcha below. It will help you avoid seeing error messages in the rails console.

Common Gotcha
One Common Gotcha
Inside this rails console, we're writing and executing ruby code. In ruby, we can enter text by starting and ending the "text section" with either a single quote (') or double quote (").

For example, take the case where we want to represent the text hello or awesome inside ruby. Let's look at a few commands to show you how we can represent text inside our rails console:



We will encounter problems inside the rails console if we try to put an apostrophe in a line of text that starts off with the single quote ('). Let's think about representing the line of text: You're Awesome in ruby. If we run this command in the rails console, we'll see problems like the one below:



If you're inside the rails console and after pressing enter you don't get the greater-than sign (>) starting the line, it means your rails console is not ready for your next command. In other words, this means you can't add more commands, or press enter.

What's happening here is ruby sees a closing apostrophe in the word "You're" and thinks we're trying to end the line of text, when what we really wanted to use the apostrophe for was to connect "You" and "are." If that happens, ruby sees an extra quote at the end of each line. This isn't what we want and it confuses ruby and the rails console. Once this happens, nothing works anymore and our rails console hangs.

If you end up in this situation and you want to get out of it, hold CTRL+C and it will abort the previous command and give us the greater-than sign back. This means that pressing CTRL+C will make the rails console ready for more ruby code (and show us that greater-than sign again):



Now that we fixed the problem, we can look into how to represent the line of text, You're Awesome. To make this work, we need to use a technique that web developers call "escaping" the text. Basically, we tell ruby right before the second apostrophe that it shouldn't end the text, but treat our apostrophe, well, like an actual apostrophe.

We do this by using a backslash (\). Here's an example:



When we use the backslash to escape the text, we see that our rails console gives us the greater-than sign back. Boom, that means we're good to go.

The important takeaway however is to make sure after you run a command in the rails console that it gives you the greater-than sign back. If it does not, it means it neither ran your command, nor is ready to take in more. And if this happens to you, holding CTRL+C will give you the greater-than sign back without running your previous command, and you'll be ready to run more commands.

Let's keep going and create another quote
Now create a second quote, using the same type of command.

> Quote.create(saying: 'You\'re better off with a kick-ass half than a half-assed whole.', author: 'David Heinemeier Hansson')
Exit the rails console by typing:

> exit
After you type exit, you should see the dollar sign again inside your terminal window.

Now if you refresh your browser window, you should see one of your quotes up there:


Ok, this still looks very "developery," so let's adjust the page to look more like the wireframes. What we want to have is the quote in a big text, and the author underneath it in smaller text. Adjust app/views/quotes/index.html.erb to look like this:

<h1><%= @quote.saying %></h1>
<h2>- <%= @quote.author %></h2>
Awesome, now our web application pulls the "saying" together with the "author" from our database and lists it on our page.

Making it pull a random quote
Now if we refresh the page a lot of times, we see the same quote is listed time after time. But what we really want is for our app to splurt out a random quote, rather than the same quote over and over again.

So why is it always the same one?

Well, if we look in our quotes_controller.rb, we see the code that is loading up the quote that we want to display on our web application. In this line of code, we're only pulling out the very first quote from our database. It turns out that the first quote we pull out will always be the quote that we saved into our database first, which is why nothing changes.

Obviously, we want to change that. We can do that by shuffling the items in our database to always make a random quote be the very first one.

Ok, so let's make this little tweak to app/controllers/quotes_controller.rb.

def index
  @quote = Quote.order("RANDOM()").first
end 
Ok, now let's refresh the page a few times.

Cool, now it's pulling out different quotes from our application, seemingly randomly. Nice!


Do another git commit
Since we wrapped up this lesson, go through your standard git workflow and back up your code.

Push your page live on the internet using Heroku
It's good web development practice to push our code live to the server whenever we've completed another feature, making sure everything works on the live server as well.

Keep your fingers crossed, we're going live with our web application!

Go into your terminal and run the following:

$ git push heroku master
Pushing your app live to the internet will take a while; you'll need to wait a few moments for it to complete.

After the Heroku script finishes running, look at the very bottom of the script and copy the URL that looks something like http://my-awesome-app.herokuapp.com. Open that URL in a browser and see what's going on.

When we check, we see that an error message comes up on Heroku. This is expected, and errors happen all the time in the life of a web developer. Follow along for the next few steps as we fix the error with you.

We see an error message that something went wrong
Let's zoom out a little bit and understand why this is happening...
Our quotes are stored inside a database, which is a lot like an Excel file. If you think about how we would represent our data inside an Excel sheet, we would have a full sheet devoted to "quotes," and it would have separate columns for the saying and author. It would look kind of like this:



But our database on our development machine is separate and different from the database in our Heroku app. That means that our database hasn't been properly set up yet. We have two different databases, one on our local computer and one on our Heroku server.

Why? It's less important right now why we have two separate databases (one for our local machine and one for our Heroku app), but it's important to know that the two databases are different (so it's like there are two different files keeping track of our data— one for our localhost, and one for Heroku).

Right now, don't get too hung up on how the database works, where the data is stored, or why there is a separate database for our local machine vs. Heroku. Right now, it's just important to know that the two are different.

Because we have two different databases, this is where our problems come up.

Let's fix our application
A few steps back, we ran the rake db:migrate on our local machine to set up our database with columns for "saying" and "author." This worked well for our local database, but since we're using two different databases (one local and one on Heroku), we need to run the same rake db:migrate command on Heroku as well.

To add our database columns for "saying" and "author" on Heroku as well, we can run the following in our web dev terminal:

$ heroku run rake db:migrate
This command will set up the columns for our database table (saying and author), but it will not copy over the data from our local database!
There are two fundamentally different characteristics of the database. There is the structure of it, or basically the columns inside the database, which lets us know what's allowed to go inside it. We also have the data itself. Running the migrations (either locally or on Heroku like we just did above) is all about setting up the structure, or the columns. It does nothing to set up the rows, or records, which in my case are the quotes from Mark Cuban and DHH.

After we run the migrate command, it's usually good to restart our Heroku server as well (occasionally weird error messages will come up if you don't) - so let's do that now too:

$ heroku restart
Unfortunately, we still have an error message.

If we think about what we did to our database, this makes more sense. We basically went from an empty file with no sheets (or tables) to store any data in, to a single table with the headers set up. However, we still don't have any data in our table.

If our database were an Excel sheet, it would look like this:


Now if we go back to "my-awesome-app.herokuapp.com" we still seem to have an error message up there.

If we want to debug the problem, we can run heroku logs --tail in our web dev window. Right after, we should reproduce the problem by refreshing the page with our error message. If we then look into our web dev window, we can see a line that looks kinda like this (you should be able to find this in your Heroku log, but if you can't, just keep following along):

ActionView::Template::Error (undefined method `saying' for nil:NilClass):
2014-06-21T19:48:28.161800+00:00 app[web.1]:     1: <h1><%= @quote.saying %></h1>
2014-06-21T19:48:28.161801+00:00 app[web.1]:     2: <h2>- <%= @quote.author %></h2>
2014-06-21T19:48:28.161802+00:00 app[web.1]:   app/views/quotes/index.html.erb:1
Ok, to get out of this view, hold CTRL+C and you'll be returned to your dollar sign.

This is telling us that in our view, app/views/quotes/index.html.erb on line 1, we have an error message when we're trying to do @quote.saying. It's saying "undefined method `saying' for nil:NilClass." Remember when we didn't have anything in our database on our localhost and we saw that "nil" in our web application? We told you that nil basically means the blank value.

The error we see here is caused because we have set up the structure (or the columns) on our database, but we have no rows inside our table. So let's add a quote to our app so we can get a row in our table. By adding a quote to our app, we should hopefully fix our error message.

Read the Heroku Troubleshooting Guide to get more background info and also learn how to "debug" Heroku problems for your web application.

Adding a quote to our Heroku database
We have two different databases (one local, one on Heroku) and our database on Heroku simply doesn't have any quotes in it yet. By running heroku run rake db:migrate, we created a blank database, but we haven't put anything in it yet. Let's change that.

We can add a few new quotes directly into our Heroku database by doing the following:

In a web dev window (or a puTTY window for Windows users), type:

$ heroku run console
This command will load up the rails console (the place where we can directly interact with our database). However, since we added the "heroku run" part to the command, we're actually running this console on Heroku instead of on our local machine.

When you're presented with the ">" sign, enter the following (don't paste in the ">"):

> Quote.create(saying: 'If I could drink only one wine, it would be Champagne.', author: 'Gary Vaynerchuk')
Now if you refresh your browser window for "my-awesome-app.herokuapp.com" you should see your newly added quote. (Make sure to adjust the URL so it looks like the URL you use for your Heroku application.)

You will only see the quote that you added inside the Heroku console just now. So for example, my Heroku application would only show me the Gary Vaynerchuk quote, but my localhost would cycle through the two other quotes I added (the Mark Cuban and David Heinemeier Hansson quote).

Help yourself in the future by using our Heroku Troubleshooting Guide for tips on how to fix problems with Heroku.

Nice! We're done with this section. Let's go on to the next lessons and make our web application look a little nicer!

Lesson 7: Adding Bootstrap
In the previous lessons, we've configured our application to display quotes from our database. The application doesn't look well-designed, however. In this lesson, we'll integrate with Bootstrap. Bootstrap is an open source technology that will allow us to make our application look well-designed quickly, with a minimal amount of work in the next four lessons.

Classmates working on this track:
         

Right now, our application looks straight out of 1995 and not like a modernly designed web application.

To fix this, we will start to change the design of our web application by using a front-end framework called Bootstrap 4. By using Bootstrap, we get a lot of amazing design widgets and code snippets out of the box so we can continue building and launching an awesome web application at a fast pace.

Bootstrap 4 will give us fine-grained control over how our web application will look on different screen sizes and easily allow us to make our web app look perfect on mobile, tablet and desktop screens.

Take 10 minutes and go to the Bootstrap Documentation, click around, check out some of the features (remember, we need a modal later on) and read through a bit of the Bootstrap documentation. It might not all make sense right away, but we'll walk you through how to use it.

For us to pull all of the Bootstrap functionality into our app, we would normally click on the big download button and start copying and pasting many different files and hundreds of line of code into our web application. That's a pretty boring and repetitive task, and as developers, we hate to spend our time on manual processes like this. Instead, we like to have programs automatically perform the work for us.

Instead of copying and pasting code someone else wrote into our application manually, a potentially error-prone task, ruby developers will use a feature known as ruby gems.

Each ruby gem is a package of code someone else wrote that we can easily import into our application to accomplish a particular task. Think of it like a little program that we can add to our web application to give it additional features.

This is the first time we're adding a new gem to our project. We are going to integrate with many ruby gems in the course of the program.

In this case, we will integrate Bootstrap into our rails application using the bootstrap-rubygem gem. The bootstrap-rubygem gem will download the Bootstrap files and copy them into all the right places inside our web application.

Ok, let's get the Bootstrap gem into our app. To do this, all we need to do is include a couple lines of code in our project. Although we're looking at the source code and documentation on GitHub, we don't have to download the code, but we have the code available to look at if we want to do advanced open-source contribution.

Follow the documentation on the gem page
Go to the bootstrap-rubygem gem documentation and scroll down to the section titled Installation. They give you a few different options for installing the gem, but the guide we need to follow is the first one. Read the section titled Ruby on Rails.

Common Gotcha!
You might notice the documentation of the Twitter Bootstrap is a little different than the steps we outline here. This is because the Twitter Bootstrap gem is in flux currently. Following the steps in the Twitter Bootstrap documentation may cause errors. Use the steps below, to avoid these errors.

The first thing we need to do is a few lines of code to our Gemfile, but before we do that, let's take a moment to talk about what the Gemfile actually does.

The Gemfile is a listing of all the gems we need to use in our web application. Whenever we want to include a new gem in our project, we'll need to add a line of code to the Gemfile, and then run an installation command to make sure all the newly added gems are properly installed.

Let's open up the Gemfile in our project and get ready to add a line to it.

Check for jQuery
Before we countinue, we need to make sure our Rails project has the jquery-rails gem installed in the Gemfile.

New versions of Ruby on Rails will not ship with jQuery in the project by default, but this change is very recent and other versions will ship with jQuery as a default. Here's why this change happened:

jQuery is incredibly useful. Previous to the change, a lot of rails internal code depended on jQuery, which means opting out of jQuery would be difficult and break some internal things.

This change makes it optional (but not included by default). It's a step in the right direction for the framework, but as developers who want to use jQuery, it adds an extra step for us. Twitter Bootstrap 4 relies upon jQuery, so if we want to use that, we will need to first add jQuery to our project.

Open up the Gemfile and look for:

gem 'jquery-rails'
If this exists in the Gemfile, you can skip the Installing jQuery section that is next.

Installing jQuery
Open the Gemfile located in the root of the Rails project and add the following:

gem 'jquery-rails'
Save the file.

Install the gem by running the following command in the terminal:

bundle install
Next, open assets/javascripts/application.js and add the following above turbolinks:

//= require jquery
//= require jquery_ujs
//= require turbolinks
//= require_tree . 
 
Save the file.

Restart the Rails server and continue with the rest of the lesson.

Ok, so back to our Gemfile, we need to add the following lines to the bottom of the file. Make sure you add the line of code in a way such that they're not between a "group ... do" and an "end," where the indentation has some tabs in it (we'll go over what that means right after we show you the code).

gem 'popper_js', '~> 1.11.1'
gem 'bootstrap', '4.0.0.alpha6'

source 'https://rails-assets.org' do
  gem 'rails-assets-tether', '>= 1.3.3'
end
Ok, so here's an example of the wrong way to set up the code, and here's the right way. If you put the line inside one of these "groups," it doesn't pull it into your main web application, which is what we'll almost always want to do.

Save the file and run the command to tell our web app to read that Gemfile and suck in the new gem that we just added. Type the following into the terminal (we're going to need to do this command every single time we change that Gemfile).

$ bundle install
Restart the Server
Every time we run our bundle install command, we need to make sure to restart our server. Restarting our server turns off our application for a moment and fires it up again, so we have access to all the newly installed functionality.

We can restart our rails server by doing the following:

Find the web dev window where the server is running (it's the one without the dollar sign).
Hold CTRL+C to shut down the server. The dollar sign should come back.
Now type the following into the same web dev window:
[Web Dev]: /vagrant/src/splurty $ rails server -b 0.0.0.0 -p 3000
We're going to be restarting our server a lot while doing web development, so getting used to how to restart our server is important.

Continuing the Bootstrap Install Process
Ok, the next thing we see in the Bootstrap gem instructions is to add a couple lines of code into our app/assets/stylesheets/application.scss.

Unfortunately, we don't have a file with this exact name. But we do have a file that's called application.css. Basically, the application.scss is a more powerful version of our existing application.css. If you look a little further down the documentation, you'll see it suggests we rename our file. Let's do that so we can start to use the powerful features that Bootstrap offers.

We can rename application.css in the command line (the terminal with [Web Dev]), like the true hackers we are. It turns out the mv command will "move" (or rename) the file we point at it, to the place we specify. So in the command line, run this:

$ mv app/assets/stylesheets/application.css app/assets/stylesheets/application.scss
The next step we need to take is to create a stylesheet for us to add the bootstrap imports in. We are creating a new file instead of adding it directly to application.scss because we'll be adding additional styles later. Let's make a new file at app/assets/stylesheets/master.scss and add the following code in it:

@import "bootstrap"; 
Then save this file.

If we keep looking through the guide, it looks like we need to adjust our application.js file.

Let's adjust app/assets/javascripts/application.js to include popper, tether, and bootstrap-sprockets between turbolinks and require_tree . The order of the require statements is important. Be sure to add them in the following order with popper placed between turbolinks and tether, as show here:

//= require turbolinks
//= require popper
//= require tether
//= require bootstrap-sprockets
//= require_tree . 
 
 

Common Gotcha
A common gotcha
It's common to accidentally put require bootstrap instead of require bootstrap-sprockets. if you write this file incorrectly now, it may still seem to work, but in the future lessons when we try to use some of Bootstrap's cool functionality, things won't work. Make sure your file looks exactly like it does above.

Also, there is an issue with Heroku and Rails 5 and we need to place bootstrap-sprockets under turbolinks otherwise some application functionality will not work.

Then save the file.

Test it out
Ok, we just made some changes— let's test things out and see what they look like. Go back to your browser, and refresh the page.

Awesome, the font should have slightly changed.

Here's a screenshot of what our app looked like before we added Bootstrap. Here's a screenshot of how it should look now.

Common Gotcha
A common gotcha
If you see an error message, make sure you followed the step above called Restart the Server. Try doing that, then refresh the page again.


Git commit
Go through the standard git commit workflow.



<!DOCTYPE html>
<html>
  <head>
    <link rel="stylesheet" media="screen" href="/assets/marketing-f172b7bd62670f0e64f20cf0692c91e64fa0b62a82e424cc1b63d657fec69bfb.css" />
    <script src="/assets/application-7ab4550827248c75e3a67bb8cbfb220f00003e32b6c51788b3fd2a7d0fdd287b.js"></script>

    <!-- CKEditor is loaded outside the Asset Pipeline -->
    <script src="/ckeditor/ckeditor.js"></script>
    <script src="/ckeditor/config.js"></script>

    <meta name="csrf-param" content="authenticity_token" />
<meta name="csrf-token" content="nHisPrXBGvi9KZyk8/Jve3veIl9FkDNucBfxXoGII6xAjfI5njePRIlXm1pKtA3jfykTIs7uBlIS1XTLEi1rgQ==" />
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="google-site-verification" content="Hp2_fnorKeGuAV_ZAhiKqMfH8DAcAg19Fiq_vY1IrMs" />
      <title>
        Firehose Project
      </title>

      <meta content='http://www.thefirehoseproject.com' property='og:url'>
      <meta content='Firehose Project' property='og:site_name'>
      <meta content='article' property='og:type'>
      <meta content='Mentor Driven Online Coding Bootcamp' property='og:title'>
      <meta content='Build a website and learn how to solve Ruby coding challenges that screen out the majority of web development job applicants before they ever make it to the interview.' property='og:description'>
      <meta content='https://workspace.thefirehoseproject.com/assets/meta-tag-coder-49b2644049aae438c681b381a174a1cbad4f6c931a233a7dc8616d384ca7147f.png' property='og:image'>

    <link rel="icon" type="image/png" href="/assets/favicon-4e518cdac46955836fa76c5c658dff71c98078475dcf7fe6b3a60e6438acff55.png">

    <!-- TypeKit -->
      <script src="https://use.typekit.net/fmj7zgm.js"></script>
      <script>try{Typekit.load({ async: true });}catch(e){}</script>
      <script>(function() {
        var _fbq = window._fbq || (window._fbq = []);
        if (!_fbq.loaded) {
          var fbds = document.createElement('script');
          fbds.async = true;
          fbds.src = '//connect.facebook.net/en_US/fbds.js';
          var s = document.getElementsByTagName('script')[0];
          s.parentNode.insertBefore(fbds, s);
          _fbq.loaded = true;
        }
        _fbq.push(['addPixelId', '948223488529411']);
        })();
        window._fbq = window._fbq || [];
        window._fbq.push(['track', 'PixelInitialized', {}]);
      </script>

    <noscript><img height="1" width="1" alt="" style="display:none" src="https://www.facebook.com/tr?id=948223488529411&amp;ev=PixelInitialized" /></noscript>

    <link href='https://fonts.googleapis.com/css?family=Open+Sans+Condensed:300,300italic,600,700' rel='stylesheet' type='text/css'>
    <link href='https://fonts.googleapis.com/css?family=Old+Standard+TT:700' rel='stylesheet' type='text/css'>

    <!-- Kissmetrics JS snippet Start -->
      <script type="text/javascript">
        var _kmq = _kmq || [];
        var _kmk = _kmk || 'bb3a5598dcc59dffa9ab13638a8cd5d4993eeb6b';
        function _kms(u){
          setTimeout(function(){
            var d = document, f = d.getElementsByTagName('script')[0],
            s = d.createElement('script');
            s.type = 'text/javascript'; s.async = true; s.src = u;
            f.parentNode.insertBefore(s, f);
          }, 1);
        }
        _kms('//i.kissmetrics.com/i.js');
        _kms('//scripts.kissmetrics.com/' + _kmk + '.2.js');
      </script>
    <!-- Kissmetrics JS snippet End -->

  </head>

  <body data-env="production" class="signed-in splurty show   unsticky-footer">


      <link rel="stylesheet" media="screen" href="/assets/rscss/navigation/default_navigation-7bac510a8e9720bc779cd6ffea38d7a6f9f488d59e7c42dcb16e922f4f9dc913.css" />
<script src="/assets/notifications-9e655f2d279df884f8a89e4e11fa1e64fe8927ff78ff2c83f56356b05bf95f20.js"></script>

  <script src="/assets/temporary_course_side_navigation-af4549827474c62c3b46b9cd8937ee1deb56251933e5262f1562099097763c04.js"></script>
  <div id='side-nav-holder'>
    <link rel="stylesheet" media="screen" href="/assets/lesson_sidenav-94dff70254fbadcde242343736e8db33d0e4cc7db5edf175e58e8a90848f4929.css" />
<script src="/assets/dashboard_sidenav-796b8b2e3deb3738b111a3b09435fd8a8452e8b44f71c425fa824c2035927df5.js"></script>
<script src="/assets/temporary_course_side_navigation-af4549827474c62c3b46b9cd8937ee1deb56251933e5262f1562099097763c04.js"></script>


  <div id='nav-out-temp' data-toggle='streak-tooltips' rel="tooltip" title="This is placeholder.">
    <span class='glyphicon glyphicon-chevron-right'></span>
  </div>
  <div id='side-nav-container'>

    <!-- VIDEOS FOR SPA -->
    <!-- END VIDEOS FOR SPA -->

    <!-- CHAPTERS -->
      <div class='section-accordion' id="chapters-accordion">
  <div class='accordion-section-title __secondary_link'>
    <a data-toggle="collapse" data-parent="#chapters-accordion" href="#chapters-collapse" class='outer-section-collapse'>
      <div class='title-container'>
        <div class='icon-img'><img src="/assets/student_dashboard/icon_chapters-4a96036f58a26e16b9a39b91ba89677bcab0a8e08ea2ff3494b5274ad0b0c068.svg" alt="" /></div>
        <span class='icon-text'>Web App: Splurty</span>
      </div>
    </a>
  </div>

  <div id="chapters-collapse" class="panel-collapse collapse">

      <!-- For intro course - this hides the last chapter and lesson 1-->
        <div id="chapter-inner-acc0" class='accordion-inner-class'>
          <a data-toggle="collapse" data-parent="#chapter-inner-acc0" href="#chapter-collapse0" class="__primary_link">
            <div class='outside-links '>
              <span class='lesson-name-span __secondary_link'>
                1. Getting Started
              </span>
              <span class="caret-class">
                <img src="/assets/student_dashboard/caret_down-576a5f30dfc208e2dc97787e864092a14fc233b0a26c924a99e8eb0e952d08ce.svg">
              </span>
            </div>
          </a>
          <div id="chapter-collapse0" class="panel-collapse collapse -inner">
              <div class='inside-links'>
                <a href="/splurty/1">- 1: Setting Up the Project</a>
                  <span class='lesson-check-box'>
                      <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
                  </span>
              </div>
              <div class='inside-links'>
                <a href="/splurty/2">- 2: Setting Up Pipeline</a>
                  <span class='lesson-check-box'>
                      <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
                  </span>
              </div>
              <div class='inside-links'>
                <a href="/splurty/3">- 3: Wireframing</a>
                  <span class='lesson-check-box'>
                      <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
                  </span>
              </div>
          </div>
        </div>

      <!-- For intro course - this hides the last chapter and lesson 1-->
        <div id="chapter-inner-acc1" class='accordion-inner-class'>
          <a data-toggle="collapse" data-parent="#chapter-inner-acc1" href="#chapter-collapse1" class="__primary_link">
            <div class='outside-links '>
              <span class='lesson-name-span __secondary_link'>
                2. Building the Homepage
              </span>
              <span class="caret-class">
                <img src="/assets/student_dashboard/caret_down-576a5f30dfc208e2dc97787e864092a14fc233b0a26c924a99e8eb0e952d08ce.svg">
              </span>
            </div>
          </a>
          <div id="chapter-collapse1" class="panel-collapse collapse -inner">
              <div class='inside-links'>
                <a href="/splurty/4">- 4: The first page</a>
                  <span class='lesson-check-box'>
                      <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
                  </span>
              </div>
              <div class='inside-links'>
                <a href="/splurty/5">- 5: Setting up the database</a>
                  <span class='lesson-check-box'>
                      <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
                  </span>
              </div>
              <div class='inside-links'>
                <a href="/splurty/6">- 6: Show a random quote</a>
                  <span class='lesson-check-box'>
                      <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
                  </span>
              </div>
          </div>
        </div>

      <!-- For intro course - this hides the last chapter and lesson 1-->
        <div id="chapter-inner-acc2" class='accordion-inner-class'>
          <a data-toggle="collapse" data-parent="#chapter-inner-acc2" href="#chapter-collapse2" class="__primary_link">
            <div class='outside-links '>
              <span class='lesson-name-span __secondary_link'>
                3. Adding Design
              </span>
              <span class="caret-class">
                <img src="/assets/student_dashboard/caret_down-576a5f30dfc208e2dc97787e864092a14fc233b0a26c924a99e8eb0e952d08ce.svg">
              </span>
            </div>
          </a>
          <div id="chapter-collapse2" class="panel-collapse collapse -inner">
              <div class='inside-links'>
                <a href="/splurty/7">- 7: Bootstrap</a>
                  <span class='lesson-check-box'>
                      <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
                  </span>
              </div>
              <div class='inside-links'>
                <a href="/splurty/8">- 8: Top navigation bar</a>
                  <span class='lesson-check-box'>
                      <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
                  </span>
              </div>
              <div class='inside-links'>
                <a href="/splurty/9">- 9: Styling the topnav</a>
                  <span class='lesson-check-box'>
                      <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
                  </span>
              </div>
              <div class='inside-links'>
                <a href="/splurty/10">- 10: Use custom fonts</a>
                  <span class='lesson-check-box'>
                      <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
                  </span>
              </div>
              <div class='inside-links'>
                <a href="/splurty/11">- 11: Add a footer</a>
                  <span class='lesson-check-box'>
                      <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
                  </span>
              </div>
          </div>
        </div>

      <!-- For intro course - this hides the last chapter and lesson 1-->
        <div id="chapter-inner-acc3" class='accordion-inner-class'>
          <a data-toggle="collapse" data-parent="#chapter-inner-acc3" href="#chapter-collapse3" class="__primary_link">
            <div class='outside-links '>
              <span class='lesson-name-span __secondary_link'>
                4. Finishing the Functionality
              </span>
              <span class="caret-class">
                <img src="/assets/student_dashboard/caret_down-576a5f30dfc208e2dc97787e864092a14fc233b0a26c924a99e8eb0e952d08ce.svg">
              </span>
            </div>
          </a>
          <div id="chapter-collapse3" class="panel-collapse collapse -inner">
              <div class='inside-links'>
                <a href="/splurty/12">- 12: Add a quote form</a>
                  <span class='lesson-check-box'>
                      <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
                  </span>
              </div>
              <div class='inside-links'>
                <a href="/splurty/13">- 13: Save the data on submit</a>
                  <span class='lesson-check-box'>
                      <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
                  </span>
              </div>
              <div class='inside-links'>
                <a href="/splurty/14">- 14: Validating User Data</a>
                  <span class='lesson-check-box'>
                      <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
                  </span>
              </div>
              <div class='inside-links'>
                <a href="/splurty/15">- 15: Building the about page</a>
                  <span class='lesson-check-box'>
                      <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
                  </span>
              </div>
          </div>
        </div>

      <!-- For intro course - this hides the last chapter and lesson 1-->
        <div id="chapter-inner-acc4" class='accordion-inner-class'>
          <a data-toggle="collapse" data-parent="#chapter-inner-acc4" href="#chapter-collapse4" class="__primary_link">
            <div class='outside-links '>
              <span class='lesson-name-span __secondary_link'>
                5. Finishing Touches
              </span>
              <span class="caret-class">
                <img src="/assets/student_dashboard/caret_down-576a5f30dfc208e2dc97787e864092a14fc233b0a26c924a99e8eb0e952d08ce.svg">
              </span>
            </div>
          </a>
          <div id="chapter-collapse4" class="panel-collapse collapse -inner">
              <div class='inside-links'>
                <a href="/splurty/16">- 16: Adding a modal</a>
                  <span class='lesson-check-box'>
                      <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
                  </span>
              </div>
              <div class='inside-links'>
                <a href="/splurty/17">- 17: Finishing Touches</a>
                  <span class='lesson-check-box'>
                      <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
                  </span>
              </div>
          </div>
        </div>

      <!-- For intro course - this hides the last chapter and lesson 1-->
        <div id="chapter-inner-acc5" class='accordion-inner-class'>
          <a data-toggle="collapse" data-parent="#chapter-inner-acc5" href="#chapter-collapse5" class="__primary_link">
            <div class='outside-links '>
              <span class='lesson-name-span __secondary_link'>
                6. Deploying to Production
              </span>
              <span class="caret-class">
                <img src="/assets/student_dashboard/caret_down-576a5f30dfc208e2dc97787e864092a14fc233b0a26c924a99e8eb0e952d08ce.svg">
              </span>
            </div>
          </a>
          <div id="chapter-collapse5" class="panel-collapse collapse -inner">
              <div class='inside-links'>
                <a href="/splurty/18">- 18: Deploy to Heroku</a>
                  <span class='lesson-check-box'>
                      <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
                  </span>
              </div>
              <div class='inside-links'>
                <a href="/splurty/19">- 19: User Feedback</a>
                  <span class='lesson-check-box'>
                      <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
                  </span>
              </div>
          </div>
        </div>
  </div>

</div>

    <!-- END CHAPTERS -->

    <!-- JOB PREP (ITS UNIQUE) -->

    <!-- CHALLENGES -->
      <div class='section-accordion' id="challenges-accordion">
  <div class='accordion-section-title __secondary_link'>
    <a data-toggle="collapse" data-parent="#challenges-accordion" href="#challenges-collapse">
      <div class='title-container'>
        <div class='icon-img'><img src="/assets/student_dashboard/icon_coding_challenge-f26a1ad946a6c64548e090df45bdeb853b01c11a0593acc4fae65895903eb74d.png" alt="" /></div>
          <span class='icon-text'>Assignments</span>
      </div>
    </a>
  </div>

  <div id="challenges-collapse" class="panel-collapse collapse">
      <div id="challenges-inner-acc0" class="inside-links">
        <span class='lesson-name-span' id='foundations1'>
          <a href="/foundations/1">Blogging about Code</a>
        </span>
        <span class='lesson-check-box'>
            <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
        </span>
      </div>
      <div id="challenges-inner-acc1" class="inside-links">
        <span class='lesson-name-span' id='foundations2'>
          <a href="/foundations/2">Social Profiles Set-up</a>
        </span>
        <span class='lesson-check-box'>
            <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
        </span>
      </div>
  </div>

</div>

    <!-- END CHALLENGES -->

    <!-- ADV CHALLENGES -->
    <!-- END ADV CHALLENGES -->

    <!-- VIDEOS -->
      <div class='section-accordion' id="videos-accordion">
  <div class='accordion-section-title __secondary_link'>
    <a data-toggle="collapse" data-parent="#videos-accordion" href="#videos-collapse" class='outer-section-collapse2'>
      <div class='title-container'>
          <div class='icon-img'><img src="/assets/student_dashboard/icon_videos-21874a51a1f5f4f53af7ed738c02c542f7fa67f4ed9d9f7c66461a904e898400.png" alt="" /></div>
          <span class='icon-text'>Videos</span>
      </div>
    </a>
  </div>

  <div id="videos-collapse" class="panel-collapse collapse">
    <div id="videos-inner-acc0" class='accordion-inner-class'>
        <a data-toggle="collapse" data-parent="#videos-inner-acc0" href="#videos-collapse0">
          <div class='outside-links '>
            <span class='lesson-name-span __secondary_link'>
              1. MVC Overview Videos
            </span>
            <span class="caret-class">
              <img src="/assets/student_dashboard/caret_down-576a5f30dfc208e2dc97787e864092a14fc233b0a26c924a99e8eb0e952d08ce.svg">
            </span>
          </div>
        </a>
        <div id="videos-collapse0" class="panel-collapse collapse -inner">
            <div class='inside-links'>
              <span class='lesson-name-span'>
                <a href="/video-overview/1">1. HTTP Protocol</a>
              </span>
              <span class='lesson-check-box'>
                  <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
              </span>
            </div>
            <div class='inside-links'>
              <span class='lesson-name-span'>
                <a href="/video-overview/2">2. rake routes</a>
              </span>
              <span class='lesson-check-box'>
                  <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
              </span>
            </div>
            <div class='inside-links'>
              <span class='lesson-name-span'>
                <a href="/video-overview/3">3. config/routes.rb</a>
              </span>
              <span class='lesson-check-box'>
                  <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
              </span>
            </div>
            <div class='inside-links'>
              <span class='lesson-name-span'>
                <a href="/video-overview/4">4. RESTful Routes</a>
              </span>
              <span class='lesson-check-box'>
                  <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
              </span>
            </div>
            <div class='inside-links'>
              <span class='lesson-name-span'>
                <a href="/video-overview/5">5. Controllers and Views</a>
              </span>
              <span class='lesson-check-box'>
                  <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
              </span>
            </div>
            <div class='inside-links'>
              <span class='lesson-name-span'>
                <a href="/video-overview/6">6. Models</a>
              </span>
              <span class='lesson-check-box'>
                  <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
              </span>
            </div>
            <div class='inside-links'>
              <span class='lesson-name-span'>
                <a href="/video-overview/7">7. Specific Model Commands</a>
              </span>
              <span class='lesson-check-box'>
                  <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
              </span>
            </div>
            <div class='inside-links'>
              <span class='lesson-name-span'>
                <a href="/video-overview/8">8. Migrations</a>
              </span>
              <span class='lesson-check-box'>
                  <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
              </span>
            </div>
            <div class='inside-links'>
              <span class='lesson-name-span'>
                <a href="/video-overview/9">9. Local vs. Production</a>
              </span>
              <span class='lesson-check-box'>
                  <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
              </span>
            </div>
            <div class='inside-links'>
              <span class='lesson-name-span'>
                <a href="/video-overview/10">10. A Controller Recap</a>
              </span>
              <span class='lesson-check-box'>
                  <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
              </span>
            </div>
            <div class='inside-links'>
              <span class='lesson-name-span'>
                <a href="/video-overview/11">11. Full Overview</a>
              </span>
              <span class='lesson-check-box'>
                  <img src="/assets/student_dashboard/icon_checkmark-178cb9da56e640fda81da66ca82ee75578f884f896573fcda17bebfad3972a2e.svg" alt="" />
              </span>
            </div>
        </div>
    </div>

  </div>

</div>

    <!-- END VIDEOS -->

    <!-- QUIZZES -->
    <!-- END QUIZZES -->

    <!-- INDUSTRY KNOWLEDGE SECTION -->
    
    <!-- END INDUSTRY KNOWLEDGE SECTION -->

  </div>

</div><!-- End Sidenav container -->

<script>
  sidenav_engine("/splurty/8");
</script>

  </div>

<div class='topnav-container-placeholder'></div>
<div class='topnav-container'>

  <div class='brand-container'>
    <a href="http://www.thefirehoseproject.com">
      <img class="logo" alt="Firehose Logo" src="/assets/marketing_pages/homepage/logo_wired_topnav_black-2ccda6f98de82f363a038e4260b34a97f68defdb21d1728e932da18230cf8041.svg" />
</a>  </div>

  <div class="navigation-container ">

    <!-- Navigation shown on Desktop -->
      <ul class='left-nav-list'>
  <li class="dropdown left-nav-item">
    <a href="/courses" class="dropdown-toggle disabled main-nav-link" id='bootcamp-prep-dropdown-link' data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">Full-Stack Web Development Program <img src="/assets/default_navigation/arrow_dropdown_down-afabafa6262f2b7b277c24d88505de58c51117ffcba52f1e717a94fb89ec24d6.png" alt="" /></a>

    <ul class="dropdown-menu" id='bootcamp-prep-dropdown-menu'>
      <li><a href="/job-prep">Job Prep</a></li>
    </ul>
  </li>

  <li class='left-nav-item'><a id="community-link" class="main-nav-link" href="/community">Community</a></li>

  <li class='left-nav-item'><a id="timeline-link" class="main-nav-link" href="/timeline">Timeline</a></li>

  <li class='left-nav-item'><a id="student-support-link" class="main-nav-link" href="/student-support">FAQ</a></li>

</ul>


    <!-- Navigation shown on Mobile -->
    <nav class="navbar navbar-default mobile-navigation">
  <div class="container-fluid">
    <!-- Brand and toggle get grouped for better mobile display -->
    <div class="navbar-header">
      <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#mobile-top-navigation-target" aria-expanded="false">
        <span class="sr-only">Toggle navigation</span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
    </div>

    <!-- Collect the nav links, forms, and other content for toggling -->
    <div class="collapse navbar-collapse" id="mobile-top-navigation-target">
      <ul class='nav navbar-nav'>
        <li>
          <a class="-bold" href="/courses">Dashboard</a>
        </li>

          <li class='left-nav-item'>
            <a href="/job-prep">Job Prep</a>
          </li>

        <li class='left-nav-item'>
          <a id="community-link" href="/community">Community</a>
        </li>
        <li>
          <a href="/timeline">Timeline</a>
        </li>
        <li>
          <a href="/student-support">FAQ</a>
        </li>

      </ul>

    </div>
  </div>
</nav>


  </div>

  <!-- Nofication Bell and User -->
  <div class='right-side-container'>
      <div id='topnav-user-container'>
        <img id="top-nav-bell" alt="Notification Bell" src="/assets/default_navigation/notification_bell-c1c1925f107e6606f89686fb9770ff7c03a82279722c434131d4910d541f385b.png" />
        <span class= "notification-number hide-number" id='notification-number' data-firebase-key="AIzaSyBK3zU8cQDwly82lE7eyzyL4jyHsa1auuM" data-firebase-auth="firehose-production.firebaseapp.com" data-firebase-database="https://firehose-production.firebaseio.com" data-firebase-storage="firehose-production.appspot.com" data-firebase-messaging="401914555144" data-firebase-channel="user=30307">
          0
        </span>
        <a id="topnav-user-name" href="javascript:void(0);">
          <img id="topnav-user-avatar" alt="User Avatar" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/30307/e5ed9251.png" />
          <img id="topnav-user-caret" src="/assets/default_navigation/arrow_dropdown_down-afabafa6262f2b7b277c24d88505de58c51117ffcba52f1e717a94fb89ec24d6.png" alt="" />
</a>      </div>
      <div class='top-nav-bell-drop-down-holder'  style='display:none;'>
        <div id='top-nav-bell-drop-down' style='display:none;'></div>
      </div>
      <div id='user-profile-dropdown' style='display:none;'>
        <a class="drop-down -link -bold" href="/users/edit">Edit Profile</a>
          <a class="drop-down -link -bold" href="/student-dashboard">Mentor Session Feedback</a>
          <a href='https://thefirehoseproject.com/referral-program', target= '_blank', rel='noopener noreferrer', class='drop-down -link -bold'>Join Our Referral Program</a>
        <a class="drop-down -link" rel="nofollow" data-method="delete" href="/users/sign_out">Sign Out</a>

          <hr />
          <div class='drop-down'><b>Start Date:</b> September 09, 2018</div>
          <div class='drop-down'><b>End Date:</b> February 10, 2019</div>
          <div class='drop-down'><b>Remaining Mentor Sessions:</b> 20</div>

      </div>
  </div>
</div>


<script>
  var title = document.title;
</script>

  <script>
    $(function(){
      setSiteTitle("0");
      loadNotificationsToBell([{"id":1425708,"title":"Introduce yourself to the community. ","description":"on our Community Page.","user_id":30307,"created_at":"2018-08-25T09:37:50.720-07:00","updated_at":"2018-08-25T09:37:50.720-07:00","path":"https://workspace.thefirehoseproject.com/community/comments/15423?utm_source=platform\u0026utm_medium=bell_notification","notification_type":"temp","plain_text":"Share a quick tidbit about your background and get to know other Firehosers ","location":"Bell","clicked?":false},{"id":1426032,"title":"Nev ","description":"Environment Change heads up for Mac Users","user_id":30307,"created_at":"2018-08-27T05:53:57.567-07:00","updated_at":"2018-08-27T05:53:57.567-07:00","path":"https://workspace.thefirehoseproject.com/community/comments/41942?utm_source=platform\u0026utm_medium=notification_bell\u0026utm_campaign=new_community_post","notification_type":"temp","plain_text":"just started a new discussion in the community.","location":"Bell","clicked?":false},{"id":1426226,"title":"Ken Mazaika published a Quora answer","description":"What are some things you wish you knew when you started programming","user_id":30307,"created_at":"2018-08-28T11:10:36.228-07:00","updated_at":"2018-08-28T11:10:36.228-07:00","path":"https://www.quora.com/What-are-some-things-you-wish-you-knew-when-you-started-programming/answer/Ken-Mazaika","notification_type":"temp","plain_text":null,"location":"Bell","clicked?":false},{"id":1426228,"title":"Joel Choi published a student blog post","description":"You need to stop thinking and start doing","user_id":30307,"created_at":"2018-08-28T11:47:58.348-07:00","updated_at":"2018-08-28T11:47:58.348-07:00","path":"https://realworldcoding.io/you-need-to-stop-thinking-and-start-doing-6dc90054b259#.nzhcf58yc","notification_type":"temp","plain_text":null,"location":"Bell","clicked?":false},{"id":1426230,"title":"Ken Mazaika published a Firehose blog post","description":"Here's what you can learn in 10 minutes","user_id":30307,"created_at":"2018-08-28T12:15:57.379-07:00","updated_at":"2018-09-01T21:44:32.588-07:00","path":"http://blog.thefirehoseproject.com/posts/10-minutes-learn-programming/","notification_type":"temp","plain_text":null,"location":"Bell","clicked?":true},{"id":1426686,"title":"Comment Response:","description":"Ken just responded to your comment in the forum.","user_id":30307,"created_at":"2018-09-10T16:45:30.811-07:00","updated_at":"2018-09-10T17:11:26.186-07:00","path":"/comments/42085","notification_type":"temp","plain_text":null,"location":"Bell","clicked?":true},{"id":1426689,"title":"Comment Response:","description":"Ken just responded to your comment in the forum.","user_id":30307,"created_at":"2018-09-10T17:20:11.401-07:00","updated_at":"2018-09-10T17:20:11.401-07:00","path":"/comments/42085","notification_type":"temp","plain_text":null,"location":"Bell","clicked?":false},{"id":1426690,"title":"Comment Response:","description":"Ken just responded to your comment in the forum.","user_id":30307,"created_at":"2018-09-10T17:27:36.653-07:00","updated_at":"2018-09-10T17:27:36.653-07:00","path":"/comments/42085","notification_type":"temp","plain_text":null,"location":"Bell","clicked?":false},{"id":1426691,"title":"Comment Response:","description":"Ken just responded to your comment in the forum.","user_id":30307,"created_at":"2018-09-10T19:37:35.126-07:00","updated_at":"2018-09-10T19:54:54.116-07:00","path":"/comments/42085","notification_type":"temp","plain_text":null,"location":"Bell","clicked?":true},{"id":1426692,"title":"Update your Profile:","description":"Upload your favorite headshot, link your Twitter and Github accounts, and more.","user_id":30307,"created_at":"2018-09-10T19:57:58.446-07:00","updated_at":"2018-09-10T19:58:39.769-07:00","path":"https://workspace.thefirehoseproject.com/users/edit","notification_type":"temp","plain_text":null,"location":"Bell","clicked?":true},{"id":1426696,"title":"Firehose Slack:","description":"Describe who you are and share your goals with the community","user_id":30307,"created_at":"2018-09-10T23:14:03.876-07:00","updated_at":"2018-09-10T23:14:15.881-07:00","path":"https://thefirehoseproject.slack.com","notification_type":"temp","plain_text":null,"location":"Bell","clicked?":true},{"id":1426702,"title":"New Assignment Unlocked:","description":"Why Blogging About Code is Important","user_id":30307,"created_at":"2018-09-11T10:14:52.754-07:00","updated_at":"2018-09-11T10:14:57.975-07:00","path":"https://workspace.thefirehoseproject.com/foundations/1","notification_type":"temp","plain_text":null,"location":"Bell","clicked?":true},{"id":1427041,"title":"New Algorithm Unlocked:","description":"How to Approach Algorithm Problems","user_id":30307,"created_at":"2018-09-11T12:54:35.085-07:00","updated_at":"2018-09-11T12:54:38.740-07:00","path":"https://workspace.thefirehoseproject.com/foundations/3","notification_type":"temp","plain_text":null,"location":"Bell","clicked?":true},{"id":1427049,"title":"New Video Sessions Unlocked:","description":"Model-View-Controler - How a web application works","user_id":30307,"created_at":"2018-09-11T14:41:33.007-07:00","updated_at":"2018-09-11T14:41:40.126-07:00","path":"https://workspace.thefirehoseproject.com/video-overview/1","notification_type":"temp","plain_text":null,"location":"Bell","clicked?":true},{"id":1427055,"title":"Comment Response:","description":"Ken just responded to your comment in the forum.","user_id":30307,"created_at":"2018-09-11T16:03:55.075-07:00","updated_at":"2018-09-11T16:05:40.086-07:00","path":"/comments/42108","notification_type":"temp","plain_text":null,"location":"Bell","clicked?":true},{"id":1427057,"title":"Comment Response:","description":"Ken just responded to your comment in the forum.","user_id":30307,"created_at":"2018-09-11T16:15:12.058-07:00","updated_at":"2018-09-11T16:15:24.373-07:00","path":"/comments/42108","notification_type":"temp","plain_text":null,"location":"Bell","clicked?":true},{"id":1427058,"title":"Great Job!","description":"Post the finished version of your Splurty app in the student Google+ Group","user_id":30307,"created_at":"2018-09-11T16:18:50.547-07:00","updated_at":"2018-09-11T16:19:24.168-07:00","path":"https://plus.google.com/u/0/communities/114073605360096585795","notification_type":"temp","plain_text":null,"location":"Bell","clicked?":true},{"id":1427087,"title":"New Algorithm Unlocked:","description":"Image Blur #1","user_id":30307,"created_at":"2018-09-13T03:28:48.238-07:00","updated_at":"2018-09-13T03:29:02.020-07:00","path":"https://workspace.thefirehoseproject.com/foundations/4","notification_type":"temp","plain_text":null,"location":"Bell","clicked?":true},{"id":1427088,"title":"New Quiz Unlocked:","description":"Web Development Pipeline","user_id":30307,"created_at":"2018-09-13T04:13:20.011-07:00","updated_at":"2018-09-13T04:13:26.700-07:00","path":"https://workspace.thefirehoseproject.com/quizzes/1","notification_type":"temp","plain_text":null,"location":"Bell","clicked?":true},{"id":1427121,"title":"New Video Sessions Unlocked:","description":"Object Oriented Programming - How to organize code in classes","user_id":30307,"created_at":"2018-09-14T23:24:55.492-07:00","updated_at":"2018-09-14T23:24:55.492-07:00","path":"https://workspace.thefirehoseproject.com/oop/1","notification_type":"temp","plain_text":null,"location":"Bell","clicked?":false},{"id":1427414,"title":"Justin ","description":"My First Blog Post! (May have done it a bit early)","user_id":30307,"created_at":"2018-09-14T23:37:55.551-07:00","updated_at":"2018-09-14T23:41:50.541-07:00","path":"https://workspace.thefirehoseproject.com/community/comments/42140?utm_source=platform\u0026utm_medium=notification_bell\u0026utm_campaign=new_community_post","notification_type":"temp","plain_text":"just started a new discussion in the community.","location":"Bell","clicked?":true},{"id":1427448,"title":"Comment Response:","description":"Ken just responded to your comment in the forum.","user_id":30307,"created_at":"2018-09-15T17:17:02.814-07:00","updated_at":"2018-09-15T18:48:14.445-07:00","path":"/comments/42139","notification_type":"temp","plain_text":null,"location":"Bell","clicked?":true},{"id":1427455,"title":"Mentorship in the program: ","description":"Learn more about mentor sessions and how to make the most of working with your mentor.","user_id":30307,"created_at":"2018-09-16T06:05:08.446-07:00","updated_at":"2018-09-16T06:05:08.446-07:00","path":"https://workspace.thefirehoseproject.com/student-support/mentorships/what-are-mentor-sessions","notification_type":"temp","plain_text":"Working 1-on-1 with your senior developer mentor is core to your learning. ","location":"Bell","clicked?":false},{"id":1427774,"title":"Zaki ","description":"Posted my first Medium blog-post today about Coding!","user_id":30307,"created_at":"2018-09-16T19:41:33.196-07:00","updated_at":"2018-09-16T20:20:45.558-07:00","path":"https://workspace.thefirehoseproject.com/community/comments/42147?utm_source=platform\u0026utm_medium=notification_bell\u0026utm_campaign=new_community_post","notification_type":"temp","plain_text":"just started a new discussion in the community.","location":"Bell","clicked?":true},{"id":1427803,"title":"Get support: ","description":"Check out and bookmark the Student Support Page.","user_id":30307,"created_at":"2018-09-17T06:05:09.173-07:00","updated_at":"2018-09-18T17:41:04.615-07:00","path":"https://workspace.thefirehoseproject.com/student-support","notification_type":"temp","plain_text":"Any questions you have about your experience in the program, answered. ","location":"Bell","clicked?":true},{"id":1427847,"title":"Comment Response:","description":"Joe just responded to your comment in the forum.","user_id":30307,"created_at":"2018-09-19T07:00:41.741-07:00","updated_at":"2018-09-19T07:00:41.741-07:00","path":"/comments/42159","notification_type":"temp","plain_text":null,"location":"Bell","clicked?":false},{"id":1427856,"title":"Comment Response:","description":"Ken just responded to your comment in the forum.","user_id":30307,"created_at":"2018-09-19T14:17:03.076-07:00","updated_at":"2018-09-19T15:19:24.068-07:00","path":"/comments/42159","notification_type":"temp","plain_text":null,"location":"Bell","clicked?":true},{"id":1427861,"title":"New feedback from Conrad:","description":"Click here to read the notes and add your own.","user_id":30307,"created_at":"2018-09-19T20:00:22.978-07:00","updated_at":"2018-09-19T20:03:27.314-07:00","path":"https://workspace.thefirehoseproject.com/students/mentor_sessions/9511/student_sessions/new","notification_type":"temp","plain_text":"Your mentor just posted some notes about your last session together. ","location":"Bell","clicked?":true}]);
      firebaseNotificationSubscription('/notifications', '0');
    });
  </script>






      <!--  Google Analytics Tracking Pixel -->
      <script>
  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
  })(window,document,'script','//www.google-analytics.com/analytics.js','ga');

  ga('create', 'UA-49340848-1', 'thefirehoseproject.com');
  
  if (document.cookie.includes('user_is_admin')) {
    var dimensionValue = 'true';
    ga('set', 'dimension1', dimensionValue);
  }

  ga('send', 'pageview');

</script>



    <div class="content">

      <link rel="stylesheet" media="screen" href="/assets/splurty-b44c7d9113682c6009ea5277f779af3b918174729684633e42525bdc86d2ac32.css" />

<div class='track-lesson-container'>
  <link rel="stylesheet" media="screen" href="/assets/lesson_improvement-3e40c1f8b7b3f56864794ae8751335a29e02f8becb82559970fdf6ec05447df4.css" />
<script src="/assets/lesson_improvements-edd4c5496e559f88212e7268e5dcd60d3735009a817885e1f12a14de3efc1a63.js"></script>
<button aria-label="Give feedback on how to improve this lesson" class='no-padding-no-border' id='lesson_improvement_button'>
	<img id="lesson_improvement_edit_icon" src="/assets/lessons/edit-17a0dd4e531097da2d8ce81e189c5ef73933a342b7023b70517e45e22b0e1635.svg" alt="" />
</button>
<div class='col-xs-10 col-xs-offset-1'>
  <h1 class='__page_heading'>Lesson 8: Adding a Top Navigation Bar</h1>
  <p class='__text_body'>In the previous lessons, we've started building a web application and have integrated with Bootstrap. In this lesson, we will add the header that will be present on every single page of our web application. We will also start using some of the design power from the Bootstrap framework.</p>
    <nav id="classmates-container">
  <div class="container-fluid">
    <!-- Collect the nav links, forms, and other content for toggling -->
    <div class="collapse navbar-collapse" id="classmate-navbar-collapse">
      <div class='__text_secondary_body' id="classmates-text">
        Classmates working on this track:
      </div>
      <ul class="nav navbar-nav" id='classmate-navbar'>
        <!-- Students on current app -->
        <li class="dropdown" id="users-on-app">
              <span data-content="Kari S.<br>On Lesson 19<br><a href='https://thefirehoseproject.slack.com/messages/coding-help/team/' target='_blank' rel='noopener noreferrer'>Find Them in Slack</a>" class='pop'>
                <img class="user-avatar-for-lessons" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/29757/1f05587e.jpg" alt="" />
              </span>
              <span data-content="Leon U.<br>On Lesson 19<br><a href='https://thefirehoseproject.slack.com/messages/coding-help/team/' target='_blank' rel='noopener noreferrer'>Find Them in Slack</a>" class='pop'>
                <img class="user-avatar-for-lessons" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/29959/a00e14b7.jpg" alt="" />
              </span>
              <span data-content="Zoe B.<br>On Lesson 9<br><a href='https://thefirehoseproject.slack.com/messages/coding-help/team/' target='_blank' rel='noopener noreferrer'>Find Them in Slack</a>" class='pop'>
                <img class="user-avatar-for-lessons" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/17056/4296a2d8.jpg" alt="" />
              </span>
              <span data-content="Juan A.<br>On Lesson 19<br><a href='https://thefirehoseproject.slack.com/messages/coding-help/team/' target='_blank' rel='noopener noreferrer'>Find Them in Slack</a>" class='pop'>
                <img class="user-avatar-for-lessons" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/27679/24e355d0.jpg" alt="" />
              </span>
              <span data-content="9 more students<br>
            working on this<br><a href='https://thefirehoseproject.slack.com/messages/coding-help/team/' target='_blank' rel='noopener noreferrer'>Find Them in Slack</a><hr>Ambrose C.<br> Justin O.<br> Jonah Y.<br> Phil G.<br> Michael S.<br> Mitch M.<br> Kenneth C.<br> Marley H.<br> Bella M.<br> " class='pop' id='plus-icon'><img class="user-avatar-for-lessons" src="/assets/subnav/plus-22258915238490fc8bb6a9ff41fe41e00a141c0a3238d16615ad4e2303e3b5f2.png" alt="" />
              </span>
        </li>

      </ul>
    </div><!-- /.navbar-collapse -->
  </div><!-- /.container-fluid -->

</nav>

<br>

<script>
  $(document).ready(function () {
    $('.pop').each(function () {
      var $elem = $(this);
      $elem.popover({
        placement: 'bottom',
        trigger: 'hover',
        html: true,
        container: $elem,
        animation: true
      });
    });
  });
</script>

  <br style='clear: both;'>
  <hr id='classmates-on-app-custom-hr'>
</div>
	<link rel="stylesheet" media="screen" href="/assets/lesson_improvement-3e40c1f8b7b3f56864794ae8751335a29e02f8becb82559970fdf6ec05447df4.css" />
<script src="/assets/lesson_improvements-edd4c5496e559f88212e7268e5dcd60d3735009a817885e1f12a14de3efc1a63.js"></script>

<div id='myLessonImprovementModal' class="modal fade" tabindex="-1" role="dialog">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header lesson-improvement-title">
        <button type="button" id="close_button" class="close close-btn -top" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
        Improve this Firehose Lesson
      </div>
      <div class="modal-body lesson-improvement-body">
        <div id='lesson_improvement_suggestion'>
          <br/>
          Helping out is simple:
          <br/><br/>
          <ol class='lesson-improvement-ol'>
            <li>Copy &amp; paste the section that you want to improve into the field below.</li>
            <li>Add your improvement to it.</li>
            <li>Select the type of improvement from the drop-down list.</li>
            <li>Hit submit.</li><br/>
          </ol>
          <!-- form for the suggestion entry -->
          <img class="lesson-improvement-avatar" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/30307/e5ed9251.png" alt="" />
          <div class="new-suggestion-form">
            <div id='new_suggestion_form_triangle'></div>
            <form novalidate="novalidate" class="simple_form new_lesson_improvement" id="new_lesson_improvement" action="/lesson_improvements" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="LBfZZ62Tx487PGQYD1FzMuJpLX4D7ZR3O4B5ECMciVLw4odghmVSMw9CY+a2FxGq5p4cA4iToUtZQvyFsLnBfw==" />
              <div class="input hidden lesson_improvement_user_id"><input value="30307" class="hidden form-control" type="hidden" name="lesson_improvement[user_id]" id="lesson_improvement_user_id" /></div>
              <div class="input hidden lesson_improvement_course"><input value="splurty" class="hidden form-control" type="hidden" name="lesson_improvement[course]" id="lesson_improvement_course" /></div>
              <div class="input hidden lesson_improvement_lesson"><input value="8" class="hidden form-control" type="hidden" name="lesson_improvement[lesson]" id="lesson_improvement_lesson" /></div>
              <div class="input ckeditor required lesson_improvement_suggested_improvement"><textarea ckeditor="{:toolbar=&gt;&quot;Mini&quot;}" id="suggestion" class="ckeditor required form-control" name="lesson_improvement[suggested_improvement]">
</textarea></div>
              <br/>
              <div class='lesson-improvement-category'>What's your improvement related to?</div>
              <div class="input select optional lesson_improvement_category"><select class="select optional form-control" name="lesson_improvement[category]" id="lesson_improvement_category"><option value=""></option>
<option value="typo">typo</option>
<option value="code snippets">code snippets</option>
<option value="confusing wording">confusing wording</option>
<option value="something else">something else</option></select></div>
              <div id="down-arrow-icon"></div>

              <div id = "improvement_errors" class='hidden red-text'>The suggested improvement can't be blank.</div>
</form>          </div>
        </div>
        <div id='lesson_improvement_response' class='hidden'>
          <div class='text-center white-background'>
            <button type="button" id="bottom_close_button" class="close close-btn -bottom" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
            <br class='clr'/>
            <i class="glyphicon glyphicon-ok-sign font-size-100" ></i>
            <br/>
            <h1 class='Open-Sans-Bold'>Awesome!</h1>
            <br/>
            <p class='Open-Sans-Bold'>The entire Firehose Team sends you a high-five for helping out.</p>
            <br/>
          </div>
        </div>
      </div>
      <div class="modal-footer lesson-improvement-footer">
        <div id='lesson_improvement_suggestion_footer'>
          <button class='comment-btn' id="lesson_improvement_submit_button">Submit</button>
        </div>
        <div id='lesson_improvement_response_footer' class='hidden'>
          <div class='blue-background text-center'>
            <br/><br/>
            <button class='comment-btn lesson-improvement-button hide_lesson_improvement' data-dismiss='modal'>Keep Coding</button>
            <br/><br/>
          </div>
        </div>
      </div>
    </div><!-- /.modal-content -->
  </div><!-- /.modal-dialog -->
</div><!-- /.modal -->



<script>
  setUpLessonImprovementSubmission("30307", "/lesson_improvements");
</script>


  <div class='col-xs-10 col-xs-offset-1 col-sm-10 col-sm-offset-1 booyah-box'>

<p>If we quickly check back to our wireframes, we can see that we want to add a top navigation to our web application.</p>

<p>
If we take a step back and think about how most web applications are built, we quickly realize that there are some features that are on every single page. The top navigation, which includes links to other pages, is a great example of a feature that goes on more than just a single page.
</p>

<p>
At first it might make sense to put our top nav on all of the pages in our web application by copying and pasting. While this works at the very beginning when we only have a handful of pages, think about how much extra work we'll have created for ourselves once our web application grows to hundreds of pages and we need to make a small adjustment to the top navigation (like change the word "about" to "team"). We would have to make that single small change on hundreds of pages - that's no fun!
</p>

<p>
In order to get around that, we want to avoid copying and pasting the code that goes on every page onto all the different pages inside our application. Instead, we'll use a special file called <code>application.html.erb</code> which contains the things that are shared across all the pages. In fact, the line that says <code>yield</code> actually pulls in all the page-specific stuff.
</p>

<div class="well">
  <h2 class="lesson-sub-heading text-center">Pro-tip</h2>
  <p>
    <small>Using the keyboard shortcut, command + P (or CTRL + P for Windows / Linux) inside the Sublime Text or Atom editor will open a fuzzy-finding file-opening dialog. Start typing the name of the file, and when the file you want is listed at the top, click enter and boom, the file will be opened. In this case, command + P and typing "application.h" then hitting enter will open the file. If you want to quickly open a file, this is a super useful feature.</small>
  </p>
</div>

<!-- TODO: the little write up I did about application.html.erb should be in nomster too.  Copy &amp; Paste it into nomster/lesson_8.html.erb -->


<p>So if we want to create a place for our top navigation, it should be in our <code>application.html.erb</code>. To do this, let's start by adding a header tag into <code>app/views/layouts/application.html.erb</code> right under the body tag and with the bootstrap 4 <code>row</code> class:</p>

<pre data-line="10-11"><code class="language-markup">&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;Splurty&lt;/title&gt;
    &lt;%= csrf_meta_tags %&gt;
    &lt;%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %&gt;
    &lt;%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;header class="row"&gt;
    &lt;/header&gt;

   &lt;%= yield %&gt;

  &lt;/body&gt;
&lt;/html&gt;</code></pre>

<p>
  Make sure you still have the yield (<code>&lt;%= yield %&gt;</code>) in there. Then save the file and refresh the page.
</p>

<p>
The <code>header</code> tag (note: this is different from the <code>head</code> tag) is an HTML5 tag where you can put header stuff— in our case, if you look back to the wireframes, the logo, slogan, and links.
</p>

<p>
Ok, inside the header let's add a spot for the logo inside of a division (<code>div</code>):
</p>

<pre data-line="11-13"><code class="language-markup">&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;Splurty&lt;/title&gt;
    &lt;%= csrf_meta_tags %&gt;
    &lt;%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %&gt;
    &lt;%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;header class="row"&gt;
      &lt;div&gt;
        LOGO
      &lt;/div&gt;
    &lt;/header&gt;

   &lt;%= yield %&gt;

  &lt;/body&gt;
&lt;/html&gt;</code></pre>

<p>
  A <code>div</code> stands for "division" and basically means we have a box that we can put things inside.
</p>

<p>
Save the file and refresh.
</p>

<p>
Cool, now we have the text "LOGO," which we can flesh out in a little bit.
</p>

<p>
  Next, let's work on getting our slogan on the page. We want to position our slogan right next to the logo. Since we're using Bootstrap, we can position elements on our page using something called the Bootstrap 4 grid system.
</p>

<p>
  Take a few minutes and read up on the Bootstrap 4 grid system <a href="https://v4-alpha.getbootstrap.com/layout/grid/">here</a>.
</p>

<p>In short, the grid that we have on our page is 12 columns wide and we're going to give each element— the logo, slogan and links— a few columns of space. Our logo is probably good with 3 columns of space, and maybe the slogan should take 4 columns of space. Doing this will basically ensure that our boxes are next to each other.</p>

<p>Bootstrap allows us to specify the width of our box for different devices, such as laptop, tablet and mobile screens. Let's start making things look good on mobile first and worry about bigger screens later.
</p>

<p>
So let's switch this up, add our <code>col-*</code> classes and see what we get:
</p>

<pre data-line="11,14-16"><code class="language-markup">&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;Splurty&lt;/title&gt;
    &lt;%= csrf_meta_tags %&gt;
    &lt;%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %&gt;
    &lt;%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;header class="row"&gt;
      &lt;div class="col-3"&gt;
        LOGO
      &lt;/div&gt;
      &lt;div class="col-4"&gt;
        Splurting out unsolicited advice about entrepreneurship since 2016
      &lt;/div&gt;
    &lt;/header&gt;

    &lt;%= yield %&gt;

  &lt;/body&gt;
&lt;/html&gt;</code></pre>

<p>
Cool, save this and refresh.
</p>

<p>
This places our logo and slogan side by side. Unfortunately, it sucks the main body into the top nav as well, but we'll fix that in the next step.
</p>

<p>
Let's add a spot for the links in our web application. If we look to our wireframes, we can see that we want to have a link to contribute a quote and a link to our about page. Right now, we don't know where these will go, so we'll use a special symbol, the hashtag (#) which will be a placeholder that we can update later.
</p>

<p>
If we put our links into 5 columns by using <code>col-5</code>, we're using up the entire 12 columns of horizontal space on our page, and things should line up a bit better.
</p>

<p>
To create the actual links, we're writing our first line of ruby code inside one of our views, like so:
</p>

<pre data-line="17-20"><code class="language-markup">&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;Splurty&lt;/title&gt;
    &lt;%= csrf_meta_tags %&gt;
    &lt;%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %&gt;
    &lt;%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;header class="row"&gt;
      &lt;div class="col-3"&gt;
        LOGO
      &lt;/div&gt;
      &lt;div class="col-4"&gt;
        Splurting out unsolicited advice about entrepreneurship since 2016
      &lt;/div&gt;
      &lt;div class="col-5"&gt;
        &lt;%= link_to 'Contribute', '#' %&gt;
        &lt;%= link_to 'About', '#' %&gt;
      &lt;/div&gt;
    &lt;/header&gt;

    &lt;%= yield %&gt;

  &lt;/body&gt;
&lt;/html&gt;</code></pre>

<p>
Save the file and refresh the page.
</p>

<p>
Ok, it's getting there, but now we see that the quote is still getting sucked into the top navigation. Let's fix this after we take a moment to zoom out and understand how HTML &amp; CSS and ruby code work.
</p>


<h2 class='__section_heading'>Zooming out HTML &amp; CSS</h2>

<p>
HTML is the content on the page that we can see. All of our HTML files exist inside the <code>app/views/*</code> folders and the actual code is always broken up into "tags." These tags start with an opening tag like <code>&lt;h1&gt;</code> and end with a closing tag like <code>&lt;/h1&gt;</code>. HTML is all about the <strong><u>content</u></strong> of the page.
</p>

<p>
CSS is short for Cascading Style Sheets and represents the styles of a page, or the <strong><u>visual</u></strong> components on a website that make it look better. CSS consists of selectors that we can attach to certain parts of our HTML code. By attaching specific CSS styles to certain parts of HTML, we can very precisely define how things actually look for different sections of our page.
</p>

<p>
Let's stay zoomed out a minute longer and look at the different ways we can write ruby code.
</p>


<h2 class='__section_heading'>The different ways ruby code can be executed in a web application</h2>

<p>
  There are basically three different ways that ruby code is typically run:
</p>

<ol>
  <li><code>.rb</code> files</li>
  <li><code>&lt;%=</code> inside <code>.html.erb</code> files
  <li><code>&lt;%</code> inside <code>.html.erb</code> files
</ol>

<p>
<strong>Inside files that have the file extension <code>.rb</code></strong>. These are regular ruby files, and consist entirely of code that is written in the ruby programming language. Code inside these <code>.rb</code> files does not need anything special to execute and run our ruby code.
</p>

<p>
<strong>Inside files in our view folder that have the file extension <code>.html.erb</code></strong>. In these files, ruby code is executed a little bit differently. These files consist mostly of HTML, or the content on our pages. Occasionally, we need to use ruby code right on our HTML page. Some good examples are when we want to pull something out of our database and show it on the page, or when we want to create a link to a specific page.
</p>

<p>
In our example from above, we created a link and showed it inside our HTML page. If we look at the example of the <code>&lt;%= link_to 'Contribute', '#' %></code>, that is calling out to ruby and having ruby figure what the link should be. Notice the equals sign in the <code>&lt;%=</code>.
</p>

<p>
<strong>There are two different ways to execute the ruby code inside the <code>.html.erb</code> files. First, If you omit the equals sign and instead of <code>&lt;%=</code> you type <code>&lt;%</code>, it will execute the ruby code but will not display anything on the page. Second, if you want your ruby code output to be shown on the HTML page— like the above case where we need to show the link so a user can click on it— use: <code>&lt;%=</code></strong>
</p>

<p>
If you're ever writing code inside an <code>html.erb</code> file, and instead of putting the content you expect on the page, it actually outputs nothing, double-check that you have <code>&lt;%=</code> and not <code>&lt;%</code>.
</p>


<h2 class='__section_heading'>Adding a clear tag</h2>
<p>
Now that we're a bit more familiar with how HTML &amp; CSS interact together, let's actually write a line of CSS code and apply its rule to a part of our page.
</p>

<p>
After our header, we should really "clear out" our Bootstrap columns so the quotes are not showing up inside of our top navigation bar. Let's do this by adding a "clearing br tag."
</p>

<pre data-line="23"><code class="language-markup">&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;Splurty&lt;/title&gt;
    &lt;%= csrf_meta_tags %&gt;
    &lt;%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %&gt;
    &lt;%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;header class="row"&gt;
      &lt;div class="col-3"&gt;
        LOGO
      &lt;/div&gt;
      &lt;div class="col-4"&gt;
        Splurting out unsolicited advice about entrepreneurship since 2016
      &lt;/div&gt;
      &lt;div class="col-5"&gt;
        &lt;%= link_to 'Contribute', '#' %&gt;
        &lt;%= link_to 'About', '#' %&gt;
      &lt;/div&gt;
    &lt;/header&gt;

    &lt;br class="clear" /&gt;

    &lt;%= yield %&gt;

  &lt;/body&gt;
&lt;/html&gt;</code></pre>

<p>
  After we've added our clear tag, we need to write some CSS code. To do this, lets open our file we made recently at <code>app/assets/stylesheets/master.scss</code> and add the following code in it.
</p>

<pre data-line="3-5"><code class="language-css">@import "bootstrap";

.clear {
  clear: both;
}</code></pre>

<p>
  Ok, now save and refresh.
</p>

<p>
  Nice, now the top nav stuff is "cleared" and the rest of the content is pushed down the page.
</p>

<p>
  If we zoom out again, we see that our <code>master.scss</code> is the file that will allow us to write the CSS rules to decide how the page will look.
</p>

<p>
CSS is something you learn best by doing, so we're going to tell you to write certain lines of it and as soon as they make your page look different, you'll understand what's going on.
</p>

<h2 class='__section_heading'>The World's Fastest CSS Crash Course</h2>
<p>
CSS really has two different parts to it: CSS properties define the actual styling details, and CSS selectors connect the CSS properties to the correct place on a website.
</p>

<p>
Let's look at both in more detail:
</p>

<p><b>CSS Properties</b> define exactly what kind of style and design are used for a specific property. Think about things like <code>font-family</code> or <code>font-size</code>, which are all part of the CSS property. In CSS, each of these properties are within an opening and closing curly brace, <code>{}</code>.
</p>

<p>In this <strong>example</strong> the CSS property is <code>font-size</code> and the CSS selector is <code>my_headline_font_size</code>.</p>

<pre><code class="language-css">.my_headline_font_size {
  font-size: 24px;
}</code></pre>

<p>
<b>CSS selectors</b> allow us to specify <em>what</em> we call the CSS property we just created above. For example, we can imagine our <code>font-size</code> property from above being used for a headline, since it's a rather large font size. That's why we used our CSS selector to give it the name of <code>my_headline_font_size</code>. In other words, the part of the CSS that tell us WHAT should have the specific property happens right before the opening curly brace.
</p>

<p>
<b>We can use our CSS selectors to apply our CSS properties with three different types: matching by class, by tag and by id.</b>
</p>

<p>
Let's look at each of them below:
</p>

<p>
If our HTML has a class set (for example, <code> &lt;div class='my_headline_font_size' /&gt;</code>), we use <code>.my_headline_font_size { ... }</code> as the matcher to say, "apply what's in the curly braces to anything that has the class "my_headline_font_size" set in the HTML." Throughout HTML, you can use the same class for multiple items and in different places without any trouble.
</p>

<p>
We can also match every single HTML tag. For example, if we wanted to match every single <code>&lt;h1&gt;</code> tag on the page, we can do that by making the CSS look something like this: <code>h1 { ... }</code>. That will apply what's between the curly braces to every h1 tag we encounter.
</p>

<p>
Finally, we can also match by id. In HTML, we can put an id on an element. Unlike with our classes, we can only have a single item with a certain id on any given page. For example, <code>&lt;h1 id="my_headline_font_size"&gt;Yolo Swag&lt;/h1&gt;</code> sets a headline with the id <code>my_headline_font_size</code>. From there, you can write CSS that applies style properties to the item with that particular id: <code>#my_headline_font_size { ... }</code>.
</p>

<p>
It might be a little fuzzy now, but as you practice and write more and more CSS it will become apparent when to use which CSS selectors and how to make your page look awesome.
</p>


<!-- TODO: add the edited blurb for CSS Selectors into nomster/lesson_8 -->

<img class="glyphicon-picture" src="/assets/githubbranch-a6df2fb8c4b89a8e76c9fbf7b0b9e5d26266c2014a6493f14800d7b4e184bd70.png" alt="" />
<h2 class='__section_heading'>Git commit</h2>
<p>Go through the standard git commit workflow.</p>


  <br>

<div id='error-message-container'></div>

<div class='mark-lesson-completion-status' id="lesson_complete" style="display:none;">
  <a class="btn btn-primary mark-lesson-as-complete-or-not" href="#">
    MARK LESSON 8 COMPLETE
</a></div>

  <div class='mark-lesson-completion-status' id="next_lesson_button" style="display:none;">
    <a class="btn btn-primary mark-lesson-as-complete-or-not" href="../splurty/9">
      GO TO NEXT LESSON <span class='glyphicon glyphicon-arrow-right'></span>
</a>  </div>

<div class='mark-lesson-completion-status mark-lesson-as-not-complete' id="lesson_incomplete" style="display:none;">
  <a class="" href="#">
    or mark lesson 8 not complete
</a></div>

<br style='clear:both;' />
<br style='clear:both;' />

<script>
  $(document).ready(function(){
    var my_data = {"id":300415,"user_id":30307,"name":"splurty","number":8,"status":true,"created_at":"2018-09-10T23:56:45.183-07:00","updated_at":"2018-09-10T23:56:45.192-07:00"};

    // If there is no lesson_status or the status of it is false
    if (my_data === null || my_data.status == false)
    {
      $('#lesson_complete').show();
    } else if (my_data.status == true)
    {
      if ("9" != "") {
        $('#next_lesson_button').show();
      } else {
        $('#go_to_courses_button').show();
      }
      $('#lesson_incomplete').show();
    }

    // PATCH request for marking lesson complete
    $('#lesson_complete').click(function(event){
      event.preventDefault();

      var data = {
        _method: 'PATCH',
        lesson_status: {
          user_id: 30307,
          status: true,
          name: "splurty",
          number: 8
        }
      }



      $.ajax({
        url: "/lesson_statuses/splurty/8",
        type: 'POST',
        data: data
      }).success(function(){
        my_data = {"id":300415,"user_id":30307,"name":"splurty","number":8,"status":true,"created_at":"2018-09-10T23:56:45.183-07:00","updated_at":"2018-09-10T23:56:45.192-07:00"};
        $('#lesson_complete').hide("slow");
        if ("9" != "") {
          $('#next_lesson_button').show();
        } else {
          $('#go_to_courses_button').show();
        }
        $('#lesson_incomplete').show("slow");
      }).fail(function(){
        $('#error-message-container').empty().append("<p class='form-error-message-notification'>There was an issue marking your lesson as complete. Please refresh the page and try again.</p>");
      });
    });

    // PATCH request for marking lesson incomplete
    $('#lesson_incomplete').click(function(event){
      event.preventDefault();

      var data = {
        "_method": 'PATCH',
        lesson_status: {
          user_id: 30307,
          status: false,
          name: "splurty",
          number: 8
        }
      }

      $.ajax({
        url: "/lesson_statuses/splurty/8",
        type: 'POST',
        data: data
      }).success(function(){
        my_data = {"id":300415,"user_id":30307,"name":"splurty","number":8,"status":true,"created_at":"2018-09-10T23:56:45.183-07:00","updated_at":"2018-09-10T23:56:45.192-07:00"};
        $('#lesson_incomplete').hide("slow");
        $('#lesson_complete').show(400);
        $('#next_lesson_button').hide("slow");
        $('#go_to_courses_button').hide("slow");
      }).fail(function(){
        $('#error-message-container').empty().append("<p class='form-error-message-notification'>There was an issue marking your lesson as incomplete. Please contact Matt at matt@thefirehoseproject.com</p>");
      });
    });
  });
</script>



    </div>



<script src="/assets/comments_ask_question_modal-c06ceec81bd498da9edd1b738d9fe0c50600921d22184e47ea3e1531f697b0fb.js"></script>
<link rel="stylesheet" media="screen" href="/assets/rscss/comments/for_lesson-c5a67fe0c8a25bb134fdfdc7c7745933c0721021bacd9db6636c691b3183d9d6.css" />

<br style="clear:both;" /><br />
<div class="discussion" id="forum_section">
  <br style="clear:both;" />
  <hr/><hr/>
  <div class='col-xs-11 col-xs-offset-1'>
      <br style="clear:both;"/>
      <h3>Forum Discussions</h3>
      <br style="clear:both;"/>
  </div>
  <div class="col-xs-12 col-sm-7 col-sm-offset-1">

      <h5 style="margin:0;">
        <img class="comment-avatar-small" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/27913/e0145c3a.gif" alt="" />
        <a href="/comments/41027">LOGO gets cutoff on my local3030</a> | Will at 06/06/2018
      </h5>
      <br style="clear:both;" />

      <h5 style="margin:0;">
        <img class="comment-avatar-small" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/27679/24e355d0.jpg" alt="" />
        <a href="/comments/40477">Restarted PC, now http://localhost:3030/ will not show</a> | Juan at 04/29/2018
      </h5>
      <br style="clear:both;" />

      <h5 style="margin:0;">
        <img class="comment-avatar-small" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/27679/24e355d0.jpg" alt="" />
        <a href="/comments/40476">Restarted PC, now http://localhost:3030/ will not show</a> | Juan at 04/29/2018
      </h5>
      <br style="clear:both;" />

      <h5 style="margin:0;">
        <img class="comment-avatar-small" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/27534/d5e2d83c.jpg" alt="" />
        <a href="/comments/39825">css styles not changing</a> | Brittany at 03/22/2018
      </h5>
      <br style="clear:both;" />

      <h5 style="margin:0;">
        <img class="comment-avatar-small" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/26013/c97c08a3.jpg" alt="" />
        <a href="/comments/38535">Why use ruby links over HTML5?</a> | Thomas at 01/20/2018
      </h5>
      <br style="clear:both;" />

      <h5 style="margin:0;">
        <img class="comment-avatar-small" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/23588/b4fedb94.jpg" alt="" />
        <a href="/comments/38485">Progress Review: Navigation Bar</a> | Linda at 01/18/2018
      </h5>
      <br style="clear:both;" />

      <h5 style="margin:0;">
        <img class="comment-avatar-small" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/22266/7d62b2b4.jpg" alt="" />
        <a href="/comments/37650">No Create Button</a> | Justin at 12/13/2017
      </h5>
      <br style="clear:both;" />

      <h5 style="margin:0;">
        <img class="comment-avatar-small" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/22266/7d62b2b4.jpg" alt="" />
        <a href="/comments/37628">master.scss not working. </a> | Justin at 12/13/2017
      </h5>
      <br style="clear:both;" />

      <h5 style="margin:0;">
        <img class="comment-avatar-small" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/21292/f9220868.png" alt="" />
        <a href="/comments/35998">Columns for LOGO and slogan not showing up</a> | Nelson at 10/11/2017
      </h5>
      <br style="clear:both;" />

      <h5 style="margin:0;">
        <img class="comment-avatar-small" src="/assets/kirk-2dcea0d34e37ef703640a4f5d4792a1f7f2bdd8878a43632a093edc81aea7e51.jpg" alt="" />
        <a href="/comments/34941">Header is stacked vertically not horizontally</a> | Rebecca at 09/13/2017
      </h5>
      <br style="clear:both;" />

      <h5 style="margin:0;">
        <img class="comment-avatar-small" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/10681/ebbc4979.jpg" alt="" />
        <a href="/comments/28908">Network Error:Connection refused</a> | Stuart at 05/18/2017
      </h5>
      <br style="clear:both;" />

      <h5 style="margin:0;">
        <img class="comment-avatar-small" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/8454/04a6c1de.jpg" alt="" />
        <a href="/comments/27616">Issues with GitHib connection</a> | Morgan at 05/02/2017
      </h5>
      <br style="clear:both;" />

      <h5 style="margin:0;">
        <img class="comment-avatar-small" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/11713/77359bd5.JPG" alt="" />
        <a href="/comments/26740">I am entering the .scss file correctly</a> | Dennis at 04/17/2017
      </h5>
      <br style="clear:both;" />

      <h5 style="margin:0;">
        <img class="comment-avatar-small" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/10453/904cde94.jpg" alt="" />
        <a href="/comments/25221">Ruby error when adding .clear class to css file</a> | Daniel at 03/22/2017
      </h5>
      <br style="clear:both;" />

      <h5 style="margin:0;">
        <img class="comment-avatar-small" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/8820/e8e9a55e.JPG" alt="" />
        <a href="/comments/23974">CSS syntax not being highlighted in master.scss</a> | Zayn at 02/26/2017
      </h5>
      <br style="clear:both;" />

      <h5 style="margin:0;">
        <img class="comment-avatar-small" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/8679/4bf39363.jpg" alt="" />
        <a href="/comments/22589">Should the header have class=&quot;row&quot;?</a> | Laura at 02/10/2017
      </h5>
      <br style="clear:both;" />

      <h5 style="margin:0;">
        <img class="comment-avatar-small" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/8183/551bc47a.jpg" alt="" />
        <a href="/comments/21195">How do I get localhost 3030 going</a> | Rebecca at 01/26/2017
      </h5>
      <br style="clear:both;" />

      <h5 style="margin:0;">
        <img class="comment-avatar-small" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/6685/4c23af6d.jpg" alt="" />
        <a href="/comments/21095">Header is vertically not horizontally</a> | Jorge at 01/25/2017
      </h5>
      <br style="clear:both;" />

      <h5 style="margin:0;">
        <img class="comment-avatar-small" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/7945/539f61ae.JPG" alt="" />
        <a href="/comments/20977">LOGO and slogan and links for contribute and about are stacked vertically, not laid out horizontally.</a> | Kalen at 01/25/2017
      </h5>
      <br style="clear:both;" />

      <h5 style="margin:0;">
        <img class="comment-avatar-small" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/5276/f6358155.PNG" alt="" />
        <a href="/comments/15982">Why do we put all the css in master.css.scss? </a> | Celia at 10/10/2016
      </h5>
      <br style="clear:both;" />
  </div>


  <br style="clear:both;" /><br />
  <br style="clear:both;" /><br />

</div>
<br style="clear:both;" /><br />

<script>

</script>


<link rel="stylesheet" media="screen" href="/assets/rscss/comments/ask_question_modal-66ef016bc65fccc632666023576c948250aaade7df0872c6853018b6bfca374f.css" />

<div class="modal fade" id= 'askQuestionModal' tabindex="-1" role="dialog" aria-labelledby= 'askQuestionModalLabel' aria-hidden="true">
  <div class="modal-dialog ask-question-modal">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
        <br class='clr'/>
        <h4 class="modal-title">What is your question about?</h4>
        <div class='dropdown title-dropdown'>
          <button data-toggle='dropdown' id="askQuestionModalLabel" class='dropdown-button'>
            <span class='title-text'>Button</span>
            <span class='caret dropdown-toggle'></span>
          </button>
          <ul class='dropdown-menu'>
              <li id='generic_error_title'>Error in my code/app</li>
              <li id='heroku_error_title'>Error with Heroku</li>
              <li id='general_error_title'>General question or error</li>
          </ul>
        </div>
      </div>
      <div class="modal-body">
        <div class='left-col'>
          <img class="comment-lesson-avatar" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/30307/e5ed9251.png" alt="" />
          <form novalidate="novalidate" class="simple_form new_comment" id="new_comment" enctype="multipart/form-data" action="/forums/2/comments?lesson=8" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="RWvHVuoz+VsisA3hRYfSlqRB/uCPsDCmQaVYSO1n+p+ZnplRwcVs5xbOCh/8wbAOoLbPnQTOBZojZ93dfsKysg==" />
            <div class="input hidden comment_category"><input value="not set" class="hidden form-control" type="hidden" name="comment[category]" id="comment_category" /></div>
            <div class="input string required comment_title"><label class="string required control-label" for="comment_title"><abbr title="required">*</abbr> Question</label><input class="string required form-control" placeholder="Please enter a descriptive title for your question" type="text" name="comment[title]" id="comment_title" /></div>
            <span id='comment_title_error' class='comment-error'>Your question must be at least 15 characters.</span>

            <div class="input url optional comment_github_url"><label class="url optional control-label" for="comment_github_url">First, push your latest code to GitHub, then copy the URL to your repo below:</label><input class="string url optional form-control" placeholder="GitHub URL" type="url" name="comment[github_url]" id="comment_github_url" /></div>
            <span id='comment_github_url_error' class='comment-error'>Please be sure your URL follows the format: github.com/username/repository-name.</span>

            <div class="input url optional comment_heroku_url"><input class="string url optional form-control" placeholder="Heroku URL" type="url" name="comment[heroku_url]" id="comment_heroku_url" /></div>
            <span id='comment_heroku_url_error' class='comment-error'>Please be sure you've included your full Heroku URL. To find your app URL, type <code class="ruby">heroku apps:info</code> inside the application directory.</span>

            <div class="input text optional comment_heroku_logs"><label class="text optional control-label" for="comment_heroku_logs"><a target="_blank" data-toggle="tooltip" title="In order to help you resolve your issue with Heroku, we will need to know details about the error message that exists on Heroku that is only accessible in the logs. Click here for directions on accessing your Heroku logs." href="/cheat-sheets/forum-faq#Debugging-Heroku-Issues">Click here for directions on accessing Heroku log data.</a></label><textarea rows="5" class="text optional form-control" placeholder="Heroku logs" name="comment[heroku_logs]" id="comment_heroku_logs">
</textarea></div>
            <span id='comment_heroku_logs_error' class='comment-error'>Please be sure you've included your Heroku logs.</span>

            <p class='zip-file'>First, <a target="_blank" href="/cheat-sheets/forum-faq#Create-A-Zip-File">create a .zip file</a> containing the contents of your portfolio folder, then upload it: </p>
            <div class="input file optional comment_website_zip_file"><input class="file optional form-control" type="file" name="comment[website_zip_file]" id="comment_website_zip_file" /></div>
            <span id='comment_website_zip_error' class='comment-error'>Please be sure you've included your zip file.</span>

            <div class="input text optional comment_code_with_errors"><textarea rows="5" class="text optional form-control" placeholder="Copy and paste the code related to your question" name="comment[code_with_errors]" id="comment_code_with_errors">
</textarea></div>
            <span id='comment_code_error' class='comment-error'>Please be sure you've included the code you'd like help with.</span>

            <div class="input text optional comment_message"><textarea rows="5" class="text optional form-control" placeholder="Describe your question and how you arrived at the code above" name="comment[message]" id="comment_message">
</textarea></div>
            <span id='comment_message_error' class='comment-error'>Your description must be at least 50 characters.</span>
            <p class='photo-text'><span class='bold'>Optional:</span> Upload an image with your question. You can include up to 5 images.</p>
            <div id='comment_photos'>
              <a class="add_fields" data-association="comment_photo" data-associations="comment_photos" data-association-insertion-template="&lt;div class=&quot;nested-fields remove-comment-photo&quot;&gt;
  &lt;div class=&quot;input file optional comment_comment_photos_picture&quot;&gt;&lt;input class=&quot;file optional form-control&quot; type=&quot;file&quot; name=&quot;comment[comment_photos_attributes][new_comment_photos][picture]&quot; id=&quot;comment_comment_photos_attributes_new_comment_photos_picture&quot; /&gt;&lt;/div&gt;
  &lt;input type=&quot;hidden&quot; name=&quot;comment[comment_photos_attributes][new_comment_photos][_destroy]&quot; id=&quot;comment_comment_photos_attributes_new_comment_photos__destroy&quot; value=&quot;false&quot; /&gt;&lt;a class=&quot;remove_fields dynamic&quot; href=&quot;#&quot;&gt;
    &lt;span class=&quot;glyphicon glyphicon-remove&quot;&gt;&lt;/span&gt;
&lt;/a&gt;  &lt;br&gt;&lt;br&gt;
&lt;/div&gt;" href="#"></a>            </div>
            <div class='submit-line'>
              <button type="button" class='cancel-button' data-dismiss="modal" aria-label="Close"><span aria-hidden="true">Cancel</span></button>
              <input type="submit" name="commit" value="Post Your Question" class="submit-question" id="comment-submit-question-button" data-disable-with="Processing..." />
            </div>
</form>        </div>
        <div class='right-col'>
          <h4>Tips</h4>
          <p class='-bold'>
            Keep your question relevant to this space.
          </p>
          <p>
            Make sure you've selected the correct space to post your question. This way your question is most likely to be answered.
          </p>
          <p class='-bold'>
            Check for existing answers.
          </p>
          <p>
            You can search for your question to see if an answer has already been provided. Avoid posting duplicate questions.
          </p>
          <p class='-bold'>
            Keep it clear and concise.
          </p>
          <p>
            Other users will only be able to help you if you provide enough details and are clear about your question. Use the body field to provide the details of your question.
          </p>
          <p class='-bold'>
            Be polite.
          </p>
          <p>
            Typing questions and comments in all caps and using unnecessary punctuation (!!1!/???) will not increase the likelihood of your question being answered.
          </p>
        </div>
      </div>
    </div>
  </div>
</div>

<script>
  $(function(){
    submitNewComment("/comments");
  });
</script>



  <script src="/assets/floating_nav-3fa5297423146bf9c8a599361ff1e3c072868e0cde99d79e53923a839b55869f.js"></script>

<div class="floating-nav affix-top full-width" data-spy="affix">
  <ul class="nav navbar-nav">
      <li>
        <a href="../splurty/7">
          <img class="img-responsive nav-icon" alt="Left Pointing Arrow" src="/assets/icons/icon_previouslesson-f6994ad560dbeae27afb8c06fbcc5bd136d3d078b0c57732362f4b2c6a1273d8.png" /> Previous Lesson
</a>      </li>
    <li class='float-right search-section'>
      <form target="_blank" rel="noopener noreferrer" action="/comments" accept-charset="UTF-8" method="get"><input name="utf8" type="hidden" value="&#x2713;" />
        <input alt=" " type="image" src="/assets/icons/magnifying-glass-fe2c625f5ae54f4601caeaf8e21634cbbd57ea80de12ef65c335733ab7a3c19b.png" class="search" data-disable-with="Searching..." />
        <input type="text" name="q" id="q" placeholder="Search Answers..." class="search-box" />
</form>    </li>
      <li id='question' class='float-right question-section'>
        39 Questions
      </li>
    <li class='float-right active-section'>
          <img class="student-portrait student-1" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/17056/4296a2d8.jpg" alt="" />
          <img class="student-portrait student-2" src="https://firehose-avatars.s3.amazonaws.com/uploads/user/avatar/345/d7197ff6.png" alt="" />
          <img class="student-portrait student-3" src="/assets/kirk-2dcea0d34e37ef703640a4f5d4792a1f7f2bdd8878a43632a093edc81aea7e51.jpg" alt="" />
      3 Active
    </li>
  </ul>
</div>

</div>

    </div>

    <script src="https://www.gstatic.com/firebasejs/3.5.1/firebase.js"></script>
    <!-- Don't show hellobar if user is signed in or if on applicants pages -->

      <script id="IntercomSettingsScriptTag">
  window.intercomSettings = {"app_id":"cynq5t9i","email":"clarkngo@gmail.com","custom_data":{"utm_campaign_first_click":null,"utm_medium_first_click":null,"utm_source_first_click":null,"utm_campaign_last_click":"new_community_post","utm_medium_last_click":"notification_bell","utm_source_last_click":"platform"},"user_hash":"d2eb70e32e2d2f1fddc1134f424c1f30b1846eebcc27e063091ad0218e199a51"};
</script>
<script>(function(){var w=window;var ic=w.Intercom;if(typeof ic==="function"){ic('reattach_activator');ic('update',intercomSettings);}else{var d=document;var i=function(){i.c(arguments)};i.q=[];i.c=function(args){i.q.push(args)};w.Intercom=i;function l(){var s=d.createElement('script');s.type='text/javascript';s.async=true;s.src='https://widget.intercom.io/widget/cynq5t9i';var x=d.getElementsByTagName('script')[0];x.parentNode.insertBefore(s,x);}if(w.attachEvent){w.attachEvent('onload',l);}else{w.addEventListener('load',l,false);}};})()</script>

      <!-- checks and updates session count -->
<script>
  document.addEventListener("visibilitychange", handleChange("/user_account_data/30307"));
</script>

    <!-- GOOGLE REMARKETING TAGS -->
    <!--
Remarketing tags may not be associated with personally identifiable information or placed on pages related to sensitive categories. See more information and instructions on how to setup the tag on: http://google.com/ads/remarketingsetup
-->

<!--
This script can be used to add custom params
to the remarketing tag
-->

<!--
<script type="text/javascript">
  var google_tag_params = {
    site_location: 'marketing_pages'
  };
</script>
-->

<script type="text/javascript">
  /* <![CDATA[ */
  var google_conversion_id = 927357968;
  var google_remarketing_only = true;

  // Enable line if we want to use custom params
  // var google_custom_params = window.google_tag_params;
  /* ]]> */
</script>
<div style='display:none'>
  <script type="text/javascript" src="//www.googleadservices.com/pagead/conversion.js">
  </script>
</div>

<noscript>
  <div style="display:inline;">
  <img height="1" width="1" style="border-style:none;" alt="" src="//googleads.g.doubleclick.net/pagead/viewthroughconversion/927357968/?guid=ON&amp;script=0"/>
  </div>
</noscript>

  </body>
</html>


