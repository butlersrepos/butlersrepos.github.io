---
layout: post
title:  "How I Work In JS"
image: ''
date:   2017-04-18 21:00:00
tags:
- javascript
- tools
- web
description: ''
categories:
- Javascript 
---

<img src="http://www.reactiongifs.com/r/2012/11/typing.gif" />
<center>^ That's me typing this article, so fast...</center>

## What's this?
I wanted to take a few minutes and explain the setup I use when I'm writing some web stuff at home, for fun. I'll list the current repetoire of tools and libraries I like to start with that I find quick and enjoyable to use. But before I get to that I want to articulate a few things I emphasis to people trying to up their workflow game.

## The importance of learning shortcuts
VIM vs Emacs. Mac vs Windows vs Linux. Eclipse vs IntelliJ. Sublime vs Atom vs VS Code. Whatever your preference, I don't care. If we work together you can use a custom IDE you built yourself in your own damned programming language - so long as you can explore, find, navigate, and refactor without losing your train of thought. One of my biggest pet peeves is watching a programmer hold a good thought or a chunk of context in their head and then have to sit and watch as it evaporates because they get distracted trying to visually scour a folder structure for the next file they want to open or because they know what operation they want to do (Replace All?) but are trying to see if it's under `Edit` or `View` or some wierd third option. 

My firm belief is that you as a developer are hired to be solving problems and when you lose track of your own problem-solving because you don't know your tool well enough then you should feel bad. If your team seems to have an agreeance on a common toolset then you should give it a try and pick up those new shortcuts. It pays to be "workstation agnostic" sometimes.

## The importance of removing obstacles
Why are you exponentially more likely to never visit a gym that's twice as far away? Because static friction is strong. This holds true for coding in your free time too. I love coding but I realize that if I have an idea and nothing else - I'm likely to just store it away until I forget it (the next day). But if I keep around a few starter projects that I can easily `git clone` and fire up? Then it's like I moved that gym into my house! Now I just have to change clothes... 

Take this notion to an extreme if you can. Anytime you encounter something rout, something discouraging - try to eliminate it, make it faster, be DRY with it, automate it. And obviously take this idea into your work life too. Remove the chaff from your daily work and leave just the tasty problem-solving and implementing parts for yourself and your team.

- Don't let tests start to take so long nobody runs them
- Browsersync
- One line builds/deploys
- Create aliases for things you should do more
	- git committing with a message
	- test runs (`npm test`!)
- Spend an hour and make a template starter-project with a few of your favorite tech choices NOW or find one of the many good ones

### Application Toolset
- Webstorm
- VS Code
- iTerm
	- buncha aliases
- `cmder` (at home on my windows box)
- Chrome

### Library Toolset
- `riotjs`
- `npm` scripts
- `jest`
- `webpack`
- the `fetch` polyfill

### Starter projects
- <a href="https://expressjs.com/en/starter/generator.html">Express JS</a>
- <a href="https://github.com/facebookincubator/create-react-app">React</a>
- <a href="https://github.com/butlersrepos/riot-web-starter">My own Riot Starter</a>

