---
layout: post
title: "Intelligent Agents"
category:
tags: []
---
{% include JB/setup %}
Well I had to write a little one page paper for AI class about agents so here it is incase anyone else is ever thinking about a simple little agent that plays a wierd cave game called Wumpus world. Also, I guess some of the Ideas are a little interesting. The code to run and test everything is provided in my extended entry if you want it. (The code isn't the prettiest or well commented seeing as I had other work to do and had to finish the entire assignement in less than two days, but it works and the smart agent does do better thant he simple one.)

    Agents

I created the two agents, the dumb agent that was mostly random and the more intelligent agent. The dumb agent got an avg of -450 which was close to the naive agent the professor had coded up, which averaged -390. So everything with my world and agent seemed pretty close. I then began work on the intelligent agent. I found it significantly harder than expected to add features that improved performance. Many times adding rules that I thought would help improve the agents performance and these rules would actually result in far lower scores. After trying a few pretty simple ideas I developed what my final agent became. My final agent had an average score of -60 which wasn't great, but still significantly better than the dumb agent. I added one extra constraint to the game for fun, since I am a vegetarian I decided that I would never kill the Wumpus. So my algorithm would simple avoided the Wumpus in attempts to navigate to the gold. This lead to more impossible maps and therefor a lower overall score. It will still be interesting to see how my animal friendly agent performed in comparison to others.My more intelligent agent worked on the right hand on the maze wall idea. I would go forward until i found a area that could present a problem. A problem being either a stench or a breeze, if this problem was found i would turn around and walk the other direction and then try a different route, with my right hand facing the problem. This worked well at avoiding pits since I also had a higher percent of the time the choice of moving forward, and always would move forward if there was no chance of danger. This quickly lead to the problem of certain pits providing an infinite loop. Lowering my score by getting in a safe, but useless route. To fix this if I encountered the same pit problem multiple times i would then just walk threw the sensed breeze in hopes that the pit was not the direction I was going. This could have been improved by first trying alternate routes around the pit, but could have then left the problem of many different infinite loops.The improvement of the agent was significant and noticeable, but also illustrated the difficulties of simple relying on a simple set of rules. I think a more effective route would have been to have the agent slowly walk along any known safe route while mapping problem areas to his known portion of the map and only after exhausting all safe possibilities (and trying to create safe possibilities by killing the Wumpus) picking at random a unsafe point of passage that would lead to the most possible options for a next move.

<script src="https://gist.github.com/2014472.js?file=wumpus.java"></script>