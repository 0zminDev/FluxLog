+++
date = '2025-09-06T10:31:53+02:00'
draft = false
title = "It's All C afterall"
+++

> In the beginning, there was chaos…

… and from this chaos emerged a whole bunch of wrong decisions, mistakes, and failures that eventually turned into FluxEngine.

In this blog, I’m going to show how a simple intern managed to start creating an engine… instead of accidentally deleting the production DB.

I've always wanted to build a game engine,  
so all the dudes on the internet telling me *“build games, not game engines”*… well, they sucked for me.

Game engine architecture is clear, complex, and looks **sexy af**.  
Meanwhile, game code looks by definition like **spaghetti on top of more spaghetti**.  

It’s not the developers’ fault – sometimes art requires moving your code into the hacky realm of quick fixes and rewrites on demand.  

The engine, however, is the place for the technologically gifted (or introverted enough to spend all their life in front of a PC).  

And game engine code is the one place where **no designer or artist can hurt you**.

---

The first very important question I had to solve was: **what language am I going to use?**

So I did the worst thing you can do in that position – I asked Reddit.  
Oh boy. If only I knew what kind of mistake that was.  

The replies flooded in like a tidal wave of unsolicited, contradictory advice. One comment thread devolved into a 50-reply argument about memory safety. Another was just a single, cryptic message: "Have you considered Lisp?" A chorus of users ignored the question entirely to tell me I should be building games, not engines, and that I was wasting my life. For every helpful suggestion, there were three pedantic corrections about my terminology and five people recommending their obscure pet language that has 12 stars on GitHub.

![Me after posting the question](/images/openheimer.png)  
*Me after posting the question*

Ok, but let’s cut the crap. After a couple of minutes, I had a list of candidates:

1. **C** – almighty C, some say it can compile on a potato. Very verbose and ideal in its own way. The problem? It’s *too* simple. For some that’s a plus, but I wanted to learn new stuff. Also, my previous game engine attempt was already in C, so I wanted something else.  
2. **Zig** – another great possibility. The trendy, modern, safe low-level kid on the block. But it’s not stable. Even tiny version bumps break the build system and core concepts entirely. Not something I want for a long-term project.  
3. **Odin** – yet another new kid. I haven’t tried it (yet), but it’s compiled with a C ABI, so in theory it’s more stable than Zig. Supposedly “finished” too, at least according to its author. Maybe one day.  
4. **Rust** – my second failed attempt. I tried to learn it, but stopped when I discovered (maybe mistakenly) that making static libs or DLLs requires going through C. My thought was: if in the end it’s all C anyway, what’s the point?  
5. **C++** – last but not least. Basically C with extra toys. My plan: use C-style C++ for the low-level guts, and modern C++ for the abstract stuff. I actually built an engine in C++ back in middle school, on OpenGL. I didn’t know what I was doing, but hey – this time I’ve got Vulkan.

---

So yeah, after all the drama, I went with **C++**.  
Because in the end… **everything is C anyway.**

![It's all C](/images/itsallc.png)

Next time I’ll talk about actually setting up the damn project,  
because (spoiler) **CMake is pain in the ass. As always.**

See you soon
