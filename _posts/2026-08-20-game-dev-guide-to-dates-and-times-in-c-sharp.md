---
title: A Game Developer's Guide to Dates & Times in C#
categories: Scripting
tags: beginner-c-sharp
excerpt: "_Metal Gear Solid 3: Snake Eater_ had a creative feature that few expected when it was released on the PlayStation 2 back in 2004. It had a boss fight where, if you closed the game and didn't play it for two weeks, the boss would die of old age, and you'd proceed to the next level."
image:
    path: /assets/images/dates_times_article/dates_times_article_thumbnail.jpg
    thumbnail: /assets/images/dates_times_article/dates_times_article_thumbnail.jpg
---

_Metal Gear Solid 3: Snake Eater_ had a creative feature that few expected when it was released on the PlayStation 2 back in 2004.

It had a boss fight where, if you closed the game and didn't play it for two weeks, the boss would die of old age, and you'd proceed to the next level.

Incidentally, if you closed the game and set the console's date to two weeks in the future, the same thing would happen.

Here's one likely approach Konami took to implement the feature.

The code accesses the console's date when the player reaches the boss fight, saves it, and, whenever the player relaunches the game later, compares the current date to the date they first reached the boss fight level.

If the time between exceeds or matches two weeks, the code sets a [boolean]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-booleans-in-c-sharp %}) value, such as `bossIsDefeated` to `true`, and the player proceeds to the next section.

It's a very clever way to use dates reminiscent of what you'd expect from Hideo Kojima himself.

You don't have to be as creative with dates when working in the [Unity Game Engine](https://youtu.be/kOo1CaDdCF0?si=m_SoO0x0rxHZoHEL), but knowing how to use them can go a long way.

This article assumes you know how to work with [classes]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-classes-in-c-sharp %}) and [methods]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-methods-in-c-sharp %}) in C#.

If you're a visual learner, you can watch the video version below.

<div class="responsive-embed responsive-embed-16by9">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/0B6u71YKwdc?si=up0s6yj9DcgHw1Vw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

{% include toc %}

## Dates in C#

C# provides a struct called `DateOnly` you can use to **work with dates**. Think of a struct as a mini class.

You can create an instance of this struct and provide the day, month, and year to create a new date.

```csharp
var releaseDate = new DateOnly(2025, 12, 7);

Debug.Log(releaseDate);

// Output: 12/7/2025 (Defaults to US date format)
```

`DateOnly` has some helpful methods like `AddDays()` and `AddMonths()` if you want to update the date object you created.

You can even convert the date to the extended version, where the day and month are spelled out instead of [numbers]({{ site.baseurl }}{% post_url 2025-09-24-game-dev-guide-to-numbers-in-c-sharp %}) separated by forward slashes.

```csharp
var releaseDate = new DateOnly(2025, 12, 7);

Debug.Log(releaseDate); // Logs '12/7/2025'.

// Logs 'Sunday, December 7, 2025'.
Debug.Log(releaseDate.ToLongDateString());

Debug.Log(releaseDate.AddMonths(2)); // Logs '2/7/2026'.
```

**Interested in making games in Unity?** [Become a patron](https://www.patreon.com/cw/heightabovesealevel) on Patreon and gain access to cheat sheets, behind-the-scenes content, advanced scripting videos, and more.
{: .notice--primary}

## Time in C#

The `TimeOnly` struct in C# lets you **work with different times of the day**. You can create an instance of it and specify the hours, minutes, and seconds of a time.

```csharp
var startTime = new TimeOnly(10, 30, 22);

Debug.Log(startTime); // Logs '10:30 AM'.
```

`TimeOnly` also offers helpful methods like `AddHours()` and `AddMinutes()` to advance the time, and methods like `ToLongTimeString()` if you want to see the seconds together with the hours and minutes.

```csharp
var startTime = new TimeOnly(10, 30, 22);

Debug.Log(startTime); // Logs '10:30 AM'.

Debug.Log(startTime.ToLongTimeString()); // Logs '10:30:22 AM'.

Debug.Log(startTime.AddMinutes(15)); // Logs '10:45 AM'.
```

**_Tip:_** `TimeOnly` is different from the `Time` class Unity provides. `TimeOnly` handles the **hardware's time and any time you explicitly declare**, while Unity's `Time` class handles **in-game time** as the game runs.
{: .notice--info}

## Working with Both Dates and Times

If you want to use both dates and times, you can use the `DateTime` struct.

It combines the methods and [properties]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-fields-and-properties-in-c-sharp %}) of the `DateOnly` and `TimeOnly` structs for easier [access]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-access-modifiers-in-c-sharp %}) and use.

```csharp
var dateAndTime = new DateTime(2025, 12, 7, 10, 30, 22);

Debug.Log(dateAndTime); // Logs '12/7/2025 10:30:22 AM'.
```

## Time Spans in C#

C# has a `TimeSpan` struct for working with time spans that can be helpful if you need to know the amount of time that has passed between two dates.

You can set a time span manually by creating an instance of the `TimeSpan` struct or by subtracting one `DateTime` object from another.

The `TimeSpan` object has helpful properties like `TotalHours` and `TotalMinutes` for a more granular perspective of the time that has passed.

```csharp
var timespan = new TimeSpan(5, 10, 00);

Debug.Log(timespan); // Logs '05:10:00'.

Debug.Log(timespan.TotalMinutes); // Logs '310'.
```

If you need to, you can use the `DateOnly`, `TimeOnly`, `DateTime`, and `TimeSpan` structs in [fields]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-fields-and-properties-in-c-sharp %}) and properties, method parameters, or as method return types.

```csharp
public class Dashboard
{
    private DateTime _dateTime; // <- 'DateTime' field.

    public TimeOnly Time { get; set; } // 'TimeOnly' property.

    public DateOnly GetDate() // <- Returns 'DateOnly' type.
    {
        return new DateOnly(2025, 6, 3);
    }
}
```

You don't have to use these structs to implement dates and times in your Unity game. They're merely one of many ways to approach it.

You could alternatively use a counter that counts up to 7 and assigns a day of the week to each number.

Every 20 minutes, the counter increases by 1, and the current day updates to the next one in the [enum]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-enums-in-c-sharp %}) or [list]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-lists-and-arrays-in-c-sharp %}). The counter then resets to 1 after reaching 7.

## Recap

- The `DateOnly` struct provides methods and properties to work with **dates alone**.

- The `TimeOnly` struct provides methods and properties to work with **times alone**.

- The `DateTime` struct lets you work with **both dates and times**.

- The `TimeSpan` struct lets you work with **time spans**.

- All the date and time structs work with **hardware dates or explicitly declared dates**, while the Unity-provided `Time` class handles **in-game time**.

This article is the last in a series breaking down common C# concepts used in game development with the Unity Game Engine.

Remember to check the other articles on [baking lights]({{ site.baseurl }}{% post_url 2025-11-01-baking-lights-in-unity-getting-started %}) to learn [how to light up your levels in Unity]({{ site.baseurl }}{% post_url 2025-11-01-how-to-bake-lights-in-unity-guide %}).

Here's the complete list of articles in the series:

1. [A Game Developer's Guide to Variables in C#]({{ site.baseurl }}{% post_url 2025-09-19-game-dev-guide-to-variables-in-c-sharp %})
2. [A Game Developer's Guide to Constants in C#]({{ site.baseurl }}{% post_url 2025-09-21-game-dev-guide-to-constants-in-c-sharp %})
3. [A Game Developer's Guide to Numbers in C#]({{ site.baseurl }}{% post_url 2025-09-24-game-dev-guide-to-numbers-in-c-sharp %})
4. [A Game Developer's Guide to Operators in C#]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-operators-in-c-sharp %})
5. [A Game Developer's Guide to Strings in C#]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-strings-in-c-sharp %})
6. [A Game Developer's Guide to Booleans in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-booleans-in-c-sharp %})
7. [A Game Developer's Guide to Enums in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-enums-in-c-sharp %})
8. [A Game Developer's Guide to Conditional Statements in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-conditional-statements-in-c-sharp %})
9. [A Game Developer's Guide to Loops in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-loops-in-c-sharp %})
10. [A Game Developer's Guide to Classes in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-classes-in-c-sharp %})
11. [A Game Developer's Guide to Access Modifiers in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-access-modifiers-in-c-sharp %})
12. [A Game Developer's Guide to Fields & Properties in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-fields-and-properties-in-c-sharp %})
13. [A Game Developer's Guide to Methods in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-methods-in-c-sharp %})
14. [A Game Developer's Guide to Lists & Arrays in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-lists-and-arrays-in-c-sharp %})
15. A Game Developer's Guide to Dates & Times in C# _(you are here)_