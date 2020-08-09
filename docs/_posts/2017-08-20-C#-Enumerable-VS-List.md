---
title: C# - IEnumerable vs. IList
published: true
---

When programming in C#, we might always be wondering: should we just be using `IEnumerable` here or
`IList`?

This is a classic question in C# programming, and, in fact, a lot of people have asked this already.
People are asking similar questions everywhere, such as stackoverflow. And if you do some research,
the answer to this question is oddly clear and vague at the same time. Clear in a sense of saying, it depends
on what you need. And, of course, this is vague. One question, after reading all these answers from
the Internet (BTW, some of them are really good where they really have explained everything in detail),
that you might still have is: What do I really need?


## Enumerable and List

From [MSDN](https://docs.microsoft.com/en-us/), the definition of `IEnumerable` is:

```
Exposes an enumerator, which supports a simple iteration over a non-generic collection.
```

Where for `IList`, it is:

```
Represents a non-generic collection of objects that can be individually accessed by index.
```

So clearly, when you use `IEnumerable`, you will get a collection that you can iterate though while
for `IList`, items are indexed in the collection. That is the main difference. But when to use which?

The simple answer is:

| Interface   | Scenario                                                                                                    |
| -           | -                                                                                                           |
| IEnumerable | You only want to iterate the elements in the collection                                                     |
| -           | -                                                                                                           |
| IList       | You want to be able to iterate, query the elements through the index, or sort the elements                  |

So, at this point, it should be somewhat clearer that what you might want to use. If in the current
context of your code, you will need to access some specific element(s) in the collection, or sort
the elements based on the business logic, then you have to use `IList` or `List` to have a list.
And that is when you will see where `.ToList()` comes into play.

However, if in the current method(s) or functions, you don't want to, or don't need to manipulate
the collection, or you only need to iterate the collection, for example, use `Foreach`, then you should
use `IEnumerable` instead.

For a more concrete example, consider the following linq expressions:

```csharp
// If you have a students collection of class Student that has a property Name

// If you only want a student name collection
var studentNames = students.Select(x => x.Name)

// If you want to access any student name based on the index, or sort the names
var studentNames = students.Select(x => x.Names).ToList()
```

Note the difference is `ToList()`, where the first expression returns an `Enumerable` and the second
expression returns you a `List`. Choosing one over the other totally depends on your code logic, but
keep in mind that `.ToList()` is very costy. As it will turn the whole collection into an indexed
list, and this operation is going to put everything in the list into the memory.
Especially when you have too many elements, this operation is going to be very expensive. So
under any circumstances, you should try to avoid using `.ToList()` whenever possible unless it is really
necessary.

## Method Argument Types and Method Return Type

### Argument Types

But what should we choose for the arguments of a method? One basic principle is, for OOP, "Depending
on abstractions instead of implementations", you should only consider `IEnumerable` or `IList` over
`List`. And then you should double check what are you going to do with this variable in this method.
Again, based on what we have discussed above, if you only want to iterate, or just keep the collection
, then use `IEnumerable`, otherwise `IList`. And also, when you design your code, keep in mind that
[Be conservative in what you send, be liberal in what you accept](https://en.wikipedia.org/wiki/Robustness_principle)
from `Robustness Principle`. That generally speaking, if there is a possibility of both types might
exist for one collection, you should just use `IEnumerable`, unless you are so sure about the whole
lifecycle of it. Meaning that you are dealing with some concrete data type rather than a generic.

### Method Return Type

Still considering the `Robustness Principle`, we might be using a concrete type when we return the
value from a method. So a `List` would be an ideal choice. But again, if you don't need to sort or
access any of the element in the collection, then `IEnumerable` is a good enough. So it really depends...

## Summarization

I don't know if the explanation helps you get the concept clearer. The unfortunate answer is still:
It depends. But based on some examples and scenarios I listed, it should somewhat give you a better
idea when to choose what. If you have a different opinion, feel free to contact me.
