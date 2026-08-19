---
title: A Game Developer's Guide to Loops in C#
categories: C#
tags: beginner-c# scripting
excerpt: "Loops are one of the fundamental tools you'll use when making a game in the Unity Game Engine. You can use them to execute code multiple times without repeating it or to search a collection of items for one that meets a specific criterion."
image:
    path: /assets/images/loops_article/loops_article_thumbnail.jpg
    thumbnail: /assets/images/loops_article/loops_article_thumbnail.jpg
---

Loops are one of the fundamental tools you'll use when making a game in the [Unity Game Engine](https://youtu.be/kOo1CaDdCF0?si=m_SoO0x0rxHZoHEL).

You can use them to **execute code multiple times without repeating it** or to **search a collection of items for one that meets a specific criterion**.

This article assumes you're familiar with other C# concepts, such as [variables]({{ site.baseurl }}{% post_url 2025-09-19-game-dev-guide-to-variables-in-c-sharp %}), [operators]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-operators-in-c-sharp %}), [numbers]({{ site.baseurl }}{% post_url 2025-09-24-game-dev-guide-to-numbers-in-c-sharp %}), [booleans]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-booleans-in-c-sharp %}), and [conditional statements]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-conditional-statements-in-c-sharp %}).

If you're a visual learner, you can watch the video version below.

<div class="responsive-embed responsive-embed-16by9">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/l4jiGjc6jiI?si=nkd53pCJctQ7dhXv" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

{% include toc %}

## Loops in C# Explained

When something happens in a loop, it progresses until the end and then restarts from the beginning. A loop could also mean something happens continuously.

The latter explanation is closer to the C# definition of loops. Loops in C# **execute code repeatedly based on a condition**.

You, the game developer, control when the loop starts or stops and how many times it executes.

**_Tip:_** Loops are also known as **iteration statements**.
{: .notice--info}

There are four types of loops in C#:

1. `for` loop

2. `foreach` loop

3. `while` loop

4. `do-while` loop

These loops can be used interchangeably depending on your requirements, but there'll be scenarios when one is better than the others.

## `for` Loop

A `for` loop consists of three parts:

- Initializer

- Condition

- Iterator

The **initializer section** is where you **create the variable that counts each cycle**. Despite being part of the loop, this section **executes once** to create the variable.

The **condition section** determines **how many times the loop executes**. The condition is often a comparison between the number created in the initializer section and the number of times you want the loop to execute.

If the variable from the initializer section reaches the number you specified, the loop stops.

This condition **must be a boolean value that's `true` at the start**. If it's `false`, the loop will never execute.

You can also compare any two variables in the condition section, provided that at some point, the condition becomes `false`, and the loop stops. Otherwise, the loop will execute infinitely and break your Unity game's code.

The **iterator section** is where the variable created in the initializer section is updated so the **loop moves to the next cycle**.

```csharp
var cycles = 5;

/*
    * 'int i = 0;' - Initializer
    * 'i < cycles;' - Condition
    * 'i++' - Iterator
*/
for (int i = 0; i < cycles; i++)
{
    Debug.Log("This code has been executed.");
}

// Output

// This code has been executed.
// This code has been executed.
// This code has been executed.
// This code has been executed.
// This code has been executed.
```

An increment (`++`) or decrement (`--`) operator is common in the iterator section to move one cycle, but you can adjust the variable in any way you like if you wish.

**_Tip:_** A loop cycle is also known as an **iteration**.
{: .notice--info}

Let's say the game you're making in Unity has a turret that fires 5 times when the player is in range.

One approach would be to manually repeat the code to fire the turret, which would be tedious and prone to bugs.

A better way would be to write the code that fires the turret once in a loop that executes 5 times.

```csharp
var turretFireCount = 5;

/*
    * This is part of classes, which are discussed
    * in a separate article.
*/
var turret = new Turret();

for (int i = 0; i < turretFireCount; i++)
{
    turret.Fire();
}
```

## `foreach` Loop

The **`foreach` loop only works with collection types, such as lists or arrays**.

Unlike the `for` loop, you can't explicitly specify how many times a `foreach` loop executes because **the total items in the collection determines the number of cycles**.

A `foreach` loop also **doesn't require an explicit condition to start or stop execution**. It starts automatically and stops when the code inside it has been executed the same number of times as the total items in the collection.

Let's say you're making an adventure game in Unity where the player must solve a puzzle by rotating four statues to face the correct position.

You can store the statues' direction in an array and then loop through the array using a `foreach` loop to check if each is facing the right way.

```csharp
// Remember enums??
public enum Direction { North, East, South, West }

var statueDirections = new Directions[]
{
    Direction.East,
    Direction.West,
    Direction.North,
    Direction.South
}

foreach (var statueDirection in statueDirections)
{
    if (statueDirection == Direction.North)
        Debug.Log("Light the torch.");
}

/*
    * Only the third statue in the 'statueDirections' collection
    * is currently facing North, so only that torch will be lit.
*/
```

Read the code above as, "For each statue direction in the `statueDirections` collection, if the statue's direction is 'North', light the torch."

The `statueDirection` variable represents the current statue's direction you're looping over, and `statueDirections` represents the collection of items.

The variable's name can be anything you want. You could rename it to `statueOrientation` or `direction`. The most important thing is the actual collection you're looping over, which comes after the `in` keyword.

You can read the code above as, "If the player falls from a high point **or** an enemy attacks them, take away 10 hit points."

**Interested in making games in Unity?** [Become a patron](https://www.patreon.com/cw/heightabovesealevel) on Patreon and gain access to cheat sheets, behind-the-scenes content, advanced scripting videos, and more.
{: .notice--primary}

## `while` Loop

A `while` loop executes when a specified condition is satisfied, but, unlike a `for` loop, **the code to stop the loop is inside the loop**.

**The condition must be `true` to begin with**, and the code inside the loop eventually makes it `false` after a certain number of cycles. The loop stops when the condition is `false`.

Let's say you're making a 3D platformer game where the player collects scrap metal by breaking boxes, and large boxes contain 100 scrap metal.

You can use a `while` loop to animate the user interface (UI) so that one unit is added to the scrap metal total at a time until it reflects all 100.

The _Crash Bandicoot_ series implements something similar when you break special boxes, and the player's total animates the addition of each Wumpa fruit.

```csharp
var scrapMetalHeld = 234;
var scrapMetalCollected = 100;

// This loop will execute 100 times.
while (scrapMetalCollected > 0)
{
    // Increase scrap metal held by 1.
    scrapMetalHeld++;

    // Code to play UI animation goes here.

    /*
        * Continuously deduct 1 so this value eventually
        * reaches 0 and the loop stops because its
        * condition is false i.e. 'scrapMetalCollected' is not
        * greater than 0 anymore.
    */
    scrapMetalCollected--;
}
```

You can read the code as, "While the scrap metal collected is greater than 0, deduct 1 and add it to the player's total."'

This loop will continue until the scrap metal collected reaches 0, at which point, the player's total will reflect all 100.

## `do-while` Loop

A `do-while` loop is similar to a `while` loop, with the main difference being that a `do-while` loop is **guaranteed to execute at least once**, regardless of whether the condition is `true` or not.

```csharp
var woodCollected = 100;

do
{
    Debug.Log("That's a lot of wood!");
}
while (woodCollected > 100)

/*
    * 'woodCollected' is not greater than 100, but
    * 'That's a loot of wood!' will still be logged to the
    * console once.
*/
```

This loop isn't as common as the other three, but it's worth knowing in case you encounter a scenario where it might be beneficial.

## C# Loops Comparison

| `for` Loop | `foreach` Loop | `while` Loop | `do-while` Loop |
|--- | --- | --- |
| Must specify total cycles. | Collection decides total cycles. | Total cycles optional. | Total cycles optional. |
| 3 parts in condition. | No condition. | Condition is one part. | Condition is one part. |
| Condition must be `true`. | No condition. | Condition must be `true`. | 1 cycle guaranteed even if condition is `false`. |
| Requires `true` condition to run. | Starts/ends automatically. | Requires `true` condition to run. | Requires `true` condition after 1st cycle. |
| Medium risk of infinite loop. | Low risk of infinite loop. | High risk of infinite loop. | High risk of infinite loop. |

## Breaking Loops and Skipping Cycles

You can break a loop any time using the `break` keyword. Breaking a loop early can be beneficial when you're searching a collection for a particular item.

Let's say the game you're building in Unity has a gadget that can highlight the location of a hidden collectible randomly placed in one of 50 hiding spots.

You could store the hiding spots in an array, and then loop through each hiding spot while checking if the current hiding spot has the collectible.

Once the loop reaches the hiding spot with the collectible, you highlight it, and then break out of the loop since there's no need to go through the remaining items looking for something you've already found.

```csharp
public class HidingSpot
{
    // Hiding spot code here...
}

var hidingSpots = new HidingSpot[]
{
    new HidingSpot(false),
    new HidingSpot(true),
    new HidingSpot(false),
    new HidingSpot(false),
    // 46 other hiding spots not included here for brevity.
}

foreach (var hidingSpot in hidingSpots)
{
    if (hidingSpot.HasCollectible)
    {
        hidingSpot.Highlight();
        break;
    }
}
```

**_Tip:_** A `break` statement is usable inside any loop.
{: .notice--info}

You can also break out of a loop using the `return` keyword, but this does more than break the loop. The methods article covers it in more detail.

Aside from breaking a loop, you can also **skip cycles** based on a condition using the `continue` keyword.

Suppose your Unity game has a set of tiles on the floor, and you want to place a trap on the even-numbered tiles.

You can store all the tiles in an array, and, while looping through them, check if the tile is an even number using the remainder operator (`%`). If it is, place a trap. Otherwise, skip it using the `continue` keyword.

```csharp
public class Tile
{
    // Tile code here...
}

var tiles = new Tile[]
{
    new Tile(),
    new Tile(),
    new Tile(),
    new Tile(),
    // Remaining tiles ommitted for brevity.
}

foreach (var tile in tiles)
{
    if (tile.Number % 2 != 0) // <- Checks if the tile is an odd number.
        continue; // <- Skips to the next tile if current tile is odd number.
    
    title.PlaceTrap(); // <- Only executes for even-numbered tiles.
}
```

## Recap

- Loops **execute code repeatedly** or **search for a particular item in a collection**.

- The four types of loops are `for`, `foreach`, `while`, and `do-while`.

- A `foreach` loop is the only loop that **doesn't require a condition to execute**.

- You can break a loop at any time using the `break` keyword.

- You can skip loop cycles using the `continue` keyword.

This article is the ninth in a series breaking down common C# concepts used in game development with the Unity Game Engine.

The next one discusses how to use classes in C# to build large, scalable games.

Here's the complete list of articles in the series:

1. [A Game Developer's Guide to Variables in C#]({{ site.baseurl }}{% post_url 2025-09-19-game-dev-guide-to-variables-in-c-sharp %})
2. [A Game Developer's Guide to Constants in C#]({{ site.baseurl }}{% post_url 2025-09-21-game-dev-guide-to-constants-in-c-sharp %})
3. [A Game Developer's Guide to Numbers in C#]({{ site.baseurl }}{% post_url 2025-09-24-game-dev-guide-to-numbers-in-c-sharp %})
4. [A Game Developer's Guide to Operators in C#]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-operators-in-c-sharp %})
5. [A Game Developer's Guide to Strings in C#]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-strings-in-c-sharp %})
6. [A Game Developer's Guide to Booleans in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-booleans-in-c-sharp %})
7. [A Game Developer's Guide to Enums in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-enums-in-c-sharp %})
8. [A Game Developer's Guide to Conditional Statements in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-conditional-statements-in-c-sharp %})
9. A Game Developer's Guide to Loops in C# _(you are here)_
10. [A Game Developer's Guide to Classes in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-classes-in-c-sharp %})
11. A Game Developer's Guide to Access Modifiers in C#
12. A Game Developer's Guide to Fields & Properties in C#
13. A Game Developer's Guide to Methods in C#
14. A Game Developer's Guide to Lists & Arrays in C#
15. A Game Developer's Guide to Dates & Times in C#