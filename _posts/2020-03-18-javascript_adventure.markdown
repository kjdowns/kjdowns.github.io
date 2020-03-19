---
layout: post
title:      "Javascript Adventure"
date:       2020-03-19 00:18:20 +0000
permalink:  javascript_adventure
---


Playing games has always been a hobby and a passion of mine. Learning how to make them was what originally got me interested in coding, so now that I had the tools to actually do it I decided that for my Javascript project it would be fitting to finally create a game. I chose the name Javascript Adventure simply because it was an adventure game made with Javascript, but it turned out to be a very fitting name, because this project sure took me on an adventure through the world of Javascript. 

The game itself is a 2D dungeon crawler style adventure game where a player is put through a series of 10 levels. Each level increases with both difficulty and number of monster that must be slain. Slay all of the enemies on every level and emerge victorious! It sounds like such a simple concept, and I thought as much when I originally came up with the idea, but that was far from the case. I learned throughout this process that there are so many things to handle in even a simple game.

My first struggle was learning how to utilize HTML Canvas to draw what I needed to the screen. HTML Canvas is an HTML element that you can add to a webpage that allows you to draw, clear, and render a number of different things and basically acts as a game viewport. After adding the element to your html file, you can use good old Javascript to grab it and start drawing items to the screen for the player to see and interact with.

The second and largest hurdle I had to clear was the process of animating all of the game objects. I think we can all agree that a game without animations would be pretty dull and uninteresting. The most efficient way I found to facilitate the animation was with the use of sprite sheets. The process of anmating is really just playing a series of images in quick succession, just like a flip book or a video. It would take quite a lot of work though and get pretty messy if you had to have seperate images for every frame of every movement of every object. Cue sprite sheets to the rescue. 

Basically how a sprite sheet works is that it is a single image that contains all of the individual animation frames for a single game object. You then set the height and width of the image you want to cut it out of the image file. Then its as simple as iterating over each "frame" in the row in quick succession to play the animation.

![example sprite sheet](http://jslim89.github.com/images/posts/2014-09-12-create-spritesheet-for-cocos2d-x-using-with-texturepacker/spritesheet-demo.png)

So I had that working after a little bit of playing around with it, but now I had a new problem - My animations were playing, but they seemed to be flickering. I struggled with this problem for a few days, not really having a solid understanding of what was going on in my game loop to cause the issue or having any knowledge about animation to know where to start to fix it. After taking a break to work on other aspects of the project, I finally really sat down and did a deep dive into how the animation works. 

I found out soon that things were flickering because the frames were being iterated through every single time the game loop was iterating, which at the time was about 30 times per second. In order to solve the issue, I had to do quite a bit of refactoring - which ended up making the rest of the time working on the project pretty nice since all my code was now nice and neat. After that I was able to re-write the parts that animated my game objects to include a delay counter. Basically what this allowed me to do was set a delay so that the frames would update at the speed I wanted them to (every 10 updates instead of each and every update). This solved my problem! It felt really great to finally find the solution to this problem that had been plaguing me for days.

With the problem of animation no longer nagging me, and with my code now was more organized than it was before - I was able to move on to the last bits of the game: finalizing the game loop and adding a save feature. The game loop itself is pretty simple: render all of the objects that are supposed to exist, where the player expects them to be, check for updates to game objects such as movement or collision, and then update the objects with those changes in preparation for the next render. 

For the save and load feature I used a Rails API backend. When the user enters a name to be associated with a save file and then clicks either the save or load button, a request is sent to the back end server. Based on the response that was set, it will either create or update a save on the server, or load an existing one from the server into the game.

I feel like I learned so much during the creation of this project that I could write for hours about it. It really is true, at least for me, that actually creating or doing something can teach you so much more than just reading about it. For example, I found event listeners and fetch requests very confusing when I first came across them in the curriculum, but after working with them in this project, they felt like one of the easier items to implement and work with.

You can check out the game at the links below. Give it a go, I hope you have as much fun playing it as I did making it!

[Walkthrough Video](https://www.youtube.com/watch?v=auZfl9-soSo)

[Github Repo](https://github.com/kjdowns/js-adventure)
