---
layout: post
title:      "Collect User Input With HTML Forms"
date:       2020-01-09 20:18:39 +0000
permalink:  collect_user_input_with_html_forms
---


After having just completed the CLI Gem portion of the curriculum here at Flatiron School, the time has come to move on from creating simple command line applications with Ruby. In this next portion of the course we are moving on to Sinatra, using this powerful library to connect our Ruby code to the web and allow us to create websites that are interactive, flexible, and responsive. Sinatra is an insanely powerful tool that abstracts a lot of the work involved with getting a web application up and running, but there are also other essential tools that we need to learn in order to add key functionality. Enter HTML and CSS. Today I will be discussing a specific tool that HTML brings to the <table>: Forms.

When we think of the modern web, we think about things like interactivity, connections, and applications. The web would be pretty boring without those things, don't you think? The ability to view information from anywhere in the world on your own personal device is pretty powerful on its own, however; the web would be a pretty static and uneventful place without the ability for users to interact with the pages that they visit. One of the ways in which we are able to facilitate communication between a user and a website is with HTML Forms. These form tags allow a website to gather input from a user and operate or display it in some way, adding an essential interactive component to the web as we know it. Imagine how dull modern websites would be without the ability to input login information, or to input an address for package delivery while shopping online, or even the ability to simply input a search query into a site like Google.

HTML Forms are relatively straightforward, but also extremely powerful. The only thing you need is a simple form tag in your HTML file like this:

```
<form> </form>
```


Okay, so its not exactly that simple. There are a few things that we need to do to get everything up and running. (Side note: We are learning how to hook these forms up to our website with Sinatra so we will only be talking about using forms in that context)

In practical use, we will need to utilize two keywords along with our form tag: "method" and "action". First, the method attribute will specify which HTTP method to be used when the user submits the form data to our server. You have the option of specifying GET ot POST, though generally POST is the method you will most often want to be using. The second keyword is the action attribute. This attribute will specify the route in our application controller that the HTTP method will be sent to. Lets take a look at what a functional form tag would look like:

```
<form method="POST" action="/submit"></form>
```

The above snippet will take the data the user inputs into our form, wrap it up in a nice POST request to the specified route "/submit" in our application controller and allow us to do whatever we would like with that data. The form tag itself however isn't doing much right now, its just a blank form. In fact, if you were to just add the above code to an HTML file it wouldn't be doing much of anything. It wouldn't even show up to our user. HTML Forms use another type of tag inside of the `<form>` block: the `<input>` tag.

The `<input>` tag allows us to add in individual input fields where our users can put in whatever input we would like to get from them. There are two main atributes that we will need to specify for our input tags: a type and a name. The type attribute will allow us to specify the type of input we would like our field to take in. There are many different built in input types such as text, radio buttons, checkboxes, etc. The second attribute "name" specifies a hash key that we will use when the data is sent to our controller to retrieve the input. If this attribute is omitted we will have no way to access that data, and in fact it will not be sent to our controller at all.

Lets take a look at what a simple example form might look like:

```
<form method="POST" action="/login">
  Username: 
  <input type="text" name="user_name"><br>
  Password: 
  <input type="password" name="password">
  <br><br>
  <input type="submit" id="submit">
</form>
```

If we look at the code, we can see that we have created a form that will send a POST method to our /login route. The form contains a field for a username and password as well as a submit button that will send the request. The information will be sent in the form of a hash called params that we can access and manipulate in our controller with the name attribute specifying the key. the params hash from this form would look something like this:

```
params #=> { :user_name => "kjdowns", password=> "s3CuR3P455w0Rd"}
```

These are example values obviously, but we can see that we can easily access the user input using our params hash. Let's see an example of how we might operate on that data with Sinatra to create a new user profile:

```

post '/login' do
  @user = User.new
	@user.user_name = params[:user_name]
	@user.password = params[:password]
	erb :new_user
end

```

You can see above we were able to create an instance of a new user, assign it a username and password variable, and then load a new file called new_user.erb. Aren't HTML forms great? 

This is obviously just a quick overview of the HTML Forms tool, but we can easily see how simple and powerful of a tool it is to use. If you'd like to learn more about forms, you can check out some documentation [here](https://www.w3schools.com/html/html_forms.asp) or even check out a cool lesson on Learn.co [here](https://learn.co/tracks/online-software-engineering-structured/html-continued/html-forms/html-forms).


