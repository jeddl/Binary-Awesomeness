---
title: C#-Enumerable vs. List
published: false
---

When programming in C#, we might always be wondering: should we just be using `Enumerable` here or
`List`?

This is a classic question in C# programming, and, in fact, a lot of people has asked this already.
People are asking similar questions everywhere, such as stackoverflow. And if you do some research,
the answer to this problem is clear and vague at the same time. Clear in a sense of saying, it depends
on what you need. And, of course, this is vague. One question, after reading all these answers from
the Internet (BTW, some of them are really good where they really have explained everything in detail),
that you might still have is: What do I really need?

So in this post, I am just going to explain when and why we should use one over the other based on my
personal experience and perspective.

## Enumerable and List
 - What are they?

## Why Enumerable
 - Not loading everything at the same time
 - Iteratable
 - Fast

## Why List
 - More concrete
 - Easier to manipulate
 - Indexed

## How Are We Going to Decide
 - Need to load everything?
 - `ToList()`
 - What do we really need?
