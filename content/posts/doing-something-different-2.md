---
title: "Something Different #2 - Games"
date: 2023-08-14T14:05:18+01:00
draft: false
---

The first thing I tried, was learning how to make games<!--more-->

As discussed in the previous chaper, I have a long history with games. My parents were self-employed and always had computers at home, which I could comandeer after they finished working with my latest shareware floppy disk. I spent the first seven or so years of my career as a games tester at Codemasters, and continue to play games as a hobby.

When I was thinking about possible career paths to explore then, games development seemed like a good one for the list.

## The Plan

My plan was to create a couple of working prototypes over several weeks, in the process learning how to use a games engine. After a little casting about I settled on [Godot](https://godotengine.org/) for its active community, good documentation, availability of tutorials, Python-esque scripting language which prioritised productivity and free-ness. 

I also came armed with an idea that I had been toying with for a while in a non-committal way - a game where you control drones working for a spy organisation in the 1970s using clicky clacky IBM computers - but the goal here was really to explore the process of making a game and how it differed from web development in which I'd worked for the last decade or so.

## How It Went

### No Name Drone Game

My first protype then, described above, was to be part story, part typing/terminal based, and part social commentary … yikes.

Wow this was hard, and for a while quite disheartening - especially as the first thing since I'd started to try and Do Something Different.

Alongside that though, it was really interesting, because it taught me a lot - not so much about the technical side - but about the challenges and skills involved in designing a game which is fun to play; taking an abstract idea and turning it into a concrete set of logic which creates the feelings and experiences you're aiming for is _really_ hard.

I struggled getting this idea to take shape as something that was fun to play. I loved the [Godot](https://godotengine.org/) engine and editor - I was quickly into creating various node types and scripting out their behaviour. However, I hit some major roadblocks defining how I wanted this drone-control-spy-story-computer-terminal thing to actually work. 

Would the game play during a mission be real time, or turn based? If it was real time, typing into a computer terminal real fast might not be that fun or fair a challenge. If it was turn based then the player can stop and think, but the game would then be too easy. How do I weave the story into it all? Would just typing into a terminal be boring? How does the player even get rewarded?

I talk more about the challenges of this open-ended nature of games design below, but in the end, and despite some great advice from people who actually do design work instead of just dabbling like I was, I realised I just couldn't 'find the fun' in this game idea. Over a couple of weeks I had tried a number of approaches and reworks, created design docs for the basic game play loop, and implemented a couple of different versions (real time and turn based) in Godot with a simple mission briefing, movement and results setup. However, it just didn't feel as I'd imagined it yet and I couldn't at this point see what to do to fix it. Feeling a little chastened and not wanting to turn down Sunk Cost Fallacy Boulevard, I called time on it and moved on.

Fail fast … right?

### Pluccy

This was my second prototype and I decided to approach a much more simple idea, with a more well defined genre and expectations, then give it a little twist.

Briefly, Pluccy is a pretty standard 2D platformer created with a lovely free asset pack. You move through several short levels jumping to avoid enemies and obstacles while collecting keys. The (small) twist is that when you reach the end of these short levels, you are confronted by an NPC who is angry that you moved all his keys and you are tasked with putting them back. As you go back through the levels replacing keys you find that each level has been reimagined into a harder version, with additional and sometimes too-difficult platforming required to make it through.

In this prototype I found it much easier to keep making forward progress, as the design was pretty simple and most challenges were around implementation. I will say however that tuning the difficulty of the platforming was both fun and tricky, given the highly variable nature of player ability. I think here I learned a touch less about the game design process, but a lot more about Godot and games engines in general by removing those design concerns. It involved adding simple animations, physics, audio, score tracking, restarting and data storage (to remember which keys you took on the first run through) and using tile sets. I was also pleased with the nifty way I created the 'harder' versions of each level, namely by using the same node but programmatically swapping out tilesets and changing a few parameters to convert them between 'easy' and 'hard' mode.

The end result, while short and simple, was a lot more encouraging than my No Name Drone Game, because I had more to show for it at the end, gained a lot more practice with Godot and felt I'd created a playable - if short - experience.

## Learning and Thoughts

The first thing I discovered over this four weeks was that my brain was conditioned in the wrong way for this kind of task. With a background in testing, working more on the implementation side of things, my thought process tended to work back from the end of the development timeline.

Regardless of efforts to Test Left, testing is naturally more concerned with the right hand side of the process. Certainly in traditional testing (and setting aside my actual feelings on doing testing this way) by the time you become involved the designs are usually at least somewhat settled, and your job is to facilitate a quality implementation. This generally means you take other people's work and go backwards a bit, to oppose assumptions and find potentially missed scenarios or better approaches. More succinctly, you challenge work which is already in progress or completed.

In design you work from the opposite direction - you create from scratch and push from left to right, defining behaviours and pathways. There is no other work to start from and refine, and this was quite the reversal in my thought process.

Furthermore, the open and flexible nature of game creation was a change from the more restrictive and rote world of web technology and design. By its nature web design has some tendency to coagulate around certain conventions (nav bars, log in forms, modals, banners etc.) which leads on from the central standardised view through which you see websites - browsers, and their support for HTML and JavaScript.

In games, these barriers don't exist or are much less well defined. If you can imagine it (and have the requisite skill and time), chances are you can build it. Genres are often blurred and remixed, new and interesting ways to tell stories are discovered and interactions are a great deal more varied. To the first time games maker coming from a background of web development, this was scary.

## Conclusion

Overall I was pleased with what I'd learned in this month, but a little deflated that I hadn't managed to turn my dream idea into much of anything. I did gain understanding of the [Godot](https://godotengine.org/) engine (an engine I would now heartily recommend), although naturally there was still much, much more that I hadn't even touched on yet. Not least 3D games, aside from the 3D tutorial project. I also gained an insight into the challenges of designing in such an open ended medium with no prior games design experience.

I think during this period I was also adjusting from my previous routine of 9-5 job to being in control of my own day, and finding it to be … well … wonderful. I found I could settle to a task without interruption, driven by my own interest and motivation rather than the needs of a project I didn't necessarily believe in. On many occasions I would sit and work for several hours at a time without realising it. I also discovered that if I worked when I was feeling productive and energetic, then took breaks when my energy levels waned to do more mundane household tasks, I got much more work done each day than I had in full time employment.

To conclude, I found myself enjoying the coding and implementation side of the games development process more than the design side, and also settled into a new pattern of working which suited me and made me more productive.

This will lead me nicely onto my next plan: learn Go. More on that soon.