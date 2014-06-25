# Intro to Sinatra

## Sinatra is a light weight web server that runs on Ruby. 

### First Sinatra app without html pages. Displays text directly.
### Setup:

* Install Sinatra gem

		$ gem install sinatra
		

* Create a directory for todays's work

		$ mkdir first_sinatra_app
		$ cd first_sinatra_app
		
		$ touch first_app.rb
		$ mine .

		
### Let's ceate the first route: '/' - the 'root' route

* Edit 'first_app.rb' as follows:

		require 'sinatra'
		
		get '/' do           # '/' is the route - the "root" route
		  "Hello, World!"
		end
		  
* Go to the command line and run the app: 

		$ ruby first_app.rb
		
* Go to the browser to view the running app:

		localhost:4567
		
### Let's revise 'first_app.rb' to use html tags

* Edit 'first_app.rb' as follows:

		require 'sinatra'
		
		get '/' do
		  "<h1>Hello, World!</h1>" +
		  "<h3>This is my first app</h3>"
		end
* Stop server: 

		control-C  # in the server window
* Start server:  

		$ ruby first_app.rb


### Let's add a second route: '/greeting'

* Modify the root route ('/') to add an anchor tag:

		get '/' do
		  "<h1>Hello, World!</h1>" +
		  "<h3>This is my first app</h3>" +
		  "<a href='/greeting'>Go to greeting page</a>"    # '/greeting' is the new route
		ebd
		
* Add a method for the '/greeting' route in 'first_app.rb':

		get '/greeting' do
		  "<h1>This is the greeting page</h1>" +
		  "<a href='/'>Back to root page</a>"
		end

* Stop server: 

		control-C  # in the server window
* Start server:  

		$ ruby first_app.rb

		
### Let's redo this app with actual pages for our views:
* Create a views directory.

* Create an root.erb file in the views directory:

	views/root.erb:
		
		<h1>root.erb</h1>
		<h1>Hello, World!</h1>
		<h3>This is my first app</h3>
		<a href="/greeting">Go to greeting page</a>

* Create a 'greeting.erb' page in the views directory:
		
	views/greeting.erb:
		
		<h1>greeting.erb</h1>
		<h1>This is the greeting page</h1>	
		<a href='/'>Back to root page</a>

* Modify the 'first_app.rb' file as follows:

		require 'sinatra'
		
		get '/' do  
		  erb :root  # renders the root.erb page in the views directory
		end
		
		get '/greeting' do
		  erb :greeting  # renders the greeting.erb page in the views directory
		end

* Stop server: 

		control-C  # in the server window
* Start server:  

		$ ruby first_app.rb
		
### Let's pass a variable to the greeting.erb view page

* Edit 'first_app.rb':

		get '/greeting' do
		  erb :greeting, :locals => { :salutation => "Aloha", :name => "Spencer"}
		end

* Edit 'greeting.erb':

		<h1>greeting.erb</h1>
		<h1><%= salutation %> <%= name %>!</h1>
		<h1>This is the greeting page</h1>	
		<a href='/'>Back to root page</a>
		
		

##@@@@@@@@ Deploy to Heroku @@@@@@@@@@@

### First push to Github
* Go to Github and create a repository. 
* Follow instructions on Github to push your code to the repository.

### Then push to Heroku

* Prepare same directory for Heroku depoyment

		$ heroku create

* Push to Heroku

		$ git push heroku master



###@@@@@@@@ Extra items @@@@@@@@@@@

### It is a pain to stop and start the server every time you make a code change. 
### There is a gem for that! It's called 'sinatra-reloader' ('sinatra-reloader' is a part of the 'sinatra-contrib' gem).

* Install common Sinatra extensions with the 'sinatra-contrib' gem. 'sinatra-reloader' is a part of the sinatra-contrib gem and allows you to refresh the browser to see changes without stopping and restarting the server.

		$ gem install sinatra-contrib
		
		# for inside your app file
		require 'sinatra/reloader'  

### It is common practice to have a layout.rb file in the views directory that provides the html, head and body tags that wraps around the .erb files.

* Create a layout.rb file in the views directory. The '<%= yield %>' line, yields to the
  different '.erb' files that are 

		<html>
			<head>
				<title>first app</title>
			</head>
			<body>
				<h1>First Application</h1>
				
				  <%= yield %>
				  
				</body>
		</html>



		