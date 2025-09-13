+++ 
draft = true
date = 2025-09-08T21:36:43+02:00
title = "Choosing Your Poison: The C++ Build System Saga"
description = "A deep dive into the nightmare that is C++ build systems - from CMake to Bazel, and why setting up a modern C++ project makes you question your life choices."
slug = "cpp-build-system-is-programming-hell"
authors = ["0zminDev"]
tags = ["c++", "cmake", "build-systems", "programming", "game-engine"]
categories = ["development", "game-engine"]
externalLink = ""
series = []
keywords = ["c++", "cmake", "build-systems", "compilation", "make", "ninja"]
author = "0zminDev"
image = "/images/cmake-hell.png"
+++

Every great human advancement has at least one huge flaw that makes using it a pain in the ass. For space travel, it's **cosmic radiation**. For the internet, it's **Twitter**. And for C++, it's the **build system**.

> *"Choosing C++ is easy. Setting up the build system is where souls go to die."*

In the previous post, I talked about my language of choice. I landed on C++ for a couple of reasons (which you can find and criticize there). But I knew that choosing a C-style language came with a tradeoff, a devil's bargain sealed in the 1970s: **the build system**.

You see, along the years we've seen many great approaches to building stuff. But C++ build systems? They still feel like they were designed to **punish you**. I'm making fun of it, but in the 70s, it was probably groundbreaking. Well, it isn't 1970 anymore, and the whole process has started to get a little... *stinky*.

There's a new wave of C-style build tools trying to break the old rust off the topic, but they all wrestle with the original sin of C: **header files**.

It's a great idea on paper—seeing the definition of a class in a neat `.h` file. But as we'll discuss, most, if not all, of C-style coding sins come from the beautiful, terrible, and absolutely necessary evil that is the **header file**.

Of course, this won't stop me. I use **JavaScript** in my professional work, after all. I'm a savage. But when planning a huge-ass project like **FluxEngine**, it's important to discuss the possibilities and why I chose one over the other.

**Fair warning**: This post will probably have a sequel. While learning stuff for this article, I started having second thoughts about my own approach. And I've decided if I'm going to pivot, it's better to do it *now* than when the project is a tangled mess of dependencies.

So, for now, I'm going to discuss the options out there. I'll tell you what I chose, and why I'm already thinking about changing it.

With that cleared up, let's dive into the wonderful, horrifying world of C/C++ build tools.

---

---

## The Sigma Option: Just Write a Shell Script

Before we talk about all the fancy third-party systems, we need to address the elephant in the room—the **DIY approach**.

You think you're smarter than decades of tool development? You think you can outsmart the experts? Well, you can just write a shell script (`build.sh` or `build.bat`) that calls the compiler directly with all your files and flags.

### The Pros

- You have **absolute, god-tier control**
- No extra dependencies. Just you, your code, and the compiler
- It's simple and straightforward

### The Cons

- It's not cross-platform unless you want to maintain scripts for every OS
- **No incremental builds**. You change one line and recompile the entire universe. Forget a semicolon? Compile it all again, idiot
- It requires competence and experience, two words I'm not entirely familiar with yet

So yeah, I'm sticking to third-party solutions for now.

---

## The Workers vs. The Managers

In the world of C++ builds, there's a clear divide. Think of it like a factory floor. You have the **workers** who actually operate the machinery, and you have the **managers** who tell them what to do.

### The Workers (Build Systems)

These are the tools that actually do the building. They take a set of instructions, figure out which files have changed, and then run the preprocessor, compiler, and linker. Their main job is to be fast and efficient at the actual "make my 1s and 0s" part.

- **Make**: The OG. The grizzled veteran of build systems. Legend says your father built his code using Make, and his father before him. It's old, reliable, and everywhere. It reads Makefiles, which have a syntax that feels like a cryptic incantation.

- **Ninja**: The new kid on the block, and my current favorite. Ninja is *FAST*. Its whole philosophy is to be a "small build system with a focus on speed." It's not meant to be written by hand. It's designed to be the target for a meta-build system. You don't write Ninja files; you generate them.

- **NMake**: The Microsoft solution. It's... there. If you're deep in the Visual Studio ecosystem, you'll encounter it. But hence its stinky Microsoft nature, I'm going to not talk about it.

### The Managers (Meta-Build Systems)

The workers are great, but you don't want to be writing their instructions by hand for a project on Windows, macOS, and Linux. That's where the managers come in. They are called **meta-build systems** because they don't build anything themselves. Instead, they generate the project files (Makefiles, Ninja files, Visual Studio solutions, etc.) for the workers.

They handle the cross-platform shit, find libraries on your system, and let you define your project in a higher-level language. They are both easier *and* harder to write than a raw Makefile. Weird, I know.

- **CMake**: The undisputed king. The industry-standard pain in the ass. It's powerful, it supports everything under the sun, and almost every C++ library in existence has a `CMakeLists.txt` file. The problem? Its scripting language was designed by someone who either hated developers or was a time-traveler from the 1980s. The learning curve isn't a curve; it's a vertical cliff face with angry goats throwing rocks at you.

- **Meson**: A modern, sane alternative to CMake. It uses a simple, Python-like syntax and is designed to be user-friendly and fast. It almost always pairs with Ninja. It's gaining a lot of traction, and frankly, it's looking pretty damn good.

- **Premake**: Another popular alternative, especially in the game dev world. It uses Lua for its scripting, which is a big plus for many game developers who are already familiar with it. It's simpler than CMake but very capable.

---

## My Choice (And My Regret)

So, after staring into the abyss, what did I choose?

### I went with **CMake + Ninja**

**Why?** Because despite its horrifying syntax, CMake is the devil I know. It's the *standard*. When I need to pull in a library like Vulkan, glfw, or glm, I know there's a 99% chance it has robust CMake support. Using it feels like the "responsible adult" choice. And pairing it with Ninja means my actual builds are blazing fast.

But as I was writing this, a thought started creeping in. A little voice whispering...

> *"You could just use Meson. It's so much cleaner. Think of the time you'd save. Think of your sanity."*

And damn it, **that voice has a point**. The project is still young. If I'm going to make a change, now is the time.

So the next post might just be a story about changing the build system in the middle of development. Or maybe not, if the process is surprisingly easy (which I'm doubtful of).

For now, the plan is to stick with **CMake**. But it's on thin ice.

---

*See you soon.*
