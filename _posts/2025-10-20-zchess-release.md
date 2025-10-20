---
title: zChess Release
date: 2025-10-20
categories: [Personal Projects, iOS]
tags: [iOS, Swift, Chess]
pin: true
math: false
mermaid: true
image:
  path: /assets/lib/2025-10-20-zchess-release/banner.png
  lqip: data:image/webp;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAgGBgcGBQgHBwcJCQgKDBQNDAsLDBkSEw8UHRofHh0aHBwgJC4nICIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL/2wBDAQkJCQwLDBgNDRgyIRwhMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjL/wAARCAAIABADASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSExBhJBUQdhcRMiMoEIFEKRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwD1C0nkYENUazzQ3ZP8NFFVYk//2Q==
  alt: Download on the App Store
---

## Building zChess

I didn’t set out to build a chess app, I just wanted to learn something.

A month ago I was looking for a project that would stretch my skills with Swift/SwiftUI. Something that wasn’t another to-do list or weather app with a good balance of complexity. Like many others, I got into chess while navigating COVID-19 lockdowns and discovering The Queen's Gambit on Netflix, and the idea of making a chess-playing app of some kind seemed like an homage to that time.

I wasn't even sure what the app would be yet, I just started making my [zChessKit](/posts/zchesskit-1.0.0/) project. Whatever the app could be, it'd need a robust model for chess games and moves.

That’s where zChess began, not from a business plan or a feature list, but from curiosity.

## The Idea That Stuck

The first two weeks the project was entirely in [zChessKit](/posts/zchesskit-1.0.0/). No interface, no prototypes, just getting the logic of chess moves supported.

I did finally get the first interface together about two weeks into the project, and soon realized I finally needed a direction for the app to go. Obviously I could allow users to play games locally, but I only thought to make an Opening Trainer and Puzzle Mode when I realized they would share a lot of ideas. Both ideas expect the user to make the one move in a given position. But only when I started prototyping it was I able to really grasp the scope of the problem.

How do you represent a chess opening as data? How about a chess puzzle?

How do you know when the user “remembers” a move?

What’s the right pacing to make learning stick?

That led me down a rabbit hole of spaced repetition, move trees, and the quirks of building something interactive but structured. It turned into a surprisingly fun technical puzzle — half chess logic, half user experience experiment.

## Building it Anyway

I built this entirely in SwiftUI, mostly because I wanted to get better at it. Every piece of the app (board rendering, move animations, progress tracking) was an excuse to explore a new concept.

Most of it didn’t work the first time.

Some of it didn’t work the tenth time.

But that’s what made it enjoyable. It was a slow process of getting comfortable with the weird corners of the framework, learning to debug layout issues, and figuring out when it was time to rewrite something from scratch.

Somewhere in there, it stopped being just a playground and started feeling like an actual app.

## Keeping It Small

The biggest challenge wasn’t technical, it was deciding when to stop. There’s always something else you could add: online play, AI opponents, an Analysis Board, Custom Openings. But I kept coming back to the original reason I started this: to learn.

So I decided to keep zChess focused and self-contained.

No accounts. No cloud sync. No clutter.

Just a simple, local training tool that works offline and feels fast.

It’s not meant to replace other chess apps. At best it’s more like a small companion, something you can open for ten minutes and genuinely learn from. Maybe something you can warm up before getting online, or while you sit on a train. That constraint ended up shaping the whole design.

## The Quiet Parts of Development

The most satisfying parts of this project weren’t the “big milestones”, it was the small moments:

the first time the board rendered correctly, the first working animation (and especially when I refactored it to animate better), the first saved training session.

Those little breakthroughs are what make solo development so addictive. You go from “this is impossible” to “oh wait, it actually works”, sometimes in a single evening.

I think that’s why I love projects like this. They remind me why I started coding in the first place: not to ship something big, but to tinker, to learn, to see an idea come alive on-screen.

## What's Next

Now that zChess is live on the App Store, I’m giving myself permission to slow down a bit and use it like a real user. I have a small roadmap (more courses, better analysis tools,maybe endgame modes) but I want to evolve it naturally.

For me, the interesting part isn’t what zChess is right now, but what I learned making it:

how to design around simplicity, how to work without external pressure, and how to build something that’s genuinely yours.

If you’re curious, you can see more at [zchess.app](https://www.zchess.app). But mostly, I hope this post nudges someone to start that small idea sitting in the back of their head. The one that doesn’t need to be perfect, just real enough to learn from.
