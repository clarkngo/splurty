# README

TEMPORARY README

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




Lesson 8: Adding a Top Navigation Bar
In the previous lessons, we've started building a web application and have integrated with Bootstrap. In this lesson, we will add the header that will be present on every single page of our web application. We will also start using some of the design power from the Bootstrap framework.



If we quickly check back to our wireframes, we can see that we want to add a top navigation to our web application.

If we take a step back and think about how most web applications are built, we quickly realize that there are some features that are on every single page. The top navigation, which includes links to other pages, is a great example of a feature that goes on more than just a single page.

At first it might make sense to put our top nav on all of the pages in our web application by copying and pasting. While this works at the very beginning when we only have a handful of pages, think about how much extra work we'll have created for ourselves once our web application grows to hundreds of pages and we need to make a small adjustment to the top navigation (like change the word "about" to "team"). We would have to make that single small change on hundreds of pages - that's no fun!

In order to get around that, we want to avoid copying and pasting the code that goes on every page onto all the different pages inside our application. Instead, we'll use a special file called application.html.erb which contains the things that are shared across all the pages. In fact, the line that says yield actually pulls in all the page-specific stuff.

Pro-tip
Using the keyboard shortcut, command + P (or CTRL + P for Windows / Linux) inside the Sublime Text or Atom editor will open a fuzzy-finding file-opening dialog. Start typing the name of the file, and when the file you want is listed at the top, click enter and boom, the file will be opened. In this case, command + P and typing "application.h" then hitting enter will open the file. If you want to quickly open a file, this is a super useful feature.

So if we want to create a place for our top navigation, it should be in our application.html.erb. To do this, let's start by adding a header tag into app/views/layouts/application.html.erb right under the body tag and with the bootstrap 4 row class:

<!DOCTYPE html>
<html>
  <head>
    <title>Splurty</title>
    <%= csrf_meta_tags %>
    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>
  <body>
    <header class="row">
    </header>

   <%= yield %>

  </body>
</html> 
 
Make sure you still have the yield (<%= yield %>) in there. Then save the file and refresh the page.

The header tag (note: this is different from the head tag) is an HTML5 tag where you can put header stuff— in our case, if you look back to the wireframes, the logo, slogan, and links.

Ok, inside the header let's add a spot for the logo inside of a division (div):

<!DOCTYPE html>
<html>
  <head>
    <title>Splurty</title>
    <%= csrf_meta_tags %>
    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>
  <body>
    <header class="row">
      <div>
        LOGO
      </div>
    </header>

   <%= yield %>

  </body>
</html> 
 
 
A div stands for "division" and basically means we have a box that we can put things inside.

Save the file and refresh.

Cool, now we have the text "LOGO," which we can flesh out in a little bit.

Next, let's work on getting our slogan on the page. We want to position our slogan right next to the logo. Since we're using Bootstrap, we can position elements on our page using something called the Bootstrap 4 grid system.

Take a few minutes and read up on the Bootstrap 4 grid system here.

In short, the grid that we have on our page is 12 columns wide and we're going to give each element— the logo, slogan and links— a few columns of space. Our logo is probably good with 3 columns of space, and maybe the slogan should take 4 columns of space. Doing this will basically ensure that our boxes are next to each other.

Bootstrap allows us to specify the width of our box for different devices, such as laptop, tablet and mobile screens. Let's start making things look good on mobile first and worry about bigger screens later.

So let's switch this up, add our col-* classes and see what we get:

<!DOCTYPE html>
<html>
  <head>
    <title>Splurty</title>
    <%= csrf_meta_tags %>
    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>
  <body>
    <header class="row">
      <div class="col-3">
        LOGO
      </div>
      <div class="col-4">
        Splurting out unsolicited advice about entrepreneurship since 2016
      </div>
    </header>

    <%= yield %>

  </body>
</html> 
 
 
 
Cool, save this and refresh.

This places our logo and slogan side by side. Unfortunately, it sucks the main body into the top nav as well, but we'll fix that in the next step.

Let's add a spot for the links in our web application. If we look to our wireframes, we can see that we want to have a link to contribute a quote and a link to our about page. Right now, we don't know where these will go, so we'll use a special symbol, the hashtag (#) which will be a placeholder that we can update later.

If we put our links into 5 columns by using col-5, we're using up the entire 12 columns of horizontal space on our page, and things should line up a bit better.

To create the actual links, we're writing our first line of ruby code inside one of our views, like so:

<!DOCTYPE html>
<html>
  <head>
    <title>Splurty</title>
    <%= csrf_meta_tags %>
    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>
  <body>
    <header class="row">
      <div class="col-3">
        LOGO
      </div>
      <div class="col-4">
        Splurting out unsolicited advice about entrepreneurship since 2016
      </div>
      <div class="col-5">
        <%= link_to 'Contribute', '#' %>
        <%= link_to 'About', '#' %>
      </div>
    </header>

    <%= yield %>

  </body>
</html> 
 
 
 
Save the file and refresh the page.

Ok, it's getting there, but now we see that the quote is still getting sucked into the top navigation. Let's fix this after we take a moment to zoom out and understand how HTML & CSS and ruby code work.

Zooming out HTML & CSS
HTML is the content on the page that we can see. All of our HTML files exist inside the app/views/* folders and the actual code is always broken up into "tags." These tags start with an opening tag like <h1> and end with a closing tag like </h1>. HTML is all about the content of the page.

CSS is short for Cascading Style Sheets and represents the styles of a page, or the visual components on a website that make it look better. CSS consists of selectors that we can attach to certain parts of our HTML code. By attaching specific CSS styles to certain parts of HTML, we can very precisely define how things actually look for different sections of our page.

Let's stay zoomed out a minute longer and look at the different ways we can write ruby code.

The different ways ruby code can be executed in a web application
There are basically three different ways that ruby code is typically run:

.rb files
<%= inside .html.erb files
<% inside .html.erb files
Inside files that have the file extension .rb. These are regular ruby files, and consist entirely of code that is written in the ruby programming language. Code inside these .rb files does not need anything special to execute and run our ruby code.

Inside files in our view folder that have the file extension .html.erb. In these files, ruby code is executed a little bit differently. These files consist mostly of HTML, or the content on our pages. Occasionally, we need to use ruby code right on our HTML page. Some good examples are when we want to pull something out of our database and show it on the page, or when we want to create a link to a specific page.

In our example from above, we created a link and showed it inside our HTML page. If we look at the example of the <%= link_to 'Contribute', '#' %>, that is calling out to ruby and having ruby figure what the link should be. Notice the equals sign in the <%=.

There are two different ways to execute the ruby code inside the .html.erb files. First, If you omit the equals sign and instead of <%= you type <%, it will execute the ruby code but will not display anything on the page. Second, if you want your ruby code output to be shown on the HTML page— like the above case where we need to show the link so a user can click on it— use: <%=

If you're ever writing code inside an html.erb file, and instead of putting the content you expect on the page, it actually outputs nothing, double-check that you have <%= and not <%.

Adding a clear tag
Now that we're a bit more familiar with how HTML & CSS interact together, let's actually write a line of CSS code and apply its rule to a part of our page.

After our header, we should really "clear out" our Bootstrap columns so the quotes are not showing up inside of our top navigation bar. Let's do this by adding a "clearing br tag."

<!DOCTYPE html>
<html>
  <head>
    <title>Splurty</title>
    <%= csrf_meta_tags %>
    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>
  <body>
    <header class="row">
      <div class="col-3">
        LOGO
      </div>
      <div class="col-4">
        Splurting out unsolicited advice about entrepreneurship since 2016
      </div>
      <div class="col-5">
        <%= link_to 'Contribute', '#' %>
        <%= link_to 'About', '#' %>
      </div>
    </header>

    <br class="clear" />

    <%= yield %>

  </body>
</html> 
After we've added our clear tag, we need to write some CSS code. To do this, lets open our file we made recently at app/assets/stylesheets/master.scss and add the following code in it.

@import "bootstrap";

.clear {
  clear: both;
} 
 
 
Ok, now save and refresh.

Nice, now the top nav stuff is "cleared" and the rest of the content is pushed down the page.

If we zoom out again, we see that our master.scss is the file that will allow us to write the CSS rules to decide how the page will look.

CSS is something you learn best by doing, so we're going to tell you to write certain lines of it and as soon as they make your page look different, you'll understand what's going on.

The World's Fastest CSS Crash Course
CSS really has two different parts to it: CSS properties define the actual styling details, and CSS selectors connect the CSS properties to the correct place on a website.

Let's look at both in more detail:

CSS Properties define exactly what kind of style and design are used for a specific property. Think about things like font-family or font-size, which are all part of the CSS property. In CSS, each of these properties are within an opening and closing curly brace, {}.

In this example the CSS property is font-size and the CSS selector is my_headline_font_size.

.my_headline_font_size {
  font-size: 24px;
}
CSS selectors allow us to specify what we call the CSS property we just created above. For example, we can imagine our font-size property from above being used for a headline, since it's a rather large font size. That's why we used our CSS selector to give it the name of my_headline_font_size. In other words, the part of the CSS that tell us WHAT should have the specific property happens right before the opening curly brace.

We can use our CSS selectors to apply our CSS properties with three different types: matching by class, by tag and by id.

Let's look at each of them below:

If our HTML has a class set (for example, <div class='my_headline_font_size' />), we use .my_headline_font_size { ... } as the matcher to say, "apply what's in the curly braces to anything that has the class "my_headline_font_size" set in the HTML." Throughout HTML, you can use the same class for multiple items and in different places without any trouble.

We can also match every single HTML tag. For example, if we wanted to match every single <h1> tag on the page, we can do that by making the CSS look something like this: h1 { ... }. That will apply what's between the curly braces to every h1 tag we encounter.

Finally, we can also match by id. In HTML, we can put an id on an element. Unlike with our classes, we can only have a single item with a certain id on any given page. For example, <h1 id="my_headline_font_size">Yolo Swag</h1> sets a headline with the id my_headline_font_size. From there, you can write CSS that applies style properties to the item with that particular id: #my_headline_font_size { ... }.

It might be a little fuzzy now, but as you practice and write more and more CSS it will become apparent when to use which CSS selectors and how to make your page look awesome.


Git commit
Go through the standard git commit workflow.

Lesson 9: Making the Top Nav Look Awesome
In the previous lesson, we started setting up the header that will be displayed on all pages. In this lesson, we will tweak the header's appearance by modifying the HTML and CSS that our application generates.



Working on the logo
Let's keep our web designer hats on for a little bit longer and start creating a simple logo for our web app. One place we can check for some inspiration is cssdeck.com. CSSDeck is a listing of small and very well-designed widgets that we can easily pull into our app.

If you search around for logos a bit, you can find this circle which we can use to style our logo.

First, let's copy the HTML in the top left pane of CSSDeck and replace "LOGO" in app/views/layouts/application.html.erb.

<!DOCTYPE html>
<html>
<head>
  <title>Splurty</title>
  <%= csrf_meta_tags %>
  <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
  <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
</head>
<body>
  <header class="row">
    <div class="col-3">
      <div class="circle">
        <br />
        YOLO
        <br />
        LOL
        <br />
        OMG
      </div>
    </div>
    <div class="col-4">
      Splurting out unsolicited advice about entrepreneurship since 2016
    </div>
    <div class="col-5">
      <%= link_to 'Contribute', '#' %>
      <%= link_to 'About', '#' %>
    </div>
  </header>

  <br class="clear" />

<%= yield %>

</body>
</html> 
 
 
 
 
 
 
 
Save the file and refresh the page. You should see the logo changed, but it doesn't have the cool colors and effects that the demo we saw on CSSDeck had. That's because we haven't pulled in the CSS styles yet.

Let's do that. Open up app/assets/stylesheets/master.scss and copy and paste the stuff we see on the CSSDeck website:

.clear {
  clear: both;
}

.circle {
    font-weight: bold;
    font-style: italic;
    position: relative;
    border-radius: 100%;
    background: #f84342;
    border: 1px solid #F7F7F7;
    width: 80px;
    height: 80px;
    margin: 10px 10px;
    text-align: center;
    color: #FFF;
    font-size: 10px;
    line-height: 16px;
    cursor: pointer;
    transform: rotate(11deg);
    -ms-transform: rotate(11deg); /* IE 9 */
    -webkit-transform: rotate(11deg); /* Opera, Chrome, and Safari */
} 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
Save and refresh. Awesome - our logo is starting to look good.

Now let's update the text in our logo. Open up app/views/layouts/application.html.erb and change it to a blurb that applies to your application. Here's what I did:

<div class="circle">
  <br />
  You know
  <br />
  you need
  <br />
  to code
</div> 
 
 
 
 
 
Then we should save the file, and refresh the page.

Styling the slogan
If we look at our slogan with our web designer hats on, we can see that we're not really using a good font. Since fonts are super important to the feel and design of any web application, let's switch our fonts out to something better.

First, let's add another class inside our div tag, so we can match it with a CSS style. Change application.html.erb to look like this:

<header class="row">
  <div class="col-3">
    <div class="circle">
      <br />
      You know
      <br />
      you need
      <br />
      to code
    </div>
  </div>
  <div class="col-4 slogan">
    Splurting out unsolicited advice about entrepreneurship since 2016
  </div>
  <div class="col-5">
    <%= link_to 'Contribute', '#' %>
    <%= link_to 'About', '#' %>
  </div>
</header> 
A good font for our slogan would be a "Garamond" type font that's also italic.

If you've never played around with fonts, Chris Coyier's CSS tricks is a great resource. Check it out and choose a stack of fonts that you like. Each of these different font stacks will give your application a different look and feel, so try a couple out.

Note: We'll show you a few different ways to adjust the fonts in your application throughout this tutorial. For now, let's just adjust the font in the slogan.

For now, let's go with the "Traditional Garamond-based serif stack."

To implement our new font stack, add this to the bottom of app/assets/stylesheets/master.scss.

.slogan {
  font-family: "Palatino Linotype", Palatino, Palladio, "URW Palladio L", "Book Antiqua", Baskerville, "Bookman Old Style", "Bitstream Charter", "Nimbus Roman No9 L", Garamond, "Apple Garamond", "ITC Garamond Narrow", "New Century Schoolbook", "Century Schoolbook", "Century Schoolbook L", Georgia, serif;
}
Next, let's make the slogan italic.

.slogan {
  font-family: "Palatino Linotype", Palatino, Palladio, "URW Palladio L", "Book Antiqua", Baskerville, "Bookman Old Style", "Bitstream Charter", "Nimbus Roman No9 L", Garamond, "Apple Garamond", "ITC Garamond Narrow", "New Century Schoolbook", "Century Schoolbook", "Century Schoolbook L", Georgia, serif;
  font-style: italic;
} 
Now let's push the slogan a little bit down the header. To do that, we're going to add a touch of padding to our slogan division (aka div) box, like so:

.slogan {
  font-family: "Palatino Linotype", Palatino, Palladio, "URW Palladio L", "Book Antiqua", Baskerville, "Bookman Old Style", "Bitstream Charter", "Nimbus Roman No9 L", Garamond, "Apple Garamond", "ITC Garamond Narrow", "New Century Schoolbook", "Century Schoolbook", "Century Schoolbook L", Georgia, serif;
  font-style: italic;
  padding-top: 26px;
} 
Save the file and refresh. Awesome, our new font looks a lot better.

Styling the top nav links
As we just learned, whenever we want to style something, we first need to add a new class to the div inside our HTML file, then specify the properties of that new style as a CSS class inside our master.scss file.

Open up app/views/layouts/application.html.erb and add the the new CSS class - let's call it "links" - to the div:

<header class="row">
  <div class="col-3">
    <div class="circle">
      <br />
      You know
      <br />
      you need
      <br />
      to code
    </div>
  </div>
  <div class="col-4 slogan">
    Splurting out unsolicited advice about entrepreneurship since 2016
  </div>
  <div class="col-5 links">
    <%= link_to 'Contribute', '#' %>
    <%= link_to 'About', '#' %>
  </div>
</header> 
Save the file.

Now we can jump into our master.scss stylesheet and create the actual CSS styles. Just like we did with the slogan, let's push our links down the page a bit further. Open back up app/assets/stylesheets/master.scss and add this line to the bottom:

.links {
  padding-top: 26px;
}
Now let's override the color of all the links inside the "links" div to be black. To do this, we start by saying .links because that will match anything that is a links box. Then we add a so it matches all the links inside a link box. (The ruby code link_to turns into an HTML tag that looks like this: <a href="#">Link Text</a>, so we add the a here so it matches the links.) Then we can specify the color. Add this to master.scss.

.links a {
  color: black;
}
Save and refresh. Cool, the color of the links just switched to black. Let's make these a bit bigger too.

.links a {
  color: black;
  font-size: 25px;
} 
Save the file and refresh. Nice, the font is a bit bigger and our links stand out more.

Next, let's underline our links by simply adding a border to the bottom of the link. We're going to want to specify that our border has a height of 1px (1 pixel), and is a solid line with a grey color.

If you want to play around with colors a bit more, check out colorpicker.com and find the color you want to try. At the top of colorpicker.com, you'll see a 6-digit hex number (a hex number is 0-9+ABCDEF). Once you find a color you like, highlight and copy it over.

I'm going with a grey-ish color with the hex code of #dfdfdf. Make sure to include the hashtag at the beginning of the color code; colorpicker.com won't automatically copy that.

Now, let's add our CSS code to actually create the underline effect:

.links a {
  color:black;
  font-size: 25px;
  border-bottom: 1px solid #dfdfdf;
} 
Save the file and refresh. Awesome - it's starting to look good.

Adding some borders to the navbar
Now let's add a border to the navbar. I want to add a 9-pixel-thick border with a very dark grey color (hex code: #222222). Add this to the bottom of master.scss.

header {
  border-top: 9px solid #222222;
}
Save the file, and refresh the page so you can preview the change.

Now let's add a horizontal rule underneath the navbar so a visitor can clearly see where the navbar ends. Horizontal rules are divider lines.

Open up app/views/layouts/application.html.erb and add this code:

<header class="row">
  <div class="col-3">
    <div class="circle">
      <br />
      You know
      <br />
      you need
      <br />
      to code
    </div>
  </div>
  <div class="col-4 slogan">
    Splurting out unsolicited advice about entrepreneurship since 2016
  </div>
  <div class="col-5 links">
    <%= link_to 'Contribute', '#' %>
    <%= link_to 'About', '#' %>
  </div>
</header>

<hr />

<br class="clear" /> 
Save and refresh. Hmm, nothing got displayed on the page. The reason being that the horizontal rule is getting sucked into the navigation and it's not being displayed. We need to make the horizontal rule clear out the Bootstrap columns. Open up master.scss and add this to the bottom.

hr {
  clear:both;
}
Save the file and refresh. Nice, the top nav is looking pretty good. We still need to adjust the font of the links. Let's do that next when we adjust the fonts of the main quote and author as well.


Git commit
Go through the standard git commit workflow.

Lesson 10: Getting our Font Styles Perfect
In the previous lessons, we've started building a web application, but we've been using the default fonts the application chose for us. In the intro course we showed the importance of font selection when it comes to design elements of the page.

In this lesson, we will cover using custom fonts inside Ruby on Rails web applications. We will show three different ways to specify fonts. First, we will show you how to specify a font that the web browser can show without loading any special fonts. Second, we'll show you how to load custom fonts using the Google Font API. Third, we'll show you how to bring custom fonts into your web application, allowing you to use fonts downloaded from sites like fontsquirrel.com into your web application.



Fonts are a super important design element of every web application, especially because adding a new font to our application will make it look a lot more unique.

Since fonts are so important from a design perspective, we're going to walk you through 3 different ways to adjust the fonts in your application: Easy, Intermediate and Advanced.

Easy - Making a Simple Font Change
Setting the quote to a better looking font by using one of the regularly available fonts is the easiest way to adjust fonts. In this method, we can also play with a couple of other variables, like the font-weight, or how bold (or thin) the font is, and the letter-spacing, or how close together the letters are.

Since our quote is wrapped inside an h1 tag, we can simply add some CSS styles in the master.scss file to specify font size, weight, color, etc.

To start, let's set the font to be Helvetica and adjust the weight and letter spacing. Add this to the bottom of app/assets/stylesheets/master.scss.

h1 {
  font-family: "Helvetica Neue", Helvetica, sans-serif;
  font-weight: 600;
  letter-spacing: -1.5px;
}
Save and refresh. Cool, that made our quote look a lot better.

Let's do the same for h2. Add this to the bottom of app/assets/stylesheets/master.scss. Note: Make sure you have two style blocks, one for the h1 and another for the h2.

h2 {
  font-family: "Helvetica Neue", Helvetica, sans-serif;
  font-weight: 600;
  letter-spacing: -1.5px;
}
Save the file and refresh. Cool, now our app looks better using a different font.

Now let's take it to the next level.

Intermediate - Using Google Fonts
The easy method above will change the font on the page, but will only work for your users if they have the font you used installed on their machine.

Google provides us with web fonts that allow us to use a lot of customized fonts for our application without having to worry if a user has those fonts installed in their browser or not. We simply load the font from the Google server and can use it inside of any web application.

First, let's find a good looking font on google.com/fonts. Once you find a font you like, click on the red plus button:

Google Font Step 1 Screenshot
The plus button will add the font to your "selection" and open a window on the bottom of the screen which you need to click to open. Click on the black selected window at the bottom of the screen and then click "@IMPORT".

Google Font Step 2 Screenshot
Awesome. Now if you copy the line of code between the style tags that starts with @import, and paste it at the very top of app/assets/stylesheets/master.scss, we can actually access our new font.

Note: You may have a different URL than we are using.

@import url('https://fonts.googleapis.com/css?family=Overpass');
 

Common Gotcha
A common gotcha
Make sure you copy the semicolon at the end of the url that google fonts gives you.

Also, make sure you paste the font code on a new line and not on the same line as some other code.

Make sure the google font url has https, not http. Otherwise, it will not work with Heroku.

Let's use it
If we scroll down to our h1 and h2 CSS right now, it looks like this:

h1 {
  font-family: "Helvetica Neue", Helvetica, sans-serif;
  font-weight: 600;
  letter-spacing: -1.5px;
}

h2 {
  font-family: "Helvetica Neue", Helvetica, sans-serif;
  font-weight: 600;
  letter-spacing: -1.5px;
}
Let's remove the font-weight and letter-spacing from the CSS class. If we go back to the Google Fonts page, we can see under "Specify in CSS" what we should set our font-family to:

Google Font Step 3 Screenshot
Adjust the h1 and h2 to look like this:

h1 {
  font-family: 'Overpass', sans-serif;
}

h2 {
  font-family: 'Overpass', sans-serif;
} 
 
Note: You may have a different font than we are using. Feel free to pick any font you want!

Save the file and refresh. Awesome! The font changed and is now using the one we pulled from Google Fonts.

Advanced Fonts - Using Custom Web Fonts
Google Web Fonts is nice, and it allows us to have access to a bigger variety of fonts, but we can get even more specific and use our very own fonts, or use fonts that fewer people have access to.

All fonts listed on Google Web Fonts are open source. Building fonts takes a lot of work, and a lot of times font developers don't want to release them under a very open license. This means there are higher-quality font foundries out there on the net.

One place that has some really awesome free fonts— many of which are higher quality than Google Web Fonts— is FontSquirrel.

Find the font you like on FontSquirrel.com and press the blue download button.

After the download, you should have a .zip file in your download folder. For me, I have a file called Nobile.zip. Unzip the file and find the actual raw font files - either .ttf, .otf, etc.

First, we need to convert the raw font into a web font. It turns out FontSquirrel will help us with that too. If you look in the FontSquirrel navbar, you can click on Generator and you should see a form where you can upload a font.

Click on the "Upload Fonts" button and navigate to the font file you just unzipped.

In my case, the Nobile font has two fonts I want to pull into my application: Nobile-Regular.ttf and Nobile-MediumItalic, so I'm going to upload both those files. The font you choose may or may not have multiple options, so use your judgment.

Leave the 'Optimal' radio button selected, and then check the "Yes, the fonts I'm uploading are legally eligible for web embedding" box. Once you check that, a purple button appears to download your web font kit. Click the purple "Download Your Kit" button.

This takes a couple of moments, and converts your font into the best version for the web.

Once it finishes, you get a .zip file. Unzip it so you see a bunch of different files.

We need to copy these files into your project. Open up Windows Explorer or Finder to the location of your web application, and navigate into the app/assets folder.

The next step is to create a new folder where our new fonts will live. Do this by creating a fonts folder inside app/assets.

Now copy all the .eot, .svg, .tff, and .woff files from the .zip file into your newly created fonts folder.

To use our new fonts, we need to copy a few lines of CSS code into our application.

Go to your Sublime Text editor and open the file called stylesheet.css that lives in your font's zip archive.

It should look something like this:

/* Generated by Font Squirrel (https://www.fontsquirrel.com) on October 28, 2016 */
@font-face {
    font-family: 'nobileregular';
    src: url('nobile-regular-webfont.eot');
    src: url('nobile-regular-webfont.eot?#iefix') format('embedded-opentype'),
         url('nobile-regular-webfont.woff') format('woff'),
         url('nobile-regular-webfont.ttf') format('truetype'),
         url('nobile-regular-webfont.svg#nobileregular') format('svg');
    font-weight: normal;
    font-style: normal;
}

@font-face {
    font-family: 'nobilemedium_italic';
    src: url('nobile-mediumitalic-webfont.eot');
    src: url('nobile-mediumitalic-webfont.eot?#iefix') format('embedded-opentype'),
         url('nobile-mediumitalic-webfont.woff') format('woff'),
         url('nobile-mediumitalic-webfont.ttf') format('truetype'),
         url('nobile-mediumitalic-webfont.svg#nobilemedium_italic') format('svg');
    font-weight: normal;
    font-style: normal;
}
Copy the whole file, then go into your web application and create a new file called fonts.scss at app/assets/stylesheets/fonts.scss and paste everything into it.

One of the things we need to adjust inside the font CSS code is the asset helper method. In short, our fonts live in a folder called 'assets/fonts,' so we need to change the method to direct us to the fonts folder, like this:

/* Generated by Font Squirrel (https://www.fontsquirrel.com) on October 28, 2016 */
@font-face {
  font-family: 'nobileregular';
  src: font_url('nobile-regular-webfont.eot');
  src: font_url('nobile-regular-webfont.eot?#iefix') format('embedded-opentype'),
       font_url('nobile-regular-webfont.woff') format('woff'),
       font_url('nobile-regular-webfont.ttf') format('truetype'),
       font_url('nobile-regular-webfont.svg#nobileregular') format('svg');
  font-weight: normal;
  font-style: normal;
}

@font-face {
  font-family: 'nobilemedium_italic';
  src: font_url('nobile-mediumitalic-webfont.eot');
  src: font_url('nobile-mediumitalic-webfont.eot?#iefix') format('embedded-opentype'),
       font_url('nobile-mediumitalic-webfont.woff') format('woff'),
       font_url('nobile-mediumitalic-webfont.ttf') format('truetype'),
       font_url('nobile-mediumitalic-webfont.svg#nobilemedium_italic') format('svg');
  font-weight: normal;
  font-style: normal;
} 
 
 
 
 
 
 
 
 
 
Make sure you save the file.

The last thing to do is prepare our rails application to serve font files (all files with the extensions .svg, .eot, .woff or .ttf) from our new font folder. By default, only images, stylesheets and javascript files are pulled in.

Do this by adjusting config/application.rb to look like this:

require File.expand_path('../boot', __FILE__)

require 'rails/all'

# Require the gems listed in Gemfile, including any gems
# you've limited to :test, :development, or :production.
Bundler.require(:default, Rails.env)

module Splurty
  class Application < Rails::Application
    # Settings in config/environments/* take precedence over those specified here.
    # Application configuration should go into files in config/initializers
    # -- all .rb files in that directory are automatically loaded.

    # Set Time.zone default to the specified zone and make Active Record auto-convert to this zone.
    # Run "rake -D time" for a list of tasks for finding time zone names. Default is UTC.
    # config.time_zone = 'Central Time (US & Canada)'

    # The default locale is :en and all translations from config/locales/*.rb,yml are auto loaded.
    # config.i18n.load_path += Dir[Rails.root.join('my', 'locales', '*.{rb,yml}').to_s]
    # config.i18n.default_locale = :de

    # Add the fonts path
    config.assets.paths << "#{Rails.root}/app/assets/fonts"

    # Precompile additional assets
    config.assets.precompile += %w( .svg .eot .woff .ttf )

  end
end 
 
 
 
 
Save the file. Cool, now our application knows how to deal with these font files, and we added our font to our application.

Remember, anytime we make changes inside config/application.rb, we need to restart our server. Let's do that now.

Cool, so now our application has access to this font, but we haven't set anything to actually use the font.

If we open up our app/assets/stylesheets/fonts.scss, we see these two font-families defined:

font-family: 'nobileregular';
font-family: 'nobilemedium_italic';
To use your new font, copy the name after font-family that you want to use. For the main quote (the h1) in my app, I'm going to switch the font to nobileregular.

Since we're going to switch our font from using Google Web Fonts, we should delete the line at the top of app/assets/stylesheets/master.scss that looks like this:

@import url('https://fonts.googleapis.com/css?family=Overpass');
Ok, now adjust the font-family in h1 to match the font we just copied onto our clipboard. So mine looks like this:

h1 {
  font-family: 'nobileregular', sans-serif;
} 
Looking good. Cool, now let's make the font bold:

h1 {
  font-family: 'nobileregular', sans-serif;
  font-weight: bold;
} 
And finally, let's make the font a bit bigger. Say, 48 pixels tall.

h1 {
  font-family: 'nobileregular', sans-serif;
  font-weight: bold;
  font-size: 48px;
} 
Finishing the rest of the fonts
Now we have our application ready to roll with fonts, and all we need to do is specify the font that we want to use in each case.

The next font we should update is our h2, which we're using for the author of the quote. I want to use this font-family that we have defined above in the CSS file:

font-family: 'nobilemedium_italic';
It's called nobilemedium_italic, and I'm going to dig into the h2 in master.scss.

h2 {
  font-family: 'nobilemedium_italic', sans-serif;
} 
Save the file and refresh. Our application is really starting to come together!

Lastly, in this section let's adjust the links in the top navigation to use our new font. Return to the app/views/layouts/application.html.erb file and find the code that looks like this:

<div class="col-5 links">
  <%= link_to 'Contribute', '#' %>
  <%= link_to 'About', '#' %>
</div>
This means that if we want to adjust the font-family in this part of the page, we will need to adjust the .links a CSS selector. Edit app/stylesheets/master.scss to look like this:

.links a {
  color: black;
  font-size: 25px;
  border-bottom: 1px solid #dfdfdf;
  font-family: 'nobileregular', sans-serif;
} 
And let's make this bold as well...

.links a {
  color: black;
  font-size: 25px;
  border-bottom: 1px solid #dfdfdf;
  font-family: 'nobileregular', sans-serif;
  font-weight: bold;
} 
Awesome. Now save the file and refresh the page. Ah, fonts are a beautiful thing!


Git commit
Go through the standard git commit workflow.

Lesson 11: Adding a Footer
In the previous lessons, we've built the foundations of our application and improved some of the fonts. In this lesson, we'll add a footer to the application and adjust how it looks.



When we look back to our wireframes we can see that we want to have a footer on our pages.

Splurty Homepage
splurty homepage
Before we start building the footer ourselves, let's take a look in the Bootstrap documentation and find the "Sticky Footer" example. A sticky footer just means that it always sticks to the bottom part of the page no matter how much content we have on our page.

If we open the Bootstrap page with the Google Chrome web browser (the best web browser for web development), we can actually look at all the HTML and CSS code straight inside of our browser. Right-click the "Sticky Footer" page and click "View Source." This brings up the HTML for this particular page. So if we look at the example of this "Sticky Footer" page with the goal of applying the same footer to our page, we see that the main content of the page is wrapped in a div with the class container and the footer section is wrapped in a div with the class footer.

This sounds right, so let's apply these changes to app/views/layouts/application.html.erb:

<!DOCTYPE html>
<html>
  <head>
    <title>Splurty</title>
    <%= csrf_meta_tags %>
    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>
  <body>
    <header class="row">
      <div class="col-3">
        <div class="circle">
          <br />
          You know
          <br />
          you need
          <br />
          to code
        </div>
      </div>
      <div class="col-4 slogan">
        Splurting out unsolicited advice about entrepreneurship since 2016
      </div>
      <div class="col-5 links">
        <%= link_to 'Contribute', '#' %>
        <%= link_to 'About', '#' %>
      </div>
    </header>
    <hr />
    <br class="clear" />

    <div class="container">
      <%= yield %>
    </div>

    <div class="footer">
      <div class="container">
        <div class="row">
          <p class="text-muted">Place sticky footer content here.</p>
        </div>
      </div>
    </div>

  </body>
</html> 
 
 
 
 
 
 
 
 
 
Save the file and refresh. Cool, it added the footer, but it's not sticky.

In the source of the HTML document, we see the "Sticky Footer" page linking to this file: sticky-footer.css. This sounds like the file where we can find the CSS styles we need to add to our page.

Looking at the sticky-footer.css file, it seems that the CSS code is split into two sections. One is a "Sticky footer style" section and one is a "Custom page CSS (not required for template or sticky footer method)."

Let's take the top part and put it in a new file inside of app/assets/stylesheets and call it footer.scss.

/* Sticky footer styles
-------------------------------------------------- */
html {
  position: relative;
  min-height: 100%;
}
body {
  /* Margin bottom by footer height */
  margin-bottom: 60px;
}
.footer {
  position: absolute;
  bottom: 0;
  width: 100%;
  /* Set the fixed height of the footer here */
  height: 60px;
  background-color: #f5f5f5;
}
Save the file and refresh.

Awesome! This just stuck our grey footer to the bottom of the page.

That said, if we look at our wireframes, it looks like we don't want the footer to be grey, but white-ish instead. So in the footer.scss, let's remove the line that says background-color: #f5f5f5:

/* Sticky footer styles
-------------------------------------------------- */
html {
  position: relative;
  min-height: 100%;
}
body {
  /* Margin bottom by footer height */
  margin-bottom: 60px;
}
.footer {
  position: absolute;
  bottom: 0;
  width: 100%;
  /* Set the fixed height of the footer here */
  height: 60px;

} 
Save the file and refresh. Cool, the footer just lost the grey color and is now just white.

Now, let's put two sections in the footer and put them side by side. We can arrange them by using the grid system that comes with Bootstrap.

One section will contain, "This isn't enough, I need another" and the other will have the little blurb about how we made our web application. So adjust app/views/layouts/application.html.erb to look like this:

<div class="footer">
  <div class="container">
    <div class="row">
      <div class="col-6">
        This isn't enough, I need more
      </div>
      <div class="col-6">
        Proudly hacked in Boston, MA by <a href="http://thefirehoseproject.com">Marco & Ken</a><br />
        Want to build your own Splurty Web App - <a href="http://thefirehoseproject.com">Learn how to code here</a>
      </div>
    </div>
  </div>
</div> 
 
 
 
 
 
 
Obviously, replace "Proudly hacked in Boston, MA by Marco & Ken" to something that applies to you :)

This sets up two sections in our footer. One is the link to see another quote, and the other is a little blurb about us.

Save the file and refresh.

Since we just used the Bootstrap grid system, let's take a step back and actually understand what's going on.

A quick intro to the Bootstrap Grid System
The Bootstrap grid system is an easy way to tell our web application how things should be laid out from left to right. In addition, we can also use the grid system to specify how wide the different HTML components should be.

We're using Bootstrap 4, which was built for a mobile-first web design approach. In other words, the first thing we want to think about is, "how do we want our application to look on a smartphone?"

The number of cols can be imagined as columns that set the width for a section or a particular HTML element. We have 12 columns from left to right.

In our example above, we use col-6, which uses 6/12ths, or half, of the screen.

The other thing you'll notice is that we have "col" and a number but if you look at the Bootstrap Grid Options in its documentation, you'll notice other letters (col-sm-*, col-md-*, col-lg-*, col-xl-*). Those extra two letters specify the width of the actual device's screen. In this case, the absense of these letters means the column size will be set for every view width.

You can think of examples in which we would want to put HTML sections side-by-side if we have enough space on the screen. However, if there isn't enough space available on the screen, we're much better off stacking the sections on top of each other. By ommiting the letters, we can specify how it should look on extra small screens first, which is exactly the point of the "mobile-first" approach.

When we are using Bootstrap we always want to specify how everything should be laid out in mobile. Then, in the next step, we can think about how it will look on larger screens.

We'll build a more fine-grained grid system with Bootstrap in Lesson 15, when we build the "About" page. For now, let's take 5 minutes and look at the official Bootstrap documentation. Remember, this documentation is written for developers, so it might be a bit confusing, but it's never too early to look at the real documentation and get familiar with it.

Activating and Styling the "More Quotes" Link
One thing that's still not working inside of our footer is the, "This isn't enough, I need more" link. First, let's actually make that sentence a link. Since we don't know where this link will go, we can use a hashtag as a placeholder until we figure it out, like so:

<div class="footer">
  <div class="container">
    <div class="row">
      <div class="col-6">
        <%= link_to "This isn't enough, I need more", "#" %>
      </div>
      <div class="col-6">
        Proudly hacked in Boston MA by <a href="http://thefirehoseproject.com">Marco & Ken</a><br />
        Want to build your own Splurty Web App - <a href="http://thefirehoseproject.com">Learn how to code here</a>
      </div>
    </div>
  </div>
</div> 
Save and refresh.

Ok, now it's a link, but it doesn't look any good. Let's make it look better by adding another CSS class.

<div class="footer">
  <div class="container">
    <div class="row">
      <div class="col-6">
        <%= link_to "This isn't enough, I need more", "#", class: 'next-quote' %>
      </div>
      <div class="col-6">
        Proudly hacked in Boston MA by <a href="http://thefirehoseproject.com">Marco & Ken</a><br />
        Want to build your own Splurty Web App - <a href="http://thefirehoseproject.com">Learn how to code here</a>
      </div>
    </div>
  </div>
</div> 
To start with, let's make our next-quote link red.

Go to colorpicker.com and find a good looking red color like this one: #f84342. Open up app/assets/stylesheets/master.scss and add your new color:

.next-quote {
  color:#f84342;
}
Save the file and refresh. Nice, now our link is red.

Next, I want to set the font-family, or the font that we use for the "next quote" link, to one of our custom fonts. My custom font is called nobilemedium_italic, so that's what I'll set it to. Go ahead and use any custom font that you have.

.next-quote {
  color:#f84342;
  font-family: 'nobilemedium_italic', sans-serif;
} 
Save and refresh. Ok, nice.

This link is getting there. Now let's make it a bit bigger by adjusting the font-size:

.next-quote {
  color:#f84342;
  font-family: 'nobilemedium_italic', sans-serif;
  font-size:20px;
} 
Save the file and refresh. That looks awesome!

Cool, now let's dive into the blurb on the right and adjust the fonts. The first thing we'll need to do is add a class to this section inside the div so we can apply CSS styles to it. To do this, we'll need to open up app/views/layouts/application.html.erb and add the following class:

<div class="footer">
  <div class="container">
    <div class="row">
      <div class="col-6">
        <%= link_to "This isn't enough, I need more", "#", class: 'next-quote' %>
      </div>
      <div class="col-6 footer-blurb">
        Proudly hacked in Boston MA by <a href="http://thefirehoseproject.com">Marco & Ken</a><br />
        Want to build your own Splurty Web App - <a href="http://thefirehoseproject.com">Learn how to code here</a>
      </div>
    </div>
  </div>
</div> 
Now we need to set it to the right font in our CSS. If we look back to our master.scss, we can see that we've set the slogan to the font stack from CSS-Tricks*:

.slogan {
  font-family: "Palatino Linotype", Palatino, Palladio, "URW Palladio L", "Book Antiqua", Baskerville, "Bookman Old Style", "Bitstream Charter", "Nimbus Roman No9 L", Garamond, "Apple Garamond", "ITC Garamond Narrow", "New Century Schoolbook", "Century Schoolbook", "Century Schoolbook L", Georgia, serif;
  font-style: italic;
  padding-top: 26px;
}
So I'm going to use the font-family and the font-style inside a new selector. Open up app/assets/stylesheets/master.scss and add this to the bottom:

.footer-blurb {
  font-family: "Palatino Linotype", Palatino, Palladio, "URW Palladio L", "Book Antiqua", Baskerville, "Bookman Old Style", "Bitstream Charter", "Nimbus Roman No9 L", Garamond, "Apple Garamond", "ITC Garamond Narrow", "New Century Schoolbook", "Century Schoolbook", "Century Schoolbook L", Georgia, serif;
  font-style: italic;
}
Save the file and refresh. Nice, now we're using a much better font.

Now make the text in the footer right-aligned. We'll do that in the CSS:

.footer-blurb {
  font-family: "Palatino Linotype", Palatino, Palladio, "URW Palladio L", "Book Antiqua", Baskerville, "Bookman Old Style", "Bitstream Charter", "Nimbus Roman No9 L", Garamond, "Apple Garamond", "ITC Garamond Narrow", "New Century Schoolbook", "Century Schoolbook", "Century Schoolbook L", Georgia, serif;
  font-style: italic;
  text-align: right;
} 
And finally, let's make the footer blurb a bit smaller:

.footer-blurb {
  font-family: "Palatino Linotype", Palatino, Palladio, "URW Palladio L", "Book Antiqua", Baskerville, "Bookman Old Style", "Bitstream Charter", "Nimbus Roman No9 L", Garamond, "Apple Garamond", "ITC Garamond Narrow", "New Century Schoolbook", "Century Schoolbook", "Century Schoolbook L", Georgia, serif;
  font-style: italic;
  text-align: right;
  font-size: 10px;
} 
Save the file and refresh.

Wow, looking awesome. High five - our footer looks great and our whole page is looking a lot better too.


Git commit
Go through the standard git commit workflow.


Lesson 12: Building a Form to Save New Quotes
In the previous lessons, we've built a web application to show quotes from our database on the main page. We ultimately want our application to be user submitted quotes. In this lesson, we will add a form that will allow the user to enter quotes that will eventually be stored in the database.

However, form submission won't work properly in this lesson. In the next lesson, we will make the form submission actually work.



Right now, the only way we can get new quotes into our web application is the hacker way: going into the rails console and adding quotes directly into our database table. That's not quite the user experience we were hoping for.

If we take a quick look back at our wireframes, we see that we want to have a form letting users submit their own quotes.

Adding a Quote

One of the first things we notice is that our quote form should be inside a pop-up modal box when somebody clicks the "Contribute" link.

However, doing both steps at once— building the form feature, and adding it inside a modal— will end in confusion. So let's do what every smart web developer does when faced with a new feature that requires multiple things to happen at once: break the features into individual coding steps and execute one step after the other.

This means we should first focus on building our quote form feature, and once we have that working, move on to the modal feature.

Creating a page for our form to live
First, we want to create a form where a user can enter and save a new quote so the new quote can be shown in our application.

Before anything else, we need to create the URL for this new form and the page where it will live.

In the terminal window, run the following command to see a rather confusing map of how our web application connects requests made by web browsers to the code in our application.

$ rake routes
It looks like we only have one URL route currently set up: quotes#index.

Let's change that and add more URLs to our web application by opening config/routes.rb and adding one line of code that allows us to get additional URLs pointing to our quote form. Add the following line:

Rails.application.routes.draw do
  root 'quotes#index'
  resources :quotes
end 
Save this file, and in the terminal run the following command again:

$ rake routes
Now we can see how we just received a few additional lines inside of our URL map for our application. Adding the resources :quotes line of code gave us a standard set of URLs to Create, Read, Update and Destroy (aka CRUD) for our quotes. For now, let's not worry about this too much, since it will make a lot more sense down the line.

After setting up the URLs, we need to go back into our controller and add a so-called action that makes our quotes form work. The first action we're adding is a "new" action that basically reserves a column in our database table (like an Excel sheet) for a new quote.

To do this, open app/controllers/quotes_controller.rb and adjust the file to look like this:

class QuotesController < ApplicationController
  def index
    @quote = Quote.order("RANDOM()").first
  end

  def new
  end
end 
 
Now that we have the new action inside our quotes controller, we need to build the actual page that shows our form.

Create a new file called new.html.erb in app/views/quotes/new.html.erb and add the following line of code to it:

<h1>Enter Your Quote Details</h1>
Awesome. Now save the file and navigate to http://localhost:3030/quotes/new.

Cool, our new quotes form page actually shows up.

Creating the form with the SimpleForm Gem
Building forms on a web application is more of a hassle than you might expect. While it may seem simple to add a form field to the page, when you do that, you need to think about things like: input boxes, labels for the boxes, presenting error messages to users if there are validation errors, and a number of different specific components of the form.

Since we're running on high speed and want to ship our web application as fast as possible, let's use another gem to save us from writing a lot of repetitive code from scratch.
We're going to use the simple_form gem to deal with our form. Do a Google search for simple form and find the SimpleForm page.
If we scroll down to the install docs, we can follow the Installation section.

First, open up your Gemfile and add the following line, right under where we added the bootstrap gem.

gem 'simple_form'
Save this file. Go into the terminal and run:

$ bundle install
Remember that whenever we do bundle install, we have to restart our server, so let's do that.

Following the documentation, we run the simple form install command in the terminal:

rails generate simple_form:install --bootstrap
We see it generated a file in config/initializers. Whenever we make changes in our config folder, we want to make sure to restart our server, so let's do that.

Adding the actual form to the page
Ok, let's try to add our form to the page now.

The first step is to adjust our controller so simple form knows what to make the form for - in our case, a new quote.

Adjust app/controllers/quotes_controller.rb to look like this:

class QuotesController < ApplicationController
  def index
    @quote = Quote.order("RANDOM()").first
  end

  def new
    @quote = Quote.new
  end
end 
Save the file.

Now we can build out the actual form inside of app/views/quotes/new.html.erb. In the simple form documentation, we can see a few code examples of how to build a form using simple form. In essence, we're saying for our @quote variable (that reserved a Quotes.new space in our database table), do a few things (we call it |f|) like show an "input" field for the database table column called "saying."

Here's how we write this logic in code:

<h1>Enter Your Quote Details</h1>
<%= simple_form_for @quote do |f| %>
  <%= f.input :saying %>
<% end %> 
 
 
Ok, looking back to our wireframes it looks like we want to have an input field for author as well. Let's add that so our file looks like this:

<h1>Enter Your Quote Details</h1>
<%= simple_form_for @quote do |f| %>
  <%= f.input :saying %>
  <%= f.input :author %>
<% end %> 
Cool, those new fields just popped up on the page.

Now let's add a submit button so a user can actually submit the form:

<h1>Enter Your Quote Details</h1>
<%= simple_form_for @quote do |f| %>
  <%= f.input :saying %>
  <%= f.input :author %>
  <%= f.submit 'Create' %>
<% end %> 

Using styles to make the form look good
Let's put our web designer hats on and do some styling. First thing we can prettify is our create button by using some Bootstrap styles.

Take a look at the Bootstrap 4 button CSS styles here.

<h1>Enter Your Quote Details</h1>
<%= simple_form_for @quote do |f| %>
  <%= f.input :saying %>
  <%= f.input :author %>
  <%= f.submit 'Create', class: 'btn btn-danger' %>
<% end %> 
Nice, now our button looks better.

We can space our form out a bit by adding a few line breaks in app/views/quotes/new.html.erb.

<h1>Enter Your Quote Details</h1>
<%= simple_form_for @quote do |f| %>
  <%= f.input :saying %>
  <%= f.input :author %>
  <br />
  <%= f.submit 'Create', class: 'btn btn-danger' %>
<% end %> 
Awesome, this form looks really good.

Pointing the Contribute Link to the Quotes Form
Until we have our form inside of our modal, we should point the "Contribute" link inside of our header to our new form page.

Whenever we want to find out how to link to a page in our application, we can look up the location in the rake routes table. So let's run that command:

$ rake routes
And we see this line, which goes to quotes#new, the new form we just built, which is where we want to link our application.

new_quote GET    /quotes/new(.:format)      quotes#new
This means that if we want to send someone to this page, we can send them to the new_quote_path. (We just add "_path" to the prefix of the first row that matches our Controller#Action.)

Cool, let's adjust that link in app/views/layouts/application.html.erb:

<header class="row">
  <div class="col-3">
    <div class="circle">
      <br />
      You know
      <br />
      you need
      <br />
      to code
    </div>
  </div>
  <div class="col-4 slogan">
    Splurting out unsolicited advice about entrepreneurship since 2016
  </div>
  <div class="col-5 links">
    <%= link_to 'Contribute', new_quote_path %>
    <%= link_to 'About', '#' %>
  </div>
</header> 
Save the file and refresh. The link to contribute should now go to the new form.

Point the Logo to the Homepage
Like we did before, whenever we want to point a link to a specific page, we want to look up the path in our rake routes table.

So let's run rake routes again and see if we can find the path that goes to our homepage.

$ rake routes
Nice, I see this line in there:

root GET    /                          quotes#index
Ok, so let's jump in, find the logo, and make it become a link that goes to the root_path.

Open up app/views/layouts/application.html.erb and adjust it to look like this:

<header class="row">
  <div class="col-3">
    <%= link_to root_path do %>
      <div class="circle">
        <br />
        You know
        <br />
        you need
        <br />
        to code
      </div>
    <% end %>
  </div>
  <div class="col-4 slogan">
    Splurting out unsolicited advice about entrepreneurship since 2016
  </div>
  <div class="col-5 links">
    <%= link_to 'Contribute', new_quote_path %>
    <%= link_to 'About', '#' %>
  </div>
</header> 
 
In this particular case (unlike the other cases we've seen before), we want our link to be the entire logo, which means our link needs to wrap around multiple HTML tags in one go. This basically means we start with link_to, and anything between the do and end is going to become our link.

There is an important difference in this line compared to the other lines of code we've had in our html.erb files, did you notice it?

The first part looks similar to what we've done in the past: <%= link_to root_path do %>, but look at the second part: <% end %>. In the case of the keyword end, we're not allowed to dump it to the screen, so we need it to have <% instead of the usual <%=. This indicates that we're going to run that line of ruby code, but we're not going to spit the value out to the page.

There will be a few more instances where we want to use <% instead of <%=, so pay special attention when you're typing the code. You'll notice there are patterns to when to use each.

Alright, let's save and refresh. We're making progress.

Let's keep coding and make the logo look a bit better
Cool, now our logo is an actual link that gets us back to the homepage. But, whenever we hover over the logo link, we get an underline that doesn't look good.

Let's fix that. First, let's add an HTML class so we can write some CSS styles for it.

<%= link_to root_path, class: 'logo' do %>
  <div class="circle">
    <br />
    You know
    <br />
    you need
    <br />
    to code
  </div>
<% end %> 
Save the file then open up app/assets/stylesheets/master.scss and add this:

.logo:hover {
  text-decoration: none;
}
Save the file and refresh. Nice, now our logo looks perfect.

Setting up the footer link
While we're creating links all over the place, let's fix the footer link as well so it points to the quotes#index too. So again we'll run:

$ rake routes
And again we see this:

root GET    /                          quotes#index
This means we want our footer link to point to the root_path as well. So in the footer of app/views/layouts/application.html.erb, let's change it to look like this:

<div class="footer">
  <div class="container">
    <div class="row">
      <div class="col-6">
        <%= link_to "This isn't enough, I need more", root_path, class: 'next-quote' %>
      </div>
      <div class="col-6 footer-blurb">
        Proudly hacked in Boston MA by <a href="http://thefirehoseproject.com">Marco & Ken</a><br />
        Want to build your own Splurty Web App - <a href="http://thefirehoseproject.com">Learn how to code here</a>
      </div>
    </div>
  </div>
</div> 
Save and refresh.

Awesome - the links that have pages set up are all working. Let's keep going!


Git commit
Go through the standard git commit workflow.

Lesson 13: Making the Create Button Create a New Quote
In the previous lesson, we setup a form to accept details of new quotes that should be added to our application. In this lesson, we will actually save the quote into the database when the form is submitted.



When we take a look at our web application, we see that our quotes form is set up and looking good. Unfortunately, nothing happens when we press the "Create" button.

Put on your web developer hat, zoom out a bit, and ask yourself: What needs to happen when a user clicks the "Create" button?

Hopefully two things happen:

A quote is stored in our database
The user is sent to the page where a random quote is listed (our home or root page)
Storing the quote in the database after clicking the submit button
When a user presses the Create button on the form, the quote should be saved to our database. We can make this happen through a create action inside of our quotes controller.

This create action is responsible for actually storing our quote fields (remember, a quote consists of two pieces of information: a :saying and its :author) inside the row that was reserved for a new quote by the new action.

Let's add some code for our create action in app/controllers/quotes_controller.rb:

class QuotesController < ApplicationController
  def index
    @quote = Quote.order("RANDOM()").first
  end

  def new
    @quote = Quote.new
  end

  def create
  end
end 
 
Again, all the code between the def create and the end will be executed after a user clicks the actual "Create" button.

Let's take a step back and remember how we played hackers and created two new quotes directly in the rails console by running the following:

> Quote.create(saying: 'Work like there is someone working twenty-four hours a day to take it all away from you', author: 'Mark Cuban')
We basically want to add something very similar, but instead of hardcoding the values for saying and author, we need to suck out the values that a user entered into the quotes form. We can do this by adding a few more lines of code:

class QuotesController < ApplicationController
  def index
    @quote = Quote.order("RANDOM()").first
  end

  def new
    @quote = Quote.new
  end

  def create
    Quote.create(quote_params)
  end

  private

  def quote_params
    params.require(:quote).permit(:saying, :author)
  end
end 
 
 
 
 
 
Let's look at our new code line-by-line so we can understand what's happening.

First, the Quote.create part is what sends the saying and author parts to the database so they are saved.

The quote_params part is what actually pulls the values of saying and author from the quotes form. Without the quote_params, we wouldn't know what the user entered into the form, and we'd store empty records in our database. In addition to helping us suck the values out of the form, the params.require(:quote).permit(:saying, :author) also makes sure that our form is secure, and no evil hackers can inject anything else (we only permit ":saying" and ":author") into our database - which is always a good thing.

After we're able to store new quotes securely into our database, we want to move on to step 2 and redirect the user to the page where they can see their new quotes listed: our home or root page.

In other words, the user needs to be sent to the quotes controller and the index action.

To figure out what the actual URL path should be, we jump into the terminal and run this command:

$ rake routes
If you look at the output of that command, you want to see the line that corresponds to the page we need to send the user to. Remember, we're looking for the controller called quotes and the action called index.

In my case, it looks like this:

Prefix Verb   URI Pattern                Controller#Action
  root GET    /                          quotes#index
So if we look at the prefix, it's root, so we want to send the user to the root_path.

Let's jump into our app/controllers/quotes_controller.rb and add this.

class QuotesController < ApplicationController
  def index
    @quote = Quote.order("RANDOM()").first
  end

  def new
    @quote = Quote.new
  end

  def create
    Quote.create(quote_params)
    redirect_to root_path
  end

  private

  def quote_params
    params.require(:quote).permit(:saying, :author)
  end
end 
Nice. Let's save the file and test this out.

Jump back to localhost:3030/quotes/new, fill out the form, and press the "Create" button.

The item that we just saved into our database now shows up on our homepage if we refresh the homepage a couple of times.

Awesome job!

Git commit
Go through the standard git commit workflow.

Lesson 14: Validating User Data
In the previous lessons, we've built a web application to accept user submitted quotes. In this lesson, we will only allow quotes to enter our database if the saying is between 3 and 140 characters, and the author is between 3 and 50 characters long. When users try to enter data that is outside this range, they will see validation errors after the form is submitted.



One important feature we should always include when we develop web applications is something that ensures users only submit valid data into our database when they use any of our form fields.

In other words, we want to avoid a user saving bogus information for saying or author into our database.

Obviously, we can't control everything, but we can at least make sure that a user doesn't submit only an author name without an actual saying, or that the saying isn't 5,000 words long.

Note: You can always grab a cup of coffee and read up on all the details on how to use ActiveRecord Validations.

For now, let's work on adding validations.

Validating that a user enters a saying for the quote
Let's validate that a user doesn't enter a blank saying.

First, we'll add some code to our model to prevent items from being saved in our database with a blank saying. Let's open app/models/quote.rb and make some changes:

class Quote < ApplicationRecord
  validates :saying, presence: true
end 
Save the file.

This line of code will prevent any new quote from being saved without a saying.

While we're adding validations for our saying, let's also make sure the saying is between 3 and 140 characters long. By doing so, we avoid getting a saying pushed into our database that's too short or as long as an entire book.

class Quote < ApplicationRecord
  validates :saying, presence: true, length: { maximum: 140, minimum: 3 }
end 
Let's test it out. Try to submit a quote that consists of only 2 letters, and another quote that has more than 140 characters.

Dealing with Validation Errors on the Create Action
Hmmm, it doesn't seem to have added the quote to our database if we keep refreshing the page, but we just got sent back to our homepage without letting the user know there was an error with the form submission.

Let's take a look at app/controllers/quotes_controller.rb and see what's going on there.

def create
  Quote.create(quote_params)
  redirect_to root_path
end
It looks like the controller is trying to create a quote, and then afterwards it redirects the user to the root path.

What we want to tell our web application is:

Before we do anything with the form, check if the user actually entered a saying, and if it's the correct length.

If yes, send the user to the home or root path without any warnings.
Otherwise, send the user back to the home or root path, but show a warning.
We're going to store this error message in something called the flash. The flash is a place where we can put error messages or user notifications that will only exist on the page for a single page view. If we leave the page or do a page refresh, the message disappears, which makes the flash the ideal place to put these kind of error messages.

Let's add this logic with this code:

def create
  @quote = Quote.create(quote_params)
  if @quote.invalid?
    flash[:error] = '<strong>Could not save</strong> the data you entered is invalid.'
  end
  redirect_to root_path
end 
 
 
 
Ok, so this is saying if the quote we tried to create is invalid (doesn't pass validations), put an error message in this flash thingy.

Finally, we need to update our homepage so that if an error does happen, it is actually shown to the user on the homepage.

It turns out Bootstrap has some nice looking alert messages that we can use by adding the class alert alert-danger to our div.

Open up app/views/layouts/application.html.erb and adjust it to look like this:

<div class="container">
  <% if flash[:error].present? %>
    <div class="col-10 offset-1 alert alert-danger">
      <%= flash[:error] %>
    </div>
  <% end %>
  <%= yield %>
</div> 
 
 
 
 
Save the file and try to create a quote that consists of only 2 letters again.

It's very close to what we want. The only thing we need to adjust is the bold HTML we tried to use inside of our "flash error message." It didn't turn into bold text, but instead showed the user the actual HTML code - not good!

Ruby on Rails tries to help us out by preventing HTML from sneaking into our application through user-generated content, unless we specify that HTML is actually safe. So, we need to specify that in this case, since we're the ones who wrote the HTML, we're pretty sure it's safe.

<div class="container">
  <% if flash[:error].present? %>
    <div class="col-10 offset-1 alert alert-danger">
      <%= flash[:error].html_safe %>
    </div>
  <% end %>
  <%= yield %>
</div> 
Save the file, and let's try to create another invalid quote. Cool, that looks perfect.

Adding a validation to the author field
Finally, let's add some validations onto the author field. Hop into app/models/quote.rb and add the following line:
class Quote < ApplicationRecord
  validates :saying, presence: true, length: { maximum: 140, minimum: 3 }
  validates :author, presence: true, length: { maximum: 50, minimum: 3 }
end 
Save the file, and now trigger a validation error on the author field. Cool, now our database is guarded against users who put bad data into it!

High five!


Git commit
Go through the standard git commit workflow.

Lesson 15: Building the About Page
In this lesson, we will build the about page, which will be a static page that will tell our users details about what the application is and who built it.



Now that users can submit a quote via our form and it's actually displayed on our homepage, we should take a step back and see what other core functionality we have to build.

If we go back to our wireframes, we notice that we still have to build out our "about" page.

About Page

Before we start building our about page, we should take a quick look into our routes file to see if we actually have a URL that points to our about page. Run the following in the terminal to see your routes table:

$ rake routes
Hmmm, it looks like there's no URL set up for the about page yet. If we think about it, it makes sense why that's the case. Everything we've done up to this point was related to listing, saving, and creating quotes in our database, and had nothing to do with additional pages in our web application. Extra pages in web applications aren't set up through the resources :quotes code that gave us the URL for our quotes form. Instead, custom extra pages are always set up one-by-one manually inside of config/routes.rb:

Rails.application.routes.draw do
  root 'quotes#index'
  resources :quotes
  get 'about', to: 'quotes#about'
end 
We're basically saying, get the about URL and point it to our about action inside our quotes controller.

Now, save the routes.rb file, and let's run rake routes again:

$ rake routes
Nice, now I see this line hooked up:

about GET    /about(.:format)           quotes#about
Now that we have the URL hooked up, let's add a spot for the "about action" in our controller:

class QuotesController < ApplicationController
  def index
    @quote = Quote.order("RANDOM()").first
  end

  def new
    @quote = Quote.new
  end

  def create
    @quote = Quote.create(quote_params)
    if @quote.invalid?
      flash[:error] = '<strong>Could not save</strong> the data you entered is invalid.'
    end
    redirect_to root_path
  end

  def about
  end

  private

  def quote_params
    params.require(:quote).permit(:saying, :author)
  end
end 
 
Save this file.

Let's add a file at app/views/quotes/about.html.erb that looks like this:

<div class="col-10 offset-1">
  <h1>About Splurty</h1>
</div>
Save the file.

Now if you go to localhost:3030/about, you can see our about page. Awesome!

After we have the about page set up, we should make sure a user can actually navigate to it by changing the "About" link in our top navigation so it points to the about page.

As usual, anytime we need to create a new link, we pull up our routes table:

$ rake routes
And we see this:

about GET    /about(.:format)           quotes#about
So we're going to call this page about_path. Open up app/views/layouts/application.html.erb and make the link to the about page work:

<header class="row">
  <div class="col-3">
    <%= link_to root_path, class: 'logo' do %>
      <div class="circle">
        <br />
        You know
        <br />
        you need
        <br />
        to code
      </div>
    <% end %>
  </div>
  <div class="col-4 slogan">
    Splurting out unsolicited advice about entrepreneurship since 2016
  </div>
  <div class="col-5 links">
    <%= link_to 'Contribute', new_quote_path %>
    <%= link_to 'About', about_path %>
  </div>
</header> 
Save the file and refresh. Nice, now the about link in the top navigation goes to the right place.

Adding the team copy
Everything is working. It's time to add some good copy about our Splurty app and the team that built it. We're going to add the following HTML describing us. Make sure you adjust your copy so it's all about you in app/views/quotes/about.html.erb:

<div class="col-10 offset-1">
  <h1>About Splurty</h1>

  <p>
    Splurty was built by <a target="_blank" href="http://github.com/MarcoMorawec">Marco</a> & <a target="_blank" href="http://github.com/KenMazaika">Ken</a>. Two web developers who are on a mission to give people the technical skills needed to launch their own MVPs and turn ideas into reality.
  </p>
  <br />
  <p>
    Together they taught hundreds of students how to code and build products people want at places like Harvard Business School, Carnegie Mellon, Babson, Rhode Island School of Design, Brown University, Punohou High School and ‘Iolani High School.
  </p>
  <p>
    If you want to learn how to code - start <a target="_blank" href="http://www.thefirehoseproject.com/"> here</a>.
  </p>

</div> 
 
 
 
 
 
 
 
 
 
Save the file and refresh. Cool, that added the copy.

Adding some team bios and pictures
Since we (Marco & Ken) are working together as the founding team of Firehose Project, we should add both of our pictures on the about page. (Of course, you don't want to ruin the design of your entire web application by putting our faces on it - instead, you should find your own image.)

First, to get the images saved into our web application, copy the actual image files into the app/assets/images folder. In ours, we copied an image called ken.jpg and an image called marco.jpg into the app/assets/images folder.

After the images are saved inside the web application, we can add a little section for each of us:

<div class="col-10 offset-1">
  <h1>About Splurty</h1>

  <p>
    Splurty was built by <a target="_blank" href="http://github.com/MarcoMorawec">Marco</a> & <a target="_blank" href="http://github.com/KenMazaika">Ken</a>. Two web developers who are on a mission to give people the technical skills needed to launch their own MVPs and turn ideas into reality.
  </p>
  <br />
  <p>
    Together they taught hundreds of students how to code and build products people want at places like Harvard Business School, Carnegie Mellon, Babson, Rhode Island School of Design, Brown University, Punohou High School and ‘Iolani High School.
  </p>
  <p>
    If you want to learn how to code - start <a target="_blank" href="http://www.thefirehoseproject.com/"> here</a>.
  </p>


  <div class="row">
    <div class="col-12 col-sm-4">
      <%= image_tag 'marco.jpg', class: 'img-fluid' %>
    </div>

    <div class="col-12 col-sm-7 offset-sm-1">
      <h2 class="text-center">Marco Morawec</h2>
      <br />
      <p>
        Marco Morawec is a web developer and user experience product manager. He consulted Fortune 500 companies like P&G and John Deere, won Boston's biggest Hackathon (<a target="_blank" href="http://www.angelhack.com/">Angelhack</a>) and most recently led the user experience for <a target="_blank" href="https://www.peertransfer.com/">peerTransfer</a>, building a $500M/year international tuition payment platform. In an earlier life, he travelled around the world on <a target="_blank" href="http://25dollartravel.com">$25/day</a> for an entire year.
      </p>
    </div>
  </div>
  <br class="clear" />

  <div class="row">
    <div class="col-12 col-sm-4" style="padding-top:30px;">
      <%= image_tag 'ken.jpg', class: 'img-fluid' %>
    </div>
    <div class="col-12 col-sm-7 offset-sm-1">
      <h2 class="text-center">Ken Mazaika</h2>
      <br />
      <p>
        Ken Mazaika is a web developer and Ruby on Rails contributor. Previously he was a tech lead at Where.com (<a target="_blank" href="http://bostinno.streetwise.co/2011/04/13/nearbuys-where-rolls-out-daily-deals/">acquired by PayPal</a>) and a member of the PayPal/eBay development team in Boston. In a previous life he turned a <a target="_blank" href="http://yourfreequotes.com/">health insurance quotes generator</a> from a $400/day web application into a $40,000/day business.
      </p>
    </div>
  </div>

</div> 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
Make sure to adjust your image_tag to point to the name of your own image that you saved in your app/assets/images folder. (You could name your image "marco.jpg," but naming it your own name probably makes more sense.)

Save the file and refresh. It looks good, but the footer is a little broken. We can deal with that shortly.

Quick Recap of the Bootstrap Grid System
We talked briefly in Lesson 11 about how the Bootstrap grid system works. If you remember what you learned in Lesson 11, we said that mobile first means we always want to focus first on how the page would look on a mobile phone screen with a small amount of screen space.

Above, you typed <div class="col-12 col-sm-4">, which says we want the element to take up 12/12ths, or the full width, if there isn't a lot of screen space. However, we added col-sm-4, which gives us another option for a different screen size. Our col-sm-4 code specifies that we should take up 4/12ths, or about a third of the page, if we have more space available than on a typical smartphone (e.g. iPads).

Since we're following the mobile-first design approach, we first design for the smallest screen by defining the smallest case with col-* (no extra letters). In the next step, we define the next screen with sm. This sm definition will take over as soon as the size of the browser window is big enough.

To test this out, we can take our about page and adjust the width of the browser window. Make it super thin, and then make it extra wide. For you, it should look something like this on a thin size and something like this on a larger size. Notice how the images are stacked on top of the biographies on a small-sized screen, but on a larger one, they're side-by-side.

The different sizes available to us in increasing screen size are col-*, col-sm-*, col-md-*, col-lg-*, and col-xl-*. You can see the full details in the Bootstrap Grid System documentation here.

Let's keep coding and put the finishing touches on our About Page
It looks like the footer is creeping over our image. Adding a few brs (or breaklines) to the bottom should fix this:

<div class="col-10 offset-1">
  <h1>About Splurty</h1>

  <p>
    Splurty was built by <a target="_blank" href="http://github.com/MarcoMorawec">Marco</a> & <a target="_blank" href="http://github.com/KenMazaika">Ken</a>. Two web developers who are on a mission to give people the technical skills needed to launch their own MVPs and turn ideas into reality.
  </p>
  <br />
  <p>
    Together they taught hundreds of students how to code and build products people want at places like Harvard Business School, Carnegie Mellon, Babson, Rhode Island School of Design, Brown University, Punohou High School and ‘Iolani High School.
  </p>
  <p>
    If you want to learn how to code - start <a target="_blank" href="http://www.thefirehoseproject.com/"> here</a>.
  </p>


  <div class="row">
    <div class="col-12 col-sm-4">
      <%= image_tag 'marco.jpg', class: 'img-fluid' %>
    </div>

    <div class="col-12 col-sm-7 offset-sm-1">
      <h2 class="text-center">Marco Morawec</h2>
      <br />
      <p>
        Marco Morawec is a web developer and user experience product manager. He consulted Fortune 500 companies like P&G and John Deere, won Boston's biggest Hackathon (<a target="_blank" href="http://www.angelhack.com/">Angelhack</a>) and most recently led the user experience for <a target="_blank" href="https://www.peertransfer.com/">peerTransfer</a>, building a $500M/year international tuition payment platform. In an earlier life, he travelled around the world on <a target="_blank" href="http://25dollartravel.com">$25/day</a> for an entire year.
      </p>
    </div>
  </div>
  <br class="clear" />

  <div class="row">
    <div class="col-12 col-sm-4" style="padding-top:30px;">
      <%= image_tag 'ken.jpg', class: 'img-fluid' %>
    </div>
    <div class="col-12 col-sm-7 offset-sm-1">
      <h2 class="text-center">Ken Mazaika</h2>
      <br />
      <p>
        Ken Mazaika is a web developer and Ruby on Rails contributor. Previously he was a tech lead at Where.com (<a target="_blank" href="http://bostinno.streetwise.co/2011/04/13/nearbuys-where-rolls-out-daily-deals/">acquired by PayPal</a>) and a member of the PayPal/eBay development team in Boston. In a previous life he turned a <a target="_blank" href="http://yourfreequotes.com/">health insurance quotes generator</a> from a $400/day web application into a $40,000/day business.
      </p>
    </div>
  </div>

</div>

<br class="clear" />
<br />
<br />
<br />
<br /> 
 
 
 
 
Next, we should update the main font on our about page to match the font we used for our slogan. To start with, let's add a class to the main about box:

<div class="col-10 offset-1 about">
  <h1>About Splurty</h1>

  <p>
    Splurty was built by <a target="_blank" href="http://github.com/MarcoMorawec">Marco</a> & <a target="_blank" href="http://github.com/KenMazaika">Ken</a>. Two web developers who are on a mission to give people the technical skills needed to launch their own MVPs and turn ideas into reality.
  </p>
  <br />
  <p>
    Together they taught hundreds of students how to code and build products people want at places like Harvard Business School, Carnegie Mellon, Babson, Rhode Island School of Design, Brown University, Punohou High School and ‘Iolani High School.
  </p>
  <p>
    If you want to learn how to code - start <a target="_blank" href="http://www.thefirehoseproject.com/"> here</a>.
  </p>


  <div class="row">
    <div class="col-12 col-sm-4">
      <%= image_tag 'marco.jpg', class: 'img-fluid' %>
    </div>

    <div class="col-12 col-sm-7 offset-sm-1">
      <h2 class="text-center">Marco Morawec</h2>
      <br />
      <p>
        Marco Morawec is a web developer and user experience product manager. He consulted Fortune 500 companies like P&G and John Deere, won Boston's biggest Hackathon (<a target="_blank" href="http://www.angelhack.com/">Angelhack</a>) and most recently led the user experience for <a target="_blank" href="https://www.peertransfer.com/">peerTransfer</a>, building a $500M/year international tuition payment platform. In an earlier life, he travelled around the world on <a target="_blank" href="http://25dollartravel.com">$25/day</a> for an entire year.
      </p>
    </div>
  </div>
  <br class="clear" />

  <div class="row">
    <div class="col-12 col-sm-4" style="padding-top:30px;">
      <%= image_tag 'ken.jpg', class: 'img-fluid' %>
    </div>
    <div class="col-12 col-sm-7 offset-sm-1">
      <h2 class="text-center">Ken Mazaika</h2>
      <br />
      <p>
        Ken Mazaika is a web developer and Ruby on Rails contributor. Previously he was a tech lead at Where.com (<a target="_blank" href="http://bostinno.streetwise.co/2011/04/13/nearbuys-where-rolls-out-daily-deals/">acquired by PayPal</a>) and a member of the PayPal/eBay development team in Boston. In a previous life he turned a <a target="_blank" href="http://yourfreequotes.com/">health insurance quotes generator</a> from a $400/day web application into a $40,000/day business.
      </p>
    </div>
  </div>

</div>

<br class="clear" />
<br />
<br />
<br />
<br /> 
Save the file, and now let's go into app/assets/stylesheets/master.scss and find this line:

.slogan {
  font-family: "Palatino Linotype", Palatino, Palladio, "URW Palladio L", "Book Antiqua", Baskerville, "Bookman Old Style", "Bitstream Charter", "Nimbus Roman No9 L", Garamond, "Apple Garamond", "ITC Garamond Narrow", "New Century Schoolbook", "Century Schoolbook", "Century Schoolbook L", Georgia, serif;
  font-style: italic;
  padding-top: 26px;
}
Let's use the same font-family that we used for our .slogan, and apply it to our .about CSS class.

Add this to the bottom of master.scss:

.about {
  font-family: "Palatino Linotype", Palatino, Palladio, "URW Palladio L", "Book Antiqua", Baskerville, "Bookman Old Style", "Bitstream Charter", "Nimbus Roman No9 L", Garamond, "Apple Garamond", "ITC Garamond Narrow", "New Century Schoolbook", "Century Schoolbook", "Century Schoolbook L", Georgia, serif;
}
Save the file and refresh.

Awesome - now we have a pretty slick-looking about page!


Git commit
Go through the standard git commit workflow.

Lesson 16: Moving the Quotes Form to a Bootstrap Modal
In the previous lessons, we've built a web application that includes the form to enter new quote details on a separate page. In this lesson, we will move the form onto the main page in a pop-up form. Twitter Bootstrap provides us with the design element of a modal, which is a pop-up, which we will use.



Now that we're done with the core functionality of our web application, we can focus on making the user experience a lot better.

From looking at our wireframes, we know that the quotes form should be inside a pop-up, or in this case a Bootstrap modal:

Adding a Quote

Basically, modals are those cool-looking pop-up boxes that dim the rest of the page around them. These modal boxes are baked into Bootstrap. If you look at getbootstrap.com and click on the JavaScript section, you can scroll down to the "Modals" part and see some examples of the modal.

When you come to the part that says "Launch demo modal," you can not only see what we're about to add into our application, but also copy the example HTML code so we can easily paste it into our web application.

Getting a placeholder modal into our web app
We want to be able to pop our modal up on any page inside of our application. If we remember from earlier, the one file that includes code that gets shown on every single page is the app/views/layouts/application.html.erb file. We should paste the modal HTML code into this file like so:

<!DOCTYPE html>
<html>
  <head>
    <title>Splurty</title>
    <%= csrf_meta_tags %>
    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>
  <body>
    <header class="row">
      <div class="col-3">
        <%= link_to root_path, class: 'logo' do %>
          <div class="circle">
            <br />
            You know
            <br />
            you need
            <br />
            to code
          </div>
        <% end %>
      </div>
      <div class="col-4 slogan">
        Splurting out unsolicited advice about entrepreneurship since 2016
      </div>
      <div class="col-5 links">
        <%= link_to 'Contribute', new_quote_path %>
        <%= link_to 'About', about_path %>
      </div>
    </header>

    <!-- Button trigger modal -->
    <button type="button" class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal">
      Launch demo modal
    </button>

    <!-- Modal -->
    <div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">×</span>
            </button>
            <h4 class="modal-title" id="myModalLabel">Modal title</h4>
          </div>
          <div class="modal-body">
            ...
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
            <button type="button" class="btn btn-primary">Save changes</button>
          </div>
        </div>
      </div>
    </div>


    <hr />
    <br class="clear" />

    <div class="container">
      <% if flash[:error].present? %>
        <div class="col-10 offset-1 alert alert-danger">
          <%= flash[:error].html_safe %>
        </div>
      <% end %>
      <%= yield %>
    </div>

    <div class="footer">
      <div class="container">
        <div class="row">
          <div class="col-6">
            <%= link_to "This isn't enough, I need more", root_path, class: 'next-quote' %>
          </div>
          <div class="col-6 footer-blurb">
            Proudly hacked in Boston MA by <a href="http://thefirehoseproject.com">Marco & Ken</a><br />
            Want to build your own Splurty Web App - <a href="http://thefirehoseproject.com">Learn how to code here</a>
          </div>
        </div>
      </div>
    </div>

  </body>
</html> 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
Save the file and refresh. Nice, when we press that big ugly blue button, it pops up a blank modal for us.

Now, let's move the code for the demo button out of the actual modal section and paste it where we actually want to have the button that opens up the modal - in the top navigation bar. Replace the contribute link with the button for the modal:

<!DOCTYPE html>
<html>
  <head>
    <title>Splurty</title>
    <%= csrf_meta_tags %>
    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>
  <body>
    <header class="row">
      <div class="col-3">
        <%= link_to root_path, class: 'logo' do %>
          <div class="circle">
            <br />
            You know
            <br />
            you need
            <br />
            to code
          </div>
        <% end %>
      </div>
      <div class="col-4 slogan">
        Splurting out unsolicited advice about entrepreneurship since 2016
      </div>
      <div class="col-5 links">
        <!-- Button trigger modal -->
        <button type="button" class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal">
          Launch demo modal
        </button>
        <%= link_to 'About', about_path %>
      </div>
    </header>






    <!-- Modal -->
    <div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">×</span>
            </button>
            <h4 class="modal-title" id="myModalLabel">Modal title</h4>
          </div>
          <div class="modal-body">
            ...
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
            <button type="button" class="btn btn-primary">Save changes</button>
          </div>
        </div>
      </div>
    </div>


    <hr />
    <br class="clear" />

    <div class="container">
      <% if flash[:error].present? %>
        <div class="col-10 offset-1 alert alert-danger">
          <%= flash[:error].html_safe %>
        </div>
      <% end %>
      <%= yield %>
    </div>

    <div class="footer">
      <div class="container">
        <div class="row">
          <div class="col-6">
            <%= link_to "This isn't enough, I need more", root_path, class: 'next-quote' %>
          </div>
          <div class="col-6 footer-blurb">
            Proudly hacked in Boston MA by <a href="http://thefirehoseproject.com">Marco & Ken</a><br />
            Want to build your own Splurty Web App - <a href="http://thefirehoseproject.com">Learn how to code here</a>
          </div>
        </div>
      </div>
    </div>

  </body>
</html> 
 
 
 
 
 
 
 
Save the file and refresh. Nice, we just replaced the old "Contribute" link.

Now that we actually have a button in the top navigation to pop up the modal, we want to put on our web designer hats and make the button look like it did before.

We can make the button a link by using our link_to command, as long as we make sure to include those "data" pieces from the HTML code as well.

Let's swap the button code out to look like this:

<div class="col-5 links">
  <!-- Button trigger modal -->
  <%= link_to 'Launch demo modal', '#', data: {toggle: 'modal', target: '#myModal'} %>
  <%= link_to 'About', about_path %>
</div> 
And finally, let's change the text of the link from "Launch demo modal" back to "Contribute."

<div class="col-5 links">
  <!-- Button trigger modal -->
  <%= link_to 'Contribute', '#', data: {toggle: 'modal', target: '#myModal'} %>
  <%= link_to 'About', about_path %>
</div> 
Save the file and refresh.

Cool - press the "Contribute" button and a neat modal pops up.

Putting the quotes form in the modal
Now that we have a demo modal pop up when we press "Contribute," we need to make sure that our form is working inside of the modal.

First, let's get the easy things adjusted. Change the title of the modal from "Modal title" to "Contribute your quote."

<!-- Modal -->
<div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">×</span>
        </button>
        <h4 class="modal-title" id="myModalLabel">Contribute Your Quote</h4>
      </div>
      <div class="modal-body">
        ...
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
    </div>
  </div>
</div> 
Save the file and refresh.

Common Gotcha
Common gotcha
Make sure that the id of the modal and button are the same. If they do not match they won't be connected and will not work properly.

The modal id should be id="myModal":

<div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
The button target should be #myModal:

<%= link_to 'Contribute', '#', data: {toggle: 'modal', target: '#myModal'} %>
Press the "Contribute" button again. Cool, we've got our title updated.

Now we should add our quotes form into the "..." part of the modal code.

If you remember from before, we have the code for our quotes form in app/views/quotes/new.html.erb. Let's take a look at new.html.erb now. Here's the code we see:

<h1>Enter Your Quote Details</h1>
<%= simple_form_for @quote do |f| %>
  <%= f.input :saying %>
  <%= f.input :author %>
  <br />
  <%= f.submit 'Create', class: 'btn btn-danger' %>
<% end %>
To get our form inside of the modal, we basically want to copy all the code from the simple_form_for line down to the end into the modal where it currently says "..."

Let's do that now in app/views/layouts/application.html.erb.

<!-- Modal -->
<div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">×</span>
        </button>
        <h4 class="modal-title" id="myModalLabel">Contribute Your Quote</h4>
      </div>
      <div class="modal-body">
        <%= simple_form_for @quote do |f| %>
          <%= f.input :saying %>
          <%= f.input :author %>
          <br />
          <%= f.submit 'Create', class: 'btn btn-danger' %>
        <% end %>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
    </div>
  </div>
</div> 
 
 
 
 
 
Save the file and refresh your homepage. Make sure you refresh the homepage and test the modal on the homepage only for now, since you might get a strange error message if you test the modal in the about page. (We'll fix the about page modal in a moment.)

Press the "Contribute" button. Hmm, it looks like it's pre-populating the form with the :saying and :author from the existing quote. Why is this happening?

If we zoom a little closer into the code of our form, we wrote a line of code that looks like this: simple_form_for @quote do |f|. This line of code says we want to build a form for our @quote variable.

On our homepage, the @quote variable is currently set to the exact same quote we're displaying on the actual homepage. That's the reason why the form shows the same quote inside the form fields as the one on our home page.

On the about page, the @quote variable isn't set, so that's why we get a strange error message.

To fix this, we need to tell our form: "listen up, this quote is a new quote and not the current one you're already showing on the home page!"

We can do that with code like so:

<!-- Modal -->
<div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">×</span>
        </button>
        <h4 class="modal-title" id="myModalLabel">Contribute Your Quote</h4>
      </div>
      <div class="modal-body">
        <%= simple_form_for Quote.new do |f| %>
          <%= f.input :saying %>
          <%= f.input :author %>
          <br />
          <%= f.submit 'Create', class: 'btn btn-danger' %>
        <% end %>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
    </div>
  </div>
</div> 
Save the file and refresh. Press the "Contribute" button again.

Nice, the modal popped up and this time, it isn't populated since we're building a form for a new Quote.

Next, we should replace the blue "Save changes" button (that actually doesn't work) with a red "Create" button that does work.

For our "Create" button code to work, it needs to be placed between the simple_form_for and the end. This means we need to move the simple_form_for code to start outside of the modal-body, like we're doing below:

<!-- Modal -->
<div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">×</span>
        </button>
        <h4 class="modal-title" id="myModalLabel">Contribute Your Quote</h4>
      </div>
      <%= simple_form_for Quote.new do |f| %>
        <div class="modal-body">
          <%= f.input :saying %>
          <%= f.input :author %>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
          <%= f.submit 'Create', class: 'btn btn-danger' %>
        </div>
      <% end %>
    </div>
  </div>
</div> 
 
 
 
 
 
 
 
 
 
Save the file and preview it again.

Nice, our form is looking good now.

Cleaning up after ourselves
One good habit to get into as a web developer is very similar to regular life: clean up after yourself.

Since we moved our form into our modal, we don't need the actual page where the form was running before anymore.

This means we're not using the def new section in app/controllers/quotes_controller.rb anymore, so let's get rid of those few lines of code:

class QuotesController < ApplicationController
  def index
    @quote = Quote.order("RANDOM()").first
  end





  def create
    @quote = Quote.create(quote_params)
    if @quote.invalid?
      flash[:error] = '<strong>Could not save</strong> the data you entered is invalid.'
    end
    redirect_to root_path
  end

  def about
  end

  private

  def quote_params
    params.require(:quote).permit(:saying, :author)
  end
end 
 
 
We can also delete the actual file that contained our form. Rather than doing it the manual, point-and-click way, we're going to do it the hacker way and run the following in the terminal:

Be careful and make sure to type out the full command before pressing enter.

$ rm app/views/quotes/new.html.erb
Great job! Things are coming together really nicely.


Git commit
Go through the standard git commit workflow.


Notification Bell  User Avatar  

Lesson 17: Applying the Finishing Touches
Our web application is almost complete. In this lesson, we will cover a few small tweaks to the HTML and CSS to make the user interface have an awesome design.



Now that we're almost done with our web application, it's always good to put on our web designer hats again and polish up a few more small details. Doing so will make our user experience a lot better.

Finishing Touches to the Top Nav
We may have a lot of users who will check our web application on their mobile phones. Since our top navigation bar looks a bit crowded on a mobile screen, we should hide our slogan from the user when they view our web app on a mobile device.

Bootstrap provides us with this "hiding" functionality, and we can access it by adding a single CSS class called hidden-xs-down to the column that contains the slogan.

Adjust the rest of the top navigation in app/views/layouts/application.html.erb like so:

<header class="row">
  <div class="col-3">
    <%= link_to root_path, class: 'logo' do %>
      <div class="circle">
        <br />
        You know
        <br />
        you need
        <br />
        to code
      </div>
    <% end %>
  </div>
  <div class="col col-sm-4 hidden-xs-down slogan">
    Splurting out unsolicited advice about entrepreneurship since 2016
  </div>
  <div class="col-10 offset-1 offset-sm-0 col-sm-5 links">
    <!-- Button trigger modal -->
    <%= link_to 'Contribute', '#', data: {toggle: 'modal', target: '#myModal'} %>
    <%= link_to 'About', about_path %>
  </div>
</header> 
 
Next, we should space our "Contribute" and "About" links out a little bit. By default, HTML code assumes that if we put multiple white spaces in a row, we meant to only put a single space there. However, if we do a bit of a trick and hardcode the value with &nbsp; (you can remember this by thinking non-breaking space), we can force extra spaces into our HTML code.

Let's add two more spaces between our links with this method:

<header class="row">
  <div class="col-3">
    <%= link_to root_path, class: 'logo' do %>
      <div class="circle">
        <br />
        You know
        <br />
        you need
        <br />
        to code
      </div>
    <% end %>
  </div>
  <div class="col col-sm-4 hidden-xs-down slogan">
    Splurting out unsolicited advice about entrepreneurship since 2016
  </div>
  <div class="col-10 offset-1 offset-sm-0 col-sm-5 links">
    <!-- Button trigger modal -->
    <%= link_to 'Contribute', '#', data: {toggle: 'modal', target: '#myModal'} %>
    &nbsp;&nbsp;
    <%= link_to 'About', about_path %>
  </div>
</header> 
Save the file and refresh. Nice, the links in the header are a bit more spaced out!

Finishing touches to the footer
Let's jump back into making our web app look good on mobile.

Right now, our footer shows the, "This isn't enough, I need more" link and the, "Proudly hacked..." parts side-by-side. What we should do for our mobile viewers is stack them on top of each other.

Open up app/views/layouts/application.html.erb and adjust it to look like this:

<div class="footer">
  <div class="container">
    <div class="row">
      <div class="col-12 col-sm-6">
        <%= link_to "This isn't enough, I need more", root_path, class: 'next-quote' %>
      </div>
      <div class="col-12 col-sm-6 footer-blurb">
        Proudly hacked in Boston MA by <a href="http://thefirehoseproject.com">Marco & Ken</a><br />
        Want to build your own Splurty Web App - <a href="http://thefirehoseproject.com">Learn how to code here</a>
      </div>
    </div>
  </div>
</div> 
 
Save the file and refresh the page. Then, resize your browser window to be very narrow (aka the hackers quick-and-dirty mobile view) and watch the footer jump around.

If we change our footer-blurb CSS class to align to the left on mobile view only, and stay right-aligned on all other screens, things will probably look a bit better as well.

For this functionality, we need to write a bit of extra code inside our CSS file and create a media query. In short, media queries basically tell the browser to use a certain part of CSS styles only IF the device width is within a certain and specified threshold.

Let's add a media query to the bottom of app/assets/stylesheets/master.scss like so:

@media (max-width: 750px) {
  .footer-blurb {
    text-align: left;
  }
}
Save the file and refresh the page. As you resize the window, you'll see the text alignment change. Awesome!

Modal Quote Form Tweaks
From a user-experience point of view, it's always very helpful when a form includes a few hints or examples of what one should actually type into a certain form field.

Rather than reinventing the wheel for a feature that's very common, why don't we look under the Usage section of our simple_form documentation and see if we can specify our form label and maybe add some placeholder text inside the actual form fields.

Let's start by changing our form label to be a bit more descriptive. Open up app/views/layouts/application.html.erb and adjust it to look like this:

<!-- Modal -->
<div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">×</span>
        </button>
        <h4 class="modal-title" id="myModalLabel">Contribute Your Quote</h4>
      </div>
      <%= simple_form_for Quote.new do |f| %>
        <div class="modal-body">
          <%= f.input :saying, label: "What is the saying you want to add?" %>
          <%= f.input :author %>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
          <%= f.submit 'Create', class: 'btn btn-danger' %>
        </div>
      <% end %>
    </div>
  </div>
</div> 
Save the file and refresh. Cool, when we pop up the form, it looks like the label was updated for the saying.

Since this worked, let's adjust the label for the author too:

<!-- Modal -->
<div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">×</span>
        </button>
        <h4 class="modal-title" id="myModalLabel">Contribute Your Quote</h4>
      </div>
      <%= simple_form_for Quote.new do |f| %>
        <div class="modal-body">
          <%= f.input :saying, label: "What is the saying you want to add?" %>
          <%= f.input :author, label: "Who is the author of the quote?" %>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
          <%= f.submit 'Create', class: 'btn btn-danger' %>
        </div>
      <% end %>
    </div>
  </div>
</div> 
It looks like we can specify the placeholder text - a hint for our users about what should be typed into the form field - for each form field as well. Let's add placeholders for both form fields now:

<!-- Modal -->
<div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">×</span>
        </button>
        <h4 class="modal-title" id="myModalLabel">Contribute Your Quote</h4>
      </div>
      <%= simple_form_for Quote.new do |f| %>
        <div class="modal-body">
          <%= f.input :saying, label: "What is the saying you want to add?", placeholder: "Fear is the disease. Hustle is the antidote." %>
          <%= f.input :author, label: "Who is the author of the quote?", placeholder: "Travis Kalanick" %>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
          <%= f.submit 'Create', class: 'btn btn-danger' %>
        </div>
      <% end %>
    </div>
  </div>
</div> 
 
Save the file and refresh. Nice, our form now has two nice hints for users inside of the actual form fields. When you click inside one of the form fields and start typing, the placeholder text will disappear and make space for the user to type out actual content.

Next, let's add some space between the form fields with a few brs or breaklines.

<!-- Modal -->
<div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">×</span>
        </button>
        <h4 class="modal-title" id="myModalLabel">Contribute Your Quote</h4>
      </div>
      <%= simple_form_for Quote.new do |f| %>
        <div class="modal-body">
          <%= f.input :saying, label: "What is the saying you want to add?", placeholder: "Fear is the disease. Hustle is the antidote." %>
          <br />
          <%= f.input :author, label: "Who is the author of the quote?", placeholder: "Travis Kalanick" %>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
          <%= f.submit 'Create', class: 'btn btn-danger' %>
        </div>
      <% end %>
    </div>
  </div>
</div> 
Since we already have some pretty good looking fonts, we should make our modal consistent and use the same fonts we've used throughout our web application.

Open up app/assets/stylesheets/master.scss and add the following line to adjust the font inside the modal:

.modal {
  font-family: "Palatino Linotype", Palatino, Palladio, "URW Palladio L", "Book Antiqua", Baskerville, "Bookman Old Style", "Bitstream Charter", "Nimbus Roman No9 L", Garamond, "Apple Garamond", "ITC Garamond Narrow", "New Century Schoolbook", "Century Schoolbook", "Century Schoolbook L", Georgia, serif;
}
Finishing touches to the homepage
If we take a step back and look at our wireframes of the homepage again, we can see that we should have "SPLURTY / No. 1" along with the catchphrase above the quote that is currently shown.

Here's a quick view of the homepage to visualize what we want to have:

Splurty Homepage

Open up app/views/quotes/index.html.erb and add this line:

<h2>
  <span>SPLURTY / No. <%= @quote.id %></span>
  Here's the <u>best unsolicited startup advice</u> you can get!
</h2>

<h1><%= @quote.saying %></h1>
<h2>- <%= @quote.author %></h2> 
 
 
 
Save the file and refresh. Cool, now we have the tag line.

While we're at it, we should also change the "SPLURTY / No. ..." part to be a bolder font and grey color.

If we go to colorpicker.com, we can find the "hex code" for a nice grey color. The color I found is #dddddd.

Cool, let's open up app/assets/stylesheets/master.scss and adjust that:

h2 span {
  color: #dddddd;
}
Save the file and refresh. Nice, now that part shows in a grey color.

Next, we can copy the font-family from our h1 and paste it into our h2 span section. If we look at the h1 CSS code in our master.scss file, we see this:

h1 {
  font-family: 'nobileregular', sans-serif;
  font-weight:bold;
  font-size:48px;
}
Copy the line that looks like font-family: 'nobileregular', sans-serif; and add it into app/assets/stylesheets/master.scss like so:

h2 span {
  color: #dddddd;
  font-family: 'nobileregular', sans-serif;
}
Another thing we notice is that our page seems a bit too small and the footer overlaps with our page. Let's fix that by adding a few breaklines to app/views/quotes/index.html.erb.

<h2>
  <span>SPLURTY / No. <%= @quote.id %></span>
  Here's the <u>best unsolicited startup advice</u> you can get!
</h2>

<h1><%= @quote.saying %></h1>
<h2>- <%= @quote.author %></h2>

<br class="clear" />
<br />
<br />
<br /> 
 
 
 
Since we always want to stay as close to our wireframes as possible, let's pull the actual author name to the right-hand side of our homepage by using the Bootstrap float-right class:

<h2>
  <span>SPLURTY / No. <%= @quote.id %></span>
  Here's the <u>best unsolicited startup advice</u> you can get!
</h2>

<h1><%= @quote.saying %></h1>
<h2 class="float-right">- <%= @quote.author %></h2>

<br class="clear" />
<br />
<br />
<br /> 
The very last thing...
Warning: We're entering the super nitpicky web designer area, but wouldn't it be so cool if anytime a user selects text on our page, the selection background turns red instead of their default color? If we make it the same red color as the, "This isn't enough, I need more" link (#f84342), we even stay consistent in our color choices.

Let's add this last line to app/assets/stylesheets/master.scss:

::selection {
  background-color: #f84342;
}

Holy smokes! Your web app looks absolutely awesome! Let's ship it live!

Git commit
Go through the standard git commit workflow.

Lesson 18: Deploying our Web App Live
We've finished building our application, but we can only access our latest changes on our personal computer. In this lesson, we will update heroku and send all the code changes we've done in the previous lessons to our servers. This will update the URL we can share with friends to interact with the application.



Before our friends can tell us how awesome our new web app is, we need to ship all the awesome changes that we made in the last few steps live to the internet. Developers call this step "deploying" our code, which means moving it from our machine up to our server on Heroku.

In other words, right now all of our code lives on our localhost, or our development environment, so let's push it live to the internet.

$ git push heroku master
It takes a few minutes to complete.

Sometimes things don't go smoothly when we push our code live on the internet— know that that's the plight of any web developer out there. If you're running into problems now (or in the future), take a look over our Heroku Troubleshooting Guide for tips on how to fix problems with your web application on Heroku.

Common Gotcha
Common gotchas
Sometimes we create migrations on our machines and forget to run them on Heroku (Production). Remember, we need to run migrations on Production (Heroku) and Development (localhost) separately, each time we create a new migration file.

Make sure you run any pending migrations and restart Heroku after running migrations:

$ heroku run rake db:migrate
$ heroku restart

Lesson 19: Getting User Feedback and Next Steps
Congrats on building your first web application! In this lesson, we'll celebrate the work you've done and you will submit your app for a review from Firehose HQ, before moving on to additional coding lessons.



Awesome - you just built and shipped an awesome web application!
This is how I feel!
Riker Clap

Now, let's focus on what you should do next
First: Getting Real User Feedback
User feedback is a web developer's best friend! It helps us to determine which features we should improve and what to focus on next. Every time we listen to our users, we make more people happy and they continue using our web application - and that's a good thing.

Plus, you'll really want to see what kind of awesome quotes your friends put into your application.

Go ahead and share the URL to your web application on Facebook and Twitter, and also email it out to your friends.

Here are a few examples to get you started with collecting valuable user feedback:

Facebook: I just built and launched my Splurty App! Add a quote and let me know how I can make my web application better: http://"YOUR URL".herokuapp.com

Twitter: I just launched my Splurty App, an advice-splurting web application with @FirehoseProject http://"YOUR URL".herokuapp.com

Email: Hey Friends, I just built and launched my Splurty App, an advice-splurting web application. Let me know how I can improve my app and add your own quote here: http://"YOUR URL".herokuapp.com

Second: Continue Coding
Let's keep coding, and build our next web application, together.


Congrats on submitting your Splurty application. Right now, you probably feel like you can follow along with instructions, but might not be able to build the app from scratch without them. 

If you haven't already, watch these Web Application Overview videos, which will describe how your splurty app works. After that, checkout the Assignments to start expanding on your programming abilities. The Nomster app is your next application to start building when you are ready!
