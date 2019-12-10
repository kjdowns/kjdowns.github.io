---
layout: post
title:      "DBD Archive - A CLI project"
date:       2019-12-10 19:52:54 +0000
permalink:  dbd_archive_-_a_cli_project
---


***Welcome to the archive***

![DBD Archive](https://i.imgur.com/v89Wv5V.png)

The Dead by Daylight archive is a CLI application that I built for the CLI Gem project at Flatiron. The requirements for this project were that we create a CLI, that CLI must access data from a website, and that information must go at least "one level" deep. When thinking about what I would build, I decided that I wanted to do something that felt personal - something that I myself would want to use. I was inspired by content creators that create external resources for games they love, to share with and expand that game community. 

So what does it do? The Dead by Daylight Archive is a CLI application that provides various information about the asymetrical horror survival game Dead by Daylight. In this game four survivors are subject to trials within the realm of The Entity where they must complete objectives to escape. There to extinguish the hope of survival; however, is a singular Killer, who's job it is to injure and sacrifice the survivors before they can escape. Regardless of the outcome, the characters are returned to the campfire where they rest before resuming thier eternal game of cat and mouse for the pleasure of The Entity.

The application provides information on nearly 40 characters (both killers and survivors), thier abilities and powers, lore, items, and more. I decided to use the [DBD Wiki](https://deadbydaylight.gamepedia.com/Dead_by_Daylight_Wiki) for this purpose since it had all of the information I would need. 

![](https://steamcdn-a.akamaihd.net/steam/apps/381210/header.jpg?t=1575392832)

I started with a lot of excitement, this is a game I play with friends almost every night and it was really fun to work on something that other members of the DBD playerbase might want to use. I started designing from a perspective of building a tool that I as a player would want to use. I made a list of the most essential information I would want to know about each character and about the game in general. As you can imagine, I quickly realized that there was far too much information that I wanted to include. I had to make a decison on what would go and what would stay.

I began to think about the relationships that the information I was looking at had with one another. The most important aspects would be the characters. There would be Killers and Survivors so I started out with a `Character` class that both a `Killer` and `Survivor` class could inherit from. Building that out, I decided each charater would have both perks and lore. Killers also have Realms that they come from that act as the game map. This is where I hit my first hurdle.

After scraping all of the relevant information from the main wiki page, I began to navigate into the individual character and information pages to find that the html for this website was woefully bad. There were no class selectors, almost none of the information was organized in any way. Nokogiri uses css selectors to grab information from the website, which it now looked like would be pretty hard to do with any precision. After a lot of thinking and googling as well as a quick chat with one of our coaches, I found a solution. 

I used the `~` marker within my css selection to grab all of the specific sibling nodes of the selector I needed and filtered them according to a text pattern I identified across most of the wiki pages. There were a few stubborn exceptions, but that just required a little flow control to direct what items to pull for those pages.

```
lore_section = self.doc.css("div.floatleft ~ p")

  def add_lore(character, lore_section)
    lore_section.each do |section|
      section.text.strip.include?("These are Perks") ? return : character.lore << section.text.strip
    end
    #last item is empty and should be removed
    character.lore.pop()
  end
```

This solution was really put to the test two days in to working on the project as two new characters were released to the game. I prepared myself for the possibility that these new additions to the website would break everything I had worked on so far. Pleasantly it didn't! My selectors and flow control held up, and with some minor tweaks to fit those new characters into the patterns I created, they were added to the program no issue. 

I continued working, creating menus, establishing the relationships my objects had with one another, and creating the main logic of the program. I was presented with many more problems along the way to completing the project, but I was able to overcome them with some real head scratching and if Im honest, at times, immense frustration. 

I learned so many things during this project. Being free of the tests and having to debug and come up with my own solutions for finding issues was challenging and frustrating, but also very rewarding. Figuring out what was stopping my program from working the way I wanted it to really helped solidify my understanding of the concepts we learned, as well as boost my confidence in my knowledge. 

Tools like pry and irb were indispensible through that process and finally completing everything really reassured me that I could keep doing this. Programming is hard work, navigating through the tools available and finding new ones to use was an adventure, and implementing them to create something all of your own design was exhilarating. I'm looking forward to the new things I am going to learn and new projects I am soon to start working on!

Feel free to check out the CLI program and play around with it for yourself. Below are links to both the video walkthrough as well as the actual git repo.

[Video Walkthrough](https://www.youtube.com/watch?v=5e07OFO2uSo&t=7s)

[Github repo](https://github.com/kjdowns/dbd_archive)

