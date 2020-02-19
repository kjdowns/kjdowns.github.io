---
layout: post
title:      "Rails Project - PokePet"
date:       2020-02-19 22:55:08 +0000
permalink:  rails_project_-_pokepet
---


Phew, it's finally finished! That's something I was begining to think I would never get to say, but I made it through! 

For my Rails Project, I decided to make a Pokemon pet simulation app called PokePet. It is inspired by Tamagotchi and Neopets style pet simulators. I learned so much making this that I barely know where to begin. 

The basic idea of the application is that a user signs in and is able to adopt pets from a large list of Pokemon. The user is then tasked with feeding, playing with, training, and generally taking care of their new pet. The end goal is to max out their happiness level, which in turn maxes out their actual level. There is also a Town that users can visit in order to get more money, buy more items, train their pets, or visit their maxed out pets. 

There are three total models in the application - User, PokePet, and a join model Adoption. Users and PokePets have a many to many relationship through the Adoption join model. Since the application is mostly concerned with the interactions between a user and their pets, most of the action deals with the Adoption join table model. Most actions in the application utilize this relationship to update information about the user and their pets through this join.

The site also allows users to sign up/ login with their Google account. For this I used the goog-ouauth2 gem. After a lot of confusion and a lot of time looking through the documentation as well as referencing the Learn lessons I was able to get this feature up and running. While the set up required getting familiar with a lot of confusing documentation, the payoff was definitely worth it. Passing off user authentication to a third party definitely makes logging in easier and more user friendly.

The Town, for me, was the most fun to develop. For this, I created a custom Town controller with custom routes to accomodate the actions that I wanted available to the user. This feature relied heavily on the hidden_id tag to pass information back and forth to the controller actions in order to pass along the message of what the user wanted to do. For example, the Shop buy buttons each hold a hidden_id field with the information about the items the user wants to buy. This is picked up when the request goes to the controller action, and filtered using a model method that updates the users inventory accordingly. 

With most of the site being button based actions, another feature I had to get familiar with was flash messages. I originally attempted to use the built in error validations provided by Rails (These are used in some places such as user signup), but I ultimately ended up wanting more customization than that. It was important while I was building this that every action taken by the user had a clear confirmation. For this I added a system of flash messages that would be sent for every outcome of every action. Things like feeding and playing use this, but also when something goes wrong, like if a user tries to train a MAX level pet, or feed a pet that isn't hungry. I really had a lot of fun working out all of the different situations and handling them.

I learned an insane amount making this project. For a large portion of it though, I had a lot of doubts. I wasn't sure I was doing enough, that I really understood what I was doing, or if the app was even something people would care about. In the end though, it all came together and I am quite proud of the finished project.

I decided that for styling I was going to try something new and try using Bootstrap. This was extremely confusing for me at first, but after watching a few videos and really sitting down with the documentation, I really had a blast getting everything to look exactly the way I wanted it. Bootstrap let me focus much more on the actual design of what I wanted and less on the technical aspects of the CSS that was going into it. Once I got more confortable with it, I was also able to add my own custom styling to come elements that I wanted to tweak. All in all I'm really glad I made the decision to try and learn something new.

Take a look, and try the app out for yourself if you'd like. I hope you'll have as much fun playing around with it as I did making it!

[PokePet repo](https://github.com/kjdowns/pokepet)

[Video Walkthrough](https://www.youtube.com/watch?v=RveYfAuvLhQ)
