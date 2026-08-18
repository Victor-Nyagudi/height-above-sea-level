---
title: A Game Developer's Guide to Conditional Statements in C#
categories: C#
tags: beginner-c# scripting
excerpt: "Conditional statements control the execution of your Unity game's code, a programming concept known as control flow. One of the simplest use cases for conditional statements is moving the character in a game you're building in the Unity Game Engine."
image:
    path: /assets/images/conditional_statements_article/conditional_statements_article_thumbnail.jpg
    thumbnail: /assets/images/conditional_statements_article/conditional_statements_article_thumbnail.jpg
---

Conditional statements **control the execution** of your Unity game's code, a programming concept known as **control flow**.

One of the simplest use cases for conditional statements is moving the character in a game you're building in the [Unity Game Engine](https://youtu.be/kOo1CaDdCF0?si=m_SoO0x0rxHZoHEL).

If the player presses the <kbd>W</kbd> key, the character should move forward. If they press the <kbd>S</kbd> key, the character should move backward. You can use a conditional statement to accomplish this.

This article assumes you're familiar with [booleans]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-booleans-in-c-sharp %}), the backbone of conditional statements, as well as [variables]({{ site.baseurl }}{% post_url 2025-09-19-game-dev-guide-to-variables-in-c-sharp %}), [operators]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-operators-in-c-sharp %}), and [numbers]({{ site.baseurl }}{% post_url 2025-09-24-game-dev-guide-to-numbers-in-c-sharp %}).

If you're a visual learner, you can watch the video version below.

<div class="responsive-embed responsive-embed-16by9">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/dotDK_PBCF4?si=k-5nNjPRi8INNqCt" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

{% include toc %}

## Conditional Statements in C# Explained

You'll eventually encounter scenarios where you want to act only when a specific condition is satisfied.

For example, you might want to increase the player's health **_if_** they interact with a health orb, or turn the 3D model into a ragdoll **_when_** the player's health reaches 0.

The condition for the player's health to increase is the interaction with a health orb. Similarly, the condition for the character's 3D model to become a ragdoll is the player's health reaching 0.

**You only proceed to the next step when these conditions are satisfied**, either increasing the player's health or turning the 3D model into a ragdoll.

**_Tip:_** Should you find yourself using the words "if" or "when" while describing what you want to do in your game, a conditional statement will likely be a good option to implement it.
{: .notice--info}

By placing conditions in certain parts of your game's code, you're **controlling the flow of execution based on those conditions**.

This control ensures your game behaves how you want it to when you want it to.

The two conditional statements you'll use the most when making a game in Unity are the `if` and `switch` statements. Let's explore the `if` statement first.

## `if` Statements

An `if` statement in C# is written similarly to how you do so in plain English.

If the player picks up some money, the money in their inventory increases. Here's how you would accomplish the same thing with an `if` statement.

```csharp
/*
    * Classes are discussed in more detail in
    * a separate article, but just go with this
    * for now.
*/
// This creates a player instance.
var player = new Player();

if (player.HasPickedUpMoney() == true)
    player.MoneyHeld += 250;
```

The code in the parentheses represents the condition, and **conditions must be a boolean value**.

A boolean value can only be either `true` or `false`. Think of an `if` statement as saying, "If the condition is true, execute the code inside the code block. If not, skip the code in the code block, and execute whatever comes after the `if` statement."

You can also use **multiple conditions in an `if` statement**.

One of the earlier examples discussed increasing the player's health whenever they interacted with a health orb.

```csharp
var player = new Player();

var healthOrb = 15;

// if (player.HasPickedHealthOrb(healthOrb) == true)
//     player.Health += healthOrb;

/*
    * 'HasPickedHealthOrb' returns a boolean value,
    * so the code above can be shortened, like so.
*/
if (player.HasPickedHealthOrb(healthOrb))
    player.Health += healthOrb;
```

This code partially works but has a problem. If the player continuously interacts with health orbs at full health, their health will keep increasing infinitely.

That's a [bug](https://youtu.be/akyMZwL3bcs?si=j3roXwZ9yXQZQZEI), and it's caused by increasing the player's health without first checking if it's already at its maximum.

### AND Operator - `&&`

You can add a second condition to ensure the player's health increases if they interact with a health orb **and** they're health is below the maximum.

The symbol representing the word "_and_" in the conditions is a double ampersand **`&&`**. It's one of the [**logical operators**]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-operators-in-c-sharp %}#logical-operators).

**_Tip:_** Some developers refer to the double ampersand as the AND operator.
{: .notice--info}

```csharp
var player = new Player();

const int MaxHealth = 100;

var healthOrb = 15;

/*
    * Curly braces {} are optional when the 'if' statement
    * only has one line, but are mandatory for multiple.
*/

if (player.HasPickedHealthOrb(healthOrb) && player.Health < MaxHealth)
{
    player.Health += healthOrb;
}
```

To help you understand better, you can read the above code as, "If the player interacts with a health orb and their health is below the maximum, add them 15 hit points (HP)."

### OR Operator - `||`

Consider another scenario. Let's say the game you're making in Unity has fall damage in addition to taking damage from enemy attacks.

In this case, the player's health reduces when one of two conditions is satisfied:

1. The player jumped down from a high platform and landed hard, **or**...

2. An enemy attacked the player.

You can implement this using another logical operator, commonly referred to as the **OR** operator. Its symbol is a double pipe **`||`**.

```csharp
var player = new Player();

var fallDamageHeight = 20;

if (player.HasFallenFrom(fallDamageHeight) || player.IsAttacked())
{
    player.Health -= 10;
}
```

You can read the code above as, "If the player falls from a high point **or** an enemy attacks them, take away 10 hit points."

**Interested in making games in Unity?** [Become a patron](https://www.patreon.com/cw/heightabovesealevel) on Patreon and gain access to cheat sheets, behind-the-scenes content, advanced scripting videos, and more.
{: .notice--primary}

### Nested `if` Statements

It's possible to place `if` statements inside the code block of other `if` statements. This approach is called **nesting**. Nesting can occur if a series of conditions must be satisfied.

Let's say you want to deduct 10 HP only when the player's health is above 10 HP after they're attacked or fall hard. Here's how you'd accomplish it.

```csharp
var player = new Player();

var fallDamageHeight = 20;

// First condition to satisfy.
if (player.HasFallenFrom(fallDamageHeight) || player.IsAttacked())
{
    /*
        * This is a nested 'if' statement.
        * It only executes when one of the conditions above is satisfied.
    */
    if (player.Health > 10)
        player.Health -= 10;
}
```

The code now first checks if the player has fallen from a high platform or if an enemy has attacked them.

Once this condition is satisfied, you now know the player's health should reduce, so you check a second time to see how much remaining health they have to determine how much HP you'll deduct.

### `else` and `else if` Statements

Suppose you're building a fighting game in Unity where each fighter has a special meter that lets them perform special moves as the meter fills.

The meter enables a unique special move at 25%, 50%, 75%, and the ultimate move at 100%; however, only one can be performed before the meter resets.

Each percentage mark represents a scenario to check for. You can combine an `if` statement with an `else if` and `else` statements to achieve this.

```csharp
var player = new Player();

if (player.SpecialMeter == 25)
    Debug.Log("Sonic Pulse available.");

else if (player.SpecialMeter == 50)
    Debug.Log("Flame Fist available.");

else if (player.SpecialMeter == 75)
    Debug.Log("Gatling Gun available.");

else
    Debug.Log("Ultimate ready. Let's rock!");
```

The code searches the conditions in each `if` and `else if` statement from top to bottom and stops when it finds the first `true` condition, executing only that code block.

An `else` statement doesn't have a condition and **must come after the `if` and `else if` statements**.

The code in an `else` block only executes **if the conditions in the `if` and `else if` statements are all `false`**.

You can also use an `if` and an `else` statement without `else if` in between for scenarios where it's one thing or the other.

For example, the main character in your Unity game could play a voice line if the player tries to fire their gun with no ammo.

The code would read, "If the player has ammo, fire the gun. Otherwise, play the 'I need ammo!' voice [audio]({% post_url 2025-10-02-free-music-sfx-for-unity-games %}) clip."

```csharp
var player = new Player();

var noAmmoVoiceLine = "I need ammo!";

if (player.AmmoCount >  0)
    player.FireGun();

else
    player.PlayAudioClip(noAmmoVoiceLine);
```

Remember that `else if` and `else` statements can only be used **immediately after an `if` statement** - they can't exist on their own.

On the contrary, `if` statements can exist alone without supporting `else if` or `else` statements.

**_Tip:_** You can have as many `else if` statements between `if` and `else` statements as you like. Any more than five, and the code starts to look messy.
{: .notice--info}

## `switch` Statements

`switch` statements are generally similar to `if` statements. The biggest difference is how they're declared.

You create them using the `switch` keyword, and, instead of the parentheses containing a check, a value is placed in there to be tested for different scenarios. **The value doesn't have to be a boolean**.

Here's how you implement the earlier example discussing special moves in a fighting game using a `switch` statement.

```csharp
var player = new Player();

switch (player.SpecialMeter)
{
    case 25:
        Debug.Log("Sonic Pulse is available.");
        break;

    case 50:
        Debug.Log("Flame Fist is available.");
        break;

    case 75:
        Debug.Log("Gatling Gun is available.");
        break;

    default:
        Debug.Log("Ultimate ready. Let's rock!");
        break;
}
```

The meter's percentage is in parentheses, and each `case` inside the `switch` statement checks for a specific scenario.

You can read it as, "In the case the meter is at 25%, unlock the _Sonic Pulse_ special move. In the case the meter is at 50%, unlock the _Flame Fist_ special move, etc."

The `break` keyword is used after each `case` to **ensure the code only executes the `true` case**. Removing this would execute the code for the other cases below the `true` one.

Similar to `if` statements, a `default` case is included at the bottom when none of the cases above it are `true`; the `switch` statement equivalent of the `else` block in `if` statements.

**_Tip:_** You can have as many cases as you want before the `default` statement. Any more than five, and the code starts to look messy.
{: .notice--info}

## Switch Expressions

A [switch expression](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/switch-expression#case-guards) is similar to a `switch` statement but is declared differently.

Unlike the `switch` statement, which is a code block, **a switch expression returns a value** you can store in a variable.

```csharp
var player = new Player();

// Switch expression.
var specialMove = player.SpecialMeter switch
{
    25 => "Sonic Pulse available.",
    50 => "Flame Fist available.",
    75 => "Gatling Gun available.",
    _ => "Ultimate ready. Let's rock!",
}

Debug.Log(specialMove);
```

## `switch` Statement vs. Switch Expression: What's the difference?

| `switch` Statement | Switch Expression |
| --- | --- |
| Condition placed after `switch` keyword. | Condition placed before `switch` keyword. |
| Doesn't return a value. | Returns a value. |
| Uses `case` for different scenarios. | Uses `=>` for different scenarios. |
| Uses `default` for default scenario. | Uses `_` for default scenario. |

The main differences between a switch expression and a `switch` statement are:

- The tested value in a switch expression comes **before the `switch` keyword**, but after it in `switch` statements.

- Switch expressions **return a value**. `switch` statements do not.

- Switch expressions **use an equal sign and an arrow** (`=>`) for each scenario, while `switch` statements use the `case` keyword.

- Switch expressions use an **underscore** (`_`) when all the scenarios are `false`, while a `switch` statement uses the `default` keyword.

## `if` Statement vs. `switch` Statement: Which Should You Use?

Both statements accomplish the same goal, and choosing one over the other often comes down to personal preferences.

Given that `switch` statements must include the `case` keyword at the beginning and the `break` keyword at the end, they may be more verbose to write than an `if` statement.

You might find it easier working with `if` statements if there are multiple things you want to do inside each code block for each scenario.

`switch` statements may be easier to read and work with when you only have a line or two you want to execute for each scenario.

**_Tip:_** Conditional statements could work well when implementing a flashlight. If the player presses a button, the [lights]({% post_url 2025-11-01-baking-lights-in-unity-getting-started %}) turn on and vice versa.
{: .notice--info}

## Recap

- Conditional statements **control the flow of code execution**.

- The two most common statements are `if` and `switch` statements.

- The condition in an `if` or `else if` statement **must be a boolean**.

- The **value being tested in a `switch` statement can be multiple types**, such as a number, string, or boolean.

- Switch expressions also use the `switch` keyword and **return a value**.

This article is the eighth in a series breaking down common C# concepts used in game development with the Unity Game Engine.

The next one discusses how to use loops when working with multiple related items.

Here's the complete list of articles in the series:

1. [A Game Developer's Guide to Variables in C#]({{ site.baseurl }}{% post_url 2025-09-19-game-dev-guide-to-variables-in-c-sharp %})
2. [A Game Developer's Guide to Constants in C#]({{ site.baseurl }}{% post_url 2025-09-21-game-dev-guide-to-constants-in-c-sharp %})
3. [A Game Developer's Guide to Numbers in C#]({{ site.baseurl }}{% post_url 2025-09-24-game-dev-guide-to-numbers-in-c-sharp %})
4. [A Game Developer's Guide to Operators in C#]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-operators-in-c-sharp %})
5. [A Game Developer's Guide to Strings in C#]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-strings-in-c-sharp %})
6. [A Game Developer's Guide to Booleans in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-booleans-in-c-sharp %})
7. [A Game Developer's Guide to Enums in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-enums-in-c-sharp %})
8. A Game Developer's Guide to Conditional Statements in C# _(you are here)_
9. A Game Developer's Guide to Loops in C#
10. A Game Developer's Guide to Classes in C#
11. A Game Developer's Guide to Access Modifiers in C#
12. A Game Developer's Guide to Fields & Properties in C#
13. A Game Developer's Guide to Methods in C#
14. A Game Developer's Guide to Lists & Arrays in C#
15. A Game Developer's Guide to Dates & Times in C#