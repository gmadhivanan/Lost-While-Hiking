# Lost-While-Hiking
[Game](https://editor.p5js.org/gmadhivanan/full/TrmMwUgm4)
## Background
I wanted to make an interactive experience that had some horror elements. I'm a big fan of Cosmic/Lovecraftian Horror and wanted to work some elements from that into this. I figured a simple premise would be getting lost in the woods while something is chasing you.
## How to play
Hold the left mouse button to move the player. Move the mouse around to change where the player is facing and the direction of the flashlight. The thing that is chasing you can only be seen by illuminating it with the flashlight. If you run into a tree you will get stunned for some time. By pressing "C" on the keyboard you can click the horn on your key fob to get an idea of where you parked your car. The whispers of the other can drown out the noise of the car horn.

## Objects in my code
[code](https://editor.p5js.org/gmadhivanan/sketches/TrmMwUgm4)
### Escape
This is the get away car. There is only one of these. It is placed somewhere on the map. It has a position and a size. I added a distance so that when the player gets close enough they can escape (If I continued developing this it would be fun to add a minigame to fumble for their keys). I added a variable ct to get the sound to stay around for a certain amount of time and click as a boolean to find when the button was clicked. It does take a separate function called key pressed to determine some of this. A counter tic was added so the player can't just hold the horn button down.
### The other
The entity which is following you. There is also only one of these. I initially was not going to put in a getaway car and just have this thing follow the player around while also having some more complex behavior tree. But I didn't quite like that idea as much. This has a position, a distance to the player and a speed. It also has a variable called talk which is just a way for other agents to determine if the other is talking.
### Player
There is only one of these as well. I didn't actually use this object much until the end. I don't think I actually use the x or y variables since I translate the origin to where the player is. The speed of player is important along with the stun. There is logic in the draw function where if the player collides with a tree their stun counter goes up and they can't move until they change direction.

### Tree
There are 500 of these objects, although I did play around with these a bit to try to make it feel like there are a lot but not too many. It took a decent amount of effort to get these working. Similar to my previous assignment, these are all placed at setup and offset when the character moves. This translation created a lot of confusion which is why in addition to x and y variables this also has an offsetx and offset y. There is also a realx and realy variable. Finally this each has a distance to player as well as a size. There is also an inbuilt function to display. This just made the draw function a little simpler.

## Offset
This was just a simple way for me to set and get the offset on a regular basis.

## Make Shapes Function
This function was copied from [This p5js project](https://editor.p5js.org/v-k-/sketches/siYtDw423) and then slightly modified. I initially had the other as just a pulsing circle. I didn't find that menacing enough. I wasn't what to do to make it look otherworldly. I wanted something that was shifting so I looked into the polygon function.  While I was doing that I saw this piece of code that generated random polygons. I put this into my draw function when the other is drawn. I kept the pulsing circle and with both of them together I really like the effect. I think the code still holds up without this function, but if I need to remove it for academic integrity reasons I can.

## Setup
In the setup I make new versions of all the different objects. I had the other start at a distance of 100 to -100 in the x and y directions. Randomizing this makes it so you never know where it's coming from initially. I tried to randomize were the escape car spawns, but it seems to favor certain positions. I used a random seed to spawn the trees. I like how they get laid out on the map. 

## Draw function
This is where the meat of my code is. I'm not going into extreme detail here, but I had to do an annoying amount of trial and error to get the math to work for the collisions. I didn't know of an easy way to have the other show when it's in the beam of the light. I initially tried to use switch to radial coordinates for the calculation but was have a hard time with that. So instead what I did was calculate the distance from the other to the line going between the mouse and the player(at 0,0). Then if this was under a certain value the other would be shown. This sort of worked but if the other was behind me it would also show. So I had to determine which quadrant of the canvas the other was in and what quadrant the mouse was in. If they were in the same coordinate, then the other would show. (I used a similar technique for the stun mechanic with the trees)
I wanted the other to whisper to the player. This would give the player a rough idea of where the other is, even when the flashlight is not pointed at it. I couldn't put the text directly on top of the other though, since then the player would know exactly where the other was. So instead I randomized an offset onto the text position. This sort of worked.
To determine whether the text would show I have a random variable rand. It's greater than a certain value then the text will show. For the text I used zalgo text from https://lingojam.com/ZalgoText. I liked how hard this was to read while still retaining some ability to be read. I randomly chose from an array of creepy phrases. I would have preferred for the text to fade in and fade out. But didn't have the time to get that working.
The player has a stun counter that increases if they hit a tree. While they're stunned their move speed is zero. After the stun wears off it goes back to the original speed. Rotation in p5js is a little annoying. I wanted the player to spin with the mouse. I used some simple trig to calculate the angle of the mouse in relation to the player. Then I had to add it a bit of extracode to prevent issues potentially due to me wanting to use degrees instead of radians.

I tried to add in some code for the other so that it would have states. I wanted to continually chase the player. But if the player got to far away I wanted it to go into an idle state. Then after the idle state I wanted it to increase in speed until it got close to the player again. This was just so that the other could never truly be escaped.

I translated to where the player is located at the beginning of the draw function, which kind of messed up where the trees were located so I had to translate back before I drew them. I had to rewrite my mousequad code since it wasn't being read into the for loop. I probably could have some work for it to be more readily accessible, but I got a bit lazy there towards the end.
