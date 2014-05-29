---
layout: default
title: Rails Girls App Tutorial - Rails Girls Bucharest, 30 May 2014
extra_css:
  - spacefull
permalink: app-bucharest
---

# Rails Girls App Tutorial

<span class="muted">*Created by Vesa Vänskä, [@vesan](https://twitter.com/vesan)* and improved by many</span>

## Step 1: Create the application

### Before we start

The commands you need to run on a Windows computer are slightly different to Mac or Linux.
Select your operating system using the switcher at the bottom-right:

<div class="os-specific">
  <div class="nix">
    {% highlight text %}
    The tutorial will show the commands for Mac or Linux.
    {% endhighlight %}
  </div>

  <div class="win">
    {% highlight text %}
    The tutorial will show the commands for Windows.
    {% endhighlight %}
  </div>
</div>


### Let's start

We're going to create a new Rails app called *railsgirls*.


First, let's open a terminal:

* **Windows**: Click Start and look for *Command Prompt*, then click *Command Prompt with Ruby on Rails*.
* **Linux (Ubuntu/Fedora)**: Search for *Terminal* on the dash and click *Terminal*.
* **Mac OS X**: Open Spotlight, type *Terminal* and click the *Terminal* application.

___

Next, type this command in the terminal:

{% highlight sh %}
mkdir projects
{% endhighlight %}

You can verify that a directory named <code>projects</code> was created by running the **directory listing command**:

<div class="os-specific">
  <div class="nix">
  {% highlight sh %}
  ls
  {% endhighlight %}
  </div>

  <div class="win">
  {% highlight sh %}
  dir
  {% endhighlight %}
  </div>
</div>

You should see the <code>projects</code> directory in the output.

___

Now you want to change the current directory to the <code>projects</code> folder by running:


{% highlight sh %}
cd projects
{% endhighlight %}

You can verify that now you are in an empty directory or folder by running again the directory listing command.

___

Now you want to create a new app called <code>railsgirls</code> by running:

{% highlight sh %}
rails new railsgirls
{% endhighlight %}

This will create a new app in the folder <code>railsgirls</code>, so again change the directory to be inside of our rails app by running:

{% highlight sh %}
cd railsgirls
{% endhighlight %}


If you run the directory listing command inside of the directory, you should see folders such as <code>app</code> and <code>config</code>.

### Command prompt

Notice that the place where you can enter commands ends with a symbol:

<div class="os-specific">
  <div class="nix">
{% highlight text %}
$
{% endhighlight %}
  </div>
  <div class="win">
{% highlight text %}
>
{% endhighlight %}
  </div>
</div>

This symbol is called the **command prompt**, and when you see it you know that you can enter commands in the Terminal.


### Start the application

You can start the application by running:

{% highlight sh %}
rails server
{% endhighlight %}

Open [http://localhost:3000](http://localhost:3000) in your browser. You should see the "Welcome aboard" page, which means that the generation of your new app worked correctly.

Going back to the Terminal window, notice that now the command prompt is not visible because the Rails server took control of the window. To return to the normal command prompt, hit `CTRL-C` in the terminal to quit the server.

Now that the server isn't working, refreshing [http://localhost:3000](http://localhost:3000) in your browser will show an error page.

**Coach:** Explain what each command does. What was generated? What does the server do?

## Step 2: Create a page

Lets add a page to our app; it will show information about the author of this application — you!

{% highlight sh %}
rails generate controller pages info
{% endhighlight %}

This command will create you a new folder under `app/views` called `pages` and under that a file called `info.html.erb`, which will be your info page.

___

Now open the file `app/views/pages/info.html.erb` and inspect its contents. What you see there was generated automatically, and it is written in a language called HTML.

___


Open [http://localhost:3000/pages/info](http://localhost:3000/pages/info) in your browser to see the info page and try to figure out the connection between what is written in the `app/views/pages/info.html.erb` file and what you see in the browser (or ask your coach :D)

**Coach:** Explain what are HTML tags and what they are useful for. Explain `<h1>` and `<p>`.

___

The next step is to replace that text with some information about you. Afterwards, refresh the page in the browser to see it in the website.

___

To experiment a bit more with HTML, open [http://htmledit.squarefree.com/](http://htmledit.squarefree.com/) and play with the editor.

Then you can ask your coach to show you more HTML tags and see how they work.


## Step 3: Create the `Idea` scaffold

We're going to use Rails' scaffold functionality to generate a starting point that allows us to list, add, remove, edit, and view things; in our case ideas.

**Coach:** What is Rails scaffolding? Explain the command, the model name and related database table, naming conventions, attributes and types, etc. What are migrations and why do you need them?

___

In the Terminal, stop the Rails server by hitting `CTRL-C`. You should see the Command Prompt again (which means you can give it commands). Run

{% highlight sh %}
rails generate scaffold idea name:string description:text picture:string
{% endhighlight %}

The scaffold creates new files in your project directory, but to get it to work properly we need to run a couple of other commands to update our database and restart the server.

<div class="os-specific">
  <div class="nix">
{% highlight sh %}
bin/rake db:migrate
rails server
{% endhighlight %}
  </div>

  <div class="win">
{% highlight sh %}
ruby bin/rake db:migrate
rails server
{% endhighlight %}
  </div>
</div>

Open [http://localhost:3000/ideas](http://localhost:3000/ideas) in your browser. Click around and test what you got by running these few command-line commands.

When you're done exploring, hit `CTRL-C` in the Terminal to quit the server again.

___

**Coach:** Talk about the relationship between HTML and Rails. What part of views is HTML and what is Embedded Ruby (ERB)? What is MVC and how does this relate to it? (Models and controllers are responsible for generating the HTML views.)


## Step 4: Design


The app doesn't look very nice yet. Let's do something about that. We'll use the Twitter Bootstrap project to give us nicer styling really easily.

Open `app/views/layouts/application.html.erb` in your text editor and above the line

{% highlight erb %}
<%= stylesheet_link_tag "application", media: "all", "data-turbolinks-track" => true %>
{% endhighlight %}

add

{% highlight html %}
<link rel="stylesheet" href="//netdna.bootstrapcdn.com/bootstrap/3.1.1/css/bootstrap.min.css" />
<link rel="stylesheet" href="//netdna.bootstrapcdn.com/bootstrap/3.1.1/css/bootstrap-theme.min.css" />
{% endhighlight %}

and replace

{% highlight erb %}
<%= yield %>
{% endhighlight %}

with

{% highlight erb %}
<div class="container">
  <%= yield %>
</div>
{% endhighlight %}

Let's also add a navigation bar and footer to the layout. In the same file, under `<body>` add

{% highlight html %}
<nav class="navbar navbar-default navbar-fixed-top" role="navigation">
  <div class="container">
    <div class="navbar-header">
      <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
        <span class="sr-only">Toggle navigation</span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
      <a class="navbar-brand" href="/">The Idea app</a>
    </div>
    <div class="collapse navbar-collapse">
      <ul class="nav navbar-nav">
        <li><a href="/ideas">Ideas</a></li>
      </ul>
    </div>
  </div>
</nav>
{% endhighlight %}

and before `</body>` add

{% highlight html %}
<footer>
  <div class="container">
    Rails Girls 2014
  </div>
</footer>
<script src="//netdna.bootstrapcdn.com/bootstrap/3.1.1/js/bootstrap.min.js"></script>
{% endhighlight %}

Open `app/assets/stylesheets/application.css` and at the bottom add

{% highlight css %}
body { padding-top: 100px; }
footer { margin-top: 100px; }
{% endhighlight %}

Make sure you saved your files and refresh the browser to see the style improvements. Make a connection between the HTML that you added in the files and what you see in the browser.

___

Now, the table looks a bit crammed. Let's fix that! In the same file, `app/assets/stylesheets/application.css`, at the bottom add

{% highlight css %}
table, td, th { vertical-align: middle; border: none; padding: 5px 10px;}
th { border-bottom: 1px solid #DDD; }
{% endhighlight %}

Save the file again and refresh the browser to see what was changed.

**Coach:** Talk a little about CSS and layouts.

### Play more if you want to

[Bootstrap](http://getbootstrap.com/) is a free collection of styles that look nice. By including it in a web page, and following their conventions on how to structure the HTML, you get a nice style without much effort. 

But, if you want to experiment more with CSS and understand it better, you can play with it online. If you'd like to do that, go to [http://cssdesk.com/VFVEk](http://cssdesk.com/VFVEk).

___

You can also change the HTML &amp; CSS of your Ideas website - tell your coach what you'd like to do and they'll help you.

One example would be to add, in the header, a link to the information page (from Step 1). Open `app/views/layouts/application.html.erb` and in the middle, replace

{% highlight html %}
          <li><a href="/ideas">Ideas</a></li>
{% endhighlight %}

with

{% highlight html %}
          <li><a href="/ideas">Ideas</a></li>
          <li><a href="/pages/info">About</a></li>
{% endhighlight %}




## Step 5: Add picture uploads

We need to install a piece of software to let us upload files in Rails.

Open `Gemfile` in the project directory using your text editor and under the line

{% highlight ruby %}
gem 'sqlite3'
{% endhighlight %}

add

{% highlight ruby %}
gem 'carrierwave'
{% endhighlight %}

**Coach:** Explain what libraries are and why they are useful. Describe what open source software is.

In the terminal run:

{% highlight sh %}
bundle
{% endhighlight %}


At this point you need to **restart the Rails server process** in the terminal.

Hit `CTRL-C` in the terminal to quit the server. Once it has stopped, you can press the up arrow to get to the last command entered, then hit enter to start the server again. (This is needed for the app to load the added library.)

___

Now we can generate the code for handling uploads. In the terminal run:

{% highlight sh %}
rails generate uploader Picture
{% endhighlight %}


The `Idea` model needs to know that its `picture` field is a file, not just some text. To do that, open `app/models/idea.rb` and under the line

{% highlight ruby %}
class Idea < ActiveRecord::Base
{% endhighlight %}

add

{% highlight ruby %}
mount_uploader :picture, PictureUploader
{% endhighlight %}

The view that allows to create or edit images needs to show a field for selecting a file instead of a text field. To do that, open `app/views/ideas/_form.html.erb` and change

{% highlight erb %}
<%= f.text_field :picture %>
{% endhighlight %}

to

{% highlight erb %}
<%= f.file_field :picture %>
{% endhighlight %}


Also, change the line

{% highlight erb %}
<%= form_for(@idea) do |f| %>
{% endhighlight %}

to

{% highlight erb %}
<%= form_for(@idea, :html => {:multipart => true}) do |f| %>
{% endhighlight %}

___

In your browser, add new idea with a picture. When you upload a picture it doesn't look nice because it only shows a path to the file, so let's fix that.

Open `app/views/ideas/show.html.erb` and change

{% highlight erb %}
<%= @idea.picture %>
{% endhighlight %}

to

{% highlight erb %}
<%= image_tag(@idea.picture_url, :width => 600) if @idea.picture.present? %>
{% endhighlight %}

Now refresh your browser to see what changed.


## Step 6: Finetune the routes

When you open [http://localhost:3000](http://localhost:3000) it still shows the "Welcome aboard" page. Let's make it redirect to the ideas page.

Open `config/routes.rb` and after the first line add

{% highlight ruby %}
root :to => redirect('/ideas')
{% endhighlight %}

Test the change by opening the root path - [http://localhost:3000/](http://localhost:3000/) - in your browser.

**Coach:** Talk about routes, and include details on the order of routes and their relation to static files.


## What next?

* Improve the design design using HTML &amp; CSS
* Add picture resizing to make the page load faster
* Add commenting or ratings
* Use CoffeeScript (or JavaScript) to add interaction


## Additional Guides

* Guide 0: [Handy cheatsheet for Ruby, Rails, console etc.](https://github.com/PragTob/rails-beginner-cheatsheet)
* Guide 1: [Add commenting by Janika Liiv](/commenting)
* Guide 2: [Put your app online with Heroku by Terence Lee](/heroku) / [Put your app online with OpenShift by Katie Miller](/openshift) / [Put your app online with Ninefold](/ninefold) / [Put your app online with Shelly Cloud](/shellycloud) / [Put your app online with anynines](/anynines) / [Put your app online with Trucker.io](/trucker)
* Guide 3: [Create thumbnail images for the uploads by Miha Filej](/thumbnails)
* Guide 4: [Add design using HTML &amp; CSS by Alex Liao](/design)
* Guide 5: [Add Authentication (user accounts) with Devise by Piotr Steininger](/devise/)
* Guide 6: [Adding profile pictures with Gravatar](/gravatar)
* Guide 7: [Test your app with RSpec](/testing-rspec)
* Guide 8: [Continuous Deployment with Travis-CI](/continuous-travis) / Continuous Deployment with Codeship](/continuous)
* Guide 9: [Go through additional explanations for the App by Lucy Bain](https://github.com/lbain/railsgirls)
