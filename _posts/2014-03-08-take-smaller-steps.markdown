---
layout: post
title:  "Take smaller steps"
date:   2014-03-08 14:03:08
---

Real-life programming problems are often very complex and hard to solve. One of the most important things I learned was that I had to break down a large problem into smaller, easier tasks and solve those first. This helped me check for the intended behaviour early instead of having to build a large algorithm only to find out it didn't work after many hours of programming.

A simple example for taking small steps is a program which draws a chessboard. At first, this seems to include a lot of edge cases and some fairly complicated logic. Here's what I would do to solve this:

* Draw a single filled square as well as a single empty square. Those make up the chess board at the end.
* Draw a line of alternating filled and empty squares, once starting with a filled, once with an empty square.
* Draw an area of alternating lines, once starting with filled, once with empty squares.

This method lets you get near-instant feedback on whether the program is working or not and lets you correct mistakes early. It can also help you stay motivated by giving you a little bit of satisfaction every time you are able to draw something closer to the chess board.
