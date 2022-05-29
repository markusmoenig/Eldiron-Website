+++
title = "Development Blog May"
cover = "devblogmay2022.png"
date = "2022-05-28"
author = "markusm"
+++

#### Eldiron v0.55

I started the month by adding a new 24x24 tile-map to the already existing 16x16 tile-map. The new tile-map has more details, both focus on Ultima 4 / 5 style tiles and are production quality. As always the tile-map is MIT licensed and the full source files can be downloaded [here](https://github.com/markusmoenig/Eldiron-Assets).

---

Next I started with player handling. Although **Eldiron** already has a quite powerful node system I mostly focused on NPC behavior (Non-Player-Characters) so far. Reason being is that player based actions are quite simple to handle and NPC actions are more complex and thus i focused on these so far. Anyway, now you can walk with your player character in the game region via the Arrow Keys, only took me 5 months 😅.

In general, the player character is always named *Player* in the character view. I plan to make player handling as modular as possible, for example each command from a client executes the behavior tree of the same name in the *Player* character, allowing very easy integration of new commands in the client / server architecture.

---

I had to take a step back in the editor architecture and refactored various UI elements to make them more modular. Spend more time on this than I wanted to, but as more functionality gets added to the editor I just wanted to make sure everything is as tidy as possible.

---

Every parameter in a node is in fact a script, to set the movement speed for the *Pathfinder* node for example you can just enter a value of *8* (speed is between 1-10) or you can write a script and test if you are on horseback or in a marshland and adjust your speed accordingly.

The scripting subsystem of **Eldiron** is based on [Rhai](https://rhai.rs). I really like the syntax and flexibility of Rhai, however it is based on an AST and not on a bytecode interpreter like Lua for example. I worried that the speed may be an issue later, when **Eldiron** will potentially handle hundreds or thousands of characters. I was wondering if I should write my own bytecode interpreter for **Eldiron**, like Godot has with GDScript. I tested the speed of Rhai against Lua and found no significant difference, I guess the scripts for the nodes are small enough to not make a real difference. I mean we will not compute π in **Eldiron**. So I finally decided on sticking with Rhai and I can still invest a month or so later on to implement my own scripting language if the need should ever arise.

---

One of the last parts in **Eldiron** I had to start implementing was the *Game logic* view. This is a special node graph where the visible screens (and their content) in a game are defined and in which order they are shown.

I decided to make each behavior tree a standalone screen. You can define the start tree in case you want to jump to specific content inside a game for debugging.

Each screen can contain widget nodes which are small script based areas (widgets) on your screen. You can draw game content, UI elements, texts, images and so on. All of this is still work in progress right now. The above screenshot gives you a first impression how things will look.

Later on users can optionally also implement UIs just with nodes (and without scripts), however I had to start somewhere and the script based solution is just the one faster to implement to get started.

---

As writing scripts got more important I did spend a few days implementing a code editor, when you click on a script parameter it pops up from the bottom of the screen with a nice animation. So far the code editor is pretty basic and does for example not handle mouse based text selections or copy / paste yet but that will be easy to add.

---

Phew, thats it for **Eldiron** for May. Quite a few big design decisions were made and the architecture of all major parts is being worked on (with the exception of the Items view).

I will execute on the *Game logic* and other parts of **Eldiron** more next month. My goal is to have a fully functional visual screen editor as soon as possible. Also the [book](https://book.eldiron.com) will need quite a bit of work to reflect the documentation of the current status.

I also would like to thank my [Patreons](https://patreon.com/eldiron), thank you so much for your trust!

Until next month.
