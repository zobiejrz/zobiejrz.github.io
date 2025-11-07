---
title: The Making of zChess Clock
date: 2025-11-07
categories: [Personal Projects, iOS]
tags: [iOS, Swift, Chess]
pin: true
math: false
mermaid: false
image:
  path: /assets/lib/2025-11-07-zchess-clock-making/banner.png
  lqip: data:image/webp;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAgGBgcGBQgHBwcJCQgKDBQNDAsLDBkSEw8UHRofHh0aHBwgJC4nICIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL/2wBDAQkJCQwLDBgNDRgyIRwhMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjL/wAARCAAIABADASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSExBhJBUQdhcRMiMoEIFEKRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwD0jTd3etNc5oorKe5zVdz/2Q==
  alt: zChess Clock's main screen
---

## It's literally just a clock

But coding the clock presents it's own challenges.

I spent only a day or two on this project, all because I wondered "How could I represent a time control for chess?"

## The Process

At first glance, a simple `struct` is sufficient for 90% of all use cases. Something like this:

```swift
struct TimeControl {
  let minutes: Int
  let seconds: Int
  let increment: Int
}
```

You could even simplify it by only storing `seconds` and `increment`, but this has some obvious limitations. What about games that give 2 hours for the first 40 moves, then another 60 minutes with a 5 second increment? Maybe a `TimeControl` really needs to be an array of `Stage` objects, allowing a clock to detect and navigate to the next stage when a player meets certain thresholds.

```swift
struct TimeControl {
  let stages: [Stage]
}

struct Stage {
  let minutes: Int
  let seconds: Int
  let increment: Int
  let movesInStage: Int
}
```

This covers even more possible time controls, but at this point I remembered that some games prefer to use a *delay* instead of an increment, where the clock waits a specified period of time before continuing to count down. Enter [Associated Values](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/enumerations#Associated-Values):

```swift
struct Stage {
  let minutes: Int
  let seconds: Int
  let buffer: TimeBuffer
  let movesInStage: Int
}

enum TimeBuffer {
  case delay(seconds: Int)
  case increment(seconds: Int)
  case none
}
```

This flexibility meant that if ever I wanted to add different methods of buffering the clockmeant that in the future it would be pretty reasonable to just add a new case (like I would later do for bronstein time delay).

The last piece of the puzzle was when I learned of a different time control method, using an hour glass. This method starts each player with half of a shared pool of time. As one player uses their time, it is given to their opponent. There isn't any stages though, so it was time to apply an enumeration again!

```swift
enum TimeControl {
    case normal(stages: [Stage])
    case hourglass(baseTimeSeconds: Int)
}

struct Stage {
    var minutes: Int
    var seconds: Int
    var buffer: TimeBuffer
    var movesInStage: Int?
}

enum TimeBuffer {
    case delay(seconds: Int)
    case increment(seconds: Int)
    case bronstein(seconds: Int)
    case none
}
```

> You can see the full version of these objects with all their helper functions [on GitHub](https://github.com/zobiejrz/zChessClock/blob/main/ChessClock/ChessClock/Model/TimeControl.swift).

And that's it. With this I was able to put together an object that actually managed the clock and used these to store relevant information.

I didn't expect enumerations to be so useful initially, but by using them I didn't have to worry about a `TimeControl` struct with both a `stages` array *and* a `baseTimeSeconds` value set. Either you have an array of stages, or you have an hourglass. This kind of design allowed me to reduce bugs down the line by preventing any weird combined edge cases.

## What's next

This project probably won't ever make it to a v2.0. The next v1.1 release will allow separate time controls for each side (along with some customization settings), and I might introduce Go and Shogi specific time controls for v1.2, but after that there won't be much else. **zChess Clock** simply started as the product of a fun thought experiment and the need for a break from the next [zChess](https://zchess.app) update.

That said, the project is available [on GitHub](https://github.com/zobiejrz/zChessClock) and will be released on the App Store early next week (pending review) for the world to enjoy. Feel free to fork the project and give your own spin to it, even submit PRs to get changes on the official version.
