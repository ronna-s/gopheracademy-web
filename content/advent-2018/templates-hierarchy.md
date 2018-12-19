+++
author = ["Ronna Steinberg"]
title = "Go Templates without Hierarchy"
linktitle = "go-templates-no-hierarchy"
date = 2018-12-20T00:00:00Z
+++

In April of this year I organized a Women Who Go Berlin meetup at 
[Ecosia](https://www.ecosia.org/) about Go templates, specifically HTML. 
Before the meetup, the team at Ecosia taught me everything about the topic
and we came up with a challenge for our members: Render a widget that 
dresses a gopher according to the weather.
 
It was a fun exercise, but at the very end of the night, just before 
leaving, one of our members asked me: “But it's static, right?”, 
suggesting it is not possible to manipulate the DOM with templates. Now, 
this statement is true enough, and I could have just said yes and leave 
it at that, but I was thinking about React.js at that moment, and how 
it doesn't really manipulate the DOM but re-renders what is necessary, 
and you can hardly call React static.
It's worth noting that this particular member never asks me easy 
questions and always gets me into trouble trying to come up with good 
answers. So my answer was therefore: "I need to think about it", and oh 
boy, did I get into trouble...

It was no accident that I was thinking about React in that context. 2 
months earlier, to prepare for the workshop, I used templates to render a 
chess game, just to get the hang of it. 
And to get around the staticity of the templates I wrote a small JavaScript 
script that opened a websocket to allow the client to receive notifications 
from the server whenever the board needed re-rendering. The template was 
static, but the game wasn't, giving that reactive feel that one would 
expect from a game.
But in truth, this reactive behavior was only made possible by the 
client running JS, not only the server running Go. So I've already 
accepted that to achieve this the client is going to have to run some JS. 
What I really wanted to know was if we can bring the amount of JS 
running on the client down to a tiny little script, and fire the most 
basic onclick events on the server. 

The answer is yes. I have actually done it and it was a fun exercise. 
I'm not going to get into all the details because in the end it's a 
terrible idea from the design perspective for various reasons:

1. Running everything on the server side doesn't utilize the freely 
available CPU on the client side.
2. The server can never have any downtime, if a server must handle every 
little client-side event.
3. The server must support every older version of the UI for backward 
compatibility. 

On a side note: Using Go WebAssembly has some potential in eliminating 
the issues listed above, and I'm planning to try it out soon. 

However, while I must insist that rendering everything on the backend
is a bad to terrible idea, I bumped into some interesting  
some 
interesting 
tricks to avoid 
having to 
formalize the templates hierarchy (the way it is suggested in every 
tutorial), which might force you to re-organize it if you have a lot of 
tiny fragments of HTML that you need to  
If you are new to Go templates, I suggest you use them the recommended 
way, until you run into problems and then have a look at this post, you 
want to try to keep to the methodology first, until it doesn't work out 
for you. 


    
