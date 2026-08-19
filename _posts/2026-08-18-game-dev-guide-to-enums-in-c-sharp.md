---
title: A Game Developer's Guide to Enums in C#
categories: C#
tags: beginner-c# scripting
excerpt: "Enums in C# store related constants. Despite their storage capabilities, enums aren't the same as other types in C# used to store many values, such as lists or arrays."
image:
    path: /assets/images/enums_article/enums_article_thumbnail.jpg
    thumbnail: /assets/images/enums_article/enums_article_thumbnail.jpg
---

Enums in C# **store related [constants]({{ site.baseurl }}{% post_url 2025-09-21-game-dev-guide-to-constants-in-c-sharp %})**. If the game you're building in the [Unity Game Engine](https://youtu.be/kOo1CaDdCF0?si=m_SoO0x0rxHZoHEL) has seasons or the days of the week, you can store them in an enum.

Despite storing related constants, enums aren't the same as other types in C# used to store many values, such as lists or arrays. The differences are discussed [later in the article](#enum-vs-list-vs-array-in-c-whats-the-difference).

If you're a visual learner, you can watch the video version below.

<div class="responsive-embed responsive-embed-16by9">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/OboSgv98Km0?si=cSKnEYKHLesTyiD6" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

{% include toc %}

## How to Use Enums in Unity

Enums are created in four steps:

1. Write the access modifier.

2. Write the `enum` keyword.

3. Write the enum's name.

4. Add the enum values separated by commas.

Access modifiers are discussed in more detail in a separate article, but for now, you can use the `public` access modifier, meaning the enum is accessible anywhere in your code.

```csharp
public enum Season
{
    Spring,
    Summer,
    Autumn,
    Winter,
}

Debug.Log(Season.Winter); // Logs 'Winter'.
```

**You can't name the enum using the word "_enum_" without any modification** because that's a special keyword in C#. The values inside an enum are accessed using **dot notation**.

**_Tip:_** The word enum is short for enumeration.
{: .notice--info}

Let's say you want to make a game in Unity where the day of the week is updated every 24 in-game hours, similar to the _Grand Theft Auto_ series. Every in-game Saturday, a random special weapon is available for purchase.

One approach is to store each day of the week in a [string]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-strings-in-c-sharp %}) and then check if the current day is Saturday before releasing a special weapon.

```csharp
var wednesday = "Wednesday";
var thursday = "Thursday";
var friday = "Friday";
var saturday = "Saturday";

var currentDay = "Tuesday";

if (currentDay == saturday)
    Debug.Log("A new special weapon is available!");
```

This could work, but manually typing out the day in each string could lead to typos, a common cause of bugs in many games.

It's also unclear at a glance whether the strings are related or not because they appear as standalone [variables]({{ site.baseurl }}{% post_url 2025-09-19-game-dev-guide-to-variables-in-c-sharp %}) or constants.

**_Tip:_** The `if` statement in the code above is part of conditional statements.
{: .notice--info}

Alternatively, you can create an enum and store all the days of the week in it, eliminating the likelihood of introducing typos because each day of the week is typed once.

In addition, grouping the days of the week in an enum **signifies that all the values are connected** and shouldn't be seen as individual parts to be used separately.

```csharp
public enum DayOfWeek
{
    Monday,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday,
    Sunday
}

var currentDay = DayOfWeek.Tuesday;

if (currentDay == DayOfWeek.Saturday)
    Debug.Log("A new special weapon is available!");
```

## Enum vs. List vs. Array in C#. What's the difference?

| Enum | List | Array |
| --- | --- | --- |
| `enum` keyword **mandatory** during creation. | `List` keyword **optional** during creation. | `Array` keyword **optional** during creation. |
| Values are inherently [numbers]({{ site.baseurl }}{% post_url 2025-09-24-game-dev-guide-to-numbers-in-c-sharp %}). | Values can be multiple types. | Values can be multiple types. |
| Can't loop through. | Can loop through. | Can loop through. |
| Pascal case naming. | Camel case naming except constants. | Camel case naming except constants. |
| Can be only item in file. | Often part of other items in file. | Often part of other items in file. |

Even though enums store values, they're not the same as lists or arrays. Some of the differences are:

- **Enums are declared differently from lists and arrays**. They must have the `enum` keyword.

- **The values stored in an enum are inherently numbers**. Lists and arrays can store multiple types, such as strings, numbers, booleans, etc.

- **You can't loop through an enum**, but you can do so with lists and arrays.

- **Enums are named using Pascal Case**, while lists and arrays, unless they're constants, are named using Camel Case.

- **Enums can be the only item in a C# file**. Lists and arrays are commonly used in files containing other items, such as classes, methods, or fields and properties.

Despite their similar appearance, you should use an enum if you solely want to group related constants.

If you have a collection of items you want to manipulate by adding, removing, or updating other items, a list or array is a better choice.

**Interested in making games in Unity?** [Become a patron](https://www.patreon.com/cw/heightabovesealevel) on Patreon and gain access to cheat sheets, behind-the-scenes content, advanced scripting videos, and more.
{: .notice--primary}

## Recap

- Enums **store related constants**.

- They **must** be declared using the `enum` keyword.

- The **values in an enum are inherently numbers**.

- Enum values are accessed using **dot notation**.

- Enums, though similar to lists and arrays, are **not identical**.

This article is the seventh in a series breaking down common C# concepts used in game development with the Unity Game Engine.

The next one discusses how to use [conditional statements]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-conditional-statements-in-c-sharp %}) to control the flow of your code's execution.

Here's the complete list of articles in the series:

1. [A Game Developer's Guide to Variables in C#]({{ site.baseurl }}{% post_url 2025-09-19-game-dev-guide-to-variables-in-c-sharp %})
2. [A Game Developer's Guide to Constants in C#]({{ site.baseurl }}{% post_url 2025-09-21-game-dev-guide-to-constants-in-c-sharp %})
3. [A Game Developer's Guide to Numbers in C#]({{ site.baseurl }}{% post_url 2025-09-24-game-dev-guide-to-numbers-in-c-sharp %})
4. [A Game Developer's Guide to Operators in C#]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-operators-in-c-sharp %})
5. [A Game Developer's Guide to Strings in C#]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-strings-in-c-sharp %})
6. [A Game Developer's Guide to Booleans in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-booleans-in-c-sharp %})
7. A Game Developer's Guide to Enums in C# _(you are here)_ 
8. [A Game Developer's Guide to Conditional Statements in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-conditional-statements-in-c-sharp %})
9. [A Game Developer's Guide to Loops in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-loops-in-c-sharp %})
10. [A Game Developer's Guide to Classes in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-classes-in-c-sharp %})
11. A Game Developer's Guide to Access Modifiers in C#
12. A Game Developer's Guide to Fields & Properties in C#
13. A Game Developer's Guide to Methods in C#
14. A Game Developer's Guide to Lists & Arrays in C#
15. A Game Developer's Guide to Dates & Times in C#